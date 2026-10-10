# setchy/renovate-config

Shared [Renovate](https://docs.renovatebot.com/) presets for repositories in the
[@setchy](https://github.com/setchy) organization.

## Usage

Extend the default preset from your repository's `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["local>setchy/renovate-config"]
}
```

`local>` resolves the preset on the current host — here, GitHub. Repositories
should only add their own overrides on top, for example a schedule and any
repository-specific `packageRules`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["local>setchy/renovate-config", "schedule:daily"],
  "packageRules": []
}
```

## Presets

| Preset    | Reference                          | Description                                                                                                                                                                                                                                                                              |
| --------- | ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `default` | `local>setchy/renovate-config`     | Organization baseline: `config:best-practices`, vulnerability alerts, disabled rate limiting, semantic `chore` commits, separate major releases, Biome `$schema` version updates, the `dependency` label, the `setchy` assignee, and pinned dependency ranges (with `engines` left as ranges). |

## Development

Validate changes before opening a pull request:

```sh
npx --yes --package=renovate -- renovate-config-validator --strict default.json
```

Continuous integration runs the same validation on every pull request.
