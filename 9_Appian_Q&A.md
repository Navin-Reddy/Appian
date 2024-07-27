# Appian Q&A

## 1. Why should we use named parameters while invoking a rule/constant?
To provide clarity on which value is being mapped to which parameter so that if there is addition or omission of parameters in the future, the mapping isn't affected.

## 2. What is an environmental constant?
The env constant is used to store values specific to the environment. For example, we can have a constant called `IS_PROD` whose value will be true only in the production environment. The value of the env constant can be provided in the customization file during deployment.

## 3. Can array type constants be used for comparison of values?
No. This is because if the index of the values changes, the comparison can collapse.

## 4. What is the purpose of test cases in rules?
Test cases help viewers of the rule to test various pre-defined scenarios.

## 5. What is the function used to find the language of the logged-in user?
`userlocale()`

## 6. SAIL stands for
Self-Assembling Interface Layer

## 7. What is `a!save()` and `save!value`?
- `a!save()`: In interface `saveInto` parameters, `a!save()` updates the target with the given value. This function has no effect when called outside of a component's `saveInto` parameter.
- `save!value`: Holds the user inputted value on a temporary basis.

## 8. Will `saveInto` work for read-only fields?
No.

## 9. What is the difference between validation and validation group?
- **Validation**: Validation errors are displayed below the field when the value does not meet certain business conditions.
- **Validation Group**: Fields are validated only when a button in the same validation group is clicked.

## 10. What is the purpose of the `choiceValues` parameter of selection components?
The `choiceValues` parameter provides an array of values associated with the available choices. This is the value that gets stored when a choice is made.

## 11. What are the different ways to start a process?
1. Using Actions
2. Using Sites
3. Records (Action & Related Action)
4. Start Process
5. Sub process
6. Start Process Link
7. Start Form
8. Timer (Daily or nightly process)
9. Using Email
10. Using Web API
11. Using End/Terminate Node
12. Debugging Mode

## 12. Long activity chains - greater than 5 seconds between attended activities - are strongly discouraged because they have both an adverse effect on the performance of the system at scale and the experience of the user. True or False?
TRUE

## 13. What is a quick task?
A quick task is an on-demand task. The task does not appear in the task tab and can only be performed when activity is chained. If the task is closed without any action taken, it cannot be retrieved. The quick task stays ACTIVE when not performed. When quick task is enabled, a tilde (~) will be visible in the user input task.

## 14. What is the difference between escalation and exception?
- **Escalation**: Used to take an alternate approach/report it to others when a task isn't performed by the assignees after a certain time.
- **Exception**: Used to kill the task and proceed with the flow when the task isn't performed by the assignee after a certain time.

## 15. What is the difference between User Input Task and Process Start Form? When should one use Process Start Form?
- **Process Start Form**: Starts the instance only when a button with the `submit` attribute set to true is clicked. It avoids unnecessary instances and should be used when the user has the choice to submit the form, as it does not appear as a task in the task queue.
- **User Input Task**: Used when the task needs to be assigned to specific users.

## 16. What is the domain used to access the function variables in a function?
`fv!`

## 17. What is the domain used to suggest the data types in Appian?
`type!`

## 18. What is the output for the expression `0=tointeger({})`?
TRUE

## 19. What will be the result for the expression `a!pagingInfo(startIndex: _, batchSize: _)(1, 10)`?
`[startIndex=1, batchSize=10, sort=]`

## 20. When should XOR and OR gateways be used?
- **XOR**: Used when only the first true path should be executed based on the given conditions.
- **OR**: Used when all the true paths should be executed based on the given conditions.

## 21. What is the purpose of lane assignments?
Lane assignments provide assignments for unattended nodes (nodes with no user interaction). The assignment is given to "Whoever designed the process" because not all unattended nodes can be performed by the basic user. Designers have all privileges, so assignments are made in that manner.

## 22. Why should we build short-lived processes?
Short-lived processes are recommended because longer processes accumulate in the execution engine, taking up RAM space. Longer active processes use more engine space, which can lower system performance. Short-lived processes split various steps (initiation, approvals, etc.) into different models and are called using Start Process/asynchronous subprocesses, making the processes independent and not waiting for the child processes.

## 23. What is the difference between asynchronous subprocess and Start Process?
- **Asynchronous Subprocess**: The parent does not wait for the child to complete. Both the parent and child processes run in the same engine.
- **Start Process**: The parent does not wait for the child to complete. The parent and child processes run in the same or different engines based on the load (Appian has 3 execution engines by default).

