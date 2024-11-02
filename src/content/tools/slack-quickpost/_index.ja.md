---
title: slack-quickpost
slug: slack-quickpost
kind: page
draft: true
---

記事更新時のバージョン: [v0.8.0](https://github.com/ToshihitoKon/slack-quickpost/releases/tag/v0.8.0)

{{< ghcard "https://github.com/ToshihitoKon/slack-quickpost" >}}

旧Slack APPのIncoming Webhook主流から新AppのOAuth Token形式に移行する際に作った軽量なCLIツールです。

## 特徴

- CLIでSlackにメッセージを投稿ができる
- アイコン(絵文字名か画像URL)、ユーザー名を指定できる
- ファイルを投稿できる
- profileを作成して指定することで引数を省略して特定Workspaceの特定Channelへ投稿できる

## インストール

バイナリかgo installのどちらかから選べます。

ビルド済みバイナリは<a target="_blank" href="https://github.com/ToshihitoKon/slack-quickpost/releases">GitHub Release</a>からダウンロードすることができます。  
goを利用する場合は`go install github.com/ToshihitoKon/slack-quickpost@latest`で最新を取得できます。

## セットアップ

[https://api.slack.com/apps](https://api.slack.com/apps)から新規Slack Appを作成するか、既存のAppを選択し、OAuth Tokenを作成します。  
Slack Appに必要なSocepsは以下になります。

- `chat:write.customize`
- `files:write`

OAuth TokenはBot User OAuth Token(`xorb-`から始まるもの)を利用します。

## 投稿する

最小のオプションは、Tokenとチャンネル、投稿テキストの指定です。
```bash
$ slack-quickpost \
    --token xorb-XXX \
    --channel CXXX \
    --text "hoge"
```

tokenを毎度引数に渡すのはセキュアではないため、環境変数及びProfileを選択して利用することができます。  
slack-quickpostは`SLACK_TOKEN`環境変数がセットされている場合はデフォルトでこれを利用します。

```bash
$ export SLACK_TOKEN=xorb-XXX
$ slack-quickpost \
    --channel CXXX \
    --text "hoge"
```

### アイコン、ユーザー名の変更

オプションを付与することで、アイコンとユーザー名を任意のものに変更することができます。

```bash
$ slack-quickpost \
    --token "xorb-XXX" \
    --channel "CXXX" \
    --text "hoge" \
    --username "custom user name" \
    --icon ":thumbsup:"    
```

### ファイルの投稿

任意のファイルを添付することができます。  
テキストファイルを指定するとSnippetとして表示されます。（これはSlackの仕様のため挙動が変わる可能性があります）

```bash
$ slack-quickpost \
    --token "xorb-XXX" \
    --channel "CXXX" \
    --file image.png \
```

{{< notice info>}}
Information
{{< /notice >}}

### スニペット

### ファイルの投稿

### プロファイル

プロファイルは、OAuth TokenとChannelをファイルに保存して、ファイル名の指定で呼び出す機能です。  
プロファイルは`~/.config/slack-quickpost/*.yaml`に保存することで利用できます。  

```yaml
# ~/.config/slack-quickpost/sample.yaml
token: xorb-XXX
channel: CXXX
```

```bash
$ slack-quickpost \
    --profile sample \
    --text "hoge"
```
