# Changelog

## [1.1.0] - 2026-09-22

### Added

- **Keyboard shortcuts** — every operation is now reachable without a mouse; press F1 to open the full shortcut list, which can also be navigated with the arrow keys and Enter
- **Bookmarks** — right-click any page to add a named bookmark; jump to bookmarked pages from the Bookmarks panel; rename (F2), remove (Delete), or clear all
- **"Last read" mark** — Ctrl+R marks the current page; Ctrl+J jumps back to it; shown at the top of the Bookmarks panel
- **Search history** — Alt+↓ shows previously searched terms; select one to re-search; Delete removes an entry; clear all available
- **Zoom popup** — Ctrl+E opens a zoom popup with fit-to-width, fit-to-page, actual-size options and a numeric input field
- **Page list popup** — Ctrl+Home / Ctrl+End opens the skipped-page list for quick navigation
- **View history navigation** — Alt+← / Alt+→ steps back and forward through the page view history

### Improved

- **Search** — Alt+L toggles the search-results panel; Alt+C toggles match-case; Alt+W toggles whole-word; the scan starts from the current page and spreads outward so nearby matches appear first
- **Outline panel** — arrow keys select entries; Enter jumps; Esc closes
- **Thumbnail panel** — arrow keys select thumbnails; Enter jumps; Esc closes
- **Bookmarks panel** — arrow keys navigate entries including "Clear all"; Enter confirms; Delete removes; F2 renames
- **History / Search-history popups** — arrow keys navigate entries including "Clear all"; Enter confirms; Delete removes an entry
- **Settings** — "Opening page" and "On battery" options are now drop-down selects that respond instantly; Tab moves between fields
- **Toolbar tooltips** — all buttons show their keyboard shortcut in the tooltip
- **Page navigation keys** — Ctrl+PageUp / Ctrl+PageDown step one page; Home / End jump to the first / last page; Ctrl+G focuses the page input field
- **Tab management** — Ctrl+Tab / Ctrl+Shift+Tab switch tabs; Ctrl+W closes the active tab; Ctrl+, opens settings

### Fixed

- Navigating from a bookmark, page list, or page-input field now records a history entry so Alt+← can return to the previous location
- Japanese-path crash fixed (byte-slice comparison replaced with `starts_with`)

---

## [1.0.0] - 2026-09-10

Initial release.

### Features

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
- Color themes — built-in and custom themes via JSON files in the `themes` folder
- Language switching (English / Japanese) via the settings screen
- Window position, size, and maximized state restored on next launch
- GPU-accelerated UI via GPUI (falls back to CPU rendering if no GPU is available)
- Multi-tab support — open multiple PDFs in separate tabs
- Register as the default PDF app from the settings screen
- Adjustable scroll speed and acceleration

---

# 更新履歴

## [1.1.0] - 2026-09-22

### 追加

- **キーボードショートカット** — すべての操作をマウスなしで行えるようになりました。F1 でショートカット一覧を開けます。一覧は矢印キーと Enter でも操作できます
- **ブックマーク** — ページを右クリックして名前付きのブックマークを追加できます。サイドバーのブックマークパネルからジャンプできます。F2 で名前を変更、Delete で削除、全削除にも対応しています
- **「ここまで読んだ」** — Ctrl+R で現在ページに印を付け、Ctrl+J でそこへ戻ります。ブックマークパネルの先頭に表示されます
- **検索履歴** — Alt+↓ で過去の検索語の一覧を表示します。選ぶと再検索します。Delete で個別削除、全削除にも対応しています
- **倍率ポップアップ** — Ctrl+E で倍率の設定ポップアップを開けます。幅・全体・等倍の選択と数値入力に対応しています
- **ページリストポップアップ** — Ctrl+Home / Ctrl+End で飛ばしたページの一覧を開いてすばやくジャンプできます
- **表示履歴ナビゲーション** — Alt+← / Alt+→ で表示履歴を前後に移動できます

### 改善

- **テキスト検索** — Alt+L で検索結果パネルの開閉、Alt+C で大文字小文字の区別、Alt+W で単語単位の切り替えができます。走査が現在ページを起点に前後へ広がるようになり、近くの一致が先に見つかります
- **目次パネル** — 矢印キーで選択、Enter でジャンプ、Esc で閉じます
- **サムネイルパネル** — 矢印キーで選択、Enter でジャンプ、Esc で閉じます
- **ブックマークパネル** — 矢印キーで「すべて消す」を含む一覧を移動、Enter で確定、Delete で削除、F2 で名前変更できます
- **表示履歴・検索履歴ポップアップ** — 矢印キーで「すべて消す」を含む一覧を移動、Enter で確定、Delete で削除できます
- **設定画面** — 「開くページ」と「バッテリー動作時」がドロップダウンになり、選んだ瞬間に反映されます。Tab でフィールド間を移動できます
- **ツールチップ** — すべてのボタンにキーボードショートカットを表示するようにしました
- **ページ移動** — Ctrl+PageUp / Ctrl+PageDown で1ページ移動、Home / End で先頭・末尾へジャンプ、Ctrl+G でページ番号入力欄にフォーカスします
- **タブ操作** — Ctrl+Tab / Ctrl+Shift+Tab でタブを切り替え、Ctrl+W でタブを閉じ、Ctrl+, で設定を開きます

### 修正

- ブックマーク・ページリスト・ページ番号入力欄からのページ移動が表示履歴に記録されるようになり、Alt+← で元のページへ戻れるようになりました
- 日本語を含むパスを開いたときにクラッシュする問題を修正しました

---

## [1.0.0] - 2026-09-10

最初のリリース。

### 主な機能

- 連続スクロールと単一ページ表示の切り替え
- 1ページ表示と見開き表示の切り替え
- 幅に合わせる・ページ全体・等倍のズームモード、および拡大縮小
- ページの回転（時計回り・反時計回り）
- 大文字小文字・単語単位オプション付きのテキスト検索（Ctrl+F）
- テキストの選択とコピー（Ctrl+C・右クリックメニュー）
- 目次（アウトライン）パネル
- サムネイルパネル
- パスワード付きPDFのサポート
- 表示履歴と前回ページへの復元
- カラーテーマ（内蔵テーマおよび `themes` フォルダへのJSON配置によるカスタムテーマ）
- 設定画面からの言語切り替え（英語・日本語）
- ウィンドウの位置・サイズ・最大化状態の復元
- GPUI によるGPUアクセラレーションUI（GPU未搭載環境ではCPU描画にフォールバック）
- マルチタブ対応
- 設定画面からの既定のPDFアプリ登録
- スクロール速度と加減速度の調整
