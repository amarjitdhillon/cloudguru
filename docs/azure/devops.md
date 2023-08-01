
# Azure Devops

Azure Pipelines supports continuous integration (CI) and continuous delivery (CD) to continuously test, build, and deploy your code. You accomplish this by defining a pipeline.

!!! question "What is CI/CD?"
    `Continuous integration (CI)` automates tests and builds for your project. CI helps to catch bugs or issues early in the development cycle, when they're easier and faster to fix. Items known as `artifacts` are produced from CI systems. They're used by the continuous delivery release pipelines to drive automatic deployments.

    `Continuous delivery` automatically deploys and tests code in multiple stages to help drive quality. 




## Concepts

<center> <img src="../images/key-concepts-az-devops.svg" width="90%"> </center>

### Trigger

 A `trigger` tells a Pipeline to run. Examples: build triggers and release triggers 

### Pipeline
 A `pipeline` is made up of one or more stages. A pipeline can deploy to one or more environments.

### Stage
 A `stage` is a way of organizing jobs in a pipeline and each stage can have one or more jobs.

!!! tldr
    A stage is a logical boundary in the pipeline. It can be used to mark separation of concerns (for example, Build, QA, and production). Each stage contains one or more jobs. When you define multiple stages in a pipeline, by default, they run one after the other. You can specify the conditions for when a stage runs.

### Job
Each `job` runs on one agent. ==A job can also be agentless.==

!!! tip
    Each job runs on an agent. A job represents an execution boundary of a set of steps. All of the steps run together on the same agent. Jobs are most useful when you want to run a series of steps in different environments


### Agent
Each `agent` runs a job that contains one or more steps. An agent is computing infrastructure with installed agent software that runs one job at a time. For example, your job could run on a Microsoft-hosted Ubuntu agent.


!!! remember
    The agent communicates with Azure Pipelines or Azure DevOps Server to determine which job it needs to run, and to report the logs and job status. This communication is always initiated by the agent. 

There are 2 types of Agents as explained below:

#### Microsoft Hosted agents

<center> <img src="../images/amardhillon_diagrams-devops_agent.drawio.png" width="90%"> </center>


- If your pipelines are in Azure Pipelines, then you've got a convenient option to run your jobs using a Microsoft-hosted agent.

!!! info "Managed solution"
    With Microsoft-hosted agents, maintenance and upgrades are taken care of for you. Each time you run a pipeline, you get a fresh virtual machine for each job in the pipeline. The virtual machine is discarded after one job (which means any change that a job makes to the virtual machine file system, such as checking out code, will be unavailable to the next job). Microsoft-hosted agents can run jobs directly on the VM or in a container.


#### Self hosted agent 

- An agent that you set up and manage on your own to run jobs is a self-hosted agent.  
- Self-hosted agents give you more control to install dependent software needed for your builds and deployments
- Also, machine-level caches and configuration persist from run to run, which can boost speed.

!!! info "When to use self hosted agents?"

    Below are the scenarios in which you should look at configuring Self-Hosted Agents

      1. If 10GB free space in the Virtual Machine (Agent) is not sufficient for your build needs.
      2. When you want a `Virtual Machine`, whose capacity is greater than of `Standard DS2V2`
      3. When you would like to use a Software that is not available in the `Microsoft hosted Build Agents`

##### Agent modes 

You can run your self-hosted agent as either 

1. Service 
2. Interactive process.
 
After you've configured the agent, we recommend you first try it in `interactive mode` to make sure it works. 

### Step
A `step` can be a task or script and is the `smallest building block of a pipeline`.

### Task
A `task` is a pre-packaged script that performs an action, such as invoking a REST API or publishing a build - artifact.

### Artifact
An `artifact` is a collection of files or packages published by a run.

### Run
A run represents one execution of a pipeline. It collects the logs associated with running the steps and the results of running tests. During a run, Azure Pipelines will first process the pipeline and then send the run to one or more agents. Each agent will run jobs.

### Agent pools
An agent pool is a collection of agents. Instead of managing each agent individually, you organize agents into agent pools. When you configure an agent, it is registered with a single pool, and when you create a pipeline, you specify the pool in which the pipeline runs. When you run the pipeline, it runs on an agent from that pool that meets the demands of the pipeline.

## PAT (Personal Access Token)

Generate and use a `PAT` to connect an agent with Azure Pipelines. PAT is the only scheme that works with Azure Pipelines. The PAT must have Agent Pools (read, manage) scope (for a deployment group agent, the PAT must have Deployment group (read, manage) scope), and while a single PAT can be used for registering multiple agents, the PAT is used only at the time of registering the agent, and not for subsequent communication. 













<!-- # more info -->
<!-- https://www.alexvolok.com/2020/azure-devops-for-sql-server-dba-automating-deployments/ -->

