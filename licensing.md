# License MathWorks Products in CI Environments

Product licensing for your continuous integration (CI) pipeline depends on your project visibility and the types of products the pipeline uses:
- Public project — The CI platform integration for MATLAB&reg; automatically licenses all products available to your account, except for transformation products, such as MATLAB Coder™ and MATLAB Compiler™. For a full list of transformation products, see “Transformation Programs” in the [Program Offering Guide](https://www.mathworks.com/help/pdf_doc/offering/offering.pdf).
- Private project — The CI platform integration for MATLAB does not automatically license any products for you.

To license products that are not automatically licensed, you can request a [MATLAB batch licensing token](https://github.com/mathworks-ref-arch/matlab-dockerfile/blob/main/alternates/non-interactive/MATLAB-BATCH.md#matlab-batch-licensing-token) by submitting the [MATLAB Batch Licensing Pilot form](https://www.mathworks.com/support/batch-tokens.html). Batch licensing tokens are strings that enable MATLAB to start in noninteractive environments.

## License Types for Containers and Ephemeral Environments

Containers and cloud-hosted VMs regenerate host identifiers, such as MAC addresses and disk serial numbers, on every startup. Licensing mechanisms that validate against a stable host ID fail in these environments. Choose a licensing mechanism that is compatible with your execution environment.

| Licensing Mechanism | Container Compatible | Notes |
|---|---|---|
| Batch licensing token | Yes | The token authenticates independently of the host ID. Use batch tokens for CI. |
| Network license manager (`port@host`) | Yes | The license server validates the license, not the local host. |
| Node-locked license | No | This license type locks to a specific host ID. Use node-locked licenses only on persistent, self-hosted runners. |

For most CI workflows, use a batch licensing token. If your organization already has a network license server, you can use it in containers as well. Contact your license administrator for help choosing a licensing mechanism.

## Considerations for Batch Token Licensing

If you have products that are not automatically licensed, review the following considerations:
- Batch token licensing is recommended for scalable CI workflows and is the focus of this guide. For other licensing options, contact your license administrator.
- Batch token licensing is compatible with containers (see [License Types for Containers and Ephemeral Environments](#license-types-for-containers-and-ephemeral-environments)). You can build and customize a MATLAB container using batch token licensing and the MATLAB Package Manager (`mpm`). For a sample Dockerfile, see [Create a MATLAB Container Image for Non-Interactive Workflows](https://github.com/mathworks-ref-arch/matlab-dockerfile/tree/main/alternates/non-interactive).
- Batch token licensing does not support MATLAB Engine API for Python&reg;. Most Python-based CI workflows require a different licensing option. Contact your license administrator for alternatives.
- Polyspace&reg; products require a dedicated license server that runs on a machine separate from the CI agent.

## See Also
- [Install MathWorks Products in CI Environments](./installation.md)
- [Invoke MATLAB in CI Environments](./invoking-matlab.md)
- [Run MATLAB in Containers](./containerization.md)

----

Copyright 2026 The MathWorks, Inc.

----