## 24. What are the different types of Appian installations and state their differences?
- **On-Premise**: The physical hardware is with us and maintenance is also done by us.
- **On-Cloud**: The physical hardware is with Appian, and Appian handles the maintenance. The URL will have "appiancloud" in it.
- **Hybrid**: A combination of On-Premise and On-Cloud. For example, a training environment where the hardware is with Appian but maintenance is done by us.

## 25. What is an environment?
Any Appian installation is referred to as an environment.

## 26. What are the different licenses available and for what components are they provided?
- `k3.lic` for engines
- `k4.lic` for the data server

## 27. What is the purpose of content, personalization, execution, and analytic engines?
- **Process Execution**: Manages process execution and data for associated process models. Also referred to as exec, PX.
- **Process Analytics**: Stores information relevant for reports on a process. Also referred to as analytics, PA.
- **Content**: Stores metadata and security settings for documents and their organizational structures (communities, knowledge centers, and folders). The actual document content is stored on the file system. Also referred to as collaboration, collab, CO.
- **Personalization**: Stores information about users, groups, group membership, and group types. Also referred to as groups, PE.

## 28. Why can users be deleted or moved to another environment in Appian?
The license cost is based on the number of users per environment, and Appian maintains metadata based on users. Hence, users cannot be moved or deleted.

## 29. What is the output for the expression `milli(time(11,03,04,05)+1)`?
6

## 30. Can a related action shortcut be provided for all the views of a record?
Yes.

## 31. Can User filter have multiple selections for options?
Yes.

## 32. What is the range of filtered record list for which the "Export to Excel" button is disabled?
The button is enabled to export up to 100,000 records from the list, including rich text, images, and links.

## 33. What are the different ways to fetch details from a database?
1. Query DB smart service
2. Query Entity
3. Query rule (Deprecated)

## 34. What is a query Editor?
A tool to generate the coding of Query Entity.

## 35. What is the purpose of `fetchTotalCount` and provide a scenario where `fetchTotalCount` has to be true?
`fetchTotalCount` returns the total number of rows in a table based on the applied filters. This is usually set to false (i.e., when batch size is not -1) as it takes extra time to retrieve the total. Set to true when used in a Read-Only grid to calculate the total number of pages required.

## 36. When should one use filters instead of logical filters?
Use filters when the data is to be filtered based on only one condition.

## 37. Provide the ways to optimize the results of a query entity
1. Use selection to limit the number of columns to be returned.
2. Use filters wherever possible.
3. Use a limited batch size rather than -1.
4. Set `fetchTotalCount` to false.

## 38. Is an archived or deleted process available in the Process report?
No.

## 39. Will hidden variable data be displayed in the process report?
No.

## 40. What is a drilldown path in process reports?
The drilldown path provides additional info about a particular column of the report.

## 41. How many pages can be added in a site?
5

## 42. What is the purpose of user start page?
When configured, this allows the user to directly log in to the given site rather than the Tempo page.

## 43. What is the difference between process model and process?
- **Process Model:** The model is the object where the flow can be defined/designed.
- **Process:** Process/Instance is the implementation of the design.

## 44. For the given scenario, choose the efficient option.
*Scenario:* Interface to fill vehicle insurance details. There is a master field to capture the type of vehicle (Car/Bike etc.), and there are sets of fields that differ for the type of vehicle selected.
1. Hide the sequential fields and display only the set of fields that correspond to the selected vehicle type.
2. Display all the fields but keep them disabled. Enable only the set of fields that correspond to the selected vehicle type.  
**Answer:** Hide the sequential fields and display only the set of fields that correspond to the selected vehicle type.

## 45. What is the purpose of alerts in Process model?
Alerts in the model are used to notify the defined users about errors in the instance. The target users are the admins of the app as they are responsible for maintaining the app. This can be defined using a constant so that change management can be easier.

## 46. Why do we need the data management? When should one select the delete option in data management?
Data Management is used to clear the instances stored in the execution engine. The instance can either be archived or deleted. When there is no user interaction in a process, that process can be deleted. Data management happens only for completed or canceled instances.

## 47. What is the difference between end and terminate node? When to use End node?
- **End Node:** Completes only the path that hits it while all the other paths are active. This is used when the whole process is to be completed when all the other paths are completed.
- **Terminate Node:** Completes all the paths once it is hit. Even in a single flow, the terminate node is recommended as even the errored instances of the node are completed when the terminate node is hit.

## 48. When can the document uploaded in file upload component be accessed?
a. After uploading the document in the field  
b. After form submission  
**Answer:** After form submission

## 49. Which component can display time (hour, second, minute) but cannot take input?
`a!timeDisplayField()`

## 50. What is the purpose of the skipAutoFocus parameter in form layout? ("Don’t automatically focus on first input" attribute in Designer View)
Determines whether the first input will receive focus when a form loads. Default is false.

