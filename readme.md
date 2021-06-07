UBrowserControl
====

UWSC用ブラウザ操作モジュール

*試作版であり正常動作は全く保証されていません*  
*そのあたりがご理解いただける方のみご利用ください*  

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

|       機能名       |        関数名         | Chrome | MsEdge | Firefox |    備考    |
|--------------------|-----------------------|--------|--------|---------|------------|
| Chromeを開く       | Browser.Chrome        | 0.0.1  |        |         |            |
| MsEdgeを開く       | Browser.MsEdge        |        | 0.0.1  |         |            |
| Firefoxを開く      | Browser.Firefox       |        |        | 0.0.1   |            |
| headless           |                       | 0.0.1  | 0.0.1  |         | 引数で指定 |
| タブを閉じる       | Browser.CloseTab      | 0.0.1  | 0.0.1  |         |            |
| URLを開く          | Browser.Navigate      | 0.0.1  | 0.0.1  | 0.0.1   |            |
| リロード           |                       |        |        |         |            |
| タブ一覧取得       | Browser.GetTabList    | 0.0.1  | 0.0.1  |         |            |
| タブの切り換え     | Browser.SwitchTab     | 0.0.1  | 0.0.1  |         |            |
| エレメント取得     | Browser.FindElement   | 0.0.1  |        |         |            |
|                    | Browser.FindElements  | 0.0.1  |        |         |            |
| エレメント操作     |                       |        |        |         |            |
| - クリック         | Browser.ClickElement  | 0.0.1  | 0.0.1  |         |            |
| JavaScript実行     | Browser.ExecuteScript | 0.0.1  | 0.0.1  |         |            |
| ダイアログ操作     |                       |        |        |         |            |
| スクリーンショット |                       |        |        |         |            |

使い方
----

`UBrowserControl.uws`を実行するスクリプトと同じフォルダに置いてcallしてください

```php
call UBrowserControl.uws

BrowserId = Browser.Chrome() // Chromeを起動
Browser.Navigate(BrowserId, "https://localhost/")
```

使い方の詳細は[Wiki](https://github.com/stuncloud/UBrowserControl/wiki)にあります

ビルド方法
----

ビルド済みの`UBrowserControl.uws`が同梱されているため通常はそれを実行時にcallするだけで問題はありません  
ただし、`Chakra.dll`に依存したモジュールが含まれるため、場合によっては正常に動作しないことがあります  
そのような場合は`src\build.uws`を実行することで`json2`ベースの`UBrowserControl.uws`を生成できます

```
(root)
  |_src
    |_build.uws
    |_Modules
      |_ (各種モジュールファイル)
```

このような構成で`build.uws`を実行してください  
`Chakra`か`Json2`を選択するダイアログが表示されるのでいずれかを選択します  
このときファイル構成に不備があるとエラーメッセージと共に終了します  
構成が正常ならビルドが実行されルートフォルダに`UBrowserControl.uws`が出力されます

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

### なにかしらのエラーで停止してしまう

スクリプトエンジンがChakraになっているのが原因かもしれません  
`build.uws`を実行し、表示されたダイアログでJson2を選択してください  
Json2ベースの`UBrowserControl.uws`が出力されます

### Json2に変更したがエラーになる

以下でエラーの詳細(エラーメッセージ等)をご報告ください

- [issue](https://github.com/stuncloud/UBrowserControl/issues)
- [discord](https://discord.gg/fw7PwQuYvs)

