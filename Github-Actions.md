# Github Actions commands and Workflow

* Github Actions is a Continuous Integraion solution
* Uses Workflow which is collection of Jobs
* Runners are the compute machone where workflows are executed
* Gitflow workflows generally refers to a model where specific brances map to designated environments and new code is validated in lower environments before going to production.
* Working with YAML a pro
* .yml or .yaml file extention
* Each action is a Job in Workflow
* Step is single action in each Job


            name: Build Application Code
            on: [push]
            jobs:
                build:
                    runs-on: ubuntu-latest
                    steps:
                    -name: Check out code
                     uses: actions/checkout@v2
                    -name: Install Libraries
                     run: pip install -r requirements.txt -t .
                test:
                    runs-on: ubuntu-latest
                    needs: build
                    steps:
                    ...



## Community Actions
* CA are prepackage steps or reusable templates for common steps

## Runners
* A VM where your job runs
* Can be Linux Windows Mac
* Can be run in cloud or Private datacenter or localworkstation
* Security patching and updates should be done by user on custom runners


### Workflows

* Workflows define the event that triggers actions
* Workflows define which actions to run
* Repositories can contain multiple workflows
* Stored in .github/workflows
* mkdir -p .github/workflows
*

### Workflow Attributes
    -name : The name of the workflow
    -on   : Event when the actions should be triggered
            Attributes [push] [pull_request] [release]
            Incase of multiple [push, pull_request]
            Web hooks:
                Branch creation
                Issues
                Members
            Scheduled
                Cron tab
    Conditional Events
    on:
         push:
            branches:
                -develop
                -master

    on:
        pull_request:
            branches:
                -master

    Incase multiple

    on:
        push:
            branches:
                -xxx
        pull-request:
            branches:
                -yyy

    * Ignore branches branches-ignore

    * Use tags        tags-ignore

    * Specail characters 'feature/new-feature'
                        ' release/*' 'm?ster'

    jobs: Defines jobs for the workflow which runs in parallel by default
         job-name:

    runs-on : machine where the actions or steps run
            Attribue [windows-latest, ubuntu-latest,macos-latest]

        steps: List of actions or commands or tasks
        -name: Checkout
         uses: Execute an action in the operating system
        public repo => uses: {owner}/{repo}@{ver}
                       uses: actions/checkout@v2


        Same repo  =>  uses: ./path to the action
                       uses: ./.github/actions/my-checkout

        Diff repo  => {userID}/{repo}@{ver}
            -uses: "user/repo/path@ref"
                ref can be branch,tag or SHA

        Docker image registry
                       uses: docker://{image}:{tag}
                       uses: docker://hello-world:latest
        custom registry uses: "docker://host/image:tag"
        Example
        uses: action/checkout@v2

    Arguments for uses is passed as with param

        uses: {github accout}/{action name}
        with:
                key:value
                key:value

        Example:

        Steps:
            -name: Checkout the code
             uses: action/checkout@v2
             with:
                repository: apache/tomcat
                ref:master
                path: ./tomcat

        needs: Creating dependecy for running a job which can be an prior job

        Example
        needs: step1


        run: Executable command step

        Single line command
                     run: {command} {parameters} {arguments}
                     run: mv ./output ./archive

        Multiple line command
                run: |
                    Command 1
                    Command 2

                run: |
                npx install
                npx server

        Example:
        run: echo Hello world!


### Environment Variable
* Dynamic key-value pairs stored in memory
* Injected at runtime and case-sensistive
* GITHUB_WORKFLOW
* GITHUB_ACTION
* Use the "env" attribute
* Defined in
  * Workflows =Accessible for All jobs steps actions and commands
  * Jobs = Accessible for All steps actions and commands within Jobs
  * Steps = Accessible for the step where variable is defined
* Shell Variable Syntax : Variable is readh from the shell
  * $VARIABLE_NAME
  * $Env: VARIABLE_NAME
* YAML syntax
  * ${{ env.VARIABLE_NAME}}
  * Variable is read from the workflow
  * Variables can be used in workflow configuration
  * Variabled defined at step level can't be used in that step


### Secrets also environment variables
* Use the secrets workflow context
* ${{ secrets.SECRET_NAME }}
* Must be explicitly passed to a step

### Artifacts
* Data preserved from a workflow
* Files or collection of files
  * Complied binaries
  * Archives
  * Test results
  * Log files




