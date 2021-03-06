# WebDriverIO v4

Examples of [webdriver.io](http://v4.webdriver.io/) v4 in action!

## Installation

1. [Install webdriver.io](http://webdriver.io/guide/getstarted/install.html) using `npm i webdriverio@4`
    - Requires you have [node.js installed](https://nodejs.org/en/download/)
2. Install and Configure [Docker Desktop](https://www.docker.com/get-started)
3. [Run Tests](RUNNING.md)

## Architecture:

Our current automated GUI test architecture is:

- Written in JavaScript
- Jasmine is our test framework
- Using Chai for assertions
- Package manager is NPM
- WDIO as the test runner
- WebDriver.io as the driver / library (aka Selenium)

## Timeout strategy

Time is a crucial component in the whole test process. Each command is fired to a Selenium server and its response contains the results of the action. When a certain action depends on the state of a different action, they need to be executed in the right order and timeouts play a crucial role in this.

We set timeouts on a few levels:

1. Framework timeouts

MochaJS has a default timeout of 10 seconds which means a single test shouldn't take longer than that. Since our tests are run at the UI, they need more than 10 seconds to complete so we override it in wdio.conf.js under mochaOpts to be 40s globally.

2. WaitForXX timeouts

Also called implicit timeouts, all of our locator detections (waitForExist, waitForVisible, et. al) also have a default timeout set in wdio.conf.js to be 15s. This means we will wait for elements for up to 15 seconds before our tests fail.
