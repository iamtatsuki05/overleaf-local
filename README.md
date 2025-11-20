# overleaf-local Taskfile 使い方

## 前提
- 作業ディレクトリ: このリポジトリ直下（例: `/Users/tatsuki/src/latex/overleaf-local`）
- `task` コマンドが使えること（未導入なら `brew install go-task` など）

## ユースケース別
- 初回セットアップ + 起動（ビルド含む）
  - `task` もしくは `task up`
- 停止
  - `task toolkit_stop`
- 停止後の起動（再ビルドなし）
  - `task toolkit_start`
- 停止→再起動を一括（必要に応じて）
  - `task toolkit_restart`

## 日本語対応（TeX Live full）導入の流れ
1. コンテナ起動後に TeX Live 更新・scheme-full導入
   - `task toolkit_texlive`
   - 時間がかかるので注意
2. sharelatex コンテナをイメージ化（タグ任意、デフォルト: with-texlive-full）
   - `task toolkit_commit_image [SHARELATEX_TAG=with-texlive-full]`
3. toolkit設定でそのタグを使用するよう置換
   - `task toolkit_patch_compose [SHARELATEX_TAG=with-texlive-full]`
4. 再起動
   - `task toolkit_restart`

## その他
- clone / build を別々に実行したい場合
  - `task clone` / `task build`
- 何かおかしい場合は `task --list` でタスク一覧を確認してください。

## MARKDOWN
NOTE:
- macOS/arm64 環境で公式の sharelatex イメージが x86_64 メインのため、ローカル build 済みの `sharelatex/sharelatex:main` を既定バージョン（6.0.1）にタグ付けする処理を Taskfile に入れ、セムバ以外の version 記載による起動失敗を防ぐため。
