# Install MathWorks Products in CI Environments
To install MATLAB&reg;, Simulink&reg;, and other MathWorks&reg; products in your continuous integration (CI) environment, you can use the CI platform integrations for MATLAB or the [MATLAB Package Manager (`mpm`)](https://github.com/mathworks-ref-arch/matlab-dockerfile/blob/main/MPM.md):

- CI platform integrations for MATLAB — MATLAB integrates with several CI platforms, such as GitHub&reg; Actions, GitLab&reg; CI/CD, and Jenkins&reg;. Some of these integrations provide a built-in mechanism to install MathWorks products in CI environments. If your CI runner is compatible with such an integration, you can automatically install your preferred products using that integration. For more information, see [Use CI Platform Integrations](#use-ci-platform-integrations).
- MATLAB Package Manager (`mpm`) — The MATLAB Package Manager enables automated product installation using a programmatic interface. You can use MPM to install products from the system command line, pipeline configuration file, or Dockerfile. Use `mpm` if there is no integration to install products on your CI runner or if you want to have full control over the installation process.  For more information, see [Use MATLAB Package Manager](#use-matlab-package-manager).  

> [!TIP]
> To access the list of installed products on your system, use the [`ver`](https://www.mathworks.com/help/matlab/ref/ver.html) command.

## Use CI Platform Integrations
This table includes the integrations that you can use to install products on cloud-hosted or self-hosted runners. The integrations use `mpm` to install a specific release of MATLAB and other MathWorks products. To make the installed products available for use in CI pipelines, the integrations also prepend MATLAB to the `PATH` system environment variable.

| Platform | Installation Method | Runner Type | Integration Documentation |
|----------|---------------------|-------------|---------------------------|
| Azure DevOps&reg;  | <p>In your `azure-pipelines.yml` file, use an extension [task](https://marketplace.visualstudio.com/items?itemName=MathWorks.matlab-azure-devops-extension#install-matlab) to install MATLAB.</p> | <p><ul><li>Cloud-hosted</li><li>Self-hosted</li></ul></p> | [MATLAB (Visual Studio Marketplace)](https://marketplace.visualstudio.com/items?itemName=MathWorks.matlab-azure-devops-extension) |
| CircleCI&reg;      | <p>In your `.circleci/config.yml` file, use an orb [command](https://github.com/mathworks/matlab-circleci-orb/blob/master/README.md#install) to install MATLAB.</p> | <p>Cloud-hosted</p> | [Use MATLAB with CircleCI](https://github.com/mathworks/matlab-circleci-orb/blob/master/README.md) |
| GitHub Actions | <p>In your workflow file in the `.github/workflows` directory of your repository, use an [action](https://github.com/matlab-actions/setup-matlab/) to set up MATLAB.</p> | <p><ul><li>Cloud-hosted</li><li>Self-hosted</li></ul></p> | [Use MATLAB with GitHub Actions](https://github.com/matlab-actions) |
| Jenkins    | <p>In the Jenkins tool configuration interface, register a [tool](https://github.com/jenkinsci/matlab-plugin/blob/master/CONFIGDOC.md#automatically-install-matlab-using-matlab-package-manager) to automatically install products.</p> | <p>Self-hosted</p> | [MATLAB (Jenkins Plugins Index)](https://plugins.jenkins.io/matlab/) |

For a complete list of CI platform integrations for MATLAB, see [Continuous Integration with MATLAB on CI Platforms](https://www.mathworks.com/help/matlab/matlab_prog/continuous-integration-with-matlab-on-ci-platforms.html).

> [!NOTE]
> For cloud-hosted runners, the integrations automatically include the dependencies required to run MATLAB and other MathWorks products. However, if you are using a self-hosted runner, you must ensure that the required dependencies are available on your runner. For details, see the documentation for the corresponding CI platform integration.


## Use MATLAB Package Manager
If there is no built-in installation mechanism for your CI platform or if you want to have full control over the installation process, use the MATLAB Package Manager (`mpm`) to install MATLAB, Simulink, and other MathWorks products from the system command line, pipeline configuration file, or Dockerfile. For information on how to access and use `mpm`, see [Get MATLAB Package Manager](https://www.mathworks.com/help/install/ug/get-mpm-os-command-line.html). In particular, see [`mpm install`](https://www.mathworks.com/help/install/ug/mpminstall.html) for usage examples and limitations.

This table includes the typical use cases of `mpm` in CI environments.

| Use Case    | Solution    |
|-------------|-------------|
| Install products on a runner in a persistent fashion. | Use `mpm install` at the system command line. |
| Install products on a runner as part of your CI pipeline. | Use `mpm install` in the pipeline configuration file. |
| Install products in a container to run your CI pipeline. | Use `mpm install` in the [Dockerfile](https://github.com/mathworks-ref-arch/matlab-dockerfile/blob/main/alternates/non-interactive/Dockerfile) for noninteractive workflows. For more information, see [Create a MATLAB Container Image for Non-Interactive Workflows](https://github.com/mathworks-ref-arch/matlab-dockerfile/tree/main/alternates/non-interactive). |

> [!TIP]
> The [`build`](https://gitlab.com/explore/catalog/mathworks/components/matlab) component for GitLab CI/CD provides a built-in mechanism for running MATLAB code and Simulink models in a container. By default, jobs created from the `build` component run using the latest release of MATLAB in the [MATLAB container on Docker&reg; Hub](https://www.mathworks.com/help/cloudcenter/ug/matlab-container-on-docker-hub.html). To include your preferred products for a given release using `mpm`, create a custom image and pass it to the `matlab_image` input of the component.

## See Also
- [License MathWorks Products in CI Environments](./licensing.md)
- [Invoke MATLAB in CI Environments](./invoking-matlab.md)
- [Run MATLAB in Containers](./containerization.md)

----

Copyright 2026 The MathWorks, Inc.

----
