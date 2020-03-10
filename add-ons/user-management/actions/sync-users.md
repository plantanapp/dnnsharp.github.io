# Sync users

The Sync Ussers action will allow you to synchronize users across all portals of your website.

It basically works as a *"Copy User Profile"* action **from source**(the current portal) **to destination**(one or more portals of the same website)

![Sync Users](https://static.dnnsharp.com/documentation/sync_users.png)

> Keep in mind this is a one way action; it syncs users from source to destination. 
To do a two way synchronization between two portals you will have to use the action on both of them(be careful to properly condition it to prevent running into an infinite loop)

> <span style="font-color:red"><b>WARNING!</b></span> When used in [Sharp Scheduler](https://www.dnnsharp.com/dnn/modules/sharp-task-scheduler) with a [User Registration Trigger](/sharp-scheduler/triggers/on-user-created.html) the Sync Users action might fail to properly sync user roles because it executes before the user roles get to be assigned on source portal. To bypass this issue we recommend adding an [Execute Token](/actions/code/execute-token.html) action in which you run a Script Token that does a Thread.Sleep (_System.Threading.Thread.Sleep(5000);_)