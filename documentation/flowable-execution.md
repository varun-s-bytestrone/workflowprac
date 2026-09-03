- Flowable reads the BPMN XML definition of our process
- Each BPMN element has a corresponding behaviour inside the engine

BPMN Element
     ↓
Flowable identifies element type
     ↓
Corresponding Java behavior
     ↓
Execution logic

User Task example:

    <bpmn:userTask id="approveTask"
                   name="Approve Request"/> 
    
Flowable knows this is a UserTask

Service Task example:

    <bpmn:serviceTask id="paymentService"
                      flowable:delegateExpression=${paymentService"}/>

Flowable knows this is a service task and uses the configured delegation. On delegation, it calls the required Java bean, which executes the task.

@Component("paymentService")
public class PaymentService implements JavaDelegate {
    @Override 
    public void execute(DelegateExecution execution){
        System.out.println("Processing payment: ");
    }
}

When does Flowable execute something?

This is determined by the current execution positon, which is represented internally by an execution/process instance.

When the process starts: 
    ID: 12345
    Current activity: Start Event

After it starts: 
    Current activity: Task A

Suppose the current activity is a gateway:

<bpmn:sequenceFlow
    sourceRef="gateway"
    targetRef="taskB">

    <bpmn:conditionExpression>
        ${approved == true}
    </bpmn:conditionExpression>

</bpmn:sequenceFlow>

Flowable evaluates approved == true, and if it is true, it executes Task B, otherwise execute the other valid path.

