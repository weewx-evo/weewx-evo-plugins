# weewx-evo-plugins

The catalogue. One file, `plugins.toml`, saying which plugins exist for
[weewx-evo](https://github.com/hilman2/weewx-evo) and where they live.

One repository per plugin, each with its own issues, releases and maintainer.
What is here is the pointer, not the code.

## What is in it

`plugins.toml` is the list this table is written from. Where the two ever
disagree, the file is right: it is what weewx-evo reads.

### Drivers

One per protocol, so a station installs the one its hardware speaks and
nothing else. In detection order, which is what decides a tie when an upload
does not name a protocol.

| Plugin | `kind` | For |
|---|---|---|
| [weewx-evo-ecowitt](https://github.com/weewx-evo/weewx-evo-ecowitt) | `ecowitt` | GW1000 to GW3000, HP2551, WS3800 and their rebadges |
| [weewx-evo-ambient](https://github.com/weewx-evo/weewx-evo-ambient) | `ambient` | WS-2902, WS-5000, WS-1965 and the rest of the Ambient range |
| [weewx-evo-acurite](https://github.com/weewx-evo/weewx-evo-acurite) | `acurite` | smartHUB and Access bridges, with a 5-in-1, towers and the 899 rain gauge |
| [weewx-evo-lacrosse](https://github.com/weewx-evo/weewx-evo-lacrosse) | `lacrosse` | LW301 and LW302 gateways |
| [weewx-evo-wunderground](https://github.com/weewx-evo/weewx-evo-wunderground) | `wunderground` | Fine Offset Observer and its rebadges, Meteobridge, weather software generally |
| [weewx-evo-weatherflow](https://github.com/weewx-evo/weewx-evo-weatherflow) | `weatherflow` | Tempest, and the AIR, SKY and hub before it |
| [weewx-evo-rtl433](https://github.com/weewx-evo/weewx-evo-rtl433) | `rtl433` | Any 433, 868 or 915 MHz sensor rtl_433 decodes, heard with an RTL-SDR stick |
| [weewx-evo-purpleair](https://github.com/weewx-evo/weewx-evo-purpleair) | `purpleair` | PA-II, PA-II-SD and PA-I air quality sensors |
| [weewx-evo-airlink](https://github.com/weewx-evo/weewx-evo-airlink) | `airlink` | Davis AirLink air quality sensors |
| [weewx-evo-ecowitt-gateway](https://github.com/weewx-evo/weewx-evo-ecowitt-gateway) | `ecowitt_gateway` | The same gateways, asked on TCP 45000 instead of configured to upload |
| [weewx-evo-ambient-cloud](https://github.com/weewx-evo/weewx-evo-ambient-cloud) | `ambient_cloud` | An Ambient station that is not on this network, through ambientweather.net |
| [weewx-evo-homeassistant](https://github.com/weewx-evo/weewx-evo-homeassistant) | `homeassistant` | Any sensor Home Assistant integrates. Which entities is yours to choose |

PurpleAir and AirLink are asked rather than listened for: the sensor has
nowhere to type a server address into, so the driver goes to it on a schedule.
That is a property of the protocol and not a second kind of plugin -- same
`kind`, same entry point, same page. They come last in the table for that
reason and not by precedence: nothing arrives from them on its own, so they
are never candidates in a detection.

They share
[weewx-evo-push-common](https://github.com/weewx-evo/weewx-evo-push-common),
which pip installs with whichever one you pick. It is not listed here on
purpose: installed on its own it registers no protocol and answers on no
endpoint, and a list of things to choose from should not offer one that does
nothing when chosen.

### Exports

| Plugin | `kind` | For |
|---|---|---|
| [weewx-evo-sftp](https://github.com/weewx-evo/weewx-evo-sftp) | `sftp` | A server with SSH but no rsync |

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
