# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## リポジトリ概要

このリポジトリはJenkins Declarative Pipeline構文を使用したGroovyで書かれた実験的なJenkinsパイプライン設定を含んでいます。トリガージョブとコア処理ジョブを分離するパターンを実証しています。

## アーキテクチャ

Jenkinsパイプラインはトリガー・コアパターンで構成されています：

- **トリガーパイプライン** (`Pipeline/core-and-dependent-trigger-jobs/triggers/Jenkinsfile`): 変更を監視し、適切なパラメータでコアパイプラインを開始する軽量なトリガー
- **コアパイプライン** (`Pipeline/core-and-dependent-trigger-jobs/core/Jenkinsfile`): 実際の処理ロジックを含み、手動実行、API経由、またはアップストリームトリガーでのみ実行可能

### 主要な設計パターン

- **パラメータ受け渡し**: トリガーパイプラインがコアパイプラインにパラメータ（`TARGET_BRANCH`, `BUILD_TYPE`, `RUN_TESTS`）を渡す
- **手動実行制御**: コアパイプラインは`when`条件を使用して、手動またはAPIトリガーのみに実行を制限
- **パイプライン連携**: トリガーパイプラインは`build`ステップを使用して`wait: true`でコアパイプラインを呼び出す

## パイプライン構造

```
Pipeline/
└── core-and-dependent-trigger-jobs/
    ├── core/
    │   └── Jenkinsfile          # メイン処理パイプライン
    └── triggers/
        └── Jenkinsfile          # トリガーパイプライン
```

## Jenkinsパイプラインの操作

- Jenkinsパイプラインは`Jenkinsfile`ファイル内でGroovy構文を使用して定義
- コアパイプラインは3つの主要パラメータを受け取る：
  - `TARGET_BRANCH` (デフォルト: 'main')
  - `BUILD_TYPE` (デフォルト: 'release')
  - `RUN_TESTS` (デフォルト: true)
- トリガー条件はJenkinsの`when`ブロックと`triggeredBy`条件で管理

## 言語とコメント

コードベースにはパイプラインの動作と設定を説明する日本語コメントが含まれています。