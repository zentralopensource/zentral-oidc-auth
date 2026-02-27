# Zentral OIDC Auth — GitHub Action

Authenticate with Zentral server using GitHub OIDC tokens to obtain short-lived API tokens. No stored credentials required.

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

  - name: Use the token
    run: curl -H "Authorization: Bearer $ZENTRAL_API_TOKEN" https://api.your-platform.com/v1/apiaction
