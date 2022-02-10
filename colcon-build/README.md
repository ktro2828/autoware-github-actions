# colcon-build

This action runs `colcon build`.

## Usage

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    container: ros:galactic
    steps:
      - name: Check out repository
        uses: actions/checkout@v2
        with:
          fetch-depth: 0

      - name: Get modified packages
        id: get-modified-packages
        uses: autowarefoundation/autoware-github-actions/get-modified-packages@tier4/proposal

      - name: Build
        if: ${{ steps.get-modified-packages.outputs.modified-packages != '' }}
        uses: autowarefoundation/autoware-github-actions/colcon-build@tier4/proposal
        with:
          rosdistro: galactic
          target-packages: ${{ steps.get-modified-packages.outputs.modified-packages }}
          build-depends-repos: build_depends.repos
```

## Inputs

| Name                | Required | Description                                         |
| ------------------- | -------- | --------------------------------------------------- |
| rosdistro           | true     | ROS distro.                                         |
| target-packages     | true     | The target packages to build.                       |
| build-depends-repos | false    | The `.repos` file that includes build dependencies. |
| token               | false    | The token for build dependencies.                   |

## Outputs

None.