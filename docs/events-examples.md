# Event Samples

## 1. Application Start

As the application starts, a new event is published with the process definition. 

| #  | Action                        | Event Type             | Event                                                                                                       |
|----|-------------------------------|------------------------|-------------------------------------------------------------------------------------------------------------|
| 1  | Process definition registered | ProcessDefinitionEvent | ```json { "id": "df9d0498-e5ca-4cef-b1ec-5c795cb2efa9", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessDefinitionEvent", "time": "2024-07-17T17:22:40.107127-03:00", "data": { "id": "ccapplicationapproval", "name": "ccapplicationapproval", "version": "1.0", "type": "BPMN" }} ``` |

## 2. New Process Instance

New instance is created, nodes are executed per definnition reaching the user task.

| #  | Action                   | Event Type                       | Event                                                                                                       |
|----|--------------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------|
| 1  | Process instance created | ProcessInstanceStateDataEvent    | ```json { "id": "df900d05-0641-4063-9e37-3e3648465e44", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceStateDataEvent", "time": "2024-07-17T17:25:21.93199-03:00", "data": { "eventDate": "2024-07-17T17:25:21.931-03:00", "state": 1 }} ```                                           |
| 2  | Start node               | ProcessInstanceNodeDataEvent     | ```json { "id": "6b969407-d2b6-4108-aece-6982cc5e9abb", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceNodeDataEvent", "time": "2024-07-17T17:25:21.806167-03:00", "data": { "nodeName": "Start", "nodeType": "StartNode" }} ```                                |
| 3  | Variable initialization  | ProcessInstanceVariableDataEvent | ```json { "id": "9671402c-1eed-44fe-b34a-b9e45df0b6e2", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceVariableDataEvent", "time": "2024-07-17T17:25:21.79579-03:00", "data": { "variableName": "applicant", "variableValue": {"name": "Ian V.", "annualIncome": 50000, "creditScore": 500, "age": 50, "student": false} }} ``` |
| 4  | Script task execution    | ProcessInstanceNodeDataEvent     | ```json { "id": "d1786395-c9b1-403f-a4c0-b07941d31552", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceNodeDataEvent", "time": "2024-07-17T17:25:21.859794-03:00", "data": { "nodeName": "Log application received", "nodeType": "ActionNode" }} ```        |
| 5  | Decision task execution  | ProcessInstanceNodeDataEvent     | ```json { "id": "f2196fa2-3fb2-4cfd-9222-b4c15d2e225a", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceNodeDataEvent", "time": "2024-07-17T17:25:21.870189-03:00", "data": { "nodeName": "Credit Card Eligibility", "nodeType": "RuleSetNode" }} ```        |
| 6  | Variable update          | ProcessInstanceVariableDataEvent | ```json { "id": "363f5f4d-c491-4f8b-a56d-7fe45a85851f", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceVariableDataEvent", "time": "2024-07-17T17:25:21.915821-03:00", "data": { "variableName": "approval", "variableValue": "manual" }} ```                 |
| 7  | Gateway                  | ProcessInstanceNodeDataEvent     | ```json { "id": "8582d125-e2c0-4589-968e-952a9aa7c730", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceNodeDataEvent", "time": "2024-07-17T17:25:21.916781-03:00", "data": { "nodeName": "Split", "nodeType": "Split" }} ```                                |
| 8  | User task ready          | UserTaskInstanceStateDataEvent   | ```json { "id": "781bd118-c243-402e-b792-5ae48b72cf94", "source": "http://localhost:8080/ccapplicationapproval", "type": "UserTaskInstanceStateDataEvent", "time": "2024-07-17T17:25:21.931179-03:00", "data": { "userTaskName": "reviewApplication", "state": "Ready" }} ```                |

## 3. User Task Execution

User claims and complets the task with an update to one of the process variables.

