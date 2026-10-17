# Moonwall

決めたサイトを、開けてよい時間の外では別の URL へ迂回させる Mac 用の道具です。Chrome / Arc の拡張機能と、それを外させない見張り役（Mac アプリ）でできています。iPhone アプリとは iCloud で設定を共有します。

- 止めるサイトは足すとすぐ止まり、外すのは 24 時間後
- 開けてよい時間（例: 平日 14:30〜15:40 だけ YouTube）を決められる
- Moonwall を無効にしたブラウザや、Moonwall の入っていないブラウザ（Safari・Firefox など）は見張り役が閉じる

必要なもの: macOS 14 以上、Google Chrome または Arc

## ダウンロード

| | |
|---|---|
| Mac アプリ | 準備中 |
| Chrome / Arc 拡張機能 | [Chrome ウェブストアの Moonwall](https://chromewebstore.google.com/detail/bhdjgpdchikocailnddgmnkmappdgmck) |
| iPhone アプリ | 準備中 |

## 入れる前に

Moonwall は「衝動的に外せない」ことを目的にしています。入れると次のようになります。

- Moonwall の入っていないブラウザ（Safari・Firefox・Brave・Edge など）は、開くとすぐ閉じられる
- Chrome / Arc で Moonwall を無効にしたり、入れていないプロファイルを開いたりすると、猶予（60 秒）ののちに閉じられる
- 外すには管理者パスワードが要る（下の「外し方」）

## 入れ方

1. Moonwall.dmg を開き、Moonwall を「アプリケーション」フォルダにドラッグする
2. 「アプリケーション」の Moonwall を開く
3. システム設定の「ログイン項目」が開くので、Moonwall の「バックグラウンドでの実行を許可」をオンにする（見張り役が動き始める）
4. メニューバーの Moonwall →「Chrome に Moonwall を入れる…」（Arc なら「Arc に…」）から、プロファイルごとに拡張機能を入れる
5. 拡張機能の詳細で「シークレット モードでの実行を許可」をオンにする
6. メニューバーの Moonwall →「設定を開く…」で、止めるサイトと開けてよい時間を決める

## 外し方

1. システム設定 → 一般 → ログイン項目 →「バックグラウンドでの実行を許可」で Moonwall をオフにする
2. 「アプリケーション」の Moonwall をゴミ箱に入れる（管理者パスワードを求められる）
3. ターミナルで残った設定を消す

```sh
sudo rm -rf "/Library/Application Support/Moonwall" /Library/Google/Chrome/NativeMessagingHosts/local.moonwall.schedule.json \
  "/Library/Application Support/Chromium/NativeMessagingHosts/local.moonwall.schedule.json"
rm -f ~/Library/Application\ Support/Arc/User\ Data/NativeMessagingHosts/local.moonwall.schedule.json
```

4. 各ブラウザの拡張機能の画面で Moonwall を削除する

## プライバシーポリシー / Privacy Policy

最終更新: 2026-10-15

### 日本語

Moonwall は、利用者が決めたサイトを、開けてよい時間の外では別の URL へ迂回させる道具です。Mac アプリ、Chrome 拡張機能、iPhone アプリの 3 つでできています。

#### 扱う情報

| 情報 | 使い道 | 置き場所 |
|---|---|---|
| 止めるサイト・開けてよい時間・リダイレクト先 | 迂回するかどうかの判定 | Mac（`/Library/Application Support/Moonwall`）、iPhone のアプリ内、拡張機能の `chrome.storage`（最後に読めた設定だけ）。Mac と iPhone のあいだは利用者自身の iCloud（key-value storage）で共有する |
| 開いているタブの URL（拡張機能） | 止めるサイトとの照合。照合後は保存しない | 保存しない |
| ブラウザの拡張機能の設定と、動いているアプリ（Mac の見張り役） | Moonwall が有効か・Moonwall の入っていないブラウザが開いていないかの確認 | 保存しない（判定の記録として、ブラウザ名と理由だけを Mac の `/var/log/moonwall-watchdog.log` に残す） |
| スクリーンタイムの許可（iPhone） | 止めるサイトを iPhone の Safari などで開けなくするため（Apple の Screen Time API） | iPhone の中。どのサイトを見たかはアプリから読めない |

#### 送信・共有

Moonwall は、上記の情報を開発者のサーバーにも第三者にも送りません。開発者がこれらの情報を見ることはできません。Mac と iPhone の共有に使う iCloud は、利用者自身の Apple アカウントの中にあります。解析ツールや広告は使いません。外部のコードを読み込んで実行することもありません。

#### 削除

拡張機能を削除すると、拡張機能が保存した情報は Chrome から消えます。iPhone アプリを削除すると、アプリ内の情報は消えます。Mac の情報の消し方は、配布ページの「外し方」にあります。iCloud に置いた設定は、iPhone の「設定 → Apple アカウント → iCloud → ストレージを管理」から消せます。

#### Chrome ウェブストアのユーザーデータポリシー

Moonwall 拡張機能による情報の利用と転送は、Limited Use の要件を含む [Chrome Web Store User Data Policy](https://developer.chrome.com/docs/webstore/program-policies/policies) に従います。

#### 問い合わせ

https://github.com/kenta3578/detour-privacy/issues

### English

Moonwall redirects sites the user has chosen to another URL outside the hours the user allows. It consists of a Mac app, a Chrome extension, and an iPhone app.

#### Information handled

| Information | Purpose | Where it is kept |
|---|---|---|
| Sites to block, allowed hours, and redirect URL | Deciding whether to redirect | On the Mac (`/Library/Application Support/Moonwall`), inside the iPhone app, and in the extension's `chrome.storage` (only the last settings read). Shared between the Mac and iPhone through the user's own iCloud (key-value storage) |
| URLs of open tabs (extension) | Matched against the sites to block; not stored | Not stored |
| Browser extension settings and running apps (Mac watchdog) | Checking that Moonwall is enabled and that no browser without Moonwall is open | Not stored (only the browser name and reason are logged on the Mac in `/var/log/moonwall-watchdog.log`) |
| Screen Time authorization (iPhone) | Blocking the chosen sites in Safari and other apps on the iPhone (Apple's Screen Time API) | On the iPhone. The app cannot read which sites were visited |

#### Transmission and sharing

Moonwall does not send any of this information to the developer's servers or to third parties, and the developer cannot see it. The iCloud storage used to share settings between the Mac and iPhone belongs to the user's own Apple Account. Moonwall uses no analytics, no advertising, and no remote code.

#### Deletion

Removing the extension deletes what it stored from Chrome. Deleting the iPhone app deletes its data. How to remove Moonwall from the Mac is described under "Uninstall" on the download page. Settings kept in iCloud can be deleted from Settings → Apple Account → iCloud → Manage Storage on the iPhone.

#### Chrome Web Store User Data Policy

The use and transfer of information by the Moonwall extension adheres to the [Chrome Web Store User Data Policy](https://developer.chrome.com/docs/webstore/program-policies/policies), including the Limited Use requirements.

#### Contact

https://github.com/kenta3578/detour-privacy/issues
