# Invoke MATLAB in CI Environments
You can invoke MATLAB&reg; in continuous integration (CI) pipelines in different ways depending on where you want MATLAB to run and how you want MATLAB to integrate with your pipeline. Choose an approach based on your use case.
| Use Case | Recommended Approach |
|-------------|-------------|
| Run MATLAB directly in CI. | [CI Platform Integration for MATLAB](#ci-platform-integration-for-matlab) |
| Run MATLAB on a custom runner setup. | [Command-Line MATLAB](#command-line-matlab) (`matlab -batch`) |
| Run MATLAB without installing it. | [Packaged MATLAB Artifacts](#packaged-matlab-artifacts) (executables, Python&reg; packages, and containers) |
| Run MATLAB remotely. | [MATLAB Hosted on Server](#matlab-hosted-on-server)|
| Generate CI pipelines for Simulink&reg;. | [Advanced Simulink CI Workflows](#advanced-simulink-ci-workflows)|

## CI Platform Integration for MATLAB
MathWorks&reg; provides CI integrations that can install MATLAB, configure products, and run MATLAB noninteractively on CI runners.

Use these integrations to run MATLAB on CI runners. For other platforms, use [MATLAB from the command-line](#command-line-matlab) or the [Dockerfile](https://github.com/mathworks-ref-arch/matlab-dockerfile/tree/main/alternates/non-interactive) instead.
| CI Platform | Integration |
|-------------|-------------|
| Azure DevOps&reg; | [MATLAB Extension](https://marketplace.visualstudio.com/items?itemName=MathWorks.matlab-azure-devops-extension) |
| Bamboo&reg; | [MATLAB Plugin](https://github.com/mathworks/matlab-bamboo-plugin/blob/main/README.md) |
| CircleCI&reg; | [MATLAB Orb](https://github.com/mathworks/matlab-circleci-orb/blob/master/README.md) |
| GitHub&reg; Actions | [MATLAB Actions](https://github.com/matlab-actions)|
| GitLab&reg; CI/CD | [MATLAB `build` Component](https://gitlab.com/explore/catalog/mathworks/components/matlab?tab=readme)|
| Jenkins&reg; | [MATLAB Plugin](https://plugins.jenkins.io/matlab/)|
| TeamCity&reg; | [MATLAB Plugin](https://github.com/mathworks/matlab-teamcity-plugin/blob/main/README.md)|

To try these CI platform integrations, you can fork the [ci-configuration-examples](https://github.com/mathworks/ci-configuration-examples) repository and install the MATLAB CI plugin on your CI platform.

To standardize your MATLAB builds and support incremental builds, you can combine these integrations by using the [MATLAB build tool](https://www.mathworks.com/help/matlab/matlab_prog/overview-of-matlab-build-tool.html).

For more information, see [Continuous Integration with MATLAB on CI Platforms](https://www.mathworks.com/help/matlab/matlab_prog/continuous-integration-with-matlab-on-ci-platforms.html).

## Command-Line MATLAB
You can use the [`matlab`](https://www.mathworks.com/help/matlab/ref/matlablinux.html) command with the `-batch` option in your CI pipeline configuration file to execute scripts, functions, and statements.

For example, this command runs the code in a file named `myscript.m`:
```(shell)
matlab -batch "myscript"
```
MATLAB terminates automatically with the exit code `0` if the code executes successfully without generating an error. Otherwise, MATLAB terminates with a nonzero exit code.

Consider using `matlab -batch` when:
- Your CI platform does not have a CI platform integration for MATLAB.
- You use custom runners.
- You want to invoke MATLAB using a simple command-line call.

As alternatives to using `matlab -batch`:
- For scaled workflows, you can use the [`matlab-batch` executable](https://github.com/mathworks-ref-arch/matlab-dockerfile/blob/main/alternates/non-interactive/MATLAB-BATCH.md).
- You can call MATLAB from other languages in CI by using the associated [external language interface](https://www.mathworks.com/help/matlab/external-language-interfaces.html?s_tid=CRUX_lftnav), but these integrations typically require a specific licensing model and do not support MATLAB batch token licensing.

## Packaged MATLAB Artifacts
When you package MATLAB artifacts, you build once with MATLAB and then run the resulting artifacts without installing MATLAB.

Consider using a packaged MATLAB approach when:
- You want minimal dependencies on your CI runners.
- You run the same workflow repeatedly.

The packaged MATLAB approach:
- Applies licensing at build time
- Does not require MATLAB installation on CI runners

You can build and distribute MATLAB code as deployable artifacts, including:
- Standalone executables — For more information, see [Get Started with MATLAB Compiler](https://www.mathworks.com/help/compiler/getting-started-with-matlab-compiler.html).
- Python packages — For more information, see [Python Package Integration](https://www.mathworks.com/help/compiler_sdk/python_packages.html). For the differences between a compiled Python package and calling MATLAB from Python, see [Differences Between MATLAB Engine API for Python and MATLAB Compiler SDK](https://www.mathworks.com/help/compiler_sdk/python/difference-between-matlab-engine-api-for-python-and-matlab-compiler-sdk.html).
- Docker&reg; images with MATLAB Runtime — For more information, see [Package MATLAB Standalone Applications into Docker Images](https://www.mathworks.com/help/compiler/package-matlab-standalone-applications-into-docker-images.html).

For more information about creating deployable applications from MATLAB code using MATLAB Compiler, see [Standalone Applications](https://www.mathworks.com/help/compiler/standalone-applications.html).

## MATLAB Hosted on Server
You can run MATLAB outside of your CI platform by invoking MATLAB remotely and using CI to orchestrate execution. You can use MATLAB Production Server&trade; to expose MATLAB functionality using REST or gRPC APIs.

Consider using MATLAB Production Server when:
- You have multiple pipelines that share MATLAB workloads.
- You need more control over scaling.
- You have a platform team or service team that owns MATLAB execution separately from CI.

The server approach:
- Allows the CI platform to call an API instead of launching MATLAB directly
- Centralizes execution and scaling to a MATLAB instance that runs elsewhere
- Separates the MATLAB workflows for a pipeline
- Separates MATLAB execution from CI

For more information, see [MATLAB Production Server](https://www.mathworks.com/help/mps/index.html).

## Advanced Simulink CI Workflows
If your team uses Simulink, the CI/CD Automation for Simulink Check support package can simplify CI setup and integration.

The support package can:
- Generate CI pipeline configuration files (YAML, Jenkinsfile) for certain CI platforms.
- Run incremental builds using a `processmodel.m` file.
- Reduce manual pipeline setup and maintenance.

For more information, see:
- [Azure DevOps Integration Guide](https://www.mathworks.com/help/slcheck/padv/ug/integrate-process-into-azure-devops-with-artifact-management.html)
- [GitHub Actions Integration Guide](https://www.mathworks.com/help/slcheck/padv/ug/integrate-process-into-github-with-artifact-management.html)
- [GitLab CI/CD Integration Guide](https://www.mathworks.com/help/slcheck/padv/ug/integrate-process-into-gitlab-with-artifact-management.html)
- [Jenkins Integration Guide](https://www.mathworks.com/help/slcheck/padv/ug/integrate-process-into-jenkins-with-artifact-management.html)

Alternatively, you can use `matlab -batch` to call the `runprocess` function as shown in [Other Platforms](https://www.mathworks.com/help/slcheck/padv/ug/approaches-to-pipeline-configuration.html#mw_09108865-8cf4-4ad5-b157-e5214eae5762).

## See Also
- [Install MathWorks Products in CI Environments](./installation.md)
- [License MathWorks Products in CI Environments](./licensing.md)
- [Run MATLAB in Containers](./containerization.md)

----

Copyright 2026 The MathWorks, Inc.

----
