# Zentral OIDC Auth — GitHub Action

Authenticate with Zentral server using GitHub OIDC tokens to obtain short-lived API tokens. No stored credentials required.

The action w


## Usage

```yaml
permissions:
  id-token: write
  contents: read

steps:
  - name: Authenticate with Zentral
    id: auth
    uses: zentralopensource/zentral-oidc-auth@v1
    with:
      ztl-fqdn: https://mdm.zentral.com # required
      ztl-oidc-api-token-issuer-id: ${{ vars.ZTL_OIDC_API_TOKEN_ISSUER_ID }} # required
      ztl-api-token-name: "Token for my Github action" # optional
      ztl-api-token-validity: 1200 # optional
      ztl-oidc-debug: 1 # optional

  - name: Use the token
    run: curl -H "Authorization: Bearer $ZTL_API_TOKEN" https://api.your-platform.com/v1/apiaction
```

## Permissions

When the action runs, the ```id-token: write``` permission allows the GITHUB_TOKEN to make an API call to generate an OIDC token (which is an extra security token, a standard one).

## Inputs

### `ztl-fqdn`

**Required** your Zentral plattform fully qualifid domain name

### `ztl-oidc-api-token-issuer-id`

**Required** oidc token issuer id


### `ztl-oidc-debug`

_Optional_ a boolean (0 or 1) to manage the display of additional information in the workflow output. Defaults to false (0).


### `ztl-api-token-name`

_Optional_ name for the short-lived api token. Defaults to `Github action`


### `ztl-api-token-validity`

_Optional_ time the short-lived api token should be valid in seconds. Defaults to `600` seconds.


## Outputs

All outputs are availible as variables in the scope the workflow steps ` steps.auth.outputs.ztl-api-token`. Furthermore they will be amde available as enviroment variables in the scope of the running workflow `$ZTL_API_TOKEN`.

### `ztl-api-token` / `$ZTL_API_TOKEN`

The short-lived API token

### `ztl-api-username` / `$ZTL_API_USERNAME`

The username associated with the API token

### `ztl-api-useremail` / `$ZTL_API_USEREMAIL`

The user email associated with the API token