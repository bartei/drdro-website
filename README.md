# drdro-website

The documentation website for **drDRO** — the Kivy touchscreen DRO / rotary controller for the
drDRO STM32 board. A dependency-free static site (no build step, no external CDNs).

Live site: `https://<static-host>/drdro-website/` (served by the infra nginx-static host).

## Pages

| File | Purpose |
|---|---|
| `index.html` | Landing / overview, feature highlights, Pi compatibility summary |
| `features.html` | Full screen-by-screen functionality reference (with screenshots) |
| `screenshots.html` | Gallery of every screen |
| `videos.html` | Creator + community YouTube demos (click-to-play) |
| `flash.html` | Get started: flash wizard (live GitHub release download), first boot, tested Raspberry Pi models |
| `develop.html` | Run & develop the app locally on Linux |
| `reference.html` | Architecture, RS-485 line protocol, variable registry, firmware-update flow |

Assets live under `assets/` (`css/`, `js/`, `img/`, `shots/`). Screenshots in `assets/shots/` are
real captures of the app at 1024×600.

## Preview locally

Plain HTML/CSS/JS — serve the folder with any static server so `fetch()` and relative paths behave:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Deploy (CI/CD)

`.github/workflows/deploy-static.yml` runs on every push to `main` (and manual dispatch) on a
**self-hosted runner** (`[self-hosted, nixos]`): it stages the site into `public/` and `rsync`s it
over SSH to `$STATIC_DEPLOY_PATH/drdro-website` on the static host.

Required repository secrets:

| Secret | Meaning |
|---|---|
| `STATIC_DEPLOY_HOST` | SSH host of the static content server |
| `STATIC_DEPLOY_USER` | SSH user (the `default` static-content user) |
| `STATIC_DEPLOY_PATH` | Base path for static content on the host |
| `STATIC_DEPLOY_SSH_KEY` | Private SSH key authorised for that user |

A self-hosted runner with the `nixos` label must be registered on this repository.

## Related

- [drdro-software-f4](https://github.com/bartei/drdro-software-f4) — the app the site documents
- [drdro-firmware-f4](https://github.com/bartei/drdro-firmware-f4) — board firmware
- [drdro-arch](https://github.com/bartei/drdro-arch) — the flashable appliance image

## License

Documentation and code: GPL-3.0-or-later. Embedded videos © their respective creators.
