# Find deprecated APIs in your helm charts

This Github action checks your helm chart for deprecated k8s versions by using [pluto](https://github.com/FairwindsOps/pluto) in one single step.
You do not have to take care about the boilerplate, just define your helm chart location, target k8s version and a pluto version to get started.

# Usage

## Variables

| Name                 | Description                                                                                                                                                                          | Example                       | Default | Optional |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------- | ------- | -------- |
| K8S_VERSION          | The k8s version to check your used APIs against                                                                                                                                      | v1.24.8                       | v1.24.9 | yes      |
| HELM_CHART_DIRECTORY | The location of your helm chart relative to your project root                                                                                                                        | helm/charts/<your-chart-name> | --      | no       |
| PLUTO_VERSION        | The desired version of pluto. See [Pluto releases](https://github.com/FairwindsOps/pluto/releases) for available versions. You have to skip the `v` at the beginning of the version! | 5.16.1                        | 5.16.1  | yes      |


## Example
```yaml
name: pluto detection test

on: workflow_dispatch

jobs:
  pluto_detect:
    runs-on: ubuntu-latest
    steps:
      - name: Check out the repo
        uses: actions/checkout@v3

      - name: Check deprecated k8s APIs
        uses: eddykaya/helm-pluto-github-action@0.0.2
        with:
          PLUTO_VERSION: 5.16.1
          K8S_VERSION: v1.24.8
          HELM_CHART_DIRECTORY: helm/charts/yahc

```

You will find a working example [here](https://github.com/eddykaya/yahc)