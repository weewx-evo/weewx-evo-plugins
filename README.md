# weewx-evo-plugins

The catalogue. One file, `plugins.toml`, saying which plugins exist for
[weewx-evo](https://github.com/hilman2/weewx-evo) and where they live.

One repository per plugin, each with its own issues, releases and maintainer.
What is here is the pointer, not the code.

## What is in it

| Plugin | Kind | `kind` | For |
|---|---|---|---|
| [weewx-evo-sftp](https://github.com/weewx-evo/weewx-evo-sftp) | export | `sftp` | A server with SSH but no rsync |

## Suggesting your own

Open an issue: [Propose a plugin][propose]. Say what it does and where it
lives, and the entry gets written from that. A pull request adding the block
to `plugins.toml` yourself is just as welcome.

What is checked before it goes in:

- it installs, and `weewx-evo <kind> list` shows it afterwards
- it has a licence, and one compatible with GPL-3.0-or-later
- `options()` returns something the settings page can render
- the README says what it is for in the first paragraph

None of that is a judgement about quality. The catalogue says a plugin exists
and what it claims to do. Whether it is any good is between its author and the
people using it.

## Writing one

[Plugins](https://github.com/hilman2/weewx-evo/wiki/Plugins) in the weewx-evo
wiki: the two forms a plugin takes, the entry point groups, and what a plugin
may do that the core may not.

## Licence

The catalogue: GPL-3.0-or-later, the same as weewx-evo. Each plugin has its
own -- `plugins.toml` says which.

[propose]: https://github.com/weewx-evo/weewx-evo-plugins/issues/new?template=propose-a-plugin.yml
