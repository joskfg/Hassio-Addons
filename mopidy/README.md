# Mopidy (Hass.io Addon)

Mopidy with plugins for Hass.io. It enabled the host to play audio.
This plugin is based on the [addon from _bestlibre_](https://github.com/bestlibre/hassio-addons/tree/master/mopidy).

![Addon Stage][stage-badge]
![Supports aarch64 Architecture][aarch64-badge]
![Supports amd64 Architecture][amd64-badge]
![Supports armhf Architecture][armhf-badge]
![Supports armv7 Architecture][armv7-badge]
![Supports i386 Architecture][i386-badge]

[![Install on my Home Assistant][install-badge]][install-url]
[![Donate][donation-badge]][donation-url]

It is build with following extensions:

* [Mopidy-Local](https://docs.mopidy.com/en/latest/ext/local/)
* [Mopidy-Stream](https://docs.mopidy.com/en/latest/ext/stream/)
* [Mopidy-YouTube](https://github.com/mopidy/mopidy-youtube)
* [Mopidy-Iris](https://github.com/jaedb/iris)

Mopidy listen on `6680` for http connection, and `6600` for mpd ones.

## Local Media

The local media can be stored on `/share` (which allow an access through the samba addon).
By default the directory for media is `/share/mopidy/media`.

## Panel integration

Since Mopidy-Iris don't play well (at least out-of-the-box) with the ingress feature Mopidy can be added to the side-panel in the configuration with those lines:

```yaml
panel_iframe:
  morpidy:
    title: 'Morpidy'
    icon: 'mdi:music-circle'
    url: 'http://<homeassistant-address>:6680/iris'
```

## Configuration

### local_scan (bool)

If it is set to true, a local scan is performed on startup. A local scan can also be triggered via the web ui.

### options (list of dict)

This object accepts any configuration of the listed extenstions. It can be also used to overwrite the default values.

For example: Overwrite the media dir

```json
{"name": "local/media_dir", "value": "/share/media"}
```

## Default config

```properties
[core]
cache_dir = /data/mopidy/cache
data_dir = /data/mopidy/data_dir

[http]
hostname = 0.0.0.0

[mpd]
hostname = 0.0.0.0

[local]
media_dir = /share/mopidy/media
library = sqlite

[m3u]
playlists_dir = /share/mopidy/playlists

[stream]
enabled = true
protocols =
    http
    https

[iris]

```


[aarch64-badge]: https://img.shields.io/badge/aarch64-no-red.svg?style=for-the-badge
[amd64-badge]: https://img.shields.io/badge/amd64-yes-green.svg?style=for-the-badge
[armhf-badge]: https://img.shields.io/badge/armhf-yes-green.svg?style=for-the-badge
[armv7-badge]: https://img.shields.io/badge/armv7-yes-green.svg?style=for-the-badge
[i386-badge]: https://img.shields.io/badge/i386-yes-green.svg?style=for-the-badge
[install-url]: https://my.home-assistant.io/redirect/supervisor_addon?addon=243ffc37_mopidy
[stage-badge]: https://img.shields.io/badge/Addon%20stage-depreciated%20🕸️-red.svg?style=for-the-badge

[install-badge]: https://img.shields.io/badge/Install%20on%20my-Home%20Assistant-41BDF5?logo=home-assistant&style=for-the-badge
[donation-badge]: https://img.shields.io/badge/Buy%20me%20a%20coffee-%23d32f2f?logo=buy-me-a-coffee&style=for-the-badge&logoColor=white
[donation-url]: https://www.buymeacoffee.com/Poeschl
