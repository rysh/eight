# Claude AI作業ガイド

このドキュメントは、Claude AIがこのプロジェクト（八意 / The Eight）で作業する際に参照すべき情報をまとめたものです。

## プロジェクト概要

**リポジトリ**: `rysh/eight`
**目的**: 「八意(The Eight)」という神道傍流の宗教に関する情報を管理・共有する

### 主要ファイル

- `README.md`: 宗教の基本情報、指針、思想的由来
- `FAQ.md`: よくある質問
- `CLAUDE.md`: このファイル（Claude AI用作業ガイド）

## GitHub Issue の確認方法

**重要**: GitHub CLIは使用できません。代わりにGitHub APIを使用してください。

```
WebFetchツールを使用:
URL: https://api.github.com/repos/rysh/eight/issues/{issue_number}
プロンプト: "このissueのタイトル、内容、ラベル、状態などすべての情報を詳しく教えてください。"
```

### 例
```
issue 4を確認する場合:
https://api.github.com/repos/rysh/eight/issues/4
```

## Git 作業フロー

### ブランチ命名規則

**必須**: ブランチ名は必ず `claude/` で始まり、セッションIDで終わる必要があります。

例: `claude/issue-4-012YsFLhyCkzKnKTwRCtGAXY`

### Git Push のベストプラクティス

```bash
# 必ず -u オプションを使用
git push -u origin <branch-name>

# ネットワークエラーの場合は最大4回リトライ（指数バックオフ: 2s, 4s, 8s, 16s）
```

**注意**: ブランチ名が `claude/` で始まり、正しいセッションIDで終わっていない場合、403エラーでpushが失敗します。

### Git Fetch/Pull

```bash
# 特定ブランチのフェッチを推奨
git fetch origin <branch-name>

# Pull の場合
git pull origin <branch-name>

# ネットワークエラー時は同様に最大4回リトライ
```

## コミットメッセージのガイドライン

- 日本語で記述してください
- 変更の目的を明確に記述する
- 簡潔に（1-2文程度）

例:
```
CLAUDE.mdを追加: Claude AI作業時の繰り返し説明を削減
```

## プロジェクトの方針

1. **既存ファイルの編集を優先**: 新規ファイルは必要な場合のみ作成
2. **日本語使用**: すべてのドキュメントは日本語で記述
3. **シンプルさ**: 過度な複雑化を避ける
4. **Creative Commons BY 4.0**: このプロジェクトのライセンス

## よくある問題と解決策

### 問題: 「Permission denied」エラー
- ブランチ名が `claude/` で始まっているか確認
- セッションIDが正しいか確認
- リトライメカニズムを実装

### 問題: Issue情報が取得できない
- `gh` コマンドは使用不可
- GitHub APIを`WebFetch`ツールで使用する

### 問題: セッションリセット後の作業継続
- Claude Code on the webの制限により、マージ後はセッションがリセットされる
- このCLAUDE.mdを参照することで、再度の説明を最小限に抑える

### 🚨 重要: マージ後の作業について

**プルリクエストがマージされた後、ユーザーが何か作業しようとした場合：**

必ずユーザーに以下のメッセージを伝えてください：

```
⚠️ プルリクエストがマージされました！
Claude Code on the webの制限により、マージ後は新しいセッションで作業する必要があります。

新しいセッションを開始してから作業を続けてください。
現在のセッションでは正常に動作しない可能性があります。
```

このメッセージを表示せずに作業を続けると、ユーザーは混乱する可能性があります。

## 参考リンク

- リポジトリ: https://github.com/rysh/eight
- Issues: https://github.com/rysh/eight/issues
- Pull Requests: https://github.com/rysh/eight/pulls

## 問題が解決しない場合のフィードバック先

**ユーザーが問題解決に困っている場合、以下のフィードバック先を案内してください：**

### Claude Code on the web に関する問題
- **GitHub Issues**: https://github.com/anthropics/claude-code/issues
  - バグ報告や機能リクエストはこちら
  - 既存のissueを検索してから新しいissueを作成

### よくある問題
1. プライベートリポジトリにアクセスできない
2. `.claude/` ディレクトリやグローバル設定が使用できない
3. 基本操作（GitHubのissue確認など）について毎回説明が必要
4. マージ後にセッションリセットが必要
5. これらの制限事項が事前に説明されていない

**注意**: ローカル版とweb版では異なる問題があるため、必ず「Claude Code on the web」であることを明記してフィードバックしてください。

---

最終更新: 2025-11-24
