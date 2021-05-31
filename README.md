# Getting started

This organization is meant for TU Eindhoven students working on machine learning projects.  
First of all, contact Joaquin Vanschoren with your GutHub account name to add you as a member.

## Creating you repo
There are a few options here:

* Just create a new repo and start using it for your work (easiest). Follow the instructions to link it to a local folder.
* Transfer an existing repo to this organization. Contact Joaquin about this.
* Fork an existing repo to this organization. Follow the steps below to keep it synchronized.

## Synchronizing forks
You can use [this workflow](https://github.com/aormsby/Fork-Sync-With-Upstream-action#when-you-want-to-merge-into-an-acive-working-branch-not-recommended)

In short, click the `Actions` tab, then `New Workflow`, and then `set up a workflow yourself`. Then, copy in the workflow below, which will synchronize your code every night. Click `Start commit` to commit. That's it. You can test by clicking the `Actions` tab, then `Synchonize fork`, then `Run workflow`.

```
name: Synchronize fork

on:
  schedule:
    - cron:  '0 2 * * *'
    # scheduled at 02:00 every day
  workflow_dispatch:

jobs:
  sync_with_upstream:
    runs-on: ubuntu-latest
    name: Sync HEAD with upstream latest

    steps:
    # Step 1: run a standard checkout action, provided by github
    - name: Checkout HEAD
      uses: actions/checkout@v2
      with:
        ref: main

    # Step 2: run this sync action - specify the upstream repo, upstream branch to sync with, and target sync branch
    - name: Pull upstream changes
      id: sync
      uses: aormsby/Fork-Sync-With-Upstream-action@v2.1
      with:
        upstream_repository: Johnnynater/thesis
        upstream_branch: main
        target_branch: main
        git_pull_args: '--unshallow'
```
