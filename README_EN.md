# Session Suite / dsh-session-expand

Three session plugins in one install — and every component keeps its **own switch** on the Plugins page, so you can turn one off without uninstalling anything.

[中文](README.md) · MIT · Combines [dsh-session-tabs](https://github.com/DEVbyQIN/dsh-session-tabs), [dsh-quote-to-chat](https://github.com/DEVbyQIN/dsh-quote-to-chat) and [dsh-session-md](https://github.com/DEVbyQIN/dsh-session-md).

## Components

| Component | What it does | Version |
|---|---|---|
| `dsh-session-tabs` | Browser-like session tabs; reuses the native chat view, sidebars and workbench | 0.1.6 |
| `dsh-quote-to-chat` | Select any text in a reply → floating toolbar: quote it into the composer, start a side thread, or copy | 0.2.0 |
| `dsh-session-md` | Export a session as human-readable Markdown or self-contained HTML (turns, tool calls, reasoning) | 0.1.0 |

All three have zero runtime dependencies. The bundle itself contains no plugin code — it is only a DSH bundle layer (the mechanism for packaging several plugins together).

## Install

Install the bundle once and all three components are in place.

**Desktop GUI**: open **Plugins** in the sidebar → **Add plugin** → enter `dsh-session-expand` → **Enable now**.

**CLI** (any one):

```sh
# The desktop app's bundled CLI (profile is always desktop)
"/Applications/DeepSeek Harness.app/Contents/Resources/runtime/cli/bin/dsh" \
  plugin --profile desktop add dsh-session-expand@0.1.0

# Any dsh CLI with your own profile
dsh plugin --profile web add dsh-session-expand@0.1.0

# From GitHub instead of npm
dsh plugin --profile web add github:DEVbyQIN/dsh-session-expand#v0.1.0
```

After installing, the Plugins page shows one **Session Suite** card.

## Switch components individually

Plugins page → open the **Session Suite** card → the **Included components** list:

- every row has its own **Enable / Disable** switch; disabling one unmounts its host half and browser half immediately (no restart with HMR enabled) while the others keep running;
- a component that ships a configuration page also gets a **Configure** button on its row;
- switch state is stored as `disabled` overrides in the profile's `cordis.patch.yml`, so it survives bundle upgrades.

> The plugin list under **Settings → Built-in plugins** is read-only; the real per-component switches live on the Plugins page's bundle detail.

## Do not install the components separately at the same time

The bundle and a standalone component mount two instances of the same package; DSH's client module system rejects two active modules with the same package name (and the UI would duplicate). So uninstall the standalone `dsh-session-tabs` / `dsh-quote-to-chat` / `dsh-session-md` before installing this bundle, or vice versa. Need only one or two? Keep the bundle and switch the unwanted rows off.

## Upgrade and uninstall

- Upgrading the bundle upgrades all three pinned component versions (see the table). `CHANGELOG.md` records the mapping.
- Uninstalling removes the three components. To pause one temporarily, use its row switch instead.

## Compatibility

- DSH `0.2.x` (including desktop `0.2.1-rc.4`); Node `^22.19.0 || >=24`.
- The bundle registers no Loader entry and injects no service.

## Develop and self-test

This repository is only a bundle manifest (`package.json` + `cordis.patch.yml` + locale + docs):

```sh
node --test test/verify.mjs   # pinned versions, patch rows, locale, publish file list
npm pack --dry-run            # inspect the published file set
```

## License

MIT
