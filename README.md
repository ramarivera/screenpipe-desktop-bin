# screenpipe-desktop-bin

Arch package for the official [Screenpipe](https://screenpi.pe) desktop app (2.x),
built from Screenpipe's own `.deb`. The AUR's `screenpipe` and `screenpipe-bin`
package the older command-line recorder instead.

The app lives in `/opt/screenpipe-desktop` because it expects its bundled `bun`
next to its executable, and `extra/bun` already owns `/usr/bin/bun`.

## Updates

`.github/workflows/update.yml` checks Screenpipe's update endpoint daily. On a new
release it bumps `pkgver`, refreshes checksums and `.SRCINFO`, test-builds the
package, and commits. Once the `AUR_SSH_PRIVATE_KEY` repository secret is set, it
also pushes each bump to the AUR (`screenpipe-desktop-bin`). Run the workflow
manually with `publish_aur` for the first upload.

The in-app updater only replaces AppImages, so turn off auto-update in
Screenpipe's settings and update through pacman.

## Install from this repo

```sh
git clone https://github.com/ramarivera/screenpipe-desktop-bin.git
cd screenpipe-desktop-bin
makepkg -si
```

## License

Screenpipe is under its own commercial license: free for personal,
non-commercial use; commercial use needs an Enterprise plan. This package only
downloads Screenpipe's official build and installs its license file. The
packaging files here are 0BSD.
