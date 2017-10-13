# Engage 2017 CD workshop

This repository contains demo code for the Acquia Engage 2017 CD workshop. There are several branches, with each branch corresponding to a tutorial in the Pipelines Examples repository: https://github.com/acquia/pipelines-examples

## Deploying to on-demand environments

This tutorial demonstrates how to automatically deploy feature
branches and (if you use GitHub) pull requests to Acquia Cloud On
Demand Environments (ODEs) using the Pipelines Deploy tool.

## How it works
The Pipelines Deploy tool provides integration between Pipelines and
Cloud environments. When the Deploy tool runs during a "build" event:

* The Deploy tool checks to see if a Cloud environment already exists
  for the build branch, such as pipelines-build-feature (for a feature
  branch) or pipelines-build-pr-N (for GitHub pull request #N), that
  will hold the build artifact resulting from the current job.
* If no such Cloud environment exists, the Deploy tool creates one
  using the Cloud On Demand Environments feature and configured it to
  deploy the build branch. This requires that you have added this
  feature to your Acquia Cloud subscription.
* If such a Cloud environment already exists, it is left in place.
* Acquia Cloud will then deploy the build branch to the selected
  environment.

When the Deploy tool runs during a "pr-merged" event, which is triggered
when a GitHub pull request is merged to its base branch:

* The Deploy tool deletes any Cloud on-demand environments deploying
  the build branch, pipelines-build-pr-N (for GitHub pull request #N),
  for that pull request.

When the Deploy tool runs during a "pr-closed" event, which is triggered
when a GitHub pull request is closed without being merged to its base branch:

* The Deploy tool deletes any Cloud on-demand environments deploying
  the build branch, pipelines-build-pr-N (for GitHub pull request #N),
  for that pull request.

The net result of these behaviors by the Deploy tool is that every
feature branch and pull request will get its own on-demand environment
that is updated for every build of that branch performed by Pipelines,
and on-demand environments for pull requests are deleted automatically
when the pull request is merged.
