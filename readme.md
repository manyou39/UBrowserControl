UBrowserControl
====

UWSC用ブラウザ操作モジュール

特徴
----

- 必要なのはUWSCと対象ブラウザのみ
    - WebDriverなどの外部ファイル不要
    - Devtools Protocolを利用 ([Chrome](https://chromedevtools.github.io/devtools-protocol/), [MsEdge](https://docs.microsoft.com/en-us/microsoft-edge/devtools-protocol-chromium/))
        - FirefoxはDevtools Protocol準拠の[Remote Protocol](https://firefox-source-docs.mozilla.org/remote/index.html)
- 主要ブラウザに対応
    - Google Chrome
    - Microsoft Edge
        - Microsoft Edge Legacyは非対応
    - Mozilla Firefox
        - ☑ Developer Edition
        - ☑ Nightly
        - 🆖 通常版 (Remote Protocolがないので)

動作環境
----

Wiindows 10 以上

対応状況
----

|       機能名       |        関数名        | Chrome | MsEdge | Firefox |    備考    |
|--------------------|----------------------|--------|--------|---------|------------|
| Chromeを開く       | Browser.Chrome       | 0.0.1  |        |         |            |
| MsEdgeを開く       | Browser.MsEdge       |        | 0.0.1  |         |            |
| Firefoxを開く      | Browser.Firefox      |        |        | 0.0.1   |            |
| headless           |                      | 0.0.1  | 0.0.1  |         | 引数で指定 |
| タブを閉じる       | Browser.CloseTab     | 0.0.1  | 0.0.1  |         |            |
| URLを開く          | Browser.Navigate     | 0.0.1  | 0.0.1  | 0.0.1   |            |
| リロード           |                      |        |        |         |            |
| タブ一覧取得       | Browser.GetTabList   | 0.0.1  | 0.0.1  |         |            |
| タブの切り換え     | Browser.SwitchTab    | 0.0.1  | 0.0.1  |         |            |
| エレメント取得     | Browser.FindElement  |        |        |         |            |
|                    | Browser.FindElements |        |        |         |            |
| エレメント操作     |                      |        |        |         |            |
| JavaScript実行     |                      |        |        |         |            |
| ダイアログ操作     |                      |        |        |         |            |
| スクリーンショット |                      |        |        |         |            |

使い方
----

`UBrowserControl.uws`を実行するスクリプトと同じフォルダに置いてcallしてください

```php
call UBrowserControl.uws

BrowserId = Browser.Chrome() // Chromeを起動
Browser.Navigate(BrowserId, "https://localhost/")
```

FAQ
----

### Firefoxが操作できない

通常版は動作対象外です  
[Developer EditionまたはNightly版](https://www.mozilla.org/ja/firefox/channel/desktop/)をインストールしてください

### Developer Edition (またはNightly版) Firefoxをインストールしたのに操作できない

UBrowserControlはブラウザの実行ファイルパスを自動検出します  
そのため通常版Firefoxを起動している可能性があります  

Developer Edition (またはNightly版) Firefoxのパスを設定ファイル(`UBrowserControl.ini`)に記述してください

```ini
[BrowserPath]
Firefox={firefoxインストールフォルダ}\firefox.exe
```

