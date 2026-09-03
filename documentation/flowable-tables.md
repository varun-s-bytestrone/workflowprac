Flowable uses tables to persist process definitions,tasks,history,jobs, and other workflow data. Data is not only stored in memory, it is persisted to survive application restarts, server crashes, long workflows, etc.

Repository Tables

These store BPMN process definitions and deployed resources.
Any process which is under execution/executed is a deployed resource.

    ACT_RE_DEPLOYMENT

    These tables store deployment information. ID, Name, Deployment Time

    ACT_RE_PROCDEF

    These tables store process definitions. ID, KEY, NAME, VERSION

    ACT_GE_BYTEARRAY

    Stores binary resources such as BPMN XML files, Process diagrams, Other deployment resources

Runtime Tables

They store information about currently running process instances.

    ACT_RU_EXECUTION

    These tables store process executions. Process, Instnace ID, Current Activity, Status

    ACT_RU_TASK

    These tables store active user tasks. ID, name, assignee, process_instance_id

    ACT_RU_VARIABLE

    Stores variables belonging to active processes. These variables can be conditional variables, can be used in Service tasks, scripts, etc.

    ACT_RU_EVENT_SUBSCR

    Stores event subscriptions. For example, a process is waiting for PaymentReceived. Flowable stores the subscription so that when the appropriate event arrives, it knows which process execution should continue.

History Tables

They store information about what has already happened.

    ACT_HI_PROCINST

    Stores completed or historically tracked process instances.

    ACT_HI_ACTINST

    Stores individual activiy executions.

    ACT_HI_TASKINST

    Stores historical task information.

    ACT_HI_VARINST

    Stores historical variable values.

General Tables

They store engine level values such as ACT_GE_PROPERTY which contains schema.version

Job Tables

Some activities should not execute immediately, i.e asynchronous execution, they are stored in job tables.

    ACT_RU_JOB
    ACT_RU_TIMER_JOB
    ACT_RU_SUSPENDED_JOB
    etc.

Identity Tables

These tables store users and groups

    ACT_ID_USER
    ACT_ID_GROUP
    ACT_ID_MEMBERSHIP   




