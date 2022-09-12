# Basic CI/CD Implementation

## Table of Contents

- [Basic CI/CD Implementation](#basic-cicd-implementation)
  - [Table of Contents](#table-of-contents)
  - [Intro](#intro)
  - [Node.js CI code snippet](#nodejs-ci-code-snippet)
  - [Docker Image creation and DockerHub push](#docker-image-creation-and-dockerhub-push)
  
## Intro

As I started tinkering with Angular, I realized it would be best to start with my pipeline as early as possible, to benefit from the tools available through GitHub Actions. 

With this, I was able to automate a `Node.js` build each time I merge with my main branch. It would check for any immediate errors I would have missed during development. In the future, once I have implemented any tests with `Karma`, the tool will automatically run those tests through the GitHub Actions workflow.

The original `.yml` files are located [here](https://github.com/tick-github/tick-frontend/tree/main/.github/workflows), though I will provide a snippet down below. 

## Node.js CI code snippet

```yml
name: Node.js CI Building

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:

  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [14.x, 16.x, 18.x]

    steps:
    - uses: actions/checkout@v3
    
    - name: Caching node modules
      uses: actions/cache@v3
      with:
        path: ~/.npm
        key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
        restore-keys: |
          ${{ runner.os }}-node-
    
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
    
    - name: Install, Build and Test
      run: |
        npm ci
        npm run build:ci
        
    - uses: phish108/autotag-action@1.1.51
      with:
        github-token: ${{ secrets.GITHUB_TOKEN}}
        with-v: true
```
*Node.js CI/CD implementation as of September 12th 2022. See the current workflows [here](https://github.com/tick-github/tick-frontend/tree/main/.github/workflows).*

## Docker Image creation and DockerHub push

Since I technically have my own Linux device running during the workflow, I can also do stuff like creating images with Docker, and pushing directly to my DockerHub repository, readying them up for deployment.

```yml
name: Docker Image Building and Pushing to DockerHub
on:
  workflow_run:
    workflows: ["Node.js CI Building"]
    types:
      - completed

jobs:
  docker_build:
    runs-on: ubuntu-latest
    if: ${{ github.event.workflow_run.conclusion == 'success' }}
    
    steps:      
      - name: Checkout
        uses: actions/checkout@v3

      - name: Build & Push Docker image
        uses: mr-smithers-excellent/docker-build-push@v5        
        with:
          image: ejjvandelaar/tick-frontend
          registry: docker.io
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }} 
```

I have also provided the workflow with an if-expression. This will guarantee that these Docker actions will only happen if my previous workflow (the building and testing of the frontend application) was successful. This way, I won't publish a faulty image to my DockerHub.

The final product looks something like this, and can be run from my Docker Desktop application, or from any terminal.

![Docker Desktop view](/docs/proof/images/1-dockerhub-images.png)
