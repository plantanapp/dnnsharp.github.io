# Content Sources

According to the Architecture a content source is responsible to get new content to be indexed. The steps to develop a custom content source would be:
- Add a configuration file in _ContentSources_ folder (see local .readme.txt)
- Create your own project with a class that implements `DnnSharp.SearchBoost.Core.ContentSource.IContentSource`
    - implement the Query method that returns a `IEnumerable<Core.Indexing.IndexingJob>`. 
    - implement _ComputeResultUrl_ method. The default should be:
 `return new GenericUrlResolver(searchResult, searchContext).GetUrlForSearchResult();`

For SearchBoost >= 4.0.0 you can use the following sample:

```csharp
using DnnSharp.SearchBoost.Core.Behaviors;
using DnnSharp.SearchBoost.Core.ContentSource;
using DnnSharp.SearchBoost.Core.Indexing;
using DnnSharp.SearchBoost.Core.Search;
using System;
using System.Collections.Generic;
using System.Text;
using System.Threading;

namespace MyImplementation.MyContentSources {
    public class FirstContentSource : IContentSource {

        public static int StartId { get; set; } = 0;

        public string ComputeResultUrl(SbSearchResult searchResult, SearchContext searchContext) {
            return new GenericUrlResolver() {
                SearchResult = searchResult,
                SearchContext = searchContext
            }.GetUrlForSearchResult();
        }


        const string MyContent = @"My Test Content";

        public IEnumerable<IndexingJob> Query(SearchBehavior behavior, DateTimeOffset? since, CancellationToken cancellationToken) {

            for (var i = StartId; i < StartId + 10; i++) {
                var job = new IndexingJob();
                job.ContentSourceId = "DnnModules";
                job.Due = DateTimeOffset.Now;
                job.DatePublished = DateTimeOffset.Now;
                job.Action = "add";
                job.Priority = ePriorityIndexingJob.Low;

                job.BehaviorId = behavior.Id;
                job.PortalId = 0;
                job.TabId = 1;
                job.ModuleId = 1;

                job.Metadata.Type = "mod";
                job.Metadata.SubType = "Test Module";

                job.Metadata.Url = "";

                job.ItemId = "test-" + i;
                job.Metadata.Title = "Test " + i;
                job.Contents = Encoding.UTF8.GetBytes(MyContent);
                job.ContentType = "text/plain";
                job.Metadata.DatePublished = DateTimeOffset.Now;

                job.Metadata.ItemId = job.ItemId;
                job.Metadata.ItemPath = "test/"+i;

                job.Metadata.ContainerId = "Test";
                job.Metadata.ContainerName = "Test";
                job.Metadata.ContainerPath = "Test";

                yield return job;
            }

        }
    }
}
```
Note that you can use the _IndexingJob_ class to create your own job in other places of your code and simply call the _Save()_ method on that job object,

```csharp
    [Common2.IoC.IoCService]
    Common2.Services.Dnn.IPortalService PortalService { get; set; }

    void SaveJob(SearchBehavior behavior) {

        var job = new IndexingJob();
        job.ContentSourceId = "DnnModules";
        job.Due = DateTimeOffset.Now;
        job.DatePublished = DateTimeOffset.Now;
        job.Action = "add";
        job.Priority = ePriorityIndexingJob.Low;

        job.BehaviorId = BehaviorService.GetDefaultBehavior(PortalService.GetCurrentPortalSettings().PortalId).Id; // all jobs must belong to a behavior
        // or you can get it by name using:
        // job.BehaviorId = BehaviorService.GetAll().FirstOrDefault(x => x.Name == behaviorName && x.PortalId == portalId)
        job.PortalId = 0;
        job.TabId = 1;
        job.ModuleId = 1;

        job.Metadata.Type = "mycustomtype"; 
        job.Metadata.SubType = "SomeSubType";

        job.Metadata.Url = ""; // you can add here a custom url for search result, otherwise it will redirect to the specified tabid property

        job.ItemId = "MyUniqueId";
        job.Metadata.Title = "Job Title In Results";
        job.Contents = Encoding.UTF8.GetBytes("My Custom Content");
        job.ContentType = "text/plain";
        job.Metadata.DatePublished = DateTimeOffset.Now;

        job.Metadata.ItemId = job.ItemId;
        job.Metadata.ItemPath = "test/path_if_needed"; // useful for files, to get them from DNN when using the DnnFileClient content client

        job.ContentClient = "MyCustomContentClient"; // Content clients are defined in /Config/ContentClients folders, and here you type their ID property, like "WebClient" or "DnnFile"
        job.ContentClientOptions = new Common.SettingsDictionary(); // this is pased to the content client for further options. Not needed for the default ones.

        job.Metadata.ContainerId = "Test";
        job.Metadata.ContainerName = "Test";
        job.Metadata.ContainerPath = "Test";

        job.Save();
    }
```

## Older Versions
Here is a sample that works with SearchBoost >= 3.1.43, up until SearchBoost <= 4.0.0:

```csharp
using DnnSharp.SearchBoost.Core.ContentSource;
using DnnSharp.SearchBoost.Core.Indexing;
using DnnSharp.SearchBoost.Core.Search;
using DnnSharp.Common.Logging;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
 
namespace avt.SearchBoost.TestPlugin.ContentSources
{
    public class TestContentSource : IContentSource
    {
        public void Query(TypedLogger<SearchInstance> logger, Core.Indexing.LuceneStorage dataStore, Core.IEngineSettings config, Core.Indexing.IndexingStatistics stats) {
            
        }
 
        public IEnumerable<Core.Indexing.IndexingJob> Query(SearchInstance instance, DateTimeOffset? since, TypedLogger<SearchInstance> logger) {
            List<IndexingJob> toReturn = new List<IndexingJob>();
 
            // creating a new indexing job using the contructor with required properties:
            IndexingJob job = new IndexingJob(instance, contentSourceId: "MyContentSourceId", action: "add", type: "plugin",
                itemId: "uniqueJobId", title: "Title", portalId: 0);
 
            // we want the item to be indexed right away
            job.Due = DateTime.Now;
            // the job will have a higher priority
            job.Priority = ePriorityIndexingJob.High;
 
            // let's say the item was last modified yesterday
            job.Metadata.DatePublished = DateTime.Now.AddDays(-1).ToUniversalTime();
 
            // show item in results for all users (using DNN user roles)
            job.Metadata.Roles = new List<string> { "All Users" };
 
            job.Metadata.OriginalName = "Item original name";
            // the item result url will have added the following query string params:
            job.Metadata.QueryString = "Param1=value&Param2=otherValue";
 
            // the content that will be indexed and used for result description:
            job.Contents = Encoding.UTF8.GetBytes("xyz content");
             
            // show this description (if "Highlight search terms" is disabled)
            job.Metadata.Description = "custom description";
 
            // this is saved in index (not searchable)
            // can accessed in your custom output template with <xsl:value-of select="data/field[@name='somekey']"></xsl:value-of> (returns first element = data1) 
            // you can also filter by appending query string param sbc-somekey=filterValue
            job.Metadata.Data.Add(new Core.Model.CustomData {
                Name = "somekey",
                Values = new List<string> { "data1", "data2" }
            });
 
            // other properties:
            job.Metadata.ContainerId = "container id";
            job.Metadata.ContainerName = "container name";
 
            toReturn.Add(job);
 
            return toReturn;
        }
 
        public string ComputeResultUrl(Core.Search.SbSearchResult searchResult, Core.Search.SearchContext searchContext) {
            return new GenericUrlResolver(searchResult, searchContext).GetUrlForSearchResult();
        }
    }
}
```
