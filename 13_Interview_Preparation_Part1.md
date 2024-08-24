# Certification Exam Preparation

## Process Report

- File format: .arf
- When process report is exported, 5000 rows are exported by default.

## Process Model Security

- Process model folders differ from knowledge centers, rule folders, and document folders in that their security is never inherited by nested process model objects.
- During development, each process model will require that its own security be set.

## Creating Application

- Maximum name length: 255 characters.
- Maximum description length: 2000 characters.
- Maximum prefix length: 10 characters.
- Appian constructs a default prefix using the initial characters of the first 10 words.

## Object Security

- Appian recommends that you set security on your top-level knowledge centers and rule folders within applications and allow the objects nested below these folders to inherit security. Doing so ensures that security is consistent and easy to manage across large applications

## Document Name

- If any of the following characters are used in the name, Appian replaces them with an underscore: `\ / ; : | ? ' < > *`.

## Query Return Size

- The amount of data returned by a query is limited to 1MB by default.
- Queries that take longer than 10 seconds are canceled by default.
- The default query result limit for Appian Cloud users is 1000 rows.

## Variables

- You should not save into the same process variable in node inputs as you do in node outputs. This is because these both save at the same time, and the value you intend to end the node with may be overwritten.
- Rule input names need to be at least three characters long to be automatically associated with a new activity class parameter.

## Activity Chaining

- Long activity chains (greater than 50 node instances OR 5 seconds between attended activities) are strongly discouraged. They negatively affect system performance and user experience at scale.

## Additional Dashboards

- 20 additional record views on your record type.

## Securities

- **Record**
- **Process Model**
- **Expression**
- **Application**
- **Data Store**
- **Connected System**
- **Integration**
- **Web API**

## Appian Architecture

### Configured for Backup/Restore

#### Web Server

- Handles client requests.
- Handles static requests.
- Reduces load SSL for application server if using HTTPS.

#### Application Server

- Significant portion of Appian functionality.
- Coordinates interaction between system components.
- Central source of logging.
- Executes business rules and processes.

#### Appian Engine

- Stores metadata for rules, interface, groups and process.
- In memory real-time databases
- Metadata for instance.
- Default: 15 engines.
  - 9 individual engines.
  - 3 pairs of process executable and analytics engine.
    - Extended 32 pairs of extendable engines.

#### Content

- Metadata for the security of documents and organizational structure like community.
- Actual document content is stored on the file system, not in the engine.

#### Collaboration Statistics

- Contains statistics on document usage and storage.

#### Portal Notifications

- Stores information about system notification settings.

#### Email Notifications

- Responsible for generating and sending notifications via email.

#### Personalization

- Stores information about users, groups, group membership, and group types.

#### Process Design

- Stores all information pertaining to the design of the process models within the application.

#### Portal

- Stores all information about pages in the Apps Portal interface.

#### Channels

- Stores information about the portlet types that are displayed on portal pages in the Apps Portal interface.

#### Forums

- Stores all topics and messages posted to discussion forums in the Apps Portal interface. News content in the Tempo interface is not stored in this engine.

### Handled by Service Manager

#### Search Server

- Supports features like tracking historical performance, viewing recent user activity, and analyzing design-time impacts/dependencies.
- Runs as a standalone Java application, and multiple search servers can be configured.

### Relational Databases

- **Appian Data Source:** A relational database that stores internal Appian data and metadata, required to run Appian. Can also be used as a business data source.

### File Storage

- The application server and Appian engines are installed on and store runtime content on the file system.
- Shared storage (Windows or NFS) is required when running a distributed environment with multiple application servers or multiple engines on different servers.

### Data Server

- A novel storage layer designed from the ground up for Appian. Fault-tolerant distributed service that stores application data and metadata.

### Mail Server

- Appian requires an external SMTP server to send outgoing email, including system notifications and email messages sent by process instances.
- Appian can also be configured to receive email over POP3 or IMAP/S.

### Internal Messaging Service

- Responsible for relaying data between different components of Appian's architecture. Implemented using Apache Kafka and Zookeeper.

## Logs

- **Performance Logs:** APPIAN_HOME/logs/perflogs directory.

