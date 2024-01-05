git # Overview

This is how PartManager would interact with the services we provide
```mermaid
sequenceDiagram
    PartManager->>TaskPlanningService : plan(forge_planning_request)
    TaskPlanningService->>XPlanner : plan(generic_planning_request)
    XPlanner->>TaskPlanningService : generic_planning_response
    TaskPlanningService->>PartManager : forge_planning_response
```
This is how the WorkflowManager would interact with the services we provide
```mermaid

sequenceDiagram
WorkflowManager->>WorkflowAgent : plan(workflow_planning_request)
WorkflowAgent->>XPlanner : plan(generic_planning_request)
XPlanner->>WorkflowAgent : generic_planning_response
WorkflowAgent->>WorkflowManager : workflow_planning_response
```

### Messages:
```mermaid
classDiagram
    class ForgePlanningRequest{
        +URDF
        +SRDF
        +CellParameters
        +PlanningScene
        +Feature
        +CompositeCloud
        +Mesh
        +TaskParameters
    }

    class ForgePlanningResponse{
        +TaskPlan
    }

    class GenericPlanningRequest{
        +RobotRepresentation
        +Waypoint[]
        +WorldRepresentation
        +TaskParameters
    }

    class GenericPlanningResponse{
        +Trajectory
        +Pose[]
    }
```

### Notes:
- XPlanner is a service we will provide.
- We will also be responsible for the WorkflowAgent and TaskPlanningService
- We will have control over whether we build a different Agent/Service for each planner type

