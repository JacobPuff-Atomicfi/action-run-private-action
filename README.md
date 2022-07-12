<!-- start title -->

# GitHub Action:Hello World

<!-- end title -->
<!-- start description -->

Greet someone

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: JacobPuff-Atomicfi/action-run-private-action@undefined
  with:
    # Token to use to get access to the private repo. Required.
    token: ""
    # Private repo name e.g. "example/private-action". Required.
    repo: ""
    # Ref for private action version. Required.
    ref:
    # Json object of `inputs` to pass to private action
    # Default: "{}"
    json-inputs: ""
    # Json object of `env` to pass to private action
    # Default: "{}"
    json-env: ""
    # Where to store the private action under `$GITHUB_WORKSPACE`
    # Default: "../private-actions/"
    path: ""
```

<!-- end usage -->
<!-- start inputs -->

| **Input**         | **Description**                                             | **Default**           | **Required** |
| :---------------- | :---------------------------------------------------------- | :-------------------: | :----------: |
| **`token`**       | Token to use to get access to the private repo              |                       |   **true**   |
| **`repo`**        | Private repo name e.g. "example/private-action"             |                       |   **true**   |
| **`ref`**         | Ref for private action version                              |                       |   **true**   |
| **`json-inputs`** | Json object of `inputs` to pass to private action           | `{}`                  |   **false**  |
| **`json-env`**    | Json object of `env` to pass to private action              | `{}`                  |   **false**  |
| **`path`**        | Where to store the private action under `$GITHUB_WORKSPACE` | `../private-actions/` |   **false**  |

<!-- end inputs -->
<!-- start outputs -->

| **Output**     | **Description**                                  |
| :------------- | :----------------------------------------------- |
| `json-outputs` | Json object of `outputs` from the private action |

<!-- end outputs -->
<!-- start examples -->

### Example usage

```yaml
on: [push]

jobs:
  run-private-action:
    runs-on: ubuntu-latest
    name: Runs a private action
    steps:
      - uses: actions/checkout@v2
      - uses: JacobPuff-Atomicfi/action-run-private-action@v1.0.0
        id: private
        with:
          token: ${{ secrets.YOUR_PAT_OR_SOMETHING }}
          repo: example/private-action
          ref: v1
          json-inputs: |
            {
              "example": "this is an example"
              "test": "this is a test"
              "require-passing": true
            }
          json-env: |
            {"USE_PRETTY_PRINT": true}
      - run: echo json output ${{ steps.private.outputs.json-outputs }}
```

<!-- end examples -->