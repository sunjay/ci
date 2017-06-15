# ci

Continuous Integration utilities for Rust

**This package has not been built yet.**

Here's the vision:
> Instead of all the [insanity] in your CI configurations, why not just have a
> single command that abstracts away all the details?

You can run:
```
ci fmt
ci build
ci test
```
and the program will install whatever is necessary and run the commands.

Instead of remembering that the following command tests if the current directory
is formatted:
```
cargo fmt -- --write-mode=diff
```
You can just remember:
```
ci fmt
```
This will fail the build if the files need to be formatted.

Instead of having to write each individually, you can also group them like so:
```
ci fmt build test
```

These will run in the same order. Dependencies for each won't be installed until
each command needs them. That means you can ensure that your build won't take
longer than necessary.

The idea is that you install one thing using `cargo install --force ci` and then
you can run everything with no issues.

There are already many tools that do this like travis-cargo and cargo-travis,
but this tool should have many benefits over those:
- more supported platforms (e.g. more than just travis) and tools (rustfmt, code coverage)
- support for all the coverage providers like codecov, coveralls, etc.
- automatic install of the latest version of kcov
- checks to make sure things are not already installed before installing
- opinionated defaults, but highly configurable
- everything automatically runs in verbose mode

Ideas for commands:
- `all` - run everything in a reasonable order
- `default` or no argument - run the default test script
  - probably `build`, `test`
- `build` - just build in verbose mode
- `test` - test in verbose mode
- `fmt` - check if rustfmt has been run
  - aware of rustfmt's recent transition to nightly-only
- `coverage` - run tests with code coverage
- `bench` - run benchmarks
  - benchmark comparision with `cargo-benchcmp`?
- `codecov` - (run and) upload coverage to Codecov.io
- `coveralls` - (run and) upload coverage to Coveralls
- `doc` - build documentation

There should be a declaritive and easy way to add new things. That is, recoding
the same logic for installing dependencies and running commands should not be
necessary.

Should be some clear contributing documentation to allow other people to quickly
and easily add their own commands.

Try to find some way to avoid creating just another tool that people have to
spend 10 years configuring and tweaking just to get right. This should have
certain sets of reasonable defaults that people can just use until they need to
do more.

There should be good enough documentation that when people want to do more, they
can.

[insanity]: https://github.com/sunjay/lion/blob/02fe4343a336560a96eedb143030fd3b298a8d44/.travis.yml#L15-L28
