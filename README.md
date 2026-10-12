<div align="center">

# 🧩 Setchy Renovate config

**Shared [Renovate][renovate] presets & validation workflow** for the [setchy organization][setchy-org].

[![Renovate config validation][validator-badge]][validator-actions] [![License][license-badge]][license]

</div>

> [!NOTE]
> Public repository. It hosts the organization's shared Renovate preset, which every setchy repository inherits.

## 📦 Usage

Inherit the baseline preset from a repository's `renovate.json`:

```jsonc
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["local>setchy/renovate-config"],
  "packageRules": [
    { "description": "repo-specific rule" }
  ]
}
```

Repository-level settings and later `packageRules` take precedence over the shared baseline.

Because this repository follows Renovate's shared-preset naming convention, **new repositories are onboarded onto the preset automatically** — Renovate checks `setchy/renovate-config/default.json` before any other org default and suggests `extends: ["local>setchy/renovate-config"]`.

### ✅ Validating a repo's config

Consumer repositories can call the reusable workflow to validate their own `renovate.json`:

```yaml
jobs:
  validate:
    permissions:
      contents: read
    uses: setchy/renovate-config/.github/workflows/renovate-config-validator.yml@main
```

## 🛠️ Policy

- 🚦 Rate limiting disabled, with vulnerability alerts enabled.
- 🔖 Semantic `chore` commits and separate major releases.
- 🧬 Biome `$schema` version updates.
- 🏷️ The `dependency` label on every update.
- 📌 npm dependency ranges pinned by default, with `engines` left as ranges.
- ✋ No platform automerge.

## Presets

| File           | Purpose                                                                   |
| -------------- | ------------------------------------------------------------------------- |
| `default.json` | Baseline preset every repository inherits via `local>setchy/renovate-config`. |

## Development

Validate changes before opening a pull request:

```sh
npx --yes --package=renovate -- renovate-config-validator --strict default.json
```

Continuous integration runs the same validation on every pull request.

## 📄 License

Released under the [MIT License](LICENSE).

---

<div align="center">

<sub>Maintained by <a href="https://github.com/setchy">@setchy</a></sub>

</div>

<!-- LINK LABELS -->
[renovate]: https://renovatebot.com/
[setchy-org]: https://github.com/setchy
[validator-actions]: https://github.com/setchy/renovate-config/actions/workflows/renovate-config-validator.yml
[validator-badge]: https://img.shields.io/github/actions/workflow/status/setchy/renovate-config/renovate-config-validator.yml?logo=github&label=renovate%20config
[license]: LICENSE
[license-badge]: https://img.shields.io/badge/license-MIT-blue.svg
