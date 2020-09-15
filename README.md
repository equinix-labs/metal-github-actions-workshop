# packet-actions-example

Example of Packet Github Actions for creating and clearing [Packet](https://packet.com) Projects.

## Actions

This project demonstrates the use of two Github Actions:

* <https://github.com/displague/packet-project-action>
* <https://github.com/displague/packet-sweeper-action>

The `.github/workflows/packet.yml` workflow invokes these two actions to first create a Packet project, and then to delete that project.

The project id is emitted before the project is deleted. This is where a CI/CD workflow could be inserted that takes advantage of this project.
And resources created in that project, not cleanly disposed of by the inserted tools, will be removed by the Packet Sweeper action.

```yaml
name: 'packet'

on:
  push:
    branches:
    - master
  pull_request:

jobs:
  project:
    runs-on: ubuntu-latest
    # TODO(displague) PACKET_AUTH_TOKEN should be defined once, globally
    # TODO(displague) PROJECT_ID should also be globalized
    steps:
    - id: packet-project
      uses: displague/packet-project-action@v0.1.0
      env:
        PACKET_AUTH_TOKEN: ${{ secrets.PACKET_AUTH_TOKEN }}
    - name: Use the Project ID (display it)
      run: |
        echo Packet Project "$PROJECT_NAME" has ID "$PROJECT_ID"
      env:
        PROJECT_ID: ${{ steps.packet-project.outputs.projectID }}
        PROJECT_NAME: ${{ steps.packet-project.outputs.projectName }}
    - name: Project Delete
      uses: displague/packet-sweeper-action@v0.1.0
      env:
        PROJECT_ID: ${{ steps.packet-project.outputs.projectID }}
        PACKET_AUTH_TOKEN: ${{ secrets.PACKET_AUTH_TOKEN }}
```
