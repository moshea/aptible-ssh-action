# Github Action to deploy onto Aptible Deploy

This action runs an ssh command on an Aptible environment.

## Required input and output arguments

## Optional input and output arguments

## Secrets the action uses

## Environment variables the action uses
#### The converstion from `var` to `INPUT_VAR` is [how GitHub Actions handle Inputs](https://help.github.com/en/actions/building-actions/metadata-syntax-for-github-actions#inputs).
* `username` - passed to `aptible` CLI
* `password` - passed to `aptible` CLI
* `environment` - specifies App to be deployed
* `app` - specifies App to be deployed
* `command` - the command to run over ssh

## Example github actions usage
```yaml
name: Running a command via SSH on an aptible environment

on:
  workflow_dispatch:
    inputs:
      command:
        description: The rake command to run
        required: true
      environment:
        description: The environment to run the command on
        required: true
      app:
        description: The app to run the command on
        required: true

jobs:
  rake:
    runs-on: ubuntu-latest

    steps:
      - name: Run rake command
        uses: moshea/aptible-ssh-action@master
        with:
          username: ${{ secrets.APTIBLE_USERNAME }}
          password: ${{ secrets.APTIBLE_PASSWORD }}
          environment: ${{ github.event.workflow_dispatch.environment }}
          app: ${{ github.event.workflow_dispatch.app }}
          command: ${{ command }}
```
