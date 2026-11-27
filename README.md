# Periph APT repository

Signed Debian packages of [Periph](https://github.com/tuhde/Periph) for
Debian 13 (trixie) and Raspberry Pi OS based on it (amd64, arm64, armhf),
served by GitHub Pages at <https://tuhde.github.io/periph-apt>.

| Package | Contents |
|---------|----------|
| `python3-periph` | Python module; recommends the Linux bus libraries |
| `libperiph-dev` | C++17 static library and headers (`pkg-config periph`, CMake `periph::periph`) |
| `sigrok-decoders-periph` | Protocol decoders for sigrok-cli and PulseView |

## Use

```sh
sudo curl -fsSLo /usr/share/keyrings/periph-archive-keyring.gpg \
  https://tuhde.github.io/periph-apt/periph-archive-keyring.gpg
printf '%s\n' 'Types: deb' 'URIs: https://tuhde.github.io/periph-apt' 'Suites: trixie' \
  'Components: main' 'Signed-By: /usr/share/keyrings/periph-archive-keyring.gpg' \
  | sudo tee /etc/apt/sources.list.d/periph.sources
sudo apt update
sudo apt install python3-periph libperiph-dev sigrok-decoders-periph
```

## How this repository is maintained

Don't edit it by hand. Every Periph release (`release.yml`, job
`debian-publish`) adds the new packages with reprepro and pushes here:

- `conf/` — reprepro configuration, synced from
  [`packaging/apt-repo/`](https://github.com/tuhde/Periph/tree/main/packaging/apt-repo)
  in Periph on every publish (change it there).
- `db/` — reprepro's package database.
- `docs/` — the published repository (`dists/`, `pool/`, the public key
  `periph-archive-keyring.gpg` / `.asc`, and the landing page). GitHub Pages
  serves this folder.

Packaging details: [`packaging/README.md`](https://github.com/tuhde/Periph/blob/main/packaging/README.md).
