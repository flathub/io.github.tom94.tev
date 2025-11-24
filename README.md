# tev

High dynamic range (HDR) image viewer for people who care about colors.

This repo hosts the flatpak version of [tev](https://github.com/tom94/tev),
available at [Flathub](https://flathub.org/en/apps/io.github.tom94.tev).

As a safe, sandboxed flatpak, **tev** comes *without* network and filesystem access by default.
However, **tev** has several features that only work with network and read-only filesystem permissions enabled.

You can use [Flatseal](https://flathub.org/en/apps/com.github.tchx84.Flatseal) to manage the permissions via a GUI, or
use the following command line
```sh
flatpak override --user --share=network --filesystem=host:ro io.github.tom94.tev
```

Enabling these permissions unlocks the following features:

## Remote control over the network

Compatible rendering software (like [PBRTv4](https://github.com/mmp/pbrt-v4)) can send rendered images directly to a running instance of **tev**.
This is useful when rendering images on server clusters or in cloud environments where you don't have direct access to a graphical user interface.

There are also SDKs for various programming languages that allow you to send images and vector graphics annotations to **tev** from your own software.
- [C/C++](https://github.com/westlicht/tevclient), [Python](https://pypi.org/project/tevclient/), [Rust](https://crates.io/crates/tev_client)

## Read-only filesystem access

- **tev** can watch files for changes and automatically reload them when they are modified.
- You can open images directly from the command line. For example:
  - `flatpak run io.github.tom94.tev /path/to/image.jpg`
    - opens the image
  - `flatpak run io.github.tom94.tev --watch /folder/of/images`
    - opens all images in the folder and reloads on changes
  - `flatpak run io.github.tom94.tev :U,V multichannel.exr`
    - reads the U and V color channels from a multichannel EXR file.
  - `flatpak run io.github.tom94.tev --help`
    - shows all the other command line options (there are many!)
- Your cursor theme will be applied in **tev**, even if the theme itself is not a flatpak.

**Note:** even without filesystem access, **tev** can open and save images via drag-and-drop and file dialogs.
