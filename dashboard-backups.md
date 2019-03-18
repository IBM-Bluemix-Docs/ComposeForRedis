---

copyright:
  years: 2017,2018
lastupdated: "2018-03-02"

subcollection: compose-for-redis

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Backups
{: #dashboard-backups}

You can create and download backups from the _Backups_ tab of the _Manage_ page of your service dashboard. Daily, weekly, monthly, and on-demand backups are available. They are retained according to the following schedule:

Backup type|Retention schedule
----------|-----------
Daily|Daily backups are retained for 7 days
Weekly|Weekly backups are retained for 4 weeks
Monthly|Monthly backups are retained for 3 months
On-demand|One on-demand backup is retained. The retained backup is always the most recent on-demand backup.
{: caption="Table 1. Backup retention schedule" caption-side="top"}

Backup schedules and retention policies are fixed. If you need to keep more backups than the retention schedule allows, you should download backups and retain archives according to your business requirements.

## Viewing existing backups

Daily backups of your database are automatically scheduled. To view your existing backups, navigate to the *Manage* page of your service dashboard. 

  ![Backups](./images/redis-backups-show.png "A list of backups in the service dashboard")

Click on the corresponding row to expand the options for any available backup.

  ![Backup Options](./images/redis-backups-options.png "Options for a backup.") 

### Using the API to view existing backups

A list of backups is available at the `GET /2016-07/deployments/:id/backups` endpoint. The Foundation Endpoint with the service instance ID and the deployment ID are both shown in the service's _Overview_. For example: 
``` 
https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
```  

## Creating a backup on demand

To create a manual backup, go to the *Manage* page of your service dashboard and click *Backup now*.

### Using the API to create a backup

Send a POST request to the backups endpoint to initiate a manual backup: `POST /2016-07/deployments/:id/backups`. It returns immediately with the recipe ID and information about the backup as it is running. You need to check the backups endpoint to see whether the backup finished and find its backup_id. Use `GET /2016-07/deployments/:id/backups/`.

## Downloading a backup

To download a backup, go to the *Manage* page of your service dashboard, and click *Download* in the corresponding row for the backup you want to download.

### Using the API to download a backup

Find the backup you that want to restore from on the _Backups_ page on your service, and copy the backup_id, or use the `GET /2016-07/deployments/:id/backups` to find a backup and its backup_id through the Compose API. Then, use the backup_id to find information and a download link for a specific backup: `GET /2016-07/deployments/:id/backups/:backup_id`.

## Backup contents

Redis saves a binary snapshot of your data by default. The `dump.rdb` file can then be used as a backup for point-in-time recovery. To make the snapshot, Redis forks, so that all of the work for the snapshot is done by the child process while the parent process continues handling your data as normal. The backup process doesn't affect your application or database. You are able to both download a copy of your backups, or restore them directly into a new deployment.

## Using a backup with a local database

You can use your {{site.data.keyword.composeForRedis}} backup to run a local copy of your database.

1. Move your `dump.rdb` file into its own directory, for example `db`.
2. You need a Redis configuration file to start the Redis instance. Copy a `redis.conf` file from your install into the same directory as `dump.rdb`. For example, if you installed Redis on OSX with homebrew, the redis.conf file is in `/usr/local/etc`, so from the `db` directory run `cp /usr/local/etc/redis.conf .`
3. Edit the configuration file to point to your current directory when it starts. Open `redis.conf` in a text editor, and change `dir /usr/local/var/db/redis/` to `dir .`.
4. Save the file and exit.
5. Start the redis server in the `db` directory, supplying the configuration file `redis-server redis.conf`.

## Restoring a backup

1. Follow the steps to view existing backups.
2. Click in the corresponding row to expand the options for the backup you want to download.
3. Click **Restore**. A message is displayed that a restore has been initiated. The new service instance is automatically named "redis-restore-[timestamp]", and appears on your dashboard when provisioning starts.

### Restoring from the {{site.data.keyword.cloud_notm}} CLI

Use the following steps to restore a backup from a running Redis service to a new Redis service by using the {{site.data.keyword.cloud_notm}} CLI. 

1. If you need to, [download and install it](/docs/cli?topic=cloud-cli-overview). 
2. Find the backup that you would like to restore from on the _Backups_ page on your service and copy the backup ID.  
  **Or**  
  Use `GET /2016-07/deployments/:id/backups` to find a backup and its ID through the Compose API. The Foundation Endpoint and the service instance ID are both shown in the service's _Overview_. For example: 
  
  ``` 
  https://composebroker-dashboard-public.mybluemix.net/api/2016-07/instances/$INSTANCE_ID/deployments/$DEPLOYMENT_ID/backups
  ```  
  
  The response contains a list of all available backups for that service instance. Pick the backup you want to restore from, and copy its ID.

3. Log in with the appropriate account and credentials. Use `ibmcloud login`, or `ibmcloud login -help` to see all the login options.

4. Switch to your Organization and Space.

  `ibmcloud target -o "$YOUR_ORG" -s "YOUR_SPACE"`

5. Use the `service create` command to provision a new service, and provide the source service and the specific backup that you are restoring in a JSON object. For example:
  ``` 
  ibmcloud service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": "$BACKUP_ID" }'
  ```
  
  <dl>
  <dt>_SERVICE_</dt>
  <dd>Use `compose-for-redis`.</dd>
  <dt>_PLAN_</dt>
  <dd>Use either Standard or Enterprise depending on your environment.</dd>
  <dt>_SERVICE\_INSTANCE\_NAME_</dt>
  <dd>The name of your new service.</dd>
  <dt>_source\_service\_instance\_id_</dt>
  <dd>The service instance ID of the source of the backup. You can obtain the value by running `ibmcloud cf service DISPLAY_NAME --guid`, where _DISPLAY\_NAME_ is the name of the service the backup is from. </dd>
  </dl>
  
  Enterprise users also need to specify which cluster to deploy to in the JSON object with the `"cluster_id": "$CLUSTER_ID"` parameter.
  
### Migrating to a New Version

Some major version upgrades are not available in the current running deployment. To migrate to these versions, you need to provision a new service that is running the upgraded version, then migrate your data into it using a backup. The process is the same a restoring a backup, except that you need to specify the version you would like to upgrade to.

``` 
ibmcloud service create SERVICE PLAN SERVICE_INSTANCE_NAME -c '{"source_service_instance_id": "$SERVICE_INSTANCE_ID", "backup_id": ""$BACKUP_ID", "db_version":"$VERSION_NUMBER" }'
```

For example, restore an older version of a {{site.data.keyword.composeForRedis}} service to a new service running Redis 4.0.6 with the following command.

```
ibmcloud service create compose-for-redis Standard migrated_redis -c '{ "source_service_instance_id": "0269e284-dcac-4618-89a7-f79e3f1cea6a", "backup_id":"5a96d8a7e16c090018884566", "db_version":"4.0.6"  }'