| #  | Action                   | Event Type                       | Event                                                                                                       |
|----|--------------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------|
| 9  | User task assignment     | UserTaskInstanceAssignmentDataEvent | ```json { "id": "449629bc-2131-4c7a-b709-b4a51540dc78", "source": "http://localhost:8080/ccapplicationapproval", "type": "UserTaskInstanceAssignmentDataEvent", "time": "2024-07-17T17:25:21.928683-03:00", "data": { "userTaskName": "reviewApplication", "assignmentType": "USER_OWNERS", "users": ["jdoe"] }} ``` |
| 10 | User task claim          | UserTaskInstanceStateDataEvent   | ```json { "id": "d6892ac9-0db4-471e-9f34-96cbcde2b675", "source": "http://localhost:8080/ccapplicationapproval", "type": "UserTaskInstanceStateDataEvent", "time": "2024-07-17T17:26:59.051737-03:00", "data": { "userTaskName": "reviewApplication", "state": "Reserved", "actualOwner": "jdoe" }} ```        |
| 11 | User task variable update | UserTaskInstanceVariableDataEvent | ```json { "id": "580823d9-6fa1-4124-ba58-89400e2ad613", "source": "http://localhost:8080/ccapplicationapproval", "type": "UserTaskInstanceVariableDataEvent", "time": "2024-07-17T17:26:59.052167-03:00", "data": { "variableName": "approval", "variableValue": null }} ```                   |
| 12 | User task completion     | UserTaskInstanceStateDataEvent   | ```json { "id": "73ea4cd7-86a4-48f1-9f6b-2f8b6f832283", "source": "http://localhost:8080/ccapplicationapproval", "type": "UserTaskInstanceStateDataEvent", "time": "2024-07-17T16:04:51.265739-03:00", "data": { "userTaskName": "reviewApplication", "state": "Completed", "actualOwner": "jdoe" }} ```        |
| 13 | Process variable update  | ProcessInstanceVariableDataEvent | ```json { "id": "25874e99-6168-4b5f-bd3f-ff0e8ff19713", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceVariableDataEvent", "time": "2024-07-17T17:28:42.746515-03:00", "data": { "variableName": "approval", "variableValue": "Approved" }} ```                 |

## 4. Process Continues After User Task

The process moves forward after user task completion; Following tasks are executed until it reaching the end event.

| #  | Action                   | Event Type                       | Event                                                                                                       |
|----|--------------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------|
| 14 | Gateway                  | ProcessInstanceNodeDataEvent     | ```json { "id": "0cedd95e-c06c-4172-8a3a-5b4a7c893334", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceNodeDataEvent", "time": "2024-07-17T17:28:42.749226-03:00", "data": { "nodeName": "Split", "nodeType": "Split" }} ```                   |
| 15 | Service task execution   | ProcessInstanceNodeDataEvent     | ```json { "id": "7f0a9ccd-ec38-4dab-8300-8b3c64c44127", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceNodeDataEvent", "time": "2024-07-17T17:28:42.785997-03:00", "data": { "nodeName": "Generate CC Details", "nodeType": "WorkItemNode" }} ```                   |
| 16 | Variable update from service | ProcessInstanceVariableDataEvent | ```json { "id": "30ca0e96-892c-42e1-9355-dbe371b06fed", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceVariableDataEvent", "time": "2024-07-17T17:28:42.795168-03:00", "data": { "variableName": "creditCard", "variableValue": { "cardNumber": "4633589679941394", "cardHolderName": "Ian V.", "expirationDate": "2027-07-17", "cvv": "096", "creditLimit": 15000.0 } }} ```                 |
| 17 | End node                 | ProcessInstanceNodeDataEvent     | ```json { "id": "8c8fb70d-4cf4-47ea-a15b-43b3793e7e77", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceNodeDataEvent", "time": "2024-07-17T17:28:42.815301-03:00", "data": { "nodeName": "Approved", "nodeType": "EndNode" }} ```             |
| 18 | Process instance completion | ProcessInstanceStateDataEvent  | ```json { "id": "03e70e3a-9029-4462-b047-21ace3eb5ff1", "source": "http://localhost:8080/ccapplicationapproval", "type": "ProcessInstanceStateDataEvent", "time": "2024-07-17T17:28:42.810984-03:00", "data": { "state": 2 }} ```                                 |

