SearchTwitter [![Build Status](https://travis-ci.org/pwittchen/SearchTwitter.svg)](https://travis-ci.org/pwittchen/SearchTwitter)
=============
Android app, which allows to search tweets as user types and scroll them infinitely

Utilizes [modern Android libraries](#used-libraries)

for Dependency Injection, Reactive Programming, Networking, Images Loading, Logging, User Interface, etc.

Code quality is assured by [Unit Tests](#tests), [Static Code Analysis](#static-code-analysis) and [Continuous Integration](https://travis-ci.org/pwittchen/SearchTwitter).

Contents
--------

- [Overview](#overview)
- [Screenshot](#screenshot)
- [Configuration of Twitter API keys and tokens](#configuration-of-twitter-api-keys-and-tokens)
  - [Working with secrets in Git Repository](#working-with-secrets-in-git-repository)
- [Twitter API rate limits](#twitter-api-rate-limits)
- [Building the project](#building-the-project)
- [Tests](#tests)
- [Static Code Analysis](#static-code-analysis)
- [Code style](#code-style)
- [Used libraries](#used-libraries)
- [License](#license)

Overview
--------

User can search tweets with a given keyword as he or she types or by touching search icon. Moreover, application has so called infinite scroll for tweets. Implementation of the dynamic search is quite simple thanks to RxJava and Reactive Programming principles.

Screenshot
----------

![Screenshot](https://raw.githubusercontent.com/pwittchen/SearchTwitter/master/images/screenshot.png)

Configuration of Twitter API keys and tokens
--------------------------------------------

Go to https://apps.twitter.com/ website, register your account and Twitter app. Next, generate your keys and tokens.
When you have them, go to `gradle.properties` file in the repository
and add the following contents to this file:

```
TWITTER_CONSUMER_KEY=your-consumer-key
TWITTER_CONSUMER_SECRET=your-consumer-secret
TWITTER_ACCESS_TOKEN=your-access-token
TWITTER_ACCESS_TOKEN_SECRET=your-access-token-secret
```

and set your keys and tokens to appropriate variables.

After that, you can build and run the app.

#### Working with secrets in Git Repository

We shouldn't keep tokens and API keys in the Git repository. In order to work efficiently with Git, we can add `gradle.properties` file to `.gitignore` file in the repository or add the following aliases to our `.gitconfig` file:

```
ignore-local = update-index --assume-unchanged
unignore-local = update-index --no-assume-unchanged
ignored-local = !git ls-files -v | grep "^[[:lower:]]"
```

Then, we can execute:
```
$ git ignore-local gradle.properties
```
After that, we can add our keys and tokens to this file and our secrets won't be commited or pushed.

To undo this operation, we can simply call:
```
$ git unignore-local gradle.properties
```
To list all files ingored locally in the Git repository, we can call:
```
$ git ignored-local
```

Twitter API rate limits
-----------------------

Please remember that Twitter API has its own [rate limits](https://dev.twitter.com/rest/public/rate-limiting), so when user will perform too many requests in a short period of time, further requests may be blocked for a given amount of time. Don't worry - it's not so long. Error code for rate limit is provided in `TwitterApiProvider` class and is used by RxJava error handling in `MainActivity` class.

Building the project
--------------------

We can build project with Gradle Wrapper and the following command:

```
./gradlew build
```

Tests
-----

Tets are located in `app/src/androidTest/java` and can be executed on device or emulator with the following command:

```
./gradlew connectedCheck
```

Reports from tests are located in `app/build/reports/androidTests/` directory.

Static Code Analysis
--------------------

Project uses the following tools for static code analysis configured in `config/quality.gradle`
file:
- Checkstyle
- PMD
- FindBugs
- Android Lint

Reference to this file is added in `app/build.gradle` file.

Static Code analysis can be executed with the following command:

```
./gradlew check
```

Reports from analysis are generated in `app/build/reports/` directory.

Code style
----------

Code style used in the project is called `SquareAndroid` from Java Code Styles repository by Square available at: https://github.com/square/java-code-styles.

Used libraries
--------------
- In application
  - [RxJava](https://github.com/ReactiveX/RxJava)
  - [RxAnadroid](https://github.com/ReactiveX/RxAndroid)
  - [ReactiveNetwork](https://github.com/pwittchen/ReactiveNetwork)
  - [Dagger 2](https://github.com/google/dagger)
  - [ButterKnife](https://github.com/JakeWharton/butterknife)
  - [Joda Time](https://github.com/JodaOrg/joda-time)
  - [Picasso](https://github.com/square/picasso)
  - [Twitter4J](https://github.com/yusuke/twitter4j)
  - [MaterialSearchView](https://github.com/MiguelCatalan/MaterialSearchView)
  - [InfiniteScroll](https://github.com/pwittchen/InfiniteScroll)
  - [Timber](https://github.com/JakeWharton/timber/)
- In tests
  - [JUnit4](https://github.com/junit-team/junit)
  - [Google Truth](https://github.com/google/truth)
  - [Mockito](https://github.com/mockito/mockito)

License
-------

    Copyright 2016 Piotr Wittchen

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
