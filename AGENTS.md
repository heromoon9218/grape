# Grape Development Guide

Grape is a Ruby framework for building REST-like APIs. It is a library gem (not a web application), so there are no external services (databases, caches, etc.) to run.

## Cursor Cloud specific instructions

### Prerequisites (already installed in VM snapshot)

- Ruby >= 3.1 (Ubuntu 24.04 provides 3.2)
- `libyaml-dev` (required for `psych` gem native extension)
- Bundler

### Dependency installation

Gems are installed to `vendor/bundle` (configured via `.bundle/config`). Run:

```
bundle install
```

### Common commands

See `CONTRIBUTING.md` for full details. Key commands:

| Task | Command |
|---|---|
| Lint | `bundle exec rubocop --parallel` |
| Tests (excluding integration) | `bundle exec rspec` |
| Default rake (lint + tests) | `bundle exec rake` |
| Single spec file | `bundle exec rspec spec/grape/api_spec.rb` |

### Notes

- The default `rake` task runs both RuboCop and RSpec (see `Rakefile`).
- `rspec` excludes `spec/integration/` by default (see `Rakefile` `:spec` task pattern). Integration tests require optional gems (e.g. `grape_entity`, `hashie`, `dry-validation`); use the gemfiles in `gemfiles/` directory for matrix testing.
- There is no `Gemfile.lock` committed (it is in `.gitignore`). Bundler resolves fresh each time.
- The `vendor/bundle` directory is a local bundle path and should not be committed.
- No web server needs to be started; all tests use `rack-test` in-process.
