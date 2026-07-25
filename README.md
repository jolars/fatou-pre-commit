# fatou-pre-commit

[![CI](https://github.com/jolars/fatou-pre-commit/actions/workflows/ci.yml/badge.svg)](https://github.com/jolars/fatou-pre-commit/actions/workflows/ci.yml)

A [pre-commit](https://pre-commit.com) hook for
[fatou](https://github.com/jolars/fatou), a language server, formatter, and
linter for the Julia language.

Distributed as a thin Python package that depends on the [`fatou` PyPI
package](https://pypi.org/project/fatou/), so pre-commit installs a prebuilt
binary wheel. No Rust toolchain or Julia installation required. Wheels are
available for Linux, macOS, and Windows on both x64 and ARM64.

## Usage

Add this to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/jolars/fatou-pre-commit
    # fatou version
    rev: v0.7.0
    hooks:
      # Lint .jl files
      - id: fatou-lint
      # Format the same files in place
      - id: fatou-format
```

To apply safe lint autofixes before formatting, pass `--fix`:

```yaml
- id: fatou-lint
  args: [--fix]
- id: fatou-format
```

To check formatting without rewriting files:

```yaml
- id: fatou-format
  args: [--check]
```

Both hooks pass `--force-exclude`, so files matched by `exclude` or
`extend-exclude` in your `fatou.toml` are skipped even though pre-commit names
staged files explicitly. This requires fatou 0.7.0 or later, so `rev` tags start
at `v0.7.0`.

## Versioning

Tags mirror fatou releases: \`rev: v0.7.0 installs fatou 0.7.0. New tags are
created automatically when a new fatou version is published to PyPI.

## License

MIT
