# Buildkite Collectors for JavaScript

Official [Buildkite Test Analytics](https://buildkite.com/test-analytics) collectors for JavaScript test frameworks ✨

⚒ **Supported test frameworks:** Jest, Jasmine, and [more coming soon](https://github.com/buildkite/test-collector-javascript/issues?q=is%3Aissue+is%3Aopen+label%3A%22test+frameworks%22).

📦 **Supported CI systems:** Buildkite, GitHub Actions, CircleCI, and others via the `BUILDKITE_ANALYTICS_*` environment variables.

## 👉 Installing

1) [Create a test suite](https://buildkite.com/docs/test-analytics), and copy the API token that it gives you.

2) Add the [`buildkite-test-collector` package](https://www.npmjs.com/package/buildkite-test-collector):

    ```bash
    # If you use npm:
    npm install --save-dev buildkite-test-collector

    # or, if you use yarn:
    yarn add --dev buildkite-test-collector
    ```

3) Add the buildkite test collector to your testing framework:

    ### Jest

    Update your [Jest configuration](https://jestjs.io/docs/configuration):<br>

    ```js
      // jest.config.js

      // Send results to Test Analytics
      reporters: [
        'default',
        'buildkite-test-collector/jest/reporter'
      ],

      // Enable column + line capture for Test Analytics
      testLocationInResults: true
    ```

    ### Jasmine

    [Add the buildkite reporter to jasmine](https://jasmine.github.io/setup/nodejs.html#reporters):<br>

    ```js
      // SpecHelper.js
      var BuildkiteReporter = require('buildkite-test-collector/jasmine/reporter');
      var buildkiteReporter = new BuildkiteReporter();

      jasmine.getEnv().addReporter(buildkiteReporter);
    ```

    ### Mocha

    [Install mocha-multi-reporters](https://github.com/stanleyhlng/mocha-multi-reporters) in your project:<br>

    ```
      npm install mocha-multi-reporters --save-dev
    ```

    and configure it to run your desired reporter and the Buildkite reporter

    ```js
      // config.json
      {
        "reporterEnabled": "spec, buildkite-test-collector/mocha/reporter"
      }
    ```

    Now update your test script to use the buildkite reporter via mocha-multi-reporters:

    ```js
      // package.json
      "scripts": {
        "test": "mocha --reporter mocha-multi-reporters --reporter-options configFile=config.json"
      },
    ```

4) Run your tests locally:<br>

    ```js
    env BUILDKITE_ANALYTICS_TOKEN=xyz npm test
    ```

5) Add the `BUILDKITE_ANALYTICS_TOKEN` secret to your CI, push your changes to a branch, and open a pull request 🎉

    ```bash
    git checkout -b add-bk-test-analytics
    git commit -am "Add Buildkite Test Analytics"
    git push origin add-bk-test-analytics
    ```

## 🔍 Debugging

To enable debugging output, set the `BUILDKITE_ANALYTICS_DEBUG_ENABLED` environment variable to `true`.

## 🔜 Roadmap

See the [GitHub 'enhancement' issues](https://github.com/buildkite/test-collector-javascript/issues?q=is%3Aissue+is%3Aopen+label%3Aenhancement) for planned features. Pull requests are always welcome, and we’ll give you feedback and guidance if you choose to contribute 💚

## ⚒ Developing

After cloning the repository, install the dependencies:

```
npm install
```

And run the tests:

```
npm test
```

Useful resources for developing collectors include the [Buildkite Test Analytics docs](https://buildkite.com/docs/test-analytics) and the [RSpec and Minitest collectors](https://github.com/buildkite/rspec-buildkite-analytics).

## 👩‍💻 Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/buildkite/test-collector-javascript

## 🚀 Releasing

```sh
# Version bump the code, tag and push
npm version [major/minor/patch]
git push && git push --tags

# Publish to the NPM registry
npm publish

# Create a new GitHub release
open "https://github.com/buildkite/test-collector-javascript/releases"
```

## 📜 License

The package is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
