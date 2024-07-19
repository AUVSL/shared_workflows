# Resuable workflows for Python Files
This repository contains the reusable workflows for AUVSL. To build around the workflows in this repo, create a .github/workflows folder in your repo and follow this template: 
```
name: <workflow name>

on: [push, pull_request, workflow_dispatch, workflow_call]

permissions:
  contents: write

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Trigger by ${{ github.actor }} with ${{ github.event_name }} event"
  <workflow name>:
    needs: build
    uses: AUVSL/shared_workflows/.github/workflows/<desired workflow>.yml@main
    with:
      run-name: '<desired message>'
    secrets:
      GH_PAT: ${{ secrets.GH_PAT }}
```
