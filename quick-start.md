# Quick Start Using Example Repos

To quickly get started with running MATLAB&reg; in your CI/CD pipelines, you can fork an example repository that uses MATLAB CI platform integrations provided by MathWorks&reg;. Make sure that you have the listed requirements and then follow the quick-start steps to run the workflow examples.

## Key Requirements

To run MATLAB in CI, you need:
- A public repository or a license to use MATLAB in CI in a private repository
- An environment where MATLAB can run, such as a CI agent, a container or packaged artifact, or a remote execution service
- A way to invoke MATLAB noninteractively, such as the `matlab -batch` command or a MATLAB CI platform integration provided by MathWorks

## Quick Start

The provided examples run in public repositories and require minimal setup. For public repositories, MATLAB CI integrations automatically license products for you, except transformation products, such as MATLAB Coder&trade; and MATLAB Compiler&trade;.

To run MATLAB in a CI pipeline:
1.	Fork the [ci-configuration-examples](https://github.com/mathworks/ci-configuration-examples) repository.
2.	Install the MATLAB extension for your CI platform.
3.	Create a CI job that automatically runs MATLAB tests.
4.	Add your own MATLAB code or Simulink&reg; models.

For advanced workflows, use the [advanced-ci-configuration-examples](https://github.com/mathworks/advanced-ci-configuration-examples) repository instead.

## See Also
- [Continuous Integration with MATLAB on CI Platforms](https://www.mathworks.com/help/matlab/matlab_prog/continuous-integration-with-matlab-on-ci-platforms.html)
- [Install MathWorks Products in CI Environments](./installation.md)
- [License MathWorks Products in CI Environments](./licensing.md)

----

Copyright 2026 The MathWorks, Inc.

----
