# Git Style Guide for all of my application
My guide for using [git][] is reliant on [Git Flow][flow] as well as being based on [Vincent Driessen's post on Git][model]. It is designed for simplicity of people new to Git, as well as being compatible with [SourceTree][], which all developers should use, if they aren't using the command line.

# Starting a new repository
Repositories should be setup with Git and Git Flow from the beginning.

Starting a new Repository for Rails:

  rails new my-app && cd my-app
  git init
  git flow init

Accept all defaults, except for the Version tag prefix. Set the prefix so "v\_" (short for version).

After running the `git flow init` command, you will be on the develop branch.

# Branches
Git flow generates a standard set of branches and offers utilities to create additional branches.

## Main Branches

### Master
The master branch stores the production code for a project. It is expected that at any time, you should be able to pull the master branch to production and have fully functioning code.

### Develop
The develop branch is for code that is in development and probably not yet ready for QA or production. Developers may commit code to the develop branch to share with each other or to save their work on tasks that require multiple commits.

## Supporting Branches

### Feature
- Branch off of: develop
- Merge into: develop

Feature branches of to be used if code will take multiple days to build. The idea of a feature branch is to build out a new feature or fix a large bug without cluttering the develop branch with commits of unfinished code.

**Creating a feature branch**

    git flow feature start update-foundation
    # creates a branch called "feature/update-foundation" and checks it out

**Finishing a feature branch**

    git flow feature finish update-foundation
    # merges feature/update-foundation into develop and checks develop out

### Release
- Branch off of: develop
- Merge into: develop and master

Release branches are branches that will include code for the next release. Commits against the branch will include minor-bugfixes and preparations of meta-data (version numbers, build dates, etc) for the release. All code in the release branch should go through a QA process.

**Creating a release branch**

    git flow release start sprint-1

**Finishing a release branch**

    git flow release finish sprint-1

After starting a release branch you can commit code in feature branches and the develop branch. When you finish features of development code, it should be merged into the release branch for QA. When you finish the release branch, it will merge the code to develop and master as well as tag the master branch to mark the new release.

### Hotfix
- Branch off of: master
- Mergin into: develop and master

Hotfix branches are for creating code that needs to go out in between releases. Typically they are used to fix critical bugs, like security holes and breaking tasks.

**Creating a hotfix branch**

    git flow hotfix start bug-to-fix

**Finishing a hotfix branch**

    git flow hotfix finish bug-to-fix

When you finish a hotfix branch it will merge the code to master and develop as well as tag the master branch.


[git]: http://git-scm.com "Distributed Version Control"
[flow]: https://github.com/nvie/gitflow "Branching Model to Simplify Seperating Code"
[model]: http://nvie.com/posts/a-successful-git-branching-model/ "Simple branching model that Git Flow is based on"
[SourceTree]: http://sourcetreeapp.com/ "Git Client for Windows and Mac"
