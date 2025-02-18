<h1> Airflow Fundamentals Exam</h1>

<h2> Important Reference</h2>

1. [Apache-Airflow-Fundamentals-Study-Guide](https://www.astronomer.io/uploads/Apache-Airflow-Fundamentals-Study-Guide.pdf)
2. [Sample exam questions](https://medium.com/@ansam.yousry/test-your-knowledge-70-questions-on-apache-airflow-fundamentals-8bcb9dda6127)

<h2> Curriculum </h2>

<h3> Topic 2: Airflow Concepts </h3>

<img width="1034" alt="Screenshot 2025-02-17 at 00 23 20" src="https://github.com/user-attachments/assets/3d9f8516-685d-4a53-a54a-74440658df3b" />

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|2.1| Identify which folder the Airflow Scheduler parses when searching for new DAG files| - The Airflow Scheduler parses DAG files from the `DAGs folder`, which is specified by the dags_folder configuration in the Airflow configuration file (`airflow.cfg`). </br> - By default, the DAGs folder is: `~/airflow/dags` </br> - The folder can contain subdirectories, and Airflow will parse them as well.| 
|2.2| Identify what an Airflow provider is| - An Airflow provider is a package that extends Apache Airflow’s functionality by adding integrations with external services, tools, or systems. </br> - include hooks, operators, sensors, and connections that allow Airflow to interact with cloud services, databases, APIs, and other technologies.| 
|2.3| Identify what a DAG run is| [DAG run](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/dag-run.html) </br> - an object representing an instantiation of the DAG in time </br> - A DAG run is usually scheduled after its associated data interval has ended, to ensure the run is able to collect all the data within the time period </br> - a DAG run will only be scheduled one interval after start_date| 
|2.4| Identify the role of a worker in Airflow|| 
|2.5| Identify which programming language Airflow primarily uses. | Python| 
|2.6| Identify the purpose of an XCom|| 
|2.7| Identify the purpose of a DAG|| 
|2.8| Identify the purpose of the DAG parameter| [DAG level parameter](https://www.astronomer.io/docs/learn/airflow-dag-parameters/) </br> - affect how the entire DAG behaves| 
|2.9|  Identify the default time zone of an Airflow instance|- The time zone is set in **airflow.cfg** </br> - By default it is set to UTC </br> - [Timezone](https://airflow.apache.org/docs/apache-airflow/stable/authoring-and-scheduling/timezone.html)| 
|2.10| Identify the role of an executor in Airflow|| 
|2.11| Identify the core architectural components of Airflow|| 
|2.12| Identify the typical journey of a task|| 
|2.13| Identify what happens when two DAGs share the same `dag_id`| - When using the @dag decorator and not providing the `dag_id` parameter name, the function name is used as the dag_id </br> - When using the DAG class, this parameter is required </br> - [Airflow Dag Parameters](https://www.astronomer.io/docs/learn/airflow-dag-parameters/) </br> - If two DAG files define the same dag_id, the last one parsed by the scheduler will overwrite the previous one. </br> - If two separate DAG files share the same dag_id, tasks from one DAG might be interpreted as belonging to the other DAG.| 
|2.14| Identify optional and non-optional DAG parameters. | [Airflow Dag Parameters](https://www.astronomer.io/docs/learn/airflow-dag-parameters/)| 
|2.15| Identify what each of the task lifecycle stages does| <img width="500" alt="Screenshot 2025-02-16 at 22 51 17" src="https://github.com/user-attachments/assets/79c2baca-c752-4767-9a88-e53265cd2a85" />
|2.16| Identify valid ways to define a DAG in Airflow.| - TaskFlow API </br> - Traditional syntax </br> NB: can be mixed | 
|| Miscellaneous| - Airflow does not provide versioning features </br> - Airflow can be used for data orchestration in multi-cloud environments. </br> - Airflow is primarily designed for batch processing | 


<h3> Topic 3: Dependencies </h3>

**Reference**
1. [Notes on DAG dependencies](https://github.com/ovimihai/airflow-cert-dag-authoring/blob/main/notes/5_dag_dependencies.md)
2. [Managing Dependencies](https://www.astronomer.io/docs/learn/managing-dependencies/?tab=taskflow#dependencies-in-dynamic-task-mapping)
3. [Cross-dag-dependencies](https://www.astronomer.io/docs/learn/cross-dag-dependencies/)
4. [Trigger Rules](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/dags.html#trigger-rules)

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|3.1| Identify the purpose of task-level dependencies in Airflow|- **Upstream task:** A task that must reach a specified state before a dependent task can run. </br> - **Downstream task:** A dependent task that cannot run until an upstream task reaches a specified state. </br></br> **Miscellaneous**</br> - the tasks that are dependent on the output of other tasks through xcom variables require the preceding task to execute successfully first.</br></br>**Dynamic Task Mapping**</br> - DAGs that dynamically generate parallel tasks at runtime </br> - allows to create tasks based on the current runtime environment without having to change the DAG code </br> MapReduce model: DAG can create an arbitrary number of parallel tasks at runtime based on some input parameter (the map), and then if needed, have a single task downstream of your parallel mapped tasks that depends on their output (the reduce) </br> - can create dynamic tasks only if Airflow knows the parameters beforehand</br> - can't </br> - create tasks pased on other tasks output </br> - can create tasks based on a dictionary or a variable or even on some connection in the database</br></br> **Trigger Rules**</br> - `all_success: (default)` The task runs only when all upstream tasks have succeeded. </br> - `all_done`: The task runs once all upstream tasks are done with their execution (either succeeded or failed). </br> - `none_failed_min_one_success`: The task runs only when all upstream tasks have not failed or upstream_failed, and at least one upstream task has succeeded. </br></br> task-level dependencies define the execution order and relationships between tasks in a Directed Acyclic Graph (DAG). Their primary purposes include:</br> - **Ensuring Correct Execution Order**:Dependencies control when a task should run relative to others, ensuring that prerequisites are completed before execution.</br> - **Data Flow Management**: Dependencies help manage how data moves between tasks, ensuring that output from one task is available before the next task starts.</br> - **Handling Failures and Retries**: By enforcing dependencies, Airflow can handle failures more effectively, allowing downstream tasks to wait until upstream tasks succeed.</br> - **Parallelism and Concurrency Optimization**: Dependencies allow independent tasks to run in parallel, improving DAG execution efficiency.</br> - **Managing Conditional and Dynamic Workflows**: Airflow supports conditional branching and dynamic DAG generation using dependencies, enabling complex workflows.| 
|3.2| Identify where DAG dependencies are set up in Airflow| `t0.set_downstream(t1)`</br>`t1.set_upstream(t0)`</br>`t0 >> t1` </br>`t1 << t0`</br><img width="271" alt="Screenshot 2025-02-18 at 00 54 18" src="https://github.com/user-attachments/assets/a64889c8-fba9-4420-8215-72cb4aa42f24" /> </br></br>**Dependency functions**</br> - utilities that let you set dependencies between several tasks or lists of tasks </br> - To set parallel dependencies between tasks and lists of tasks of the same length, use the `chain()`  <img width="454" alt="Screenshot 2025-02-18 at 00 57 44" src="https://github.com/user-attachments/assets/ff45ae6a-ae24-4c39-b775-edf13400216f" /> <img width="775" alt="Screenshot 2025-02-18 at 00 58 23" src="https://github.com/user-attachments/assets/3402c447-5b2d-4edf-bf8b-70142c57c9dc" /> - To set interconnected dependencies between tasks and lists of tasks: `chain_linear()`<img width="798" alt="Screenshot 2025-02-18 at 01 00 29" src="https://github.com/user-attachments/assets/b8dc93f6-8e24-448f-85e5-29d5d964e296" /> </br> - Dependencies for dynamically mapped tasks can be set in the same way as regular tasks. </br> - The dependencies between the task group and the start and end tasks are set within the DAG's context `(t0 >> tg1() >> t3)`|
|3.3| Compare and contrast DAG task dependency relationships for equivalency|| 
|3.4| Match DAG task dependency graphs to their equivalent DAG dependency code. || 


<h3> Topic 4: Airflow CLI </h3>

<img width="919" alt="Screenshot 2025-02-17 at 00 23 56" src="https://github.com/user-attachments/assets/271dbc0f-dcfd-4abf-b20f-f071e80ac72a" />

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|4.1|Identify the purpose of specific Airflow CLI commands: ||
|4.2| `airflow tasks test`||
|4.3|`airflow db init`||
|4.4|`airflow info`||
|4.5| `airflow tasks test`||
|4.6| `airflow config list`||
|4.7| `airflow cheat sheet`||
|4.8| `airflow variables`||
|4.9| `airflow users`||
|4.10| `airflow standalone`||
|4.11| `airflow version` ||
|4.12| Identify the impact of using the Airflow CLI command with a DAG that has an XCom.||

<h3> Topic 5: Airflow UI </h3>

[UI / Screenshots](https://airflow.apache.org/docs/apache-airflow/stable/ui.html)

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|| Identify the most helpful Airflow UI view to use for real-world scenarios ||
|| Grid view | - A bar chart and grid representation of the DAG that spans across time </br> - top row: a chart of DAG Runs by duration|
|| Graph view | - Visualize your DAG’s dependencies and their current status for a specific run|
|| Gantt view | - analyse task duration and overlap </br> - can quickly identify bottlenecks and where the bulk of the time is spent for specific DAG runs|
|| DAGs view | - List of the DAGs in your environment </br> - a set of shortcuts to useful pages </br> - can see exactly how many tasks succeeded, failed, or are currently running at a glance|
|| Landing times view | - The landing time for a task instance is the delta between the dag run’s data interval end (typically this means when the dag “should” run) and the dag run completion time.|
|| Tree view ||
|| Calendar view | -  an overview of your entire DAG’s history over months or even years|
|| Identify the default time for DAGs to appear in the Airflow UI | The time it takes for a DAG to show up depends on the scheduler's DAG parsing interval. </br> **Key Configuration Parameters Affecting DAG Visibility** </br> - `dag_dir_list_interval` (Default: 30 seconds)</br>&nbsp;&nbsp; - controls how often Airflow scans the `dags_folder` for new DAG files.</br>&nbsp;&nbsp; - If a new DAG is added, it will be detected within 30 seconds by default.</br> - `min_file_process_interval` (Default: 30 seconds)</br>&nbsp;&nbsp; - how often each DAG file is reprocessed.</br>&nbsp;&nbsp; - how quickly updates to DAGs are reflected in the UI.</br> - `scheduler_heartbeat_sec` (Default: 5 seconds)</br>&nbsp;&nbsp; - Determines how often the scheduler checks for changes in DAGs.|
|| Identify the result of deleting a DAG using the Airflow UI ||
|| Identify the purpose of core Airflow UI components (e.g., The Last Run Column ||
|| Given a specific Airflow UI, identify solutions to common issues.  ||

<h3> Topic 6: DAG Scheduling </h3>

1. [Notes on Scheduling](https://github.com/ovimihai/airflow-cert-dag-authoring/blob/main/notes/1_the_basics.md)

What is the default scheduler used in Airflow? Sequential Scheduler
 What happens if a task misses its scheduled execution time in Airflow?

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|| Identify the purpose of each DAG scheduling parameter ||
|| `catchup` ||
|| `start_date` ||
|| `end_date` ||
|| `schedule_interval` ||
|| Identify which tools/commands make it possible to backfill DAGs when the parameter is set to ||
|| Identify the default value for the parameter ||
|| Identify the valid values a DAG can accept for its parameter ||
|| Given a specific DAG scheduling goal (e.g., Schedule a DAG every day at 2 PM), identify the correct DAG scheduling parameter values to accomplish the goall ||
|| Given specific DAG scheduling parameter values, identify if a specific scheduling goal will be accomplished ||

`schedule_interval=None`, which means it is not set to run automatically at any specific interval. Instead, it needs to be triggered manually for execution.

<h3> Topic 7: DAG Runs </h3>

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|| Given a specific DAG scheduling scenario or DAG code, identify the number of DAG runs that will occur ||

<h3> Topic 8: Debugging </h3>

<h3> Topic 9: XComs </h3>

1. [Notes on XComs](https://github.com/ovimihai/airflow-cert-dag-authoring/blob/main/notes/3_taskflow_api.md)

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|| Identify the purpose of each XCom method: ||
|| `xcom push` ||
|| `xcom pull` ||
|| Identify the limitations of using XComs ||

<h3> Topic 10: Operators </h3>

1. [Operators](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/operators.html)
2. [Operators and Hooks](https://airflow.apache.org/docs/apache-airflow-providers/operators-and-hooks-ref/index.html)

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|10.1| Identify what a Transfer Operator does || 
|10.2| Identify what a Sensor Operator does || 
|10.3| Identify the purpose of the Airflow `PythonOperator` || 
| | Other Operators |BranchPythonOperator, TriggerDagRunOperator | 
|| Custom Operators | subcalss BaseOperator | 


<h3> Topic 11: Best Practices </h3>

<h3> Topic 12: Connections </h3>

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|| Identify the different ways to create an Airflow connection ||
||Identify the correct way to create an Airflow connection in a fil? ||
|| Given a specific Airflow connection string, identify the connection ID ||

<h3> Topic 14: Sensors </h3>

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|| Identify the default timeout value of a senso ||
|| Identify the mode to use in a DAG when the DAGs poke_interval parameter value is set to specific durationsl ||
|| Given the code for a sensor in a DAG, identify if the sensor is properly configured to accomplish a specific goal. ||

 ExternalTaskSensor 

<h3> Topic 15: Variables </h3>

<img width="815" alt="Screenshot 2025-02-17 at 00 22 39" src="https://github.com/user-attachments/assets/30a91786-04b8-49dd-8fe0-af667bfd50a0" />

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|15.1| Identify the purpose of an Airflow variabl? || 
|15.2| Identify the types of data that can be stored in a variable? || 
|15.3| Identify the correct way to define a variable with a specific value in Airflow || 
|15.4| Identify how to fetch the value of an Airflow variable in specific formats (e.g., JSON || 
|15.5| Given a specific variable name, Identify if a variable will be visible in the Airflow UI || 

<h2> Additional Topics </h2>

| | Topic| Notes &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|:------| :------ |:---- |
|Task instance parameters| trigger_rule |"all_failed"| 
||"depends_on_past"||
| default_args parameter |||
||Airflow environment variables|[Configuration References](https://airflow.apache.org/docs/apache-airflow/stable/configurations-ref.html)</br>- AIRFLOW_HOME |
|| concurrency parameter in airflow.cfg||
|| SMTP setting||
| Parameters |||
||  Celery Executor:||||

<h2> Case Studies </h2>

<h2> Code Snippets </h2>

<h2> Miscellaneous </h2>



 




