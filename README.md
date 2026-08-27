# weewx-evo-plugins

The catalogue. One file, `plugins.toml`, saying which plugins exist for
[weewx-evo](https://github.com/hilman2/weewx-evo) and where they live.

## Why a catalogue and not a monorepo

This is the decision the repository exists to make.

**One repository per plugin.** Each has its own issues, its own releases and
its own maintainer -- and that is exactly what lets somebody who is not us keep
one alive. A plugin that is abandoned can be taken over without anybody
needing write access to everything else.

**The mistake to avoid** is the one `weewx-DWD` made: ten unrelated things in
one package, where a change to the radar code can break the forecast and a
user who only wants warnings installs all of it. That is not malice; it is
what a monorepo does over time.

**weewx-evo already has the same case.** The Ecowitt driver came from
`weewx-ecowitt`, a separate repository holding a WeeWX plugin -- and because
the two are different programs, no fix travelled usefully between them any
more. The driver is core now and that repository stays what it is. Two things,
two places, cleanly apart.

What belongs here is therefore the **pointer**, not the code.

## How a plugin works

There are two shapes, and which applies depends on what the plugin is.

**An entry point** -- for exports, uploads, feeds and forecast sources. A
pip-installable package with one line in its `pyproject.toml`:

```toml
[project.entry-points."weewx_evo.exports"]
sftp = "weewx_evo_sftp:SftpExport"
```

That is all of it. `pip install weewx-evo-sftp`, and afterwards `sftp` is in
`weewx-evo export list`, in the dropdown on the settings page and valid as
`kind = "sftp"` in the configuration -- with no change to weewx-evo.

The groups: `weewx_evo.exports`, `weewx_evo.uploads`, `weewx_evo.feeds`,
`weewx_evo.forecast`.

**A directory** -- for drivers. Those live beside the data rather than inside
the package, so that upgrading weewx-evo cannot touch them:

```bash
weewx-evo driver install https://github.com/somebody/weewx-evo-acurite
```

## What a plugin may do that the core may not

**Take a dependency.** The weewx-evo core runs on the standard library, and
that is not a slogan: it is what makes `pip install weewx-evo` work on a
Raspberry Pi with no compiler. A plugin has no such obligation -- whoever needs
`paramiko`, `pillow` or `numpy` takes it.

The first entry here does not, and its README says why: `paramiko` pulls in
`cryptography`, which on a Pi without a matching wheel means a Rust toolchain
and forty minutes. But it would have been allowed, and that is the point.

## Adding a plugin

Open a pull request that adds a block to `plugins.toml`. What is checked
before it is merged:

- it installs, and `weewx-evo <kind> list` shows it afterwards
- it has a licence, and one compatible with GPL-3.0-or-later
- `options()` returns something the settings page can render
- the README says what it is for in the first paragraph

**None of that is a judgement about quality.** The catalogue says a plugin
exists and what it claims to do. Whether it is any good is between its author
and the people using it.

`tested` is not a compatibility range. It is one fact -- the version somebody
actually ran it against -- because a range is a promise nobody can keep, and a
plugin claiming "any version" is saying nothing.

## What is in it

| Plugin | Kind | `kind` | For |
|---|---|---|---|
| [weewx-evo-sftp](https://github.com/hilman2/weewx-evo-sftp) | export | `sftp` | A server with SSH but no rsync |

## Licence

The catalogue: GPL-3.0-or-later, the same as weewx-evo. Each plugin has its
own -- `plugins.toml` says which.
