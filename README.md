# Gradle Print Code Coverage Plugin

Scraps [jacoco](http://www.eclemma.org/jacoco/) test reports and prints the 
code coverage to the console. Tools like [GitLab](https://about.gitlab.com/)
can then parse for it for better integration.

For more information see [GitLab's documentation on test coverage](https://docs.gitlab.com/ee/ci/yaml/index.html#coverage) ([examples](https://docs.gitlab.com/ee/ci/pipelines/settings.html#test-coverage-examples)).

This plugin is a fork from [de.jansauer.printcoverage](https://github.com/jansauer/gradle-print-coverage-plugin).
See the section "[Fork](#fork)" for further information on the reasoning and how to migrate to this plugin.

## Getting Started

Add this snippet to your build script.

```
plugins {
  id 'jacoco'
  id 'de.pinguinkiste.printcoverage' version '3.0.0'
} 
```

Extend your ci job configuration.

```
build-gradle:
  stage: build
  script:
    - ./gradlew build printCoverage
  coverage: '/^Coverage:\s(\d+\.\d+%)/'
```

## Tasks

* `printCoverage` The one that prints the coverage ;-) 

## Configuration

```
printcoverage {
  coverageType = 'INSTRUCTION'
}
```

* `coverageType`: Type of [coverage metric](http://www.eclemma.org/jacoco/trunk/doc/counters.html) to be printed.<br>
  One of 'INSTRUCTION', 'BRANCH', 'LINE', 'COMPLEXITY', 'METHOD' or 'CLASS'<br>
  Default: 'INSTRUCTION'

## Publishing Workflow

Every commit on this repository gets tested via GitHub Actions.
Commits that are tagged with a semantic version are also automatically 
published to the gradle plugin directory as a new version.

## Fork

This plugin is a fork from Jan Sauer's original plugin, `de.jansauer.printcoverage`.

### Reason

I decided to fork this plugin because the original plugin had a growing list of issues, and I was not able to establish contact with Jan to share the maintenance.
Some of its issues are annoying, and some are wasting build time, but it got to a point where it is no longer usable with current Gradle versions.
I depend on the plugin myself, and still think it is useful, and wanted to get it up-to-date again.

### Migrating to the plugin

Because of the fork, I had to change the plugin identifier and namespace, and bump of the major version because of that.
Version 3.0.0 represents these changes.
No other modifications on the codebase were made (except building on GitHub Actions instead of CircleCI, as well as minor plugin updates to make the workflows work).
If your builds worked before with version 2.0.0 of the original plugin, they should work with version 3.0.0 of this fork.

All changes, like bugfixes, are done after version 3.0.0 version, and will be documented in a [changelog](CHANGELOG.md).
Although I will try my best, not all of those might be backwards compatible.
I will document those changes and communicate them via semantic versioning.
So if you decide to use a version greater than 3.0.0, please check the documentation and update your build scripts accordingly.

### Planned features

* [ ] Make the plugin compatible with Gradle 8+
* [ ] Fix all open issues against the original codebase
* [ ] Support task avoidance / lazy configuration
* [ ] Ensure plugin works properly with build cache
* [ ] Update dependencies to versions without known security issues

## Contributing

Pull requests are always welcome. I'm grateful for any help or inspiration.

## License and Authors

* Jan Sauer <[jan@jansauer.de](mailto:jan@jansauer.de)> ([https://jansauer.de](https://jansauer.de)) – Original version of this plugin
* Manuel Prinz <[manuel@pinguinkiste.de](mailto:manuel@pinguinkiste.de)> – Current maintainer of this fork

```text
Copyright 2018, Jan Sauer <jan@jansauer.de> (https://jansauer.de)
Copyright 2023, Manuel Prinz <manuel@pinguinkiste.de>

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
