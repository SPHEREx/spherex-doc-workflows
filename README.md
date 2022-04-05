# spherex-doc-workflows

[Reusable GitHub Actions workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) for building SPHEREx documents.

## build-tex.yaml

The [build-tex.yaml](.github/workflows/build-tex.yaml) workflow builds SPHEREx tex documents and their landing pages, and uploads to [spherex-docs.ipac.caltech.edu](https://spherex-docs.ipac.caltech.edu). This workflow is compatible with builds triggered by `push`, `pull_request`, and `workflow_dispatch` triggers. When a tag is pushed, this workflow also creates/updates a corresponding GitHub Release with the built PDF.

Example calling workflow:

```yaml
name: CI

'on':
  push:
  pull_request:
  workflow_dispatch:

jobs:
  build-tex:
    uses: SPHEREx/spherex-doc-workflows/.github/workflows/build-tex.yaml@v1
    with:
      doc: SSDC-MS-001
    secrets:
      docs_api_password: ${{ secrets.SPHEREX_DOCS_API_PASSWORD }}
```

### Inputs

- `doc` (string, required). This is the document's identifier, which also matches the filename of the `.tex` document. For example, `SSDC-MS-001`.
- `upload` (boolean, optional). This input can be set to `false` to disable uploads to spherex-docs.ipac.caltech.edu. The default behavior is to upload on `push` and `workflow_dispatch` events.

### Secrets

- `docs_api_password` (required). The password for the `spherex-upload` user for `docs-api.ipac.caltech.edu`.
