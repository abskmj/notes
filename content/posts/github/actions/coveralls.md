---
title: "Publish test coverage on Coveralls.io with a Github Action Workflow"
date: 2021-05-03T15:12:01+05:30
tags: ['Github', 'Actions', 'Workflow', 'Continuos Delivery', 'Coveralls.io', 'Tests']
---

Configure a NodeJS module to publish test coverage on [Coveralls.io](https://coveralls.io/) with a Github Action workflow.

# Steps

- Install NPM modules
```
npm install --save-dev nyc
```

- Update NPM scripts in the `package.json` file
```json
{
  "scripts": {
    "test": "nyc --reporter=lcov --reporter=text mocha test.js",
  }
}
```

- Update the `.gitignore` file
```
.nyc_output
coverage
```

- Add a Github action at `.github/workflows/tests.yml`
```yml
name: Run Tests

on: [ push, pull_request] 

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v1
      - run: npm install-ci-test
      - name: Coveralls
        uses: coverallsapp/github-action@master
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
```