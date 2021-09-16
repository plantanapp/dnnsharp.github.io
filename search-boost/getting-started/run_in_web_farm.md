# Run in Web Farm

This guide assumes that you have a load balancer that sits on top of a few machines. The /Portals folder is located on a shared network location so all machines share the same files (or other file synchronization mechanism).

The problem with the search engine is that there can be only one index writer. So there can be only one server that indexes the content. Choose the server that will do this: 
 * Go in Host > Schedule and set for the two SearchBoost schedulers ("Search Boost - Indexer" and "Search Boost - Query Content Sources") the `Run on Servers` property to the same server name.

Don't manually index from a SearchBoost settings page as this could start on any server. Let SearchBoost [incrementallly index](/indexing-content.html) by itself - you can manually fire the _Search Boost - Query Content Sources_ schedule item.


**Note**: If you have a synchronization mechanism set it to ignore "write.lock" files.

If you are using FileBasedCachingProvider, add the setting "IsWebFarm" in web.config as follows:
 * `<add key="IsWebFarm" value="true" />`
 * If you are using a different caching provider, make sure it also has the property "IsWebFarm" to set to 'true' in the configuration. Otherwise, all the servers will try to index and sometimes you might end up with a corrupted index or other strange behaviors.

In order to reach the master server from SearchBoost Admin:

 * IIS ARR Server Affinity - [Client Affinity must be enabled](https://docs.microsoft.com/en-us/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity).
 * The cookie name must be named "ARRAffinity".
 * Find the values for each server by checking the cookie in your web browser.
 * Determine the values (IIS ARR module computes the cookie value as a hash of the server name, so it should be a fixed value for each server everytime).
 * Take those values and set them as the UniqueId column value in the webservers table for the corresponding servers.

Starting with Search Boost Version 4 the module no longer uses the DNN Schedule; it has scheduled back-end tasks: 

- QueryContentIntervalSeconds on every 10 minutes; it searches for new content to index
- ConsumeJobsIntervalSeconds on every 10 seconds; it actually indexes


