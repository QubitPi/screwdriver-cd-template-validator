# Template Validator

[![Version][NPM badge]][NPM URL]
[![GitHub Workflow Status][GitHub Workflow Status badge]][GitHub Workflow Status URL]
![GitHub Last Commit badge]
![License badge]

> A module for validating and parsing a Screwdriver Template file

## yaml

```yaml
# example.yaml
name: tkyi/nodejs_main
version: 2.0.1
description: |
  Template for a NodeJS main job. Installs the NPM module dependencies and executes
  the test target.
maintainer: tiffanykyi@gmail.com
config:
  image: node:4
  steps:
    - install: npm install
    - test: npm test
  environment:
    NODE_ENV: production
  secrets:
     - NPM_TOKEN

```

## Usage


```bash
$ npm install screwdriver-cd-template-validator
```

Validate in Node.js:

```javascript
const fs = require('fs');  // standard fs module
const validator = require('screwdriver-cd-template-validator');

// The "example.yaml" is the YAML described above
validator(fs.readFileSync('example.yaml'))
    .then((templateData) => {
        console.log(templateData);
    });
```

Output of the console.log():

```javascript
{
    "name": "tkyi/nodejs_main",
    "version": "2.0.1",
    "description": "Template for a NodeJS main ...",  //truncated for brevity
    "maintainer": "tiffanykyi@gmail.com",
    "config": {
        "environment": {
            "NODE_ENV": "production"
        },
        "image": "node:4",
        "secrets": [
            "NPM_TOKEN"
        ],
        "steps": [{
            "install": "npm install"
        }, {
            "test": "npm test"
        }]
    }
}
```





## Testing

```bash
npm test
```

## License

Code licensed under the BSD 3-Clause license. See LICENSE file for terms.

[GitHub Last Commit badge]: https://img.shields.io/github/last-commit/QubitPi/screwdriver-cd-template-validator/master?logo=github&style=for-the-badge
[GitHub Workflow Status badge]: https://img.shields.io/github/actions/workflow/status/QubitPi/screwdriver-cd-template-validator/ci-cd.yml?branch=master&logo=github&style=for-the-badge
[GitHub Workflow Status URL]: https://github.com/QubitPi/screwdriver-cd-template-validator/actions/workflows/ci-cd.yml

[License badge]: https://img.shields.io/npm/l/screwdriver-cd-template-validator.svg?style=for-the-badge

[NPM badge]: https://img.shields.io/npm/v/screwdriver-cd-template-validator.svg?style=for-the-badge
[NPM URL]: https://www.npmjs.com/package/screwdriver-cd-template-validator
