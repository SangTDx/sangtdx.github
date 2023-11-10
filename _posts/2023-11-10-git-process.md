---
layout: post
title: Git branching model
date: 2023-11-10 00:00:00
categories: [programming]
tags: [git]
last_modified_at: 2023-11-10
---


# Git Branching Model

<figure>
  <img src="/assets/img/blogs/git-branching/git-branching.png" alt="Git Banching">
  <figcaption>Git Branching Model</figcaption>
</figure>

### 1.1 Branching Meaning

* Below is branch meaning:
  * master: Storage production stable source code
  * release/*: branched release from develop branch, merged into the master branch
  * hotfix/*: special hotfix branches, merged into master branch
  * develop: where all development happens
  * feature/*: feature branches merged into develop branch. Best use ticket id as a reference. This branch must rebase the newest source from develop branch before merged.
  * bugfix/*: bugfix branches merged into develop branch. Best use ticket id as a reference. This branch must rebase the newest source from develop branch before merged.

* Number of branches:
  * master ← Only ever 1 branch
  * develop ← Only ever 1 branch
  * feature/nameOfFeature ← No branch limit
  * bugfix/nameOfBug ← No branch limit
  * release/v1.2.3 ← No branch limit, but only 1 per release
  * hotfix/v1.2.4  ← Note the version bump – no limit, but should be rare

# The process works with branches

* Rebase should always be used unless changes requested in review
* Branching should always be from the master, and non-master branch rebasing/merging should always be on/to master
* Branching from a non-master branch and rebasing/merging non-master branch on/to another non-master branch are prohibited
* Local Git should be configured with:
  * git config --global user.email {your work email}
  * git config --global user.name "{your full name in English} ({your GitLab  username})"
  * git config --global branch.autosetuprebase always
* GitLab repositories should be configured as follows:
* Settings > Options > Merge button: check only “Allow squash merging”
* Settings > Branches
* Default branch: master
* Protected branches > Choose a branch… > master
* master > Edit > Branch protection for master
* Check “Protect branch”
* Check “Require to pull request reviews before merging”
* Check “Dismiss stale pull request approvals when new commits are pushed”
* Check “Restrict who can dismiss pull request reviews”
* Check “Require status checks to pass before merging”
* Check “Require branches to be up to date before merging”

### Flow working with branch

<figure>
  <img src="/assets/img/blogs/git-branching/Flow_working_with_branch.png" alt="Flow working with branch">
  <figcaption>Flow working with branch</figcaption>
</figure>

### Documentation in Git repository

* The repository should have README.md in the top directory with the following contents
  * Development Processes
  * Purpose
  * Usage
  * Architecture
  * Repository Layout
  * Build
  * Run
  * Test
  * Deploy
* Source documentation should be preferred against standalone
* The following tools should be used for source documentation
* The repository may have README.md in the arbitrary directory for standalone documentation specific to the directory and descendants
* Source and standalone documentation in the repository should be reviewed in pull requests, with respect to quality and coverage
* If documentation requires agreement/commitment, the documentation should be committed in the repository and pull request review should be used for agreement/commitment
* Standalone documentation other than README.md in repository directory or not requiring agreement/commitment should be written in the repository wiki
* If documentation target spans to multiple repositories, a product-wide repository should be created to host such documentation
* Binary formats such as Excel/PowerPoint/Word should not be used for textual documentation, because of difficulty in revision control and collaborative editing

### Git branch with Jenkins Pipeline (optional)

* To merge a branch to the main branch. All developer must follow the rule for merge request in below:
  * Each story/hotfix branch must pass all steps
  * With develop, the branch must run with all tools and pass all step before release
* With release branch, to release production must pass all step such as:

<figure>
  <img src="/assets/img/blogs/git-branching/jenkins-git.png" alt="Git branch with Jenkins Pipeline">
  <figcaption>Git branch with Jenkins Pipeline</figcaption>
</figure>

