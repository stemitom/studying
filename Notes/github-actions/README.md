# Github Actions

## What is Github Actions?

A platform to automate developer workflows
An example of workflow is the CI/CD workflow which could go thus:
- Merged Code
- Test
- Build
- Deploy

## How Github action automate these workflows?
- Listen to gh Events (PR Requests, Issue Creation, Contributor Joined, PR Merged)
- Trigger actions (Sort, Label, Assign, Reproduce) from events with gh-actions

> Therefore, combinations of actions make up a workflow


## Examples
A common workflow pattern for most repository after committing goes:
- Test
- Build
- Push
- Deploy

## Why not another CI/CD tool?
- Same tool for OSS management so no 3rd party integration
- Pipeline is easy
- Tool for developers (this doesn't require you having an extra devops handling CI/CD integrations)

## Where does this all get executed?
- The github action runner is executed on github servers and there is no need to setup servers manually to run workflows
- Each job is run in a fresh virtual environment/server

Learn more on the [Github Action Docs](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)