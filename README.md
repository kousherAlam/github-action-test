## github action 

Practice App: https://github-actions-hero.vercel.app/
Github Context: https://docs.github.com/en/actions/learn-github-actions/contexts#github-context




we can use existing github action or create our own github action in the any point of our workflow life cycle. Github action allow us to develop our own custom Software Development Lifecycle (SDLC)s

We can listen for any every occur in github, schedule time or any action happend outside of github.


Github action can create artifact and update repository itself. 




If you are collaborating and and contributing in a softare project, then you are the part of the software workflow.




## Branch protection 
we can add branch protection to master brach, to prevent contributer directly commit on master branch




## Workflow yml file  
worflow file located root of the repository under the `.github/workflows` Directory, properties of the workflow


name: Name of the workflow, 

on: Register Event, how the workflow are triggered
	push: // which action will triggerd
		branches: [master] // we can also filter branch, tags, etc..
		tags: [] // filter for tags
		paths: ['test/*'] we can filter for path also. 
	pull_request: 
		branches: [master]


Actions: Are indivisual steps that are combaines to create a job. 

jobs: 
	build: <what we are doing>
		runs-on: ubuntu-latest <machine, in which our job will be run>
					github provide hosted runner, each a vertual machine, start fresh on every
					job. we can also use self-hosted runner, that will give us full control of 
					hardware and os.

		steps:
			- uses: actions/checkout@v2

			- name: What this step will do
			  run: bash script 

			 - name: Run a multiline script 
			   run: |
			   	echo add other actions to build,
			   	echo test, and deploy your project.


In github workflow all action run as a steps

## Github Events
- Github Webhook Events: define as `on:` github has many event such as push, pull_request, issue_comment and these types has multiple sub events such as issue_comment has created deleted, etc types. We also can filter those types. ex:
	on: 
		issue_comment: 
			branches: [main]
			types: [created, deleted] 
we can find all of the events under github developer documentation : https://developer.github.com/v3/


- Scheduled Event: `schedule`
	we can schedule a workflow to run specific UTC times using POSIX corn syntax
	Run on the latest commit on the default or base branch
	example: 
	on: 
		schedule: 
			- corn: '*/15 * * * *' # runs in every 15 mintues

- External Events: Repository_Dispatch / workflow_dispatch
	we can use github api to dispatch new events. 



## Environment Variables and Secrets 
In the settings tab of the github repository we can set secret and evironment variable and then we can privide it via `${{ secret.<NAME> }}` syntax.

Out of the box github provide following secrets
GITHUB_TOKEN: token of current repository validation


Actions: 
Reuseable pices of code, 
We can combine them in septs to perform some taks.


Artifact: 
files created when we build and test our code. 

CI/CD: 

Runners: Fresh VM. 

JOB: can run indipendendly or sequencely, the are consist or steps 

WorflowFile: yaml file that define the workflow, it has atleast one job.

Workflow run: instance of the workflow


### Strategy - Matrix 
we can define various environment for for build using matrix strategy. example: 

stragey: 
	matrix: 
		node-version: [12.x, 14.x, 16.x, 17.x]

with the help of matrix we can run our workflow against different environment as specify, 

```yml
runs-on: ${{ matrix.os }}
strategy: 
    matrix: 
        os: [ubuntu-latest, windows-latest]
```
## Customize workflow beyound Template
- Test against multiple target environments
- dedicated test jobs
- Access to build artifacts
- Branch protections
- Required reviews
- Obvious approvals 

