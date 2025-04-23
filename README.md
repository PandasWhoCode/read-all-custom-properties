# README for the project Read All Custom Properties

**Read all custom properties and values from all repos in the organization and write to a file.**

This action uses the GitHub CLI to read all properties from all repos in the organization. It can write
the results to a `repo-properties.yaml` file as well, for use with input to 
[update custom properties](https://github.com/PandasWhoCode/update-custom-properties) action.

---

## 🚀 Getting Started

1. Add this GitHub Action to your workflow.
2. Run the workflow. A new commit will be generated on the branch you run it from containing the `repo-properties.yaml`
file.

---

## Fine Grained Token Requirements

To run the action within your GitHub CI/CD pipeline you will need to create a
fine-grained token with the following permissions:

### Organization Permissions

- Read access to organization custom properties

### Repository Permissions

- Read access to Repository Metadata
- Read and Write access to Repository contents

### Additional Information

- [GitHub API for custom property for an organization](https://docs.github.com/en/rest/orgs/custom-properties?apiVersion=2022-11-28#create-or-update-a-custom-property-for-an-organization)
- [Fine-grained personal access tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token)
- The owner of the fine-grained token must have full administrative rights to the organization.

---

## 📦 Inputs

| Name                               | Description                                                            | Required | Default |
|------------------------------------|------------------------------------------------------------------------|----------|---------|
| `token`                            | GitHub Personal Access Token (Fine-Grained with: Organization custom properties `Read`, Repository contents `Read and Write` scope)     | ✅ Yes    | —       |
| `overwrite-existing-file`          | Boolean for choosing to overwrite `repo-properties.json`, if it exists | 🟥  No   | `false` |
| `dry-run-enabled`                  | Flag to dry-run the script, will not commit in repo.                   | 🟥  No   | `false` |
| `commit-author-name`               | Author Name on the commit that will be created                         | ✅ Yes    | -       |
| `commit-author-email`              | Author Email on the commit that will be created                        | ✅ Yes    | -       |
| `commit-author-gpg-key-contents`   | GPG Key for the commit that will be created (must match the `email`)   | ✅ Yes    | -       |
| `commit-author-gpg-key-passphrase` | GPG Key Passphrase for the key to sign the commit that will be created | ✅ Yes    | -       |

---

## 🛠 Usage

```yaml
jobs:
  update-schema:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: PandasWhoCode/read-all-custom-properties@1-create-an-action-to-read-all-custom-properties
        with:
          token: ${{ secrets.GH_CUSTOM_PROPS_TOKEN_WRITABLE }}
          overwrite-existing-file: ${{ inputs.overwrite-existing-file }}
          dry-run-enabled: ${{ inputs.dry-run-enabled }}
          commit-author-name: ${{ inputs.commit-author-name }}
          commit-author-email: ${{ inputs.commit-author-email }}
          commit-author-gpg-key-contents: ${{ secrets.GPG_KEY_CONTENTS }}
          commit-author-gpg-key-passphrase: ${{ secrets.GPG_KEY_PASSPHRASE }}
```

---

## 👤 Author

Andrew Brandt

[PandasWhoCode](https://pandaswhocode.com)

[andrew.brandt@pandaswhocode.com](mailto:andrew.brandt@pandaswhocode.com)

---