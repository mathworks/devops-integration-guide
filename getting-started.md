# Getting Started

This guide is for platform engineers responsible for integrating MATLAB&reg; and Simulink&reg; into CI/CD infrastructures.

Use the topics in the [main README](./README.md) to make platform-level decisions about how MATLAB runs in your CI environment, including licensing, installation, execution environments, and invocation methods.

As part of this setup, you may need to collaborate with development teams to access MATLAB code, Simulink models, and automation scripts required by your pipelines. This guide assumes collaboration across these roles:
- **Platform Engineers** - Design, implement, and maintain CI/CD infrastructure and pipelines.
- **Developers** - Create and maintain MATLAB code, Simulink models, and related artifacts.
- **Tools Engineers** - Develop automation scripts and workflows that integrate MATLAB and Simulink into development processes.

If you are a developer or tools engineer, see [Continuous Integration with MATLAB and Simulink](https://www.mathworks.com/solutions/continuous-integration.html) for workflow-specific guidance.

## Key Requirements

To run MATLAB in CI, you need:
- A public repository or a license to use MATLAB in CI in a private repository.
- An environment where MATLAB can run, such as a CI agent, a container or packaged artifact, or a remote execution service.
- A way to invoke MATLAB non-interactively, such as the `matlab -batch` command or an official MATLAB CI platform integration.

## Quick Start

Run MATLAB in CI by forking an example repository that uses official MATLAB CI platform integrations. The examples run in public repositories and require minimal setup.

For public repositories, MATLAB CI integrations automatically license products for you, except transformation products, such as MATLAB Coder&trade; and MATLAB Compiler&trade;.

### Starter

To run MATLAB in a CI pipeline:
1.	Fork the [ci-configuration-examples](https://github.com/mathworks/ci-configuration-examples) repository.
2.	Install the MATLAB CI plugin for your CI system.
3.	Create a CI job that automatically runs MATLAB tests.
4.	Add your own MATLAB code or Simulink models.

### Advanced

For advanced workflows, use the [advanced-ci-configuration-examples](https://github.com/mathworks/advanced-ci-configuration-examples) repository instead.

----

Copyright 2026 The MathWorks, Inc.

----
