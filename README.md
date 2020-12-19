# Custom dokku deploy for GitHub Actions

Deploy an application to bycoders dokku server over SSH.

## Usage

To use the action add the following lines to your `.github/workflows/main.yml`

```yaml
name: deploy

on: pull_request

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v1
      - name: Deploy the application
        uses: jackii/deploy-dokku-action@main
        with:
          PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}
          PUBLIC_KEY: ${{ secrets.SSH_PUBLIC_KEY }}
          DOKKU_HOST: ${{ secrets.DOKKU_HOST }}
          DOKKU_USER: ${{ secrets.DOKKU_USER}}
          PROJECT: project-name
          BRANCH: ${{ github.head_ref }}
```

### Required Variables

* **PRIVATE_KEY**: Your SSH private key, preferably from Secrets.
* **PUBLIC_KEY**: Your SSH public key, preferably from Secrets.
* **DOKKU_HOST**: The host the action will SSH to run the git push command. ie, `your.site.com`.
* **DOKKU_USER**: The user that will run the command.
* **PROJECT**: The project name is used to define the app name.
* **BRANCH**: Repository branch that should be used for deploy, `master` is set by default.
