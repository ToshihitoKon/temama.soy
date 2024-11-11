---
title: slack-quickpost
slug: slack-quickpost
kind: page
draft: false
---

記事更新時のバージョン: [v0.8.0](https://github.com/ToshihitoKon/slack-quickpost/releases/tag/v0.8.0)

{{< ghcard "https://github.com/ToshihitoKon/slack-quickpost" >}}

Incoming WebhookからSlack AppのOAuth Token形式に移行する際に作った軽量なCLIツールです。

## 特徴

- CLIでSlackにメッセージを投稿ができる
- アイコン(絵文字名か画像URL)、ユーザー名を指定できる
- ファイルを投稿できる
- profileで引数を省略して投稿できる

### こんな用途に

- CI/CDの通知を雑にSlackに通知したい
- 手元のログファイルをSlackに投げておきたい
- 時間かかるコマンドが終わったらSlackに通知してほしい

`slack-quickpost --profile hoge --text "おわったよ〜"`で済みます。Incoming Webhookを事前に用意しておく必要も、JSONを頑張って組み立てて`curl -d`に渡す必要もありません。  
Slack Appはアイコンとユーザー名の変更に対応しているので、旧Webhookのように通知のアイコンや名前の設定がかんたんに行えます。

## インストール

バイナリかgo installを利用できます。

<a target="_blank" href="https://github.com/ToshihitoKon/slack-quickpost/releases">ビルド済みバイナリはGitHub Release</a>からダウンロードできます。  
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
    --token "xorb-XXX" \
    --channel "CXXX" \
    --text "hoge"
```

tokenを毎度引数に渡すのはセキュアではないため、環境変数及びProfileを選択して利用することができます。  
slack-quickpostは`SLACK_TOKEN`環境変数がセットされている場合はデフォルトでこれを利用します。

```bash
$ export SLACK_TOKEN=xorb-XXX
$ slack-quickpost \
    --channel "CXXX" \
    --text "hoge"
```

テキストをファイルから読み込むことも可能です。

```bash
$ export SLACK_TOKEN=xorb-XXX
$ slack-quickpost \
    --channel "CXXX" \
    --textfile ./sample.txt
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
テキストファイルを`--textfile`ではなく`--file`で指定するとテキストスニペットとして投稿されます。このときテキストスニペットのハイライトはSlackの自動判定によって決まります。

```bash
$ slack-quickpost \
    --token "xorb-XXX" \
    --channel "CXXX" \
    --file image.png \
```

{{< notice info>}}

`--file`を指定した場合、 `--text` `--username` `--icon*`は無視されます。
{ .note }

{{< /notice >}}

### スニペット

`--text`と一緒に`--snippet`オプションを付けると、与えられたテキストはテキストスニペットとして投稿されます。  
`--textfile`でも利用することができます。


```bash
$ slack-quickpost \
    --token "xorb-XXX" \
    --channel "CXXX" \
    --text "snippet text"
```

{{< notice info>}}

`--snippet`を指定した場合、slack-quickpostはファイル名を`[タイムスタンプ].txt`として投稿します。そのためシンタックスハイライトがplain textになります。  
一度拡張子をつけたファイルに保存して`--file`で投稿することでシンタックスハイライトが効くようになります。

{{< /notice >}}

### プロファイル

プロファイルは、OAuth TokenとChannelをファイルに保存して、ファイル名の指定で呼び出す機能です。  
`~/.config/slack-quickpost/*.yaml`に保存することで利用できます。  

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
