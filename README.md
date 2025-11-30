# devcontainer

[DevContainer][devcontainer] 向けの Docker イメージを GHCR (GitHub Container Registry) に publish するリポジトリ。

## devcontainer-node

NodeJS の利用を目的としたベースイメージ。

### DevContainer 設定例

#### 基本的な設定

```json
{
  "name": "my-project",
  "image": "ghcr.io/akashic-games/devcontainer-node:latest",
  "remoteUser": "node",
  "workspaceMount": "source=${localWorkspaceFolder},target=/workspace,type=bind,consistency=delegated",
  "workspaceFolder": "/workspace"
}
```

#### 環境変数を含む設定

```json
{
  "name": "my-project",
  "image": "ghcr.io/akashic-games/devcontainer-node:latest",
  "remoteUser": "node",
  "workspaceMount": "source=${localWorkspaceFolder},target=/workspace,type=bind,consistency=delegated",
  "workspaceFolder": "/workspace",
  "containerEnv": {
    "TZ": "${localEnv:TZ:Asia/Tokyo}",
    "NODE_ENV": "development"
  },
  "mounts": ["source=${localEnv:HOME}/.npmrc,target=/home/node/.npmrc,type=bind,readonly"]
}
```

## install

```sh
pnpm install
```

## test

```sh
pnpm test
```

## publish

1. [Actions](./actions) タブから `Publish Docker Image` ワークフローを選択します。
2. `Run workflow` ボタンを押して、以下の input を設定のうえ実行してください。
   - `dockerfile_variant`
     - ビルド対象の Dockerfile バリエーション
   - `tag`
     - Docker イメージのタグ
       - 未指定の場合は `YYMMDD`の形式で実行時の日付から自動生成
       - タグ値は `[A-Za-z0-9_.-]+` のみを許可します
   - `latest`
     - latest タグを付与するかどうか

[devcontainer]: https://containers.dev/
