---
title: "Deploy functions on Spotinst using Serverless Framework"
date: 2019-01-08T09:56:04Z
tags: ["Spotinst", "Node.js", "NPM" , "Tutorial", "Serverless"]
---

[Spotinst](https://spotinst.com/products/spotinst-functions/) is one of the providers which support deploying serverless functions or FaaS (Function as a Service). [Serverless Framework](https://serverless.com/) is an NPM module which makes building serverless applications easy and open.

# Isolated Workspace
The steps listed below is different from the traditional steps listed on the official site. I always like to keep all the NPM modules and related files within the project directory to keep things isolated from other projects. This also allows me to use multiple Spotinst credentials for multiple serverless applications.

# Serverless Framework

## Installation
Install both the framework and the Spotinst plugin.

```
npm install --save-dev serverless serverless-spotinst-funtions
```

## Credentials
Save the spotinst credentials for serverless framework.
```
HOME=./ npx serverless config credentials --provider spotinst --token {{your token}}  --account {{your account id}}
```

- `HOME=./` sets the home directory as current project directory so that the Spotinst credentials are stored within the project directory instead of `~/.spotinst/credentials`.
- `npx` is used (instead of `npm`) as serverless is installed as a local module.
- Spotinst Account ID can be found at https://console.spotinst.com/#/settings/account/general
- Spotinst Token can be found at https://console.spotinst.com/#/settings/tokens/permanent

## Configuration
Create a `serverless.yml` file in the root directory of the project.
```yaml
# Welcome to Serverless!
#
# This file is the main config file for your service.
# It's very minimal at this point and uses default values.
# You can always add more config options for more control.
# We've included some commented out config examples here.
# Just uncomment any of them to get that config option.
#
# For full config options, check the docs:
#    docs.serverless.com
#
# Happy Coding!

service: demo # NOTE: update this with your service name

provider:
  name: spotinst
  #stage: <Stage Name>  #Optional. Defaults to 'dev', see https://help.spotinst.com/hc/en-us/articles/115005893409
  spotinst:
    environment: env-c0XXbXeb #<env-XXXX> Required.

functions:
  hello:
    runtime: nodejs8.3
    handler: handler.main
    memory: 128
    timeout: 30
    access: private
#    iamRoleConfig:
#      roleId: # role-id
#    activeVersions:
#        - "version": "$LATEST"
#          "percentage": 100.0
#    cors:
#        enabled: # false by default
#        origin:  # '*' by default
#        headers: # 'Content-Type,Authorization' by default
#        methods: # 'DELETE,GET,HEAD,OPTIONS,PATCH,POST,PUT' by default
#    cron:  # Setup scheduled trigger with cron expression
#      active: true
#      value: '* * * * *'
#    environmentVariables:
#      key: Value

# extend the framework using plugins listed here:
# https://github.com/serverless/plugins
plugins:
  - serverless-spotinst-functions

```
## Deployment
Add a `deploy` script to `package.json` file.
```
{
  ...
  "scripts": {
    ...
    "deploy": "HOME=./ serverless deploy"
  },
  ...
}

```
Run the script to deploy.
```
npm run deploy
```
## Version Control
Some of the serverless directories or files should not be tracked as part of the version control. These can be added to a `.gitignore` file.
```
# package directories
node_modules

# serverless directories
.aws
.config
.serverless
.serverlessrc
.spotinst
```