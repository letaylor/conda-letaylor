
# conda-letaylor

This repo contains conda recipes that are automatically built using Travis CI. It is not designed to scale to many recipes as each recipe is updated if any one recipe changes.

# Automatic Uploads to Anaconda from Travis CI

## 1. Edit config files

Edit the following files:
* `../.travis.yml` : alter packages listed after install.

## 2. Give Travis CI access to upload to Anaconda

Store both `deploy_anaconda.sh::$CONDA_USER_NAME` and `deploy_anaconda.sh::$CONDA_UPLOAD_TOKEN` securely in on Travis CI. These are used to authenticate the `anaconda upload` command.

1. Login to the account you want Travis to use to upload on [anaconda.org](https://anaconda.org).
2. Click on your username on the top left and go to 'My Settings'.
3. On the left hand panel, go to 'Access' and enter your password as requested.
4. Now we'll create an API token. Give it a name, and **check at least both 'Allow read access to the API site' and 'Allow write access to the API site'**.
5. Create the token and copy it.
6. Login to your account on [travis-ci.org](https://travis-ci.org) and go to the repository that you want to add this automatic functionality to.
7. On the right next to 'More options' go to 'Settings' in the hamburger menu.
8. Add an environment variable with the name `CONDA_UPLOAD_TOKEN` and give it the value of the API token that you copied from [anaconda.org](https://anaconda.org).
9. Add an environment variable with the name `CONDA_USER_NAME` and give it your [anaconda.org](https://anaconda.org) user name.

Or get `CONDA_UPLOAD_TOKEN` from the command line:

```bash
anaconda login
anaconda auth -c -n travis \
    --max-age 307584000 \
    --url https://anaconda.org/${CONDA_USER_NAME}/${PKG_NAME} \
    --scopes "api:write api:read"
```
