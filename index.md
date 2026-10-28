# Minai

決めたサイトを、見ていい時間の外では開けなくする Mac 用の道具です。Chrome / Arc の拡張機能と、拡張機能を止めさせない見張り役（Mac アプリの中で管理者の権限で動き、決めたとおりにブラウザを閉じる部分）でできています。

- 見ないサイトは追加すると 1 分以内に止まり、見ていい時間（例: 平日 12:00〜13:00 だけ YouTube）の中だけ開ける
- 解除と、見ていい時間を増やす変更は、毎日決めた時刻（はじめは 5:00）まで待ってから効く
- 急ぎの用があるときは、メニューバーの Minai から 5 分だけすべて開けられる

必要なもの: macOS 14 以上、Google Chrome または Arc

## ダウンロード

| | |
|---|---|
| Mac アプリ | [Minai-1.0.6.dmg](https://github.com/kenta3578/detour-privacy/releases/download/mac-v1.0.6/Minai-1.0.6.dmg)（無料） |
| Chrome / Arc 拡張機能 | [Chrome ウェブストアの Minai](https://chromewebstore.google.com/detail/bhdjgpdchikocailnddgmnkmappdgmck) |
| iPhone アプリ | 準備中 |

## 入れる前に

Minai は「衝動的に外せない」ことを目的にしています。準備を終えると、次のようになります。

- Minai を入れられないブラウザ（Safari・Firefox・Brave・Edge など）は、開くとすぐ閉じられる
- Chrome / Arc で Minai を無効にしたり、入れていないプロファイルを開いたりすると、少しの猶予ののちに閉じられる
- 閉じるのは Minai を使うと決めたアカウントのブラウザだけで、同じ Mac のほかのアカウントのブラウザは閉じない
- 外すには予約が要る（下の「外し方」）

## 入れ方

1. Minai-1.0.6.dmg を開き、Minai を「アプリケーション」フォルダにドラッグする
2. 「アプリケーション」の Minai を開き、準備のウインドウの手順を上から順に進める。途中で次の 2 つを求められる
   - システム設定の「ログイン項目」で Minai をオンにする（見張り役が動き始める）
   - Chrome・Arc のプロファイルごとに拡張機能を入れ、拡張機能の「詳細」で「シークレット モードでの実行を許可」をオンにする
3. あとから変えるときは、メニューバーの Minai →「設定を開く…」。アイコンが見えないときは、「アプリケーション」の Minai をもう一度開くと設定のウインドウが出る

## 外し方

管理者パスワードが要ります。この順に進めてください（構成プロファイルを先に外すと、見張り役がブラウザを閉じます）。

1. メニューバーの Minai →「設定を開く…」→ いちばん下の「Minai を外す予約をする…」を押す。外すまでは「外す予約を取り消す」でやめられる
2. 表示された日時を過ぎたら、同じ場所の「Minai を外す…」を押し、管理者パスワードを入れる。見張り役と Mac に置いた設定、Chrome・Arc への登録、Minai のアプリが消える。同じ Mac のほかのアカウントの Minai も止まる
3. 構成プロファイルを入れていれば、システム設定 → 一般 → デバイス管理 で Minai を削除する
4. Chrome / Arc のプロファイルごとに、拡張機能の画面で Minai を削除する。残すと、最後に読んだ設定でサイトを止め続ける

まだ何も止めていないときや、見張り役が動いていないときは、予約せずに「Minai を外す…」が出ます。アプリを先にゴミ箱に入れてしまったときは、アプリを入れ直してから 1 に進んでください。

## プライバシーポリシー / Privacy Policy

最終更新: 2026-10-28

### 日本語

Minai は、利用者が決めたサイトを、見ていい時間の外では開けなくする道具です。Mac アプリ、Chrome 拡張機能、iPhone アプリの 3 つでできています。

#### 扱う情報

| 情報 | 使い道 | 置き場所 |
|---|---|---|
| 見ないサイト・見ていい時間・止めたときに開くページ | 止めるかどうかの判定 | Mac（`/Library/Application Support/Minai`）、iPhone のアプリ内、拡張機能の `chrome.storage`（最後に読めた設定だけ）。Mac と iPhone のあいだでは共有しない |
| 開いているタブの URL（拡張機能） | 見ないサイトとの照合。照合後は保存しない | 保存しない |
| ブラウザの拡張機能の設定と、動いているアプリ（Mac の見張り役） | Minai が有効か・Minai の入っていないブラウザが開いていないかの確認 | 保存しない（判定の記録として、ブラウザ名と理由だけを Mac の `/var/log/minai-watchdog.log` に残す。プロファイル名は書かず、管理者だけが読める） |
| 一時解除・変更の申請・外す予約の記録（Mac） | 一時解除の回数と外せる時刻を数えるのと、申請を受け付けたかを Mac アプリに返すため | Mac の `/Library/Application Support/Minai/users/<アカウントの番号>/`。そのアカウントと管理者だけが読め、同じ Mac のほかのアカウントからは読めない |
| スクリーンタイムの許可（iPhone） | 見ないサイトを iPhone の Safari などで開けなくするため（Apple の Screen Time API） | iPhone の中。どのサイトを見たかはアプリから読めない |
| 初回の案内の進み具合（iPhone） | 案内のどの手順で使うのをやめたかを数え、案内を直すため。送るのは手順の名前と「見た」「次へ進んだ」だけで、各手順につき 1 回だけ | TelemetryDeck（下の「送信・共有」） |

#### 送信・共有

Minai は、上の表の情報のうち、初回の案内の進み具合のほかは（見ないサイト・見ていい時間・止めたときに開くページ・タブの URL・拡張機能の設定と動いているアプリ・一時解除と申請と外す予約の記録・スクリーンタイムの許可）、開発者のサーバーにも第三者にも送りません。開発者がこれらの情報を見ることはできません。

例外は iPhone アプリの初回の案内の進み具合だけで、解析サービスの [TelemetryDeck](https://telemetrydeck.com/privacy/) に送ります。送るのは手順の名前（例: 「見ないものを選ぶ」）と「見た」「次へ進んだ」のどちらかだけです。端末やあなたを見分ける ID、見ないもの、時間、アプリの使い方は送りません。全員が同じ値で送るので、だれの記録かは開発者にも分かりません。通信の仕組み上、通信元の IP アドレスと、通信に必ず付く言語の設定は TelemetryDeck に届きます（アプリや OS の版は送りません）。広告は使いません。外部のコードを読み込んで実行することもありません。

#### 削除

拡張機能を削除すると、拡張機能が保存した情報は Chrome から消えます。iPhone アプリを削除すると、アプリ内の情報は消えます。Mac の情報は、このページの「外し方」で消えます。

#### Chrome ウェブストアのユーザーデータポリシー

Minai 拡張機能による情報の利用と転送は、Limited Use の要件を含む [Chrome Web Store User Data Policy](https://developer.chrome.com/docs/webstore/program-policies/policies) に従います。

#### 問い合わせ

https://github.com/kenta3578/detour-privacy/issues

### English

Minai stops sites the user has chosen from opening outside the hours the user allows. It consists of a Mac app, a Chrome extension, and an iPhone app.

#### Information handled

| Information | Purpose | Where it is kept |
|---|---|---|
| Sites to block, allowed hours, and the page shown when a site is blocked | Deciding whether to block | On the Mac (`/Library/Application Support/Minai`), inside the iPhone app, and in the extension's `chrome.storage` (only the last settings read). Not shared between the Mac and iPhone |
| URLs of open tabs (extension) | Matched against the sites to block; not stored | Not stored |
| Browser extension settings and running apps (Mac watchdog) | Checking that Minai is enabled and that no browser without Minai is open | Not stored (only the browser name and reason are logged on the Mac in `/var/log/minai-watchdog.log`, without profile names and readable only by administrators) |
| Records of temporary unlocks, change requests, and uninstall reservations (Mac) | Counting temporary unlocks and when uninstalling becomes possible, and telling the Mac app whether a request was accepted | On the Mac in `/Library/Application Support/Minai/users/<account number>/`, readable only by that account and administrators, not by other accounts on the same Mac |
| Screen Time authorization (iPhone) | Blocking the chosen sites in Safari and other apps on the iPhone (Apple's Screen Time API) | On the iPhone. The app cannot read which sites were visited |
| Progress through the first-run guide (iPhone) | Counting at which step people stop using the guide, to improve it. Only the step name and "shown" or "advanced" are sent, once per step | TelemetryDeck (see "Transmission and sharing") |

#### Transmission and sharing

Apart from progress through the first-run guide, Minai does not send any of the information in the table above (the sites to block, allowed hours, blocked-site page, tab URLs, browser extension settings and running apps, records of unlocks, requests and uninstall reservations, or Screen Time authorization) to the developer's servers or to third parties, and the developer cannot see it.

The only exception is progress through the iPhone app's first-run guide, which is sent to the analytics service [TelemetryDeck](https://telemetrydeck.com/privacy/). Only the step name (for example, "choose what to block") and either "shown" or "advanced" are sent. No ID that identifies your device or you, no blocked items, no hours, and no other usage is sent. Everyone sends the same value, so not even the developer can tell whose record it is. As with any network request, your IP address and the language setting that every request carries reach TelemetryDeck (the app and OS versions are not sent). Minai uses no advertising and no remote code.

#### Deletion

Removing the extension deletes what it stored from Chrome. Deleting the iPhone app deletes its data. The data on the Mac is removed by following "外し方" (Uninstall) on this page.

#### Chrome Web Store User Data Policy

The use and transfer of information by the Minai extension adheres to the [Chrome Web Store User Data Policy](https://developer.chrome.com/docs/webstore/program-policies/policies), including the Limited Use requirements.

#### Contact

https://github.com/kenta3578/detour-privacy/issues
