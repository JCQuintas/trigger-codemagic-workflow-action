Trigger Codemagic workflow
==========================

GitHub Action to trigger a workflow on [Codemagic CI/CD](https://codemagic.io).

Quick start
-----------

Add the following configuration to `.github/workflows/main.yml` to trigger Codemagic build on any push event.

    on: push

    jobs:
      trigger-codemagic-build:
        runs-on: ubuntu-latest
        steps:
          - name: Trigger Codemagic build
            uses: codemagic-ci-cd/trigger-codemagic-workflow-action@v1.0.0
            with:
              app-id: <MY-APPLICATION-ID>
              workflow-id: <MY-WORKFLOW-ID>
              token: ${{ secrets.CODEMAGIC_API_TOKEN }}

Inputs
------

| Argument      | Description                                                                                       |
| ------------- | ------------------------------------------------------------------------------------------------- |
| `app-id`      | [Application ID](https://docs.codemagic.io/rest-api/applications/) [**required**]                 |
| `workflow-id` | [Workflow ID](https://docs.codemagic.io/rest-api/builds/) [**required**]                          |
| `token`       | [API token](https://docs.codemagic.io/rest-api/codemagic-rest-api/#authentication) [**required**] |
| `branch`      | GitHub event branch override                                                                      |
| `tag`         | GitHub event tag override                                                                         |
| `labels`      | Build labels, one label per line                                                                  |
| `xcode`       | Xcode version e.g. 14.1                                                                           |
| `flutter`     | Flutter version e.g. 3.3.3                                                                        |
| `cocoapods`   | CocoaPods version e.g. 0.29.0                                                                     |
| `node`        | Node version e.g. 16                                                                              |
| `npm`         | NPM version e.g. 8.19.2                                                                           |
| `ndk`         | NDK version e.g. 25.1.8937393                                                                     |
| `java`        | Java version e.g. 18                                                                              |
| `ruby`        | Ruby version e.g. 3.1.2                                                                           |

Note that branch and tag names are inferred from the event that triggered the action. `branch` or `tag` arguments will override the values from the event. `tag` argument takes precedence over `branch` if both arguments are provided.

Environment variables
---------------------

Use the `CM_` prefix to pass environment variables to Codemagic builds.

For example, define the `CM_FOO` variable in the GitHub Action step configuration:

    env:
      CM_FOO: bar

The corresponding variable `FOO` (without the `CM_` prefix) will be available during the Codemagic build.

Outputs
-------

Output variables can be used later in the action steps:

    - name: Build ID
      run: echo "${{ steps.build.outputs.build-id }}"

| Output variable    | Description                                       |
| ------------------ | ------------------------------------------------- |
| `build-id`         | Codemagic build ID                                |
| `build-api-url`    | Build status API endpoint                         |
| `build-url`        | Build page, requires Codemagic account for access |

Development
-----------

Install dependencies

    yarn

Complie sources and dependencies into a standalone module

    yarn ncc build --minify index.js --license LICENSE

