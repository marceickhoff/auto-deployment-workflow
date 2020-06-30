# GitHub Workflow Template for SSH Auto Deployment
![license](https://img.shields.io/github/license/marceickhoff/auto-deployment-workflow)

This repository contains a Workflow template for GitHub Actions that uses [appleboy/ssh-action](https://github.com/marketplace/actions/ssh-remote-commands) to run a deployment script via SSH on your server.

## Usage

First, paste the ``.github/workflows/auto-deployment.yml`` into your repository. Change ``on.push.branches`` to all branches that should have an auto deployment. By default, those are ``master`` and ``stage``.

Now create the ``AUTO_DEPLOYMENT_HOST``, ``AUTO_DEPLOYMENT_USER`` and ``AUTO_DEPLOYMENT_PASSWORD`` secrets in your repository settings.

On your server, in the home directory of the specified user, create a directory ``~/deployments/repository-name``. For each branch that should have auto deployment enabled, create a file ``branch-name.sh`` with all commands that should be executed when the branch is pushed. It might look like this:

```shell script
cd /home/user/www/your-website
git pull
npm i
npm run build
```

Make sure to give it the right file permissions: ``chmod +x branch-name.sh``.

That's it. When you push to one of the specified branches, the auto deployment will start.
