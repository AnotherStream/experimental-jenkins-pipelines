# Experimental Jenkins Pipelines

このリポジトリは、動作確認のための試験的なJenkinsのパイプラインをまとめるための個人的なリポジトリです。

## 概要

Jenkins Declarative Pipeline構文を使用したGroovyで書かれた実験的なパイプライン設定を含んでいます。様々なパイプラインパターンやJenkins機能の検証を目的としています。

## パイプライン構成

### Core and Dependent Trigger Jobs

`Pipeline/core-and-dependent-trigger-jobs/`

コアな処理を実走したジョブと、パラメタなどを指定してそれをトリガー実行するジョブで分離したパターンのパイプラインです。

- **triggers/Jenkinsfile**: SCMポーリングによりコアパイプラインをトリガーする軽量なジョブ
- **core/Jenkinsfile**: 実際の処理ロジックを含むメインパイプライン（手動実行またはAPI経由のみ）

#### 主要な特徴

- パラメータ受け渡し（`TARGET_BRANCH`, `BUILD_TYPE`, `RUN_TESTS`）
- 実行条件の制御（`when`ブロック使用）
- SCMポーリングによる自動トリガー
- 手動実行制御

## ファイル構成

```
Pipeline/
└── core-and-dependent-trigger-jobs/
    ├── core/
    │   └── Jenkinsfile          # メイン処理パイプライン
    └── triggers/
        └── Jenkinsfile          # トリガーパイプライン
```

## 使用方法

1. Jenkinsにパイプラインジョブを作成
2. 該当するJenkinsfileを指定
3. 必要に応じてパラメータを設定
4. トリガー条件に応じて実行

## 注意事項

- このリポジトリのパイプラインは実験的なものです
- 本番環境での使用前に十分な検証を行ってください
- 各パイプラインには日本語コメントが含まれています