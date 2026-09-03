Understanding BPMN Workflows and execution

What is BPMN?

Business Process Model and Notation is a graphical notation used to represent workflows. These diagrams can show :\

- What steps are performed
- Who performs them
- What decisions are made
- How different systems communicate
- What happens when errors or special events occur

Core Components of a BPMN workflow :

- Events
    - Events represent something that happens during a process
    - Start Event -> Indicates when the workflow begins
    - Intermediate Event -> Occurs during the workflow -> can be a timer expiry, an error, etc.
    - End Event -> Indicates that a process has finished
- Activities
    - Activities represent work that needs to be performed
    - Task is a single unit of work
        - Approve request
        - Send email
        - Process payment
    - User Task -> a human performs the task, in BPMN, the workflow may pause until a user completes the task
    - Service Task -> an automated system performs the task -> workflow engine can execute Java code or call an API
    - Script Task -> A script performs some logic -> Calculate total cost
    - Subprocess -> Groups multiple activities into a larger logical process -> process payment -> validate order +      process order + ship product
- Gateways
    - Controls how the workflow flows
    - Diamond shaped in the UI
    - Exclusive Gateway (X0R) -> Used when only one path should be selected -> Is payment valid -> Either yes or no
    - Parallel Gateway (AND) -> Used when multiple paths can run at a time -> payment completed -> Send mail + update DB
    - Inclusive Gateway (OR) -> Allows one or more paths to be selected based on a condition
- Sequence Flows
    - Determines the order in what activities/tasks occur
    - Conditional Flows can also be modeled using this
- Particaipants and Pools
    - Pool represents a major participant, such as an organization
    - Lanes are used to divide a pool according to users, departments, or roles

How do Engines like Flowable run this?

BPMN diagram is primarily a process definition. A BPMN engine interprets the definition and manages the execution.

The usual flow looks like :

                          BPMN Diagram
                               ↓
                        Deploy to Flowable
                               ↓
                      Create Process Instance
                               ↓
                        Execute Activities
                               ↓
                    Wait at User Tasks / Events
                               ↓
               Continue Based on Events or Decisions
                               ↓
                         Process Ends

If we have a simple task such as Start -> Service Task -> User Task -> Gateway -> End

Execution :

Start -> runtimeService.startProcessInstanceByKey("leaveApproval")
This starts the process by referring to the required key.

Service Task automatically executes according to configured logic, while User Task might wait for the human in the loop to finish execution.

Gateway might have condition such as approved == true? and accordingly, the engine chooses the output