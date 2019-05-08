# SQL Dependency (Experimental)

Starting with SharpScheduler 5.00.72  we implemented an alternative way of checking the database triggers. Instead of using the old method in which we would query the database every 2 seconds looking for changes in the data set, SQL Dependency is a feature in which the database notifies us of changes in the data set of a table.

This alternative method will only be used if the DNN schema owner has the necessary permissions. The permissions required and the way to grant them are as follows:

1. Create Procedure

```sql
GRANT CREATE PROCEDURE to [dnn_schema_owner]
```

2. Create Queue

```sql
GRANT CREATE QUEUE to [dnn_schema_owner]
```

3. Create Service

```sql
GRANT CREATE SERVICE to [dnn_schema_owner]
```

4. Reference

```sql
GRANT REFERENCES on
CONTRACT::[http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]
  to [dnn_schema_owner]
```

5. View Definition

```sql
GRANT VIEW DEFINITION TO [dnn_schema_owner]
```

5. Select

```sql
GRANT SELECT to [dnn_schema_owner]
```

6. Subscribe Query Notifications

```sql
GRANT SUBSCRIBE QUERY NOTIFICATIONS TO [dnn_schema_owner]
```

7. Receive

```sql
GRANT RECEIVE ON QueryNotificationErrorsQueue TO [dnn_schema_owner]
```

On every start of the AppPool, we will check if these permissions are granted and try to enable the SQL Broker. If the necessary permissions are met and the Broker enabling process is successful SharpScheduler will automatically switch to using SQL Dependency for database triggers. If the process fails or if the permissions are not met, SharpScheduler will use the old method as a fallback.

**WARNING!**

Please be weary of using this system for checking the database triggers as it **IS NOT** yet completely optimized. After using the Dependency method for a long while, the notifications queue will start filling up, and there is no method to execute a clean up until we implement our own custom queue and manage it ourselves.