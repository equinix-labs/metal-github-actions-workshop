# Workshop: Equinix Labs

<!---
Using this template in a new project? See CONTIBUTING.md for help.
--->

This repo contains instructions for the ["Equinix Labs" workshop](https://equinix-labs.github.io/equinix-labs-workshop).

To view the workshop, visit <https://equinix-labs.github.io/equinix-labs-workshop>

TODO: Below is the original README of the repo; this should go away in favor of the workshop content

## Reasons

Automation workflows on Equinix Metal can benefit from from creating Project API Keys from the Equinix Metal API with a seed User API Key.

Most CI jobs that take advantage of a Project API key to provision infrastructure work within a predefined project and then delete test infrastructure when the CI job is complete. If the CI job fails, this may leave orphaned resources behind in that project, which incur costs and pose security risks. These orphaned resources may also lead to failures in future jobs within that project (because quotas are consumed or because unexpected resources, changing the expected results of listed resources).

To alleviate this, a user may choose to create a new Project on each build and to tear down that project (with a "sweeper") at the end of the build. Because the project is not known in advance, the user can not use an existing Project API Key in this situation.

Thankfully, the Equinix Metal API allows for the dynamic generation of Project API Keys.

There are a number of benefits to using an ephemeral token with least privilege, a Project API key, in these dynamic project configurations:

* The CI test is confined to manipulating (and potentially breaking) the test Project resources
* The Project Key can be disposed of with the disposal of the project
* Leaked project keys have a narrow window of usability and minimized splash radius

In [this example project](https://github.com/equinix-labs/metal-actions-example/), we take advantage of a Github Workflow that creates a random project, performs some project specific tasks, and then deletes the project. This workflow (and the "metal-project-action" which creates the project) benefit from the ability to generate and exchange a powerful (and therefor dangerous) user API token with a confined and less-dangerous project API token for the Github actions that should be confined to work within the generated project.
