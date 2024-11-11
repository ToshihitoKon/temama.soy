---
title: slack-quickpost
slug: slack-quickpost
kind: page
draft: true
---

Version at the time of article update: [v0.8.0](https://github.com/ToshihitoKon/slack-quickpost/releases/tag/v0.8.0)

{{< ghcard "https://github.com/ToshihitoKon/slack-quickpost" >}}

This is a lightweight CLI tool created for transitioning from Incoming Webhook to Slack App OAuth Token.

## Features

- Post messages to Slack via CLI
- Specify an icon (emoji name or image URL) and username
- Upload files
- Use profiles to skip arguments when posting

### Use Cases

- Send quick CI/CD notifications to Slack
- Post local log files to Slack
- Get notified on Slack when a long-running command finishes

You can simply run `slack-quickpost --profile hoge --text "Done!"`. There’s no need to set up an Incoming Webhook beforehand, or painstakingly build JSON and pass it to `curl -d`.  
Slack Apps allow you to change the icon and username, making it easy to customize notifications like with the old Webhook.

## Installation

You can use a pre-built binary or `go install`.

You can download the [pre-built binary from GitHub Release](https://github.com/ToshihitoKon/slack-quickpost/releases).  
To use `go install`, run `go install github.com/ToshihitoKon/slack-quickpost@latest` to get the latest version.

## Setup

Create a new Slack App or select an existing App at [https://api.slack.com/apps](https://api.slack.com/apps) and generate an OAuth Token.  
The required Scopes for the Slack App are as follows:

- `chat:write.customize`
- `files:write`

Use the Bot User OAuth Token (starting with `xorb-`).

## Posting

The minimum options required are the Token, Channel, and message text.

```bash
$ slack-quickpost \
    --token "xorb-XXX" \
    --channel "CXXX" \
    --text "hoge"
```

Passing the token as an argument each time isn’t secure, so you can use environment variables or select a profile.
slack-quickpost will use the `SLACK_TOKEN` environment variable by default if it’s set.

```bash
$ export SLACK_TOKEN=xorb-XXX
$ slack-quickpost \
    --channel "CXXX" \
    --text "hoge"
```

You can also read the text from a file.

```bash
$ export SLACK_TOKEN=xorb-XXX
$ slack-quickpost \
    --channel "CXXX" \
    --textfile ./sample.txt
```

### Changing Icon and Username

You can specify options to change the icon and username to anything you like.

```bash
$ slack-quickpost \
    --token "xorb-XXX" \
    --channel "CXXX" \
    --text "hoge" \
    --username "custom user name" \
    --icon ":thumbsup:"    
```

### Posting Files

You can attach any file.
If you specify a text file with `--file` instead of `--textfile`, it will be posted as a text snippet, with syntax highlighting automatically determined by Slack.

```bash
$ slack-quickpost \
    --token "xorb-XXX" \
    --channel "CXXX" \
    --file image.png \
```

{{< notice info>}}

When using `--file`, options like `--text`, `--username`, and `--icon*` are ignored.

{{< /notice >}}

### Snippet
When using `--text` with the `--snippet` option, the provided text will be posted as a text snippet.
This can also be used with `--textfile`.

```bash
$ slack-quickpost \
    --token "xorb-XXX" \
    --channel "CXXX" \
    --text "snippet text"
```

{{< notice info>}}

When using `--snippet`, slack-quickpost saves the file name as `[timestamp].txt`, so the syntax highlighting will be plain text.
To enable syntax highlighting, save it with an extension and post it using `--file`.

{{< /notice >}}

### Profiles

Profiles allow you to save OAuth Tokens and Channels to a file and call them by specifying the file name.
You can use it by saving it in `~/.config/slack-quickpost/*.yaml`.

```yaml
# ~/.config/slack-quickpost/sample.yaml
token: xorb-XXX
channel: CXXX
```

```bash
$ slack-quickpost \
    --profile "sample" \
    --text "hoge"
```
