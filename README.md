# safari.rs

safari.rs provides some tools for interacting with Safari on the command-line.

## Commands

1.  Get the URL from a given window or tab:

    ```console
    $ # Get the URL of the frontmost tab of the frontmost window
    $ safari url
    https://github.com

    $ # Get a URL from the second window from the tab
    $ safari url --window=2
    https://example.com/foo

    $ # Third tab from the left of the second window
    $ safari url --window=2 --tab=3
    https://example.com/foo
    ```

    I have the first two commands bound to shortcuts `furl` and `2url` for quick access.

2.  Get a list of URLs from every open tab:

    ```console
    $ safari urls-all
    https://github.com
    https://example.com/foo
    https://crates.io/crates/urlparse
    ...
    ```

3.  Go through and batch close tabs:

    ```console
    $ safari clean-tabs youtube.com,twitter.com
    ```

    I find this useful for quickly cutting down my open tabs.

4.  Get a list of URLs from Reading List:

    ```console
    $ safari reading-list
    ```

5.  Get a list of URLs from all your devices with iCloud Tabs:

    ```console
    $ safari icloud-tabs
    ```

    You can get a list of known devices with `icloud-tabs --list-devices`, and filter the URLs with the `--device` flag:

    ```console
    $ safari icloud-tabs --device="Alex's iPhone"
    ```

## Installation

You need [Rust installed][rust].
Then to install:

```console
$ cargo install --git https://github.com/alexwlchan/safari.rs
```

Tested with Rust 1.17.0

[rust]: https://www.rust-lang.org/en-US/install.html

## URL transformations

The commands that produce URLs do a bit of cleaning before they return:

*   Twitter links to the mobile site (`mobile.twitter.com`) are flipped to
    point to the desktop site (`twitter.com`).
*   Tracking data is partially stripped from Amazon, Buzzfeed, Mashable and
    Medium URLs.
*   Any UTM tracking parameters in the query string are removed.
*   The `#notes` fragment is removed from Tumblr URLs.
*   The `feature=youtu.be` query parameter is removed from YouTube URLs.

## Motivation

I first got the idea for a script to access Safari URLs [from Dr. Drang][dr].
I've been through several different versions – AppleScript, shell, Python –
gradually adding the cleaning features – and now I've written a new
version in Rust.

Why Rust?

*   It's really fast.  The Rust script returns immediately – with some of
    the other versions, I had a noticeable delay when typing `;furl`.
*   I like Rust, and I’ve been enjoying playing with it recently.

[dr]: http://www.leancrew.com/all-this/2009/07/safari-tab-urls-via-textexpander/

## License

MIT license.