| Purpose                                                                                          | Log Name                                      |
|--------------------------------------------------------------------------------------------------|-----------------------------------------------|
| Whenever a process is archived or deleted, the event will be recorded                          | removed_processes log                        |
| Logs recording the data store operation time                                                    | Data Store Performance Logs                   |
| Captures information about the requests made by application server to the data server           | Data server trace log                         |
| Ads call trace                                                                                  | Ads_call_trace.csv                            |
| How object comparisons are performing                                                           | design_object_diffs_details.csv               |
| What requests the application server makes to the Appian Engines                                | engine_call_trace.csv                         |
| Status of each engine server                                                                     | engine_summary.csv                            |
| Performance of the Appian engines                                                                | perf_monitor_db_<ENGINE-ACRONYM>_<TIMESTAMP>.csv |
| Performance measurements on the building blocks of Appian expressions: functions and rules       | expressions_trace.csv                        |
| Displays all plug-in functions that take longer than 5 seconds to complete or have a result size over 100,000 AMUs | plugin_functions_slow.csv                    |
| Provides data on integration performance                                                         | integration_trace.csv                         |
| Provides performance measurements on interfaces, including record and report dashboards and start and task forms | sail_trace.csv                                |
| Provides measurements on offline mobile performance                                             | offline_trace.csv                             |
| Reports information on Appian's REST API                                                          | rest_trace.csv                                |
| Provides performance measurements on reporting functionality                                    | reporting_trace.csv                           |
| Records the replication of data to the search server for indexing                                | search_server_replication_summary.csv         |
| Reports the performance of Java Smart Services, including both Appian and plug-in Smart Services | smart_services_trace.csv                      |
| Web API performance                                                                              | web_apis_trace.csv                            |
| Activity from unattended processes that are processed by the application server                  | work_poller_summary.csv / work_poller_details.csv |

  
### Analyzing Data Metrics

- APPIAN_HOME/logs/data-metrics directory.

| Purpose                                                                                           | Log Name                                   |
|---------------------------------------------------------------------------------------------------|--------------------------------------------|
| Information about actions                                                                        | actions.csv                                |
| Record of which Administration Console branding properties have been changed from their default values | admin-branding.csv                         |
| Record of which Administration Console properties have been changed away from their default values | Admin_console.csv                          |
| A record of which Administration Console permissions have been changed from their default values | admin-permission.csv                       |
| Provides information about API keys                                                                | api_key.csv                                |
| Provides information about application server caches                                              | cache.csv                                  |
| Information about the different schemas in your Appian Cloud database                             | cloud_db_schemas.csv                       |
| Provides information about connected systems                                                      | connected_systems.csv                      |
| Provides information about connected systems and connected system plug-ins                        | connected_systems_aggregated.csv           |
| Data stored in the Content Engine Server                                                           | content.csv                                |
| Records sizing information about individual object types stored in the Content Engine Server       | rules.csv                                  |
| Metrics for the calls made by the application through data server client                           | data-server-client.csv                     |
| Metrics for the resource utilization by all the data server processes                               | watchdog.csv                               |
| Data server metrics logs capture information about how the processes that make up the data server component of the Appian platform are functioning so that Appian Technical Support can help troubleshoot issues | (No specific log name provided)            |
| Information about various types of data sources created in your environment                        | data_sources.csv                           |
| Captures the connection pool information for each data source in your environment                  | data_source_pool.csv                       |
| System and custom data types created in the system                                                 | types.csv                                  |
| Records information about design guidance (warnings and recommendations) across your environment | design_guidance.csv                        |
| Records information about the various findings (e.g. specific warnings and recommendations) across your environment | design_guidance_by_finding.csv             |
| Records information about design guidance (warnings and recommendations) for each design object type in your environment | design_guidance_by_object_type.csv         |
| Provides information about the number of environments in your DevOps Infrastructure                | devops_infrastructure.csv                  |
| Records the disk space used and available in a number of directories important to the engine server | engine_disk_usage.csv                      |
| Provides information about mobile users who are using push notifications                           | push_notifications.csv                     |
| Information about SSL Certificates                                                                  | ssl_certificates.csv                       |
| Information about the JVM environment                                                               | system.csv                                 |
| Memory spike and long transaction warning files are counted in both the Memory Spike Warnings and Long Transaction Warnings columns | (No specific log name provided)            |
| To find all objects that reference deleted data types and remove those references                  | types_outdated_refs_summary.csv            |

### Troubleshooting

| Purpose                                                                                           | Log Name                                                  |
|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| Expression errors in start forms, task forms, Tempo reports, record lists, record views, related actions, and Web APIs | design_errors.csv in the <APPIAN_HOME>/logs directory     |
| Details about Health Check runs and lists errors                                                | health-check.log in <APPIAN_HOME>/logs/health-check       |
| Records details about incoming and outgoing deployments from the environment (Direct deployment) | deployment.log in <APPIAN_HOME>/logs                      |
| Application server encounters an unexpected error                                                | tomcat-stdOut.log in <APPIAN_HOME>/logs                   |
| When the application server enters a state of high memory usage, logs entries for each plug-in function running at that time | plugin_functions_running_during_high_system_memory.csv    |
| Information about data server startup and shutdown, configuration values, and general operations and errors | Watchdog.log in <APPIAN_HOME>/logs/data-server/          |
| In the event that sensitive data might be required to troubleshoot an issue with the data server | data-server-client-errors-detail.log in <APPIAN_HOME>/logs |
| Logs for the search server                                                                       | <APPIAN_HOME>/logs/search-server/ directory                |
| The process that coordinates the Appian Engines, records information about engine startup and shutdown, checkpointing, and transaction replication | service_manager.log in <APPIAN_HOME>/logs                 |
| Information regarding locks on data types                                                         | data-type-locks.log in <APPIAN_HOME>/logs                 |


### Auditing

