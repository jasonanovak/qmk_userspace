# Ploopy Classic QMK userspace

My QMK keymap for the Ploopy Classic / Classic 2 trackball, kept as an
[external userspace](https://docs.qmk.fm/newbs_external_userspace) so it
builds against an unmodified `qmk_firmware` checkout.

The keymap lives at
`keyboards/ploopyco/trackball/keymaps/jasonanovak_ploopy_classic_tapdance/`
and its own [readme](keyboards/ploopyco/trackball/keymaps/jasonanovak_ploopy_classic_tapdance/readme.md)
documents the button layout, tap dance, and combos.

## Build targets

| Board                      | Hardware             | Output |
|----------------------------|----------------------|--------|
| `ploopyco/trackball/rev1_007` | Classic 2 (RP2040) | `.uf2` |
| `ploopyco/trackball/rev1_005` | Classic (ATmega32U4) | `.hex` |

## Building locally

One-time setup, with a `qmk_firmware` checkout already installed via `qmk setup`:

```sh
git clone git@github.com:jasonanovak/qmk_userspace.git
cd qmk_userspace
qmk config user.overlay_dir="$(realpath .)"
```

Then either build everything:

```sh
qmk userspace-compile
```

or one board:

```sh
qmk compile -kb ploopyco/trackball/rev1_007 -km jasonanovak_ploopy_classic_tapdance
```

Firmware files land in the root of this directory.

## Flashing

Classic 2 (rev1_007): hold the button on the underside while plugging in, or
run `qmk flash`. It appears as a USB drive; copy the `.uf2` onto it.

Classic (rev1_005): `qmk flash -kb ploopyco/trackball/rev1_005 -km jasonanovak_ploopy_classic_tapdance`
and reset the board when prompted.

## GitHub Actions

Every push builds both targets against upstream `qmk/qmk_firmware` master and
publishes the firmware files to the repository's Releases page.
