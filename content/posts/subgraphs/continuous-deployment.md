---
title: "Continuous Deployment pipeline for a Subgraph"
date: 2022-02-09T15:41:04+05:30
tags: ["Continuous Deployment", "Subgraphs", "TheGraph.com", "Gitlab"]
---

Steps to implement a continuous deployment (CD) pipeline to deploy a subgraph to The Graph's hosted service.

> [The Graph](https://thegraph.com/) is an indexing protocol for querying networks like Ethereum and IPFS. Anyone can build and publish open APIs, called subgraphs, making data easily accessible.

# NPM Scripts
Below scripts need to be added in the `package.json` file.

1. Generate the assembly code
2. Authenticate with The Graph's hosted service
3. Deploy

```javascript
// package.json

{
  "scripts": {
    "codegen": "graph codegen",
    "auth": "graph auth --product hosted-service",
    "deploy": "graph deploy --product hosted-service <user/subgraph>"
  }
}
```
The scripts can be used on local as well

```
npm run codegen
npm run auth <token>
npm run deploy
```

# Gitlab Pipeline
Below is a sample pipeline using Gitlab CI/CD. `$GRAPH_TOKEN` is the authentication token for The Graph's hosted service.

```yml
# .gitlab-ci.yml 

image: node:latest

deploy:
  only:
    - main
  script:
    - npm ci
    - npm run codegen
    - npm run auth $GRAPH_TOKEN
    - npm run deploy
```

# References
- [Deploy a Subgraph to the Hosted Service](https://thegraph.com/docs/en/hosted-service/deploy-subgraph-hosted/)