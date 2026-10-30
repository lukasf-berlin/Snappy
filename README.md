<!--
Module: snappy.documentation.readme
Purpose: Public introduction, installation and release instructions.
Created: 2026-10-20. Public application overview and installation instructions.
-->
# Snappy

<img src="assets/snappy.png" alt="Snappy icon" width="128">

A compact screenshot and desktop recorder for Linux, built with Rust and GTK 3.

Press **Print Screen**, select the screen or an area, and capture.

- Screenshot or record through a compact on-screen toolbar.
- Save screenshots as PNG, JPEG, BMP or GIF, with an exact encoded size preview.
- Copy images to the clipboard without saving a file.
- Record desktop sound or turn it off; stop recording when you choose.
- Choose Discord-friendly, smaller-file, high-quality or lossless video exports.
- Remember separate screenshot and video folders.
- Use English, Spanish, Greek, Brazilian Portuguese or European Portuguese.
- Capture another screenshot while earlier save dialogs remain open.

## Install

Download **one** package for your distribution from [GitHub Releases](https://github.com/NullMagic2/Snappy/releases):

| Distribution | Package |
| --- | --- |
| Ubuntu 24.04+ | `snappy-capture_<version>ubuntu1_amd64.deb` |
| Linux Mint 22+ | `snappy-capture_<version>mint1_amd64.deb` |
| Debian 13+ | `snappy-capture_<version>debian1_amd64.deb` |

These packages are for **64-bit Intel/AMD (amd64)** systems. They contain the same
application, with distribution-specific package descriptions and preferred portal
backends. They are alternative installations of the same package, not separate apps.

Open a terminal in the download directory and install the matching file, for example:

```sh
sudo apt install ./snappy-capture_*ubuntu1_amd64.deb
```

Open **Snappy** from the application menu once to complete desktop integration.
On GNOME and Cinnamon, installation assigns Print Screen to Snappy and preserves
the previous shortcut settings. It does not remove the desktop's capture packages.
If Snappy is already running during an upgrade, finish any pending captures and
quit through **Settings → Quit Snappy**, then reopen it.

### Wayland and GNOME

On GNOME Wayland, Snappy bundles a Shell extension for native capture without
portal screen-sharing dialogs. GNOME may require a sign-out and sign-in when first
discovering the extension or loading changed extension code.

Other Wayland desktops use their capture portals and may show permission prompts.
On X11, Snappy uses FFmpeg. Desktop sound uses the output monitor, not a microphone.

### Restore your shortcut or uninstall

Run the restore command as your desktop user before removing Snappy:

```sh
snappy --restore-shortcuts
sudo apt remove snappy-capture
```

Your saved screenshots and recordings are not removed.

### Verify a download

Download `SHA256SUMS` beside your package, then run:

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

The downloaded package should report `OK`. These checksums detect file corruption;
they are not a signing certificate.

## Build from source

Requires Rust **1.88 or newer** (install with [rustup](https://rustup.rs)) and the native build
dependencies:

```sh
git clone https://github.com/NullMagic2/Snappy.git
cd Snappy
sudo apt install build-essential pkg-config libgtk-3-dev libx11-dev
./build.sh
```

The executable is written to `Binaries/snappy`. The `.deb` installs runtime dependencies
automatically; for a source build install them yourself, mainly `ffmpeg`,
`gstreamer1.0-tools`, `gstreamer1.0-pipewire`, `gstreamer1.0-plugins-good`,
`gstreamer1.0-libav`, `xdg-desktop-portal` and `yaru-theme-gtk`.
The full list is in [package.sh](package.sh).

```sh
./package.sh all           # Produce Ubuntu, Mint and Debian packages
./package.sh ubuntu        # Or just one: ubuntu | mint | debian
./clean.sh                 # Remove owned build intermediates; keep published binaries
```

Packaging also needs `dpkg-deb`, FFmpeg, and Binutils. To install a source build
under your own account (run as your regular user, **without sudo**) and keep your
current Print Screen shortcut:

```sh
./install.sh --no-default
```

The binary is installed to `~/.local/bin/snappy`.

## License

MIT — see [LICENSE](LICENSE). Third-party dependency notices: [THIRD_PARTY_LICENSES.txt](THIRD_PARTY_LICENSES.txt).
```
