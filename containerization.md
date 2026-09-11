# Run MATLAB in Containers

In continuous integration (CI) workflows, you can run MATLAB&reg;, Simulink&reg;, and other MathWorks&reg; products inside a container for improved security, consistency, and performance. Containers give you full control over the environment in which MATLAB runs. You can create and customize your own containers for CI.

For information on how to create a custom container image for CI workflows using a Dockerfile, see [Create a MATLAB Container Image for Non-Interactive Workflows](https://github.com/mathworks-ref-arch/matlab-dockerfile/tree/main/alternates/non-interactive).

> [!NOTE]
> Several [CI platform integrations for MATLAB](https://www.mathworks.com/help/matlab/matlab_prog/continuous-integration-with-matlab-on-ci-platforms.html) provide APIs to install and license MATLAB automatically on build agents. For example, on GitHub&reg; Actions, you can use the `setup-matlab` action to install MATLAB on a GitHub-hosted or self-hosted runner. If you need full control over your environment, create your own container instead of relying on these integrations.


## Install Products
The [Dockerfile](https://github.com/mathworks-ref-arch/matlab-dockerfile/blob/main/alternates/non-interactive/Dockerfile) for noninteractive workflows includes:

- The latest MATLAB release (without additional toolboxes)
- The latest [`matlab-batch`](https://github.com/mathworks-ref-arch/matlab-dockerfile/blob/main/alternates/non-interactive/MATLAB-BATCH.md) executable

To include additional products in your container image, customize the Dockerfile. For details, see [Customize the Image](https://github.com/mathworks-ref-arch/matlab-dockerfile/tree/main/alternates/non-interactive#customize-the-image).

> [!TIP]
> To verify which products your container image includes, run `matlab -batch "ver"`. A missing product typically causes an `Undefined function 'functionName'` error rather than naming the missing product directly.

## License Products
To license MathWorks products in a containerized CI workflow, use a [MATLAB batch licensing token](https://github.com/mathworks-ref-arch/matlab-dockerfile/blob/main/alternates/non-interactive/MATLAB-BATCH.md#matlab-batch-licensing-token). These tokens enable MATLAB to start in noninteractive environments. Request a token by submitting the [MATLAB Batch Licensing Pilot](https://www.mathworks.com/support/batch-tokens.html) form.

> [!NOTE]
> Do not paste the token into the Dockerfile. Instead, store it as a secret in your CI environment and use that secret to set an environment variable named `MLM_LICENSE_TOKEN`. For an example, see [Use MATLAB Batch Licensing Token](https://github.com/matlab-actions#use-matlab-batch-licensing-token).
 
## Run MATLAB in Container
After building your custom container image, reference it in your CI pipeline configuration file. The syntax for the image reference depends on your CI platform. For examples using GitHub Actions and GitLab&reg; CI/CD, see [Examples](#examples).

Then, you can use the CI platform integrations for MATLAB provided by MathWorks to:
- Run a build using the MATLAB build tool.
- Run MATLAB and Simulink tests, and generate test and coverage artifacts.
- Run MATLAB scripts, functions, and statements.
  
For more information about the available integrations, see [Continuous Integration with MATLAB on CI Platforms](https://www.mathworks.com/help/matlab/matlab_prog/continuous-integration-with-matlab-on-ci-platforms.html). If MathWorks does not provide an integration for your CI platform, invoke the `matlab-batch` executable in the container instead.

## Examples
The following examples show how to define a CI pipeline to run the `"test"` task in a container. The examples have these assumptions:
- You have a MATLAB batch licensing token stored as a secret in GitHub Actions or GitLab CI/CD.
- Your repository contains a build file named `buildfile.m` with a `"test"` task for running MATLAB tests.
- Your organization provides a custom container image named `my-org/custom-matlab-image:r2025b`.

### GitHub Actions
To run a MATLAB build in GitHub Actions, use the [`run-build`](https://github.com/matlab-actions/run-build) action. To use your custom container image and batch licensing token, use the `container`, `image`, and `env` keywords in the workflow definition.

For example, to run a container from your custom image on a GitHub-hosted runner, create a YAML file in the `.github/workflows` folder in your repository. Then, use the container to run the `"test"` task with the `run-build` action. In this example, `MyToken` is the [secret](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions) that holds the MATLAB batch licensing token.

```YAML
name: CI
on:
  push:
    branches: [ main ]
jobs:
  container-build-job:
    runs-on: ubuntu-latest
    container:
      image: my-org/custom-matlab-image:r2025b
      env:
        MLM_LICENSE_TOKEN: ${{ secrets.MyToken }}
    steps:
      - name: Check out repository
        uses: actions/checkout@v6
      - name: Run build
        uses: matlab-actions/run-build@v3
        with:
          tasks: test
```

For more information, see [Running jobs in a container](https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/run-jobs-in-a-container).

### GitLab CI/CD
To run MATLAB code and Simulink models in GitLab CI/CD, use the [`build`](https://gitlab.com/explore/catalog/mathworks/components/matlab?tab=readme) component. By default, jobs created from the `build` component run using the latest release of MATLAB in the [MATLAB container on Docker&reg; Hub](https://www.mathworks.com/help/cloudcenter/ug/matlab-container-on-docker-hub.html). To use your custom image, specify it with the `matlab_image` input.

For example, using the `build` component, in a file named `.gitlab-ci.yml` in the root of your repository, define a pipeline to run the `"test"` task in your custom container. 

```YAML
include:
  - component: $CI_SERVER_FQDN/mathworks/components/matlab/build@~latest
    inputs:
      tasks: test
      matlab_image: my-org/custom-matlab-image:r2025b
```

In GitLab CI/CD, the token-to-environment variable mapping occurs in the web UI. For details, refer to the documentation of the `build` component.

## See Also
- [Create a MATLAB Container Image for Non-Interactive Workflows](https://github.com/mathworks-ref-arch/matlab-dockerfile/tree/main/alternates/non-interactive)
- [MATLAB Batch Licensing Executable](https://github.com/mathworks-ref-arch/matlab-dockerfile/blob/main/alternates/non-interactive/MATLAB-BATCH.md)

----

Copyright 2026 The MathWorks, Inc.

----
