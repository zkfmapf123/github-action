## Github Action

### Desc
- Node + Docker use Github Action

### Process
- Push -> Github.com -> Runner (Code, Data) -> 

### Example
- Git Commit의 따라서 -> Commit 메시지근거로 따라서 업무일지 작성

### Reference
- <a href="https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows">Action Event Type</a>


### Example
#### Hello-world.yml

```yml
    # This workflow will do a clean installation of node dependencies, cache/restore them, build the source code and run tests across different versions of node
# For more information see: https://help.github.com/actions/language-and-framework-guides/using-nodejs-with-github-actions

name: Hello world CI / CD

# Event
on:
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]

# Jobs use Event
jobs:
  build:
    # Runner Computers
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x, 14.x, 16.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/
    # Process
    # name -> Step name
    # run -> Actually work
    steps:
    # - uses: actions/checkout@v3
    - name: Run pwd
      run: pwd
    - name: Run ls -al
      run: ls -al

```

![hello-world.yml](./public/helloworld.png)

#### Hello-world v2 (Runner에 저장소 생성)

```yml
  name: Github-Checkout

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the "master" branch
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v3
      - name: pwd
        run: pwd
      - name: ls-al
        run: ls -al
```

### Context

```yml


# This is a basic workflow to help you get started with Actions

name: CI

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the "master" branch
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v3
      - name: print-sha
        env:
          COMMIT_ID: ${{ github.sha }}
        run:
          echo "Commit id => $COMMIT_ID"
      - name: print-repo
        env:
          REPO_INFO: ${{ github.repository }}
        run:
          echo "repo => $REPO_INFO"
``` 

### Reference
- <a href="https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows">Github Event Type</a>
- <a href="https://docs.github.com/es/actions/learn-github-actions/contexts">Github Env Context</a>