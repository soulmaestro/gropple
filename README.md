# gropple

A frontend to youtube-dl (or compatible forks, like yt-dlp) to download videos with a single click, straight from your web browser.

![Screencast](/screencast.gif)

## Pre-requisites

* some familiarity with the command line
* youtube-dl (plus any of its required dependencies, like ffmpeg)
* golang compiler (only if you'd like to build from source)

## Build

    go build

## Binaries

Binaries are available at <https://github.com/tardisx/gropple/releases>

Gropple will automatically check for available updates and prompt you to
upgrade.

## Running

    ./gropple

There are no command line arguments. All configuration is done via the web
interface. The address will be printed after startup:

    2021/09/30 23:53:00 starting gropple v0.5.0 - https://github.com/tardisx/gropple
    2021/09/30 23:53:00 go to http://localhost:6123 for details on installing the bookmarklet and to check status

## Using

Bring up `http://localhost:6283` (or your configured address) in your browser.
You should see a link to the bookmarklet at the top of the screen, and the list
of downloads (currently empty).

Drag the bookmarklet to your favourites bar, or otherwise bookmark it as you see
fit. Any kind of browser bookmark should work. The bookmarklet contains embedded
javascript to pass the URL of whatever page you are currently on back to
gropple.

Whenever you are on a page with a video you would like to download just click
the bookmarklet.

A popup window will appear. Choose a download profile and the download will
start. The status will be shown in the window, updating in real time.

You may close this window at any time without stopping the download, the status
of all downloads is available on the index page.

## Configuration

Click the "config" link on the index page to configure gropple. The default
options are fine if you are running on your local machine. If you are running it
remotely you will need to set the "server address" to ensure the bookmarklet has
the correct URL in it.

### Configuring Downloaders

Gropple's default configuration uses `yt-dlp` and has two profiles set up, one
for downloading video, the other for downloading audio (mp3).

Note that gropple does not include any downloaders, you have to install them
separately.

If you would like to use a youtube-dl compatible fork or change the options you
can do so on the right hand side. Create as many profiles as you wish, whenever
you start a download you can choose the appropriate profile.

Note that the command arguments must each be specified separately - see the
default configuration for an example.

While gropple will use your `PATH` to find the executable, you can also specify
a full path instead. Note that any tools that the downloader calls itself (for
instance, `ffmpeg`) will need to be available on your path.

### Alternate destinations

Gropple supports adding additional optional destinations. By default, all
downloads will be stored in the main download path specified in the config. You
can also add one or more destinations, and you can choose one of these
destinations when queueing a new download, or while it is still downloading from
the popup.

The file will be moved after downloading is complete.

## Portable mode

If you'd like to use gropple from a USB stick or similar, copy the config file
from its default location (shown when you start gropple) to the same location as
the binary, and rename it to `gropple.yml`.

## Problems

Many download problems are diagnosable via the log - check in the popup window
and scroll the log down to the bottom. The most common problem is that `yt-dlp`
cannot be found, or its dependency (like `ffmpeg`) cannot be found on your path.

Gropple only calls external tools like `yt-dlp` to do the downloading. If you
are having problems downloading from a site, make sure that `yt-dlp` is updated
to the latest version (`yd-dlp -U`).

For other problems, please file an issue on github.

## TODO

Many things. Please raise an issue after checking the [currently open
issues](https://github.com/tardisx/gropple/issues).
