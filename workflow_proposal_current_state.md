```mermaid

sequenceDiagram
    WorkflowEngine ->> Agent: run_planning_plugin(planning_input)
    Agent ->> Agent: create_dataset()
    Agent ->> Agent: write_file_to_dataset(feature_0.cloud.ply)
    Agent ->> APIClient: get_part_template(part_template_id)
    APIClient ->> Agent: part_template
    Agent ->> APIClient: get_feature_template(feature_template_id)
    APIClient ->> Agent: feature_template
    Agent ->> Agent: launch_cell(cell_config,calibration,cell_parameters)
    Agent ->> Agent: add_mesh_to_scene()
    Agent ->> TaskPlanningWrapper: run_planning_plugin(feature, composite_cloud, part_template, feature_template)
    TaskPlanningWrapper ->> TaskPlanningWrapper: create_planning_goal(feature, composite_cloud, part_template, feature_template)
    TaskPlanningWrapper ->> TaskPlanningActionServer: execute_planning_goal(planning_goal)
    TaskPlanningActionServer ->> TaskPlanningActionServer: write_file_to_dataset(task_plan.yaml)
    TaskPlanningActionServer ->> TaskPlanningActionServer: write_file_to_dataset(planning_report.json)
    TaskPlanningActionServer ->> TaskPlanningWrapper: success
    TaskPlanningWrapper ->> Agent: success
    Agent ->> Agent: read_file_from_dataset(task_plan.yaml)
    Agent ->> Agent: read_file_from_dataset(planning_report.json)
    Agent ->> WorkflowEngine: {UNKNOWN}
```

### Notes:
- Reliance on filesystem for Inter-Process Communication
- Each instance of Agent needs to communicate with the API
- Launching all of Forge and the entire cell just to get access to planning
