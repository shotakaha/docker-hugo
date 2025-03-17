# docker-hugo

docker compose hugo

## イメージ

- GitLab: registry.gitlab.com/pages/hugo/hugo_extended:latest
- Docker Hub: https://hub.docker.com/r/hugomods/hugo

## 手順

- Hugoの開発サーバーをDockerコンテナで実行する
- コンテンツはローカルの`./hugo/`ディレクトリをマウントする
- ライブリロードを有効にする
- テーマの設定や変更もすぐに反映する

## ディレクトリ構造

```console
docker-hugo
|-- README.md
|-- LICENSE.md
|-- compose.yaml
|-- hugo/
```

## compose.yaml

- [compose.yaml](./compose.yaml)を参照
- Hugoの公式イメージは存在しないので、コミュニティ版イメージである[hugomods/hugo](https://hub.docker.com/r/hugomods/hugo)を利用する
- タグの内容は[ドキュメント](https://docker.hugomods.com/)を確認して、適切なタグを選択する
  - `extended`かどうか、`node`を含むかどうか、などいろいろなバリエーションがある

## 新規サイトを作成

```console
// hugo new site .
$ docker compose run --rm hugo new site .
```

- `hugo new site .`をコンテナ内で実行する
- `working_dir: /workspace`に設定したため`コンテナ:/workspace/`に必要なコンテンツ一式が生成される
- `volumes:`で`./hugo:/workspace`と紐づけているため、`コンテナ:/workspace/`に生成されたファイルは`ローカル:./hugo/`の中にも生成される
- `./hugo/`の中身はとりあえずGitに追加してOK