## 51. For the given scenario, choose the efficient option.
*Scenario:* Interface to fill vehicle insurance details. There is a master field to capture the type of vehicle (Car/Bike etc.), and there are sets of fields that differ for the type of vehicle selected.
1. Hide the sequential fields and display only the set of fields that correspond to the selected vehicle type.
2. Display all the fields but keep them disabled. Enable only the set of fields that correspond to the selected vehicle type.  
**Answer:** Hide the sequential fields and display only the set of fields that correspond to the selected vehicle type.

## 52. Why should the read-only grid's pagingInfo match the data's pagingInfo?
This is because the data has to be refreshed based on each page.

## 53. Can News be configured in sites?
Yes

## 54. Can page name be configured differently for different users?
Yes

## 55. What are the different types of navigation for sites? And what is recommended for what type of sites?
- **Mercury:** Used when the site has a single page when the page name need not be shown in the navigation bar.
- **Helium:** Typically used for sites with multiple pages and where the page names are part of the navigation.

## 56. What is the purpose of process report?
It provides information about the process models, process instances, or active tasks and other activities. This is mainly used for analysis purposes.

## 57. What are the different types of process report?
1. Process models
2. Process instances
3. Active tasks

## 58. What is the function used to get the results from process report?
`a!queryProcessAnalytics()`

## 59. Process reports inherit the security from which object in Appian?
Knowledge Center

## 60. What is the extension of the process report stored in Appian?
`.arf`

## 61. How many records will be displayed in the Feed style record list?
100

## 62. Can default value be set for User filters?
Yes

## 63. If a user belongs to multiple groups that have different start pages configured, his start page will be the highest one in the grid that corresponds to a group that he belongs to.
TRUE

## 64. What are the different datatypes available in Appian? Give examples for each.
1. **Primitive:** Int, Text, Date, DateTime
2. **Appian Object:** Application, Process Model
3. **Complex:** PagingInfo, DataSubset
4. **Custom Data Type**

## 65. Why do we need a CDT?
CDT is used to minimize the usage of numerous variables and as it represents the table structure, the data storage and retrieval in DB is easier.

## 66. What is Data store and entity?
- **Data Store:** Acts as a bridge between Appian and DB.
- **Entity:** Added in the data store and represents the table in DB.

## 67. Long Table & Column Names (longer than 27 characters) are truncated in which ways?
- Vowels are removed from the name, in the order of u, o, a, e, then i. Names that begin with a vowel retain that vowel only.
- The name is split using underscores.
- The longest segment of the name is trimmed.

## 68. What is the purpose of activity chaining? What is the maximum limit?
Activity chaining is used between more than one task performed by the same user so that the user can act upon the tasks without any delay. The maximum limit is default 50 and max 100 unattended nodes between two attended nodes.

## 69. When should an input and output of the node be used?
- **Input of Node:** Used when one needs to pass the input to the node for its functionality. The input can also be defined when the output of the node is to be manipulated.
- **Output of Node:** Used to take the results of the node's functionality or to customize our own outputs by manipulating the values.

## 70. What is the purpose of using the Stored Values in write to data store entity node's output?
It is to retrieve the output of the data stored in the DB along with the PK value when PK is auto-generated.

## 71. When a process with an active task is paused, will the task be available to the user to perform?
No. An error will be shown to the user when the task is opened.

## 72. Will timer node execute when the instance is paused?
Yes

## 73. When should local variables be used?
Local variables are used when the scope is within the interface/rule and the value need not go outside that object. They are also used to define the repetitive piece of code/function/rule.

## 74. What are the different ways to refresh a local variable?
Local variables can be refreshed in the following ways:
1. **refreshAlways:** When true, the value of this local variable will be refreshed after each user interaction and each interval refresh.
2. **refreshInterval:** How often the variable value gets refreshed in minutes. When null, the variable will not be refreshed on an interval. Valid values include 0.5, 1, 2, 3, 4, 5, 10, 30, 60.
3. **refreshOnReferencedVarChange:** When true, the value of this local variable will be refreshed each time the value of any variable it references within the value parameter is updated. Default is true.
4. **refreshOnVarChange:** Refreshes the value of the local variable each time any of these specific variables change. This allows you to refresh the value when a variable that is not referenced within the value parameter is updated.
5. **refreshAfter:** Refreshes the value of the local variable after a record action, such as a related action or a record list action configured within a record type, completes from a dialog window within the Record Action Component. Instead of requiring the entire page to reload, this parameter allows you to refresh a local variable value on an interface after a record action completes. Valid values include RECORD_ACTION.

## 75. Why shouldn’t an interface have more than 500 lines of code? How to reduce the number of lines of code?
More than 500 lines of code can lead to binding issues. This can be solved using modular coding.

