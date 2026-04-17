# GitHub Actions Sample Theme

WordPress テーマを GitHub Actions でサーバーへデプロイする最小サンプルです。

## 含まれるもの

- `.github/workflows/deploy-production.yml`: push でデプロイ
- `bootstrap.sh`: リポジトリ作成・Secrets 登録の補助スクリプト

## 使い方

```bash
cd wp-content/themes/github-actions-sample
chmod +x ./bootstrap.sh
./bootstrap.sh
```

対話に従って入力後、`git push` で workflow が起動します。
