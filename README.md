# toitlang/action-code-sign

The code-sign-action action integrates with Digicert One and uses SignTool on Windows runners and JSign on Linux runners..

Forked from https://github.com/cognitedata/code-sign-action. This action is modified so it is more configurable.
------------

## Usage

### Inputs
- `certificate-host`: The host of the certificate. Defaults to `https://clientauth.one.digicert.com`.
- `certificate`: The certificate to use for signing. Must be in base64.
- `certificate-password`: The password for the certificate.
- `certificate-fingerprint`: The fingerprint of the certificate to use for signing.
- `api-key`: The API key to use for signing.
- `keypair-alias`: The alias of the keypair to use for signing.
- `path`: A path to a file or a folder that contains the files to sign.

### Examples

#### Sign a single file on Windows

```yaml
name: codesign-example-single-file
on:
  push:
    branches:
      - main
      - 'releases/*'

jobs:
  run-action:
    runs-on: windows-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run the action for a single file
        uses: toitlang/action-code-sign@v1
        with:
          certificate: ${{ secrets.DIGICERT_CERTIFICATE }}
          api-key: ${{ secrets.DIGICERT_API_KEY }}
          certificate-password: ${{ secrets.DIGICERT_PASSWORD }}
          certificate-fingerprint: ${{ secrets.DIGICERT_FINGERPRINT }}
          keypair-alias: ${{ vars.DIGICERT_KEYPAIR_ALIAS }}
          path: test\test.exe
```

#### Sign multiple files on Linux

```yaml
name: codesign-example-multiple-files
on:
  pull_request:
  push:
    branches:
      - main
      - "releases/*"

jobs:
  run-action-linux:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run the action for multiple files in directory
        uses: toitlang/action-code-sign@v1
        with:
          certificate: ${{ secrets.DIGICERT_CERTIFICATE }}
          api-key: ${{ secrets.DIGICERT_API_KEY }}
          certificate-password: ${{ secrets.DIGICERT_PASSWORD }}
          certificate-fingerprint: ${{ secrets.DIGICERT_FINGERPRINT }}
          keypair-alias: ${{ vars.DIGICERT_KEYPAIR_ALIAS }}
          path: test
```