## 76. What is the purpose of Set as Default test cases?
It will set the values given to an RI in the interface as default. Whenever the interface is opened, these values are assigned to the RI. This makes the testing of interfaces, especially read-only interfaces, easier.

## 77. What is a MNI and its best practices?
Multiple Node Instance (MNI) is used to create multiple instances of a node. This is done when the functionality of the node is to be repeated for various inputs. The best practice is to do a null check of the variable before the MNI and if the variable has more than 1000 values, it is recommended to do batch

## 78. What are the different types of records created in Appian?
1. Entity Backed Records
2. Service/Expression Backed Records
3. Process Backed Records

## 79. What is a data sync and when should I use it?
When data sync is enabled, you are caching your source data in Appian. With a cache of your data, this means Appian will only have to execute queries from the cached data instead of the external source whenever you view or interact with the record data. Refer here on when to use data sync.

## 80. When should default filters and user filters be used?
- **Default Filters:** Used when the filter has to be applied to the source while retrieving the data for the record type.
- **User Filters:** Applied by the user once the record type list is displayed.

## 81. How many additional views can be added to a record type?
Total 20 along with Summary view

## 82. What is the difference between an action and a related action?
- **Action:** Creates new data in the system.
- **Related Action:** Performs some action related to the existing data.

## 83. What are the different ways to create a CDT?
1. From Scratch
2. Duplicating the existing datatype
3. From database view or table
4. From XSD
5. From Web Services

## 84. When should a card layout be used?
Use card layouts to visually group related content.

## 85. When should a side-by-side layout be used?
The side-by-side layout is used for fine-grained control over the presentation of small groups of related components.

## 86. What should be the label position for read-only fields?
Adjacent/Justified

## 87. When the interface has several other components along with the grid, what should be the appropriate batch size of the grid?
5 - 10 items

## 88. What are the different ways to provide details about a field to a user?
- Help tooltip
- Placeholder
- Instructions

## 89. What are Gateways and their purpose?
Gateway nodes allow you to evaluate different criteria to make decisions on which path(s) your workflow should follow – as well as how many instances are allowed to follow each optional path. Click here to know about various gateways.

## 90. What is the difference between local variables and rule inputs?
- **Local Variables:** Used when the scope is within the interface/rule and the value need not go outside that object. They are also used to define the repetitive piece of code/function/rule.
- **Rule Inputs:** Used when the value has to be taken outside the object.

## 91. The process will immediately be archived or deleted after completion or cancellation by setting data management as ___
0

## 92. What are the exception types that can be configured?
- Timer
- Receive message

## 93. The triggers that can be added to a start event are:
- Receive Message
- Timer

## 94. Will a change in hidden variable be reflected in the Process History?
No

## 95. What is the difference between Task Assignee and Task Owner?
- **Task Assignees:** The people for whom the task is being assigned.
- **Task Owner:** The person who accepts a group task.

## 96. What should be the reassignment privilege for basic users?
The reassignment privilege should be No privilege as basic users should not have the ability to reassign the task to anyone in the system, and if reassignment is enabled, the tracking of it becomes difficult. This can be set in the Assignment tab of User input task under "Set Reassignment Privilege".

## 97. What is Save Draft?
Save Draft is an option available in the form to save the progress done by the user. Documents uploaded by the users won’t be saved as the document ID is generated only after the form is submitted. Save Draft does not complete the user input task node. This can be configured in the form's tab of the user input task.

## 98. Can the default task assignment mail be disabled?
Yes, under the assignment tab the option can be unchecked.

## 99. What are the benefits of modular coding?
1. Reusability of objects
2. Easy change management
3. Easy debugging
4. Reduced number of lines per interface

## 100. What is the maximum number of nodes and variables allowed per process model?
30 Nodes and 50 Variables

## 101. When should Web API, Integration/Web service be used?
- **Web API:** Should be used when Appian's data is to be exposed to the external system.
- **Integration/Web Service:** Used when external system's data is consumed by Appian.

## 102. When to use Web service and Integration?
- **Integration:** Used when the data returned by the external system is in REST structure.
- **Web Service:** Used when the data returned by the external system is in SOAP structure.

## 103. What is connected systems?
Connected Systems is an object to store the connection credentials used in integrations when connecting to an external system.

## 104. What are the things to be checked during deployment?
1. Missing Precedents
2. Security Summary
3. Proper exporting of all objects
4. Inspecting all objects and fixing issues if any
5. Importing the objects

## 105. What is a customization file?
The customization file is used to provide values to the environmental constant and connected systems when deploying to another environment so that the value changed isn't missed.
