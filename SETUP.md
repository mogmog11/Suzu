# AI秘書セットアップガイド

このリポジトリはClaude Coworkで動作するAI秘書システムの設定ファイル一式です。

## セットアップ手順

### 1. このリポジトリをClone / Coworkに読み込む

```bash
git clone <repo-url> ~/AI秘書
```

または、Claude DesktopのCoworkでこのフォルダを開く。

---

### 2. 個人情報を設定する

以下のファイルを自分の情報で更新する：

**`CLAUDE.md`**
- `[あなたの名前]` → 自分の名前
- `[CEO / PM / etc.]` → 自分の役職
- `[会社名]` → 自社名

**`context/my-profile.md`**
- 基本情報をすべて記入
- VIP送信者リストを追加
- よく使うツールのアカウント情報を記入

**`scheduled-tasks/02_news-digest.md`**
- `[業界テーマ1〜3]` を自社の業界キーワードに変更

---

### 3. コネクターを接続する

Claude Desktop の **Customize > Connectors** から以下を接続：

| コネクター | 必須/任意 | 用途 |
|-----------|---------|------|
| Gmail | 必須 | メールトリアージ・返信ドラフト |
| Google Calendar | 必須 | スケジュール確認・イベント作成 |
| Slack | 任意 | チャンネル確認・メッセージ送信 |
| Google Drive | 任意 | ドキュメントアクセス |
| Notion | 任意 | プロジェクト管理連携 |

⚠️ スケジュールタスクを設定する前に必ず接続・認証を完了させること。

---

### 4. Global Instructions を設定する

**Settings > Cowork > Global Instructions** に以下を貼り付ける：

```
あなたは私のAI秘書です。以下を常に守ってください：
1. 作業開始前に必ずCLAUDE.mdとcontext/フォルダを参照する
2. 依頼を受けたらPRJ-###として1_projects/に採番・フォルダ作成する
3. 成果物はプロジェクトのoutput/に、顧客情報は2_areas/clients/にも転記する
4. 日本語で出力、専門用語は必要に応じて英語併記
5. 完了時に実行した内容のサマリーを出力する
6. 新しい学習事項はcontext/memory/glossary.mdに記録する
```

---

### 5. スケジュールタスクを設定する

`scheduled-tasks/` フォルダ内の各ファイルを参照し、
Claude Desktopの **Scheduled** タブからタスクを作成する。

| ファイル | タスク名 | 実行タイミング |
|---------|---------|-------------|
| `01_morning-briefing.md` | 朝のブリーフィング | 平日 07:30 |
| `02_news-digest.md` | 業界ニュースダイジェスト | 毎日 08:00 |
| `03_weekly-report.md` | 週次レポート | 毎週金曜 17:00 |
| `04_file-archiving.md` | ファイル整理・アーカイブ | 毎週日曜 21:00 |

---

### 6. カスタムプラグインをインストールする（任意）

`my-secretary-plugin/` フォルダを Cowork の **Customize > Browse plugins** からインストールする。

---

### 7. テストラン

1. Coworkで「朝のブリーフィングを実行して」と依頼
2. `2_areas/daily-ops/briefings/` にファイルが生成されることを確認
3. 内容を確認し、`CLAUDE.md` や `context/` の情報を微調整

---

## フォルダ構成

```
~/AI秘書/
├── CLAUDE.md                    ← AI秘書のメインコンフィグ（ここから始める）
├── SETUP.md                     ← このファイル
├── .gitignore
├── claude_desktop_config.json   ← カスタムMCPサーバー設定（上級者向け）
│
├── 1_projects/                  ← P: ゴールと期限のある案件
│   ├── INDEX.md
│   └── PRJ-001_サンプル案件/
│
├── 2_areas/                     ← A: 継続的に管理する責任領域
│   ├── clients/
│   ├── daily-ops/
│   │   ├── briefings/
│   │   ├── email-logs/
│   │   └── meeting-notes/
│   └── company/
│
├── 3_resources/                 ← R: 参考情報・ナレッジ
│   ├── industry/
│   └── templates/
│
├── 4_archive/                   ← A: 完了・非アクティブ
│
├── context/                     ← AI秘書のメモリー
│   ├── my-profile.md
│   ├── style-guide.md
│   └── memory/
│       ├── glossary.md
│       ├── context/
│       ├── people/
│       └── projects/
│
├── my-secretary-plugin/         ← カスタムプラグイン
│   ├── .claude-plugin/
│   ├── commands/
│   └── skills/
│
└── scheduled-tasks/             ← スケジュールタスクのプロンプト集
    ├── 01_morning-briefing.md
    ├── 02_news-digest.md
    ├── 03_weekly-report.md
    └── 04_file-archiving.md
```
