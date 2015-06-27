mocha-react
===========

This is a fork of the excellent demo by [danvk][1], of using MochaJS to test a ReactJS component (with JSX and Harmony). I made a few changes to work with my setup and thought others might find it useful too.

The main differences are:

1. Helper scripts are modified to recognise JSX files via the .jsx extension
2. Due to issues with the dependency on [contextify][2], I switched from using `jsdom` to `jsdom-no-contextify`. I'm also using a modified version of [the code snippet from the original blog post][3] instead of `mocha-jsdom`.
3. Code coverage is still instrumented via Blanket, but I've shown how it can be done for [SonarQube][4] instead of Coveralls. See my [blog post][5] for more details on getting JavaScript test coverage going with Mocha.

Quick start:

```
npm install
npm test
```

What this template gets you:

- JSX/Harmony transpilation
- Opt-in module stubbing (ala Jest's "auto-mocking")
- Code coverage via Blanket, prepared for consumption by Sonar Qube

For more background and information on how this works, see [this blog post][5].

Here are the high order bits:

- A fake DOM is provided via `jsdom-no-contextify` and [`tests/utils/testdom.js`][6] (see[`tests/CheckboxWithLabel-test.jsx`][7]).
- `global.reactModulesToStub` contains a list of modules to replace with stubs (ala Jest).
- `tests/compiler.js` registers a compiler which transforms JSX/Harmony code to
  standard ES5 JS and implements the stubbing.
- `tests/blanket-stub-jsx.js` applies the same transformations, additionally
  instrumenting code for test coverage. The results can be consumed by Sonar Qube.

To run the tests using the `mocha` command line:

```
mocha --compilers jsx:tests/utils/compiler.js tests/*test.jsx
```

Inspiration and guidance for the original came from the [Testing React Components][8] blog post and the Khan Academy's [React Components Makefile][3].

[1]: https://github.com/danvk/mocha-react
[2]: https://github.com/brianmcd/contextify
[3]: http://www.hammerlab.org/2015/02/14/testing-react-web-apps-with-mocha/#mocking-the-dom
[4]: http://www.sonarqube.org/
[5]: http://blog.akquinet.de/2014/11/25/js-test-coverage/
[6]: mocha-react/tests/utils/testdom.js
[7]: mocha-react/tests/CheckboxWithLabel-test.jsx
[8]: http://www.asbjornenge.com/wwc/testing_react_components.html
[9]: https://github.com/Khan/react-components/blob/master/Makefile
