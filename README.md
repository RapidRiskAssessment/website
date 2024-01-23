# How to contribute

## Documentation, code, etc.

Propose your changes as a PR directly, in Markdown format.

## Issues and discussion

Open them directly in the project's issues. We also have a public [Matrix](https://matrix.org/faq/) chatroom: [`#RRA:matrix.org`](https://matrix.to/#/#RRA:matrix.org).

## Local testing

- Install Ruby, Gem, Bundler (e.g.: `apt-get install ruby gem bundler curl`).
- Checkout this repository.
- Don't forget to configure GEMs if you haven't, e.g. `export GEM_HOME=~/.ruby/  PATH="$PATH:~/.ruby/bin`.
- Run `bundle install` to install all dependencies.
- Run `bundle exec jekyll serve --livereload` to locally serve contents for testing.
- Run `bundle exec htmlproofer --assume-extension .html --no-enforce-https --ignore-urls https://www.pexels.com/license/ ./_site` to test for broken links locally.

## GitHub Actions status

[![site checks](https://github.com/RapidRiskAssessment/website/actions/workflows/checks.yml/badge.svg)](https://github.com/RapidRiskAssessment/website/actions/workflows/checks.yml)
[![pages-build-deployment](https://github.com/RapidRiskAssessment/website/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/RapidRiskAssessment/website/actions/workflows/pages/pages-build-deployment)