| Purpose                                                                                           | Log Name                                                    |
|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| Used to audit both the management and usage of OAuth 2.0 clients                                 | api_key.csv in <APPIAN_HOME>/logs/audit directory            |
| Information logged when file upload is blocked by the virus scanner (Cloud only) or by file extension | blocked_files.csv in <AE_HOME>/logs/audit/                  |
| Object and plug-in deletions are recorded                                                        | deletion.log in <APPIAN_HOME>/logs                           |
| Each attempted download of a file attached to a news entry is recorded                            | file_attachment_downloads.csv in <APPIAN_HOME>/logs/audit/  |
| Each product login attempt is recorded                                                            | login-audit.csv in the <APPIAN_HOME>/logs directory          |
| Each email received is recorded                                                                   | mail-listener.log in the <APPIAN_HOME>/logs directory        |
| Errors that occur when users access invalid tasks are recorded                                    | task_errors.csv in <APPIAN_HOME>/logs/audit/                 |
| Users deactivated due to inactivity                                                               | db_PE_yyyy-mm-dd_hhmm.log in the <APPIAN_HOME>/logs directory |


## Admin Console

- Only users of type System Administrator can access the Administration Console.

### Branding

- Branding settings apply only to the web interface.
- The logo file should be a PNG file with a transparent background and must be less than 100KB.
- Provide an ICO file with sizes 16x16 and 32x32. The favicon file must also be less than 100KB.

### Data Retention

- The default is 30 days. Appian recommends setting 30 days or less for package cleanup to ensure optimum disk space.

### File Upload

- Files found to contain viruses are logged in the blocked files audit log. It is recommended to enable coordination with a list of extensions to allow rather than a list of extensions to block.

### Timezone

- The Primary Time Zone dropdown allows you to select a time zone from the list. This recommended list is based on the selected language.

### Plugin

- If the plugin fails to deploy, Administrators can check the application server logs for more information.
- Deleted plugins can be tracked in the deletions log.

### Sign-in Page Links

- The maximum number of links is five, and only links that use the http, https, or mailto protocols are allowed.

### Site Typefaces

- The Sites Typeface page allows you to add and preview up to nine custom typefaces for your sites on both web and mobile.

### Session Timeout

- 15 minutes, with a maximum valid value of 480 minutes (8 hours).

### Password Settings

- **Maximum Temporary Password Age:** The default is 10080 minutes (one week).
- **Password Reset Link Duration:** The maximum allowed value is 1440 minutes (24 hours). The minimum allowed value is 1 minute.

### Maintenance Window

- Only System Administrators can sign into the site during a maintenance window. Basic users' active sessions will be expired, REST endpoints will return a 401 error.

### SAML

- Starting a process model as a web service requires using Appian's native authentication and is therefore not available to users configured to authenticate via SAML.

### Managing Environment

- Incoming connection requests will time out after 7 days if no action is taken on them.

### Current User Activity

- User activity is stored for 1 hour, and only the most recent 1000 entries are displayed.

### Import History

- The Import History page shows all imports that have occurred on the system during the last 30 days.

## Rule Performance

- A moving window of thirty days of performance metrics are gathered and stored as end users execute the rules.

## Cannot be exported

- **API Keys**
- **LDAP Authentication**
- **SAML Authentication**
- **Infrastructure**
- **Certificates**
- **Legacy Web Services**
- **Integration**

## Integration

### Certificate

- The certificate must be formatted as a PEM file. If the certificate is protected by a password, you should enter the password in the password field. This password will not be stored. The certificate will be stored in an encrypted format in the Appian data source.

### Datasource

- - You cannot create a data source with the same name as the Appian data source, as specified in the conf.data.APPIAN_DATA_SOURCE property in custom.properties.
- - Connection String - The URL for the data source. Should include the hostname, port, and database name of the data source

### Document Extraction

- - Appian's built-in document extraction capabilities related to flattened PDFs, key-value pair extraction, and table extraction are only available for Cloud customers at this time.
- - Self-managed and Appian Gov Cloud customers don't have access to these features. Other built-in capabilities are available for both Cloud and self-managed customers.

--**--

## Monitoring Tab

### Health Dashboard

- Only objects which a developer has at least Viewer permissions to are reflected in the dashboard's various summary cards and displayed in its Appian Design Guidance grid.

### Process Activity

- The Process Activity tab shows a list of all process instances related to your environment or application that are currently on the system. Developers must have at least Initiator permissions to processes to see them on this monitoring tab.

### Process Model Metrics

- Developers can view metrics for process models they have at least Viewer permissions to. Only process models with process instances on the system are shown in this report.

### Record Response Time

- Developers must have at least Viewer permissions to records to view their response times on this tab. 

### Record Sync

- Triggers a manual sync of the selected record type. The button appears only after you select a record type by checking the adjacent checkbox.

## Deployment (DevOps)

- **Web API Integration:** Purpose, Security (Service Accounts).

### Integration

- Any request or response body content over 10 KB in size will be truncated in the integration designer. The complete body is available when the integration is called from other objects in your application.

### Call Webservice Smart Service

- The user must be a member of the Process Model Creators group to configure the WSDL URL for this smart service.

### Upload Document through Web API

