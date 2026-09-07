# BuMoSm PDF Viewer

A simple PDF viewer for Windows.  
Built with [GPUI](https://github.com/zed-industries/zed/tree/main/crates/gpui) — GPU-accelerated rendering keeps CPU usage low, and falls back gracefully on systems without a dedicated GPU.

---

## Features

- Continuous scroll and single-page display modes
- Single-page and two-page spread layouts
- Zoom in/out with fit-to-width, fit-to-page, and actual size modes
- Page rotation (clockwise and counter-clockwise)
- Text search with match-case and whole-word options (Ctrl+F)
- Text selection and copy via Ctrl+C or right-click context menu
- Table of contents (outline) panel
- Thumbnail panel for quick navigation
- Password-protected PDF support
- Recent files history with per-file last-page restore
- Color themes — built-in themes and custom themes via JSON files in the `themes` folder
- Language switching (English / Japanese) via the settings screen
- Window position, size and maximized state restored on the next launch
- GPU-accelerated UI via GPUI (falls back to CPU rendering if no GPU is available)
- Multi-tab support — open multiple PDFs in separate tabs
- Register as the default PDF app from the settings screen
- Adjustable scroll speed and acceleration

## Built With

- [Rust](https://www.rust-lang.org/) — systems programming language
- [GPUI](https://github.com/zed-industries/zed/tree/main/crates/gpui) — GPU-accelerated UI framework
- [pdfium-render](https://github.com/ajrcarey/pdfium-render) — PDF rendering via Google's PDFium

## Requirements

- Windows 10 or later
- `pdfium.dll` placed in the same folder as the executable
- No additional runtime or GPU required

## Usage

### Opening a PDF

- Click the **Open** button or press **Ctrl+O** to open a file dialog
- Drag and drop a PDF file onto the window
- Select a file from the **Recent files** list in the toolbar

### Viewing

| Action | Operation |
|---|---|
| Zoom in / out | Ctrl+= / Ctrl+- |
| Fit to width | Ctrl+1 |
| Fit to page | Ctrl+2 |
| Actual size | Ctrl+0 |
| Rotate clockwise | Ctrl+Shift++ |
| Rotate counter-clockwise | Ctrl+Shift+- |
| First page | Home |
| Last page | End |
| Toggle outline | F4 |
| Toggle fullscreen | F11 |
| Jump to page number field | Ctrl+G |

### Search

Press **Ctrl+F** to open the search bar. Type to search, then press **F3** to jump to the next match or **Shift+F3** for the previous one. Press **Esc** to close the search bar.

Available options: **Match case** and **Match whole word**.

### Text selection and copy

Click and drag on a page to select text. The selection can extend beyond the visible area — drag the cursor outside the page to scroll automatically.

- **Ctrl+A** — select all text on the current page
- **Ctrl+C** — copy the selected text
- **Right-click** — opens a context menu with "Copy"

### Password-protected PDFs

When you open a password-protected PDF, a dialog appears prompting you to enter the password.

### Recent files

The toolbar shows a list of recently opened files. The number of files retained is configurable in the settings (1–100, default 20).

When **Open at the last page** is enabled in settings, opening a file from the recent list will jump directly to the page you were on last time.

### Settings

Click **Settings** to open the settings panel.

| Setting | Description |
|---|---|
| Language | Display language |
| Theme | Color theme |
| View mode | Continuous scroll or single-page |
| Page layout | Single page or two-page spread |
| Cover page | Show the first page alone or paired from the start |
| Binding | Left-bound or right-bound (affects spread order) |
| Initial zoom | Default zoom level when opening a PDF |
| Number of recent files | How many files to keep in the history (1–100) |
| Open at the last page | Resume from where you left off |
| Scroll speed | How fast one wheel notch scrolls (see [Scrolling](#scrolling)) |
| Scroll acceleration | How sharply the movement speeds up and slows down (see [Scrolling](#scrolling)) |
| Lower the frame rate on battery | Caps the frame rate at 30 FPS while running on battery |
| Set as default PDF app | Opens the Windows default apps settings page for this application |

### Scrolling

Two settings control how the view scrolls. Both apply to the mouse wheel and to jumps made from the outline, the thumbnail panel and the page number buttons.

**Scroll speed (1-10, default 5)**

How long one wheel notch takes to travel its full distance. A larger number scrolls **faster**.

| Value | Duration |
|---|---|
| 1 | approx. 467 ms |
| 3 | approx. 367 ms |
| 5 | approx. 267 ms |
| 7 | approx. 167 ms |
| 10 | approx. 17 ms (near-instant) |

**Scroll acceleration (1-5, default 3)**

How sharply the movement picks up speed at the start and settles at the end. A larger number accelerates and stops **more quickly**; a smaller number gives a softer, more gradual start and stop. This does not change the total duration set by Scroll speed.

| Value | Ramp duration |
|---|---|
| 1 | approx. 83 ms (softest) |
| 3 | approx. 50 ms |
| 5 | approx. 17 ms (sharpest) |

When Scroll speed is set to 8 or higher, the total duration is too short to fit a gradual start, so acceleration is not applied. The movement starts at full speed and eases out as it approaches its destination.

The ramp is also capped at half the total duration, so the two ends never overlap. At Scroll speed 7 with acceleration 1, the movement is pure acceleration and deceleration with no constant-speed section in between.

### Window position and size

The window position, size and maximized state are saved when the application is closed, and restored the next time it starts. The monitor the window was displayed on is recorded as well, so on a multi-monitor setup the window reopens on the same monitor.

If that monitor is no longer connected, or the saved position no longer fits on the screen, the window opens at the default position on the primary monitor.

The state is written when the window is closed normally. It is not saved if the process is terminated forcibly, for example from Task Manager.

### Default PDF app

The settings panel has a button to make this application the default PDF viewer. Pressing it registers the application with Windows and opens the Default apps settings page for it, where you can select **.pdf** and confirm.

Windows does not allow an application to change the default handler on its own, so the final choice is always made on the settings page. The button label switches to **Unset as default PDF app** once this application is the default.

If you move the executable to a different folder, press the button again to update the registered path.

### Themes

The color scheme is selected under **Theme** in the settings panel. The list is split into two groups:

- **Built-in** — the bundled light and dark schemes, plus **Follow the system**, which tracks the OS light/dark setting
- **Theme files** — schemes loaded from the `themes` folder next to the executable

Themes in the second group are plain JSON files. Editing one takes effect immediately, without restarting the application. See `README_en.txt` in the `themes` folder for the file format and the list of available color keys.

### Settings file

Settings are saved automatically to `config.json` in the same folder as the executable. The window position, size, maximized state and the monitor in use are stored in the same file. You can copy or back up this file to preserve your configuration.

### Language

The display language can be changed in the settings panel. Currently supported: **English** and **Japanese**.

The language strings are defined in `en.json` and `ja.json` in the `locales` folder next to the executable. You can edit these files to customize the wording.

Languages are read from that folder at startup, so you can add one by copying an existing file, renaming it to the language code you want (`fr.json`, `de.json` and so on) and translating its contents. The new language appears in the settings panel the next time the application starts. The name shown in the list comes from the `locale.language_name` entry inside the file.

Any entry you leave out falls back to the English text, so a partial translation still works. See `README_en.txt` in the `locales` folder for the full list of entries and what each one controls.

### Multiple instances

Only one instance of BuMoSm PDF Viewer can run at a time. If you launch a second instance, the existing window is brought to the front and the new instance exits immediately.

## License

Copyright 2026 Hiroki  
Licensed under the [Apache License, Version 2.0](LICENSE).

This software is provided "as is", without warranty of any kind.  
The author is not responsible for any damages or issues arising from its use.

## Contributing / Bug Reports

If you find a bug or have a question, please open an [Issue](https://github.com/BuMoSm-Series/BuMoSmPDFViewer/issues).

## Acknowledgements

- [GPUI](https://github.com/zed-industries/zed/tree/main/crates/gpui) — Apache 2.0
- [gpui-component](https://github.com/longbridge/gpui-component) — Apache 2.0
- [pdfium-render](https://github.com/ajrcarey/pdfium-render) — MIT / Apache 2.0

---

# BuMoSm PDF Viewer（日本語）

Windows向けのシンプルなPDFビューアです。  
[GPUI](https://github.com/zed-industries/zed/tree/main/crates/gpui) によるGPU描画でCPU負荷を低減します。GPU未搭載の環境でもCPU描画にフォールバックして動作します。

---

## 機能

- 連続スクロール表示・単一ページ表示の切り替え
- 1ページ表示・見開き表示の切り替え
- ズームイン・アウト（幅に合わせる・ページ全体・等倍）
- ページの回転（時計回り・反時計回り）
- テキスト検索（大文字小文字区別・単語一致オプション付き、Ctrl+F）
- テキスト選択とコピー（Ctrl+C・右クリックメニュー）
- 目次（アウトライン）パネル
- サムネイルパネルによるページ一覧ナビゲーション
- パスワード付きPDFの対応
- 最近開いたファイルの履歴と前回ページへの復元
- カラーテーマ（内蔵テーマ・`themes` フォルダの JSON ファイルによるカスタムテーマ）
- 設定画面から表示言語を切り替え可能（日本語・英語）
- 終了時のウィンドウ位置・サイズ・最大化状態を次回起動時に復元
- GPUIによるGPU描画（GPU未搭載の場合はCPU描画で動作）
- マルチタブ対応 — 複数のPDFを別々のタブで開ける
- 設定画面から既定のPDFアプリとして登録可能
- スクロールの速度と加減速度を調整可能

## 開発言語・フレームワーク

- [Rust](https://www.rust-lang.org/) — システムプログラミング言語
- [GPUI](https://github.com/zed-industries/zed/tree/main/crates/gpui) — GPU描画UIフレームワーク
- [pdfium-render](https://github.com/ajrcarey/pdfium-render) — Google PDFium によるPDFレンダリング

## 動作環境

- Windows 10 以降
- 実行ファイルと同じフォルダに `pdfium.dll` が必要
- 追加のランタイムやGPUは不要

## 使い方

### PDFを開く

- **開く**ボタンをクリックするか **Ctrl+O** でファイルダイアログを開く
- PDFファイルをウィンドウにドラッグ＆ドロップする
- ツールバーの**表示履歴**から選択する

### 表示操作

| 操作 | キー |
|---|---|
| ズームイン・アウト | Ctrl+= / Ctrl+- |
| 幅に合わせる | Ctrl+1 |
| ページ全体 | Ctrl+2 |
| 等倍 | Ctrl+0 |
| 時計回りに回転 | Ctrl+Shift++ |
| 反時計回りに回転 | Ctrl+Shift+- |
| 先頭ページ | Home |
| 末尾ページ | End |
| 目次の表示切り替え | F4 |
| 全画面表示の切り替え | F11 |
| ページ番号入力欄へ移動 | Ctrl+G |

### テキスト検索

**Ctrl+F** で検索バーを開きます。文字を入力して **F3** で次の一致へ、**Shift+F3** で前の一致へ移動します。**Esc** で検索バーを閉じます。

オプション：**大文字小文字を区別する**・**単語として一致するものだけを探す**

### テキストの選択とコピー

ページ上でドラッグしてテキストを選択できます。マウスカーソルをページ外へ動かすと自動でスクロールするため、画面に見えていない範囲まで続けて選択できます。

- **Ctrl+A** — 現在のページの全テキストを選択
- **Ctrl+C** — 選択したテキストをコピー
- **右クリック** — 「コピー」のコンテキストメニューを表示

### パスワード付きPDF

パスワードで保護されたPDFを開くと、パスワードの入力ダイアログが表示されます。

### 表示履歴

ツールバーに最近開いたファイルの一覧が表示されます。保持する件数は設定で変更できます（1〜100件、既定は20件）。

設定で**前回のページから開く**を有効にすると、履歴からファイルを開いたときに前回見ていたページへ自動で移動します。

### 設定

**設定**ボタンをクリックすると設定パネルが開きます。

| 設定項目 | 説明 |
|---|---|
| 言語 | 表示言語 |
| 配色 | カラーテーマ |
| 表示モード | 連続スクロールまたは単一ページ |
| ページの並べ方 | 1ページ表示または見開き表示 |
| 見開きの表紙 | 1ページ目を単独で表示するか2ページずつ並べるか |
| 綴じ方向 | 左綴じまたは右綴じ（見開きの順序に影響） |
| 初期倍率 | PDFを開いたときの既定のズーム |
| 履歴に残す件数 | 履歴に保持するファイル数（1〜100件） |
| 前回のページから開く | 前回見ていたページから再開する |
| スクロール速度 | ホイール1ノッチ分の移動の速さ（[スクロール](#スクロール)を参照） |
| スクロール加減速度 | 動き出しと止まりぎわの鋭さ（[スクロール](#スクロール)を参照） |
| バッテリー動作時はFPSを下げる | バッテリー動作中はフレームレートを30FPSに制限する |
| 既定のPDFアプリに設定する | Windowsの既定アプリ設定画面をこのアプリのページで開く |

### スクロール

2つの設定でスクロールの動きを調整できます。どちらもマウスホイールだけでなく、目次・サムネイル・ページ番号から遠くへ飛ぶときにも効きます。

**スクロール速度（1〜10、既定は5）**

ホイール1ノッチ分を動き終えるまでの時間です。数字が大きいほど**速く**なります。

| 設定値 | 所要時間 |
|---|---|
| 1 | 約 467ms |
| 3 | 約 367ms |
| 5 | 約 267ms |
| 7 | 約 167ms |
| 10 | 約 17ms（ほぼ瞬時） |

**スクロール加減速度（1〜5、既定は3）**

動き出しの加速と、止まりぎわの減速の鋭さです。数字が大きいほど**素早く**加速して素早く止まり、小さいほどゆっくり動き出してふわりと止まります。スクロール速度で決めた全体の時間は変わりません。

| 設定値 | 加減速にかける時間 |
|---|---|
| 1 | 約 83ms（最もゆるやか） |
| 3 | 約 50ms |
| 5 | 約 17ms（最も鋭い） |

スクロール速度が8以上のときは全体の時間が短く、加速する余裕がないため加減速は効きません。最初から全速で動き出し、止まりぎわだけ減速します。

加減速にかける時間は全体の半分を超えないよう抑えられるので、加速と減速が重なることはありません。スクロール速度7・加減速度1では、加速と減速だけで全体を使い切り、間の等速部分が無くなります。

### ウィンドウの位置とサイズ

終了時のウィンドウ位置・サイズ・最大化状態を保存し、次回起動時に復元します。表示していたモニターも記録するため、マルチモニター環境でも同じモニターに復元されます。

該当のモニターが接続されていない場合や、保存された位置が画面に収まらない場合は、プライマリモニターの既定位置に表示します。

保存はウィンドウを通常の操作で閉じたときに行われます。タスクマネージャーからの強制終了などでは保存されません。

### 既定のPDFアプリ

設定パネルに、このアプリをPDFの既定アプリにするためのボタンがあります。押すとWindowsにこのアプリを登録したうえで、既定アプリの設定画面をこのアプリのページで開きます。そこで **.pdf** を選んで設定してください。

Windowsの仕様上、アプリが自分で既定を切り替えることはできないため、最終的な選択は設定画面で行う必要があります。既定になっている場合、ボタンの文言は**既定のPDFアプリを解除する**に変わります。

実行ファイルを別のフォルダへ移動した場合は、もう一度ボタンを押すと登録されているパスが更新されます。

### テーマ

設定パネルの**配色**から選びます。一覧は2つのグループに分かれています。

- **標準** — 同梱のライトとダーク、および OS のライト／ダーク設定に追従する**OSの設定に従う**
- **テーマファイル** — 実行ファイルと同じフォルダの `themes` フォルダから読み込んだもの

後者は普通の JSON ファイルです。書き換えると再起動せずにその場で反映されます。ファイルの書き方と指定できる色の一覧は、`themes` フォルダの `README_ja.txt` を参照してください。

### 設定ファイル

設定は実行ファイルと同じフォルダの `config.json` に自動保存されます。ウィンドウの位置・サイズ・最大化状態・表示していたモニターも同じファイルに保存されます。このファイルをコピーまたはバックアップすることで設定を保持できます。

### 言語設定

設定パネルから表示言語を切り替えられます。現在対応している言語は**日本語**と**英語**です。

表示文字列は実行ファイルと同じフォルダの `locales` フォルダ内の `en.json`（英語）と `ja.json`（日本語）で定義されています。これらのファイルを編集すれば文言を変更できます。

起動時にこのフォルダを読むので、既存のファイルを複製して言語コードの名前（`fr.json`、`de.json` など）に変え、中身を翻訳すれば言語を追加できます。次回の起動から設定パネルの一覧に出ます。一覧に表示される名前は、ファイル内の `locale.language_name` の値です。

書かれていない項目は英語の文言が使われるので、途中まで訳した状態でも動きます。項目の一覧とそれぞれが画面のどこに出るかは、`locales` フォルダの `README_ja.txt` を参照してください。

### 多重起動の禁止

BuMoSm PDF Viewerは同時に1つのインスタンスしか起動できません。2つ目を起動しようとすると、既存のウィンドウが前面に表示されて新しいインスタンスは即座に終了します。

## ライセンス

Copyright 2026 Hiroki  
[Apache License, Version 2.0](LICENSE) のもとで公開しています。

本ソフトウェアは現状のまま（"as is"）提供されます。  
使用によって生じたいかなる損害・問題についても、作者は責任を負いません。

## バグ報告・質問

バグの報告や質問は [Issues](https://github.com/BuMoSm-Series/BuMoSmPDFViewer/issues) からお願いします。

## 使用ライブラリ

- [GPUI](https://github.com/zed-industries/zed/tree/main/crates/gpui) — Apache 2.0
- [gpui-component](https://github.com/longbridge/gpui-component) — Apache 2.0
- [pdfium-render](https://github.com/ajrcarey/pdfium-render) — MIT / Apache 2.0