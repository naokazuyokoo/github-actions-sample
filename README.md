# GitHub Actions Sample Theme

WordPress テーマを GitHub Actions でサーバーへデプロイする最小サンプルです。

`main` または `master` への push、または GitHub Actions の手動実行で、本番サーバーのテーマディレクトリへ `rsync` します。

## 含まれるもの

- `.github/workflows/deploy-production.yml`: GitHub Actions から SSH / rsync でデプロイ
- `bootstrap.sh`: リポジトリ作成、SSH 鍵準備、Secrets 登録の補助スクリプト

## 使い方

```bash
cd wp-content/themes/wp-github-actions-sample
chmod +x ./bootstrap.sh
./bootstrap.sh
```

対話に従って入力後、`git push` で workflow が起動します。

## 注意

- workflow は `rsync --delete` を使うため、デプロイ先パスは必ずテーマディレクトリを指定してください。
- `PROD_PATH` は `/path/to/wordpress/wp-content/themes/theme-name` のように、特定テーマディレクトリを指定してください。
- デプロイ時に削除・上書きされるファイルは `wp-content/.deploy-backups/theme-name/<timestamp>-<run-id>-<attempt>` に退避されます。
- バックアップは既定で最新 5 世代を保持します。変更したい場合は GitHub Actions Secret `PROD_BACKUP_KEEP` に保持数を設定してください。
- 手動実行時は `dry_run` を有効にすると、ファイルを変更せずに `rsync --dry-run` で確認できます。
- SSH 秘密鍵や接続情報は GitHub Actions Secrets に登録し、リポジトリには含めません。
- `.deploy.env` はローカル設定ファイルです。Git には含めません。
