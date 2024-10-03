<h1> Gitlab Cheetsheet</h1>

<h3> List of references <h3>

  1. [<small>Gitlab lab materials</small>](https://handbook.gitlab.com/handbook/customer-success/professional-services-engineering/education-services/gitlabcicdhandson/) 
  2. [List of pre-defined gitlab variables](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html)
  3. [Deep Dive into Review Apps](https://www.youtube.com/watch?v=HblSiPFamDI)
     
<h2> Case Studies </h2>

| Description | Code | Comments |
| :----- | :------ | :---- |
| Build and pushes a Docker image to a registry  |  <img width="600" alt="Screenshot 2024-09-18 at 18 43 21" src="https://github.com/user-attachments/assets/996424b8-86b3-4af9-abd7-fdd37af2f412">   | - `services` define additional Docker containers that will be run alongside the job <br> - `-dind` stands for "Docker in Docker," meaning a service that runs a Docker daemon inside a Docker container <br> - `DOCKER_TLS_CERTDIR: "/certs"` used for Docker's TLS (Transport Layer Security) feature. This ensures that the Docker daemon runs securely by generating and using certificates for communication|
|Upload a docker image to the  GitLab Container Registry|<img width="400" alt="Screenshot 2024-10-02 at 23 41 33" src="https://github.com/user-attachments/assets/3a1c8874-dda4-4694-aa84-edb21148ea12">| - In the left navigation pane, click Deploy > Container Registry and view the container that was just uploaded by the build image job.|
| Configure manual deployment on a production server |   <img width="400" alt="Screenshot 2024-09-22 at 13 33 35" src="https://github.com/user-attachments/assets/b1462d41-b9e1-49c1-931c-29fad9cd7d97">   | - [List of pre-defined gitlab variables](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html) <br> - `$CI_COMMIT_BRANCH`: This variable holds the name of the branch that the current commit belongs to <br> - `$CI_DEFAULT_BRANCH`: This variable holds the name of the default branch of your project. In most cases, the default branch is main or master <br> - job will only run if the current commit is made on the default branch. |
| Only trigger builds for services that have changes in their respective directories? | <img width="400" alt="Screenshot 2024-10-02 at 15 19 51" src="https://github.com/user-attachments/assets/ac91e368-fa1c-42f6-a346-e23704f04eff"> |  | 
| Stop an environment when a merge request is merged or closed | <img width="400" alt="Screenshot 2024-09-22 at 13 40 51" src="https://github.com/user-attachments/assets/233bc43e-2e69-40f7-a4c7-b2df143f7aec"> |  |
| Adding SAST | <img width="400" alt="Screenshot 2024-10-02 at 15 30 11" src="https://github.com/user-attachments/assets/ba938f50-6055-43eb-92ce-a9ae61dec88c"> |  - [<small>reference</small>](https://docs.gitlab.com/ee/user/application_security/sast/) <br> - To view the results of the SAST scan, click Secure > Vulnerability Report in the left-hand navigation pane. In the Tool drop-down list, select SAST. Click on any vulnerabilities to learn more about them.|
|Trigger a deployment job only when a commit is tagged with a version number|<img width="400" alt="Screenshot 2024-09-22 at 22 41 16" src="https://github.com/user-attachments/assets/c836e712-6c84-464e-a435-157827c1176c">||
|Install gitlab runner properly|[Hands-on Lab](https://handbook.gitlab.com/handbook/customer-success/professional-services-engineering/education-services/gitlabcicdhandsonlab2/)| **Steps** - Install Gitlab Runner <br> -Register an individual runner|
| Run multiple jobs in parallel with different combinations of variables | <img width="400" alt="Screenshot 2024-10-02 at 16 18 35" src="https://github.com/user-attachments/assets/080a5e68-e569-47a7-9a37-2dbf470a9035">| The job will run 4 times, once for each combination of `OS` and `TOOL_VERSION` |
|| <img width="400" alt="Screenshot 2024-10-02 at 16 20 36" src="https://github.com/user-attachments/assets/f810f735-135e-4080-b826-4e385a63817e">| This results in four parallel jobs|
|Add code quality scanning||- On the pipeline details screen, click the Code Quality tab above the pipeline graph|
|Job templates|||
|The job will not run if the pipeline is triggered on the main branch or by a git tag|<img width="400" alt="Screenshot 2024-10-02 at 23 52 30" src="https://github.com/user-attachments/assets/2e4a2c2a-68b1-4044-b3c8-e614fbb257dc">||
|Create a new tag|- click on Code > Tags <br> - Click on the New tag button. <br> - Type in v1.0 into the Tag name section. <br> - Click the Create tag button||



