# GitHub Actions

## Overview

GitHub Actions is a platform designed to automate tasks related to software and its management. While it focuses on CI/CD it can be easily stretched to do more for you.

## Components

### Workflows

A workflow is an automated process to perform a task through one or more _jobs_, it's defined by checking in a `YAML` file into a repository (`/.github/workflows/example.yaml`) and triggered by _events_.

### Events

An event is a specific activity that triggers a workflow configured to listen to the given event, like code push, creation of an issue, even another workflow run, scheduled or manual trigger.

### Jobs

A job is a list of _steps_ to execute to perform the task in a given workflow.
Multiple jobs can be included in a workflow and each runs in a separate _runner_.
They run in parallel by default and can depend on other jobs from the workflow.

### Steps

A step is a specific task to execute in a jobs.
It can be either a shell command to run or an _action_ and they are executed in the order they are defined.

### Actions

An action is a custom application that can handle a complex or repeatable task in a step, like checking out repository code, setting up required toolchain or send a notification.
There's a marketplace with various actions that might solve a task or you can create your own actions to minimise code duplication between workflows.
This is not to be confused with GitHub Actions, which is the name of the entire platform (thanks GitHub!)

### Runners

A runner is a container to run jobs when a workflow is triggered.
GitHub provides Ubuntu Linux, Microsoft Windows, and macOS runners. Alternatively, you can run a workflow in a self-hosted runner.

### Example workflow

```yaml
on:  # list of _events_ that trigger the workflow
  workflow_dispatch:  # manual trigger
  push:  # code push with its configuration
    paths-ignore:
      - '/docs/**'

jobs:  # list of _jobs_ in this _workflow_
  Example:  # a name describing what this job is meant to do
    runs-on: ubuntu-latest  # _runner_ selection
    steps:  # list of _steps_ in this _job_
      - uses: actions/checkout@v2  # _action_ to check out codebase
        with:  # configuration for the _action_
          path: /my/path

      - run: echo osh was here  # run specific command in the _runner_
      
      - if: failure()  # conditionally run the _step_
        env:  # provide environment variables to this _step_
          WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}
          CHANNEL_ID: ${{ secrets.SLACK_CHANNEL_ID }}
          MESSAGE: Big Bada Boom in ${{ github.repository }}/${{ github.workflow }}
        run: |  # example of multiline _run_ command, the pipe (`|`) is required
          curl -X POST --data-urlencode "payload={\
            \"channel\": \"$CHANNEL_ID\",\
            \"username\": \"GitHub Actions Bot\",\
            \"text\": \"$MESSAGE\"\
          }" $WEBHOOK_URL
```

### Viewing and running workflows

Go to https://github.com/YOUR_ORG/YOUR_REPO/actions
