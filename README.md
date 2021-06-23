# 📋 clipnotify with disable PRIMARY (selection to copy) option

**Original Patch Source**: [alexozer/clipnotify](https://github.com/alexozer/clipnotify)

clipnotify is a simple program that, using the
[XFIXES](https://cgit.freedesktop.org/xorg/proto/fixesproto/plain/fixesproto.txt)
extension to X11, waits until a new selection is available and then exits.

It was primarily designed for [clipmenu](https://github.com/cdown/clipmenu), to
avoid polling for new selections.

Here's how it's intended to be used:

    while clipnotify; do
        [an event happened, do something with the selection]
    done

clipnotify doesn't try to print anything about the contents of the selection,
it just exits when it changes. This is intentional -- X11's selection API is
verging on the insane, and there are plenty of others who have already lost
their sanity to bring us xclip/xsel/etc. Use one of those tools to complement
clipnotify.

## 🛠️ Options

Option | Description
--- | ---
`-P`, `--disable-primary` | Do not notify on changes to PRIMARY (only on changes to clipboard)

## 🏗️ How to use with clipmenu?

If you use **clipmenu**, add the `-P` or `--disable-primary` option into `clipmenud` (line 140).

```

  # Make sure we're interruptible for the sig_{en,dis}able traps
  clipnotify --disable-primary &

```

Kill your `clipmenud` (first) and `clipnotify` (after). Then, re-run or restart (if you use service) your `clipmenud`.
