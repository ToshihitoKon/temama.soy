---
title: slack-quickpost
slug: slack-quickpost
kind: page
draft: true
---

記事更新時のバージョン: [v0.8.0](https://github.com/ToshihitoKon/slack-quickpost/releases/tag/v0.8.0)

<a class="card" href="https://github.com/ToshihitoKon/slack-quickpost" target="_blank">
  <div class="card-header">
    <img src="https://avatars.githubusercontent.com/u/10419053?s=200&v=4" alt="GitHub Logo">
    <div class="card-title">
      ToshihitoKon/slack-quickpost
    </div>
  </div>
  <div class="card-description">
    slack post cli tool
</div>
  <div class="card-footer">github.com</div>
</a>

旧Slack APPのIncoming Webhook主流から新AppのOAuth Token形式に移行する際に作った軽量なCLIツールです。

## 特徴

- CLIでSlackにメッセージを投稿ができる
- アイコン(絵文字名か画像URL)、ユーザー名を指定できる
- ファイルを投稿できる
- profileを作成して指定することで引数を省略して特定Workspaceの特定Channelへ投稿できる

## インストール

バイナリかgo installを利用できます。

ビルド済みバイナリは<a target="_blank" href="https://github.com/ToshihitoKon/slack-quickpost/releases">GitHub Release</a>からダウンロードすることができます。  
goを利用する場合は`go install github.com/ToshihitoKon/slack-quickpost@latest`で最新を取得できます。

## セットアップ

<a href="https://api.slack.com/apps" target="_blank">https://api.slack.com/apps</a>から新規Slack Appを作成するか、既存のAppを選択し、OAuth Tokenを作成します。  
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


`--file`を指定した場合、 `--text` `--username` `--icon*`は無視されます。
{ .note }

### スニペット

### ファイルの投稿

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

<style>
.card {
    border: 1px solid #ddd;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.card-description,
.card-footer {
    color: #555;
}


.card {
    margin: 16px auto;
    display: block;
    border-radius: 8px;
    padding: 16px;
    max-width: 600px;
}

.card-header {
    display: flex;
    align-items: center;
    margin: 0;
}

.card img {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    margin: 0;
}

.card-title {
    font-size: 18px;
    font-weight: bold;
    margin: 10px;
}

.card-description {
    font-size: 14px;
    margin: 8px 0;
}

.card-footer {
    font-size: 13px;
    margin: 0;
    text-align: right;
}

.note {
  padding: 16px;
  margin-top: 20px;
  border-radius: 8px;
  font-size: 1em;

  background-color: #FEF0B3;
}
.dark .note {
  background-color: #2e2e33;
}

</style>
