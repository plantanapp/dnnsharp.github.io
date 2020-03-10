# Datasource Refresh

This action is usually used to refresh the grid after previously executing another action; for example, when you remove an item from the grid then refresh the grid in order to update it with the remaining items. 
> It only applies to the Grid that it is used in.

### Alternative methods to Refresh datasource for a grid

Starting with Action Grid version 5.0.216 you can also:
* either enable Auto-Refresh (update) for datasource at a specified interval
![Grid Datasource Auto Update](https://static.dnnsharp.com/documentation/grid_datasource_refresh_auto.png)
* or manually trigger it by using the:
  - _**Datasource Refresh**_ action from a button inside the grid itself
  - javascript code _**dnnsf.api.actionGrid.refresh(1234)**_ from anywhere on the page, considering that _1234_ is the moduleId of the grid that you want to refresh datasource for
  ![Grid Datasource Auto Update](https://static.dnnsharp.com/documentation/grid_datasource_refresh_manual.png)