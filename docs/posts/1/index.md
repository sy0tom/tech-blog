# React + Vite で GitHub Pages にブログを公開する

React + Vite で GitHub Pages にブログを公開する方法を紹介します。

## 目次

1. [セットアップ](#セットアップ)
1. [GitHub Pages への公開](#github-pagesへの公開)
    1. [ブランチのディレクトリ指定での公開方法](#ブランチのディレクトリ指定での公開方法)
    1. [GitHub Actionsでの公開方法](#github-actionsでの公開方法)

## セットアップ

1. NodeJSのインストール

    ```sh
    > brew install nodenv
    > exec $SHELL -l
    > nodenv install --list
    > nodenv install 20.5.1
    > nodenv global 20.5.1
    ```

1. パッケージマネージャのインストール

    ```sh
    > brew install pnpm
    > pnpm setup
    ```

1. プロジェクトの作成

    ```sh
    > pnpm create vite
      ✔️ Project name: <project name>
      ✔️ Select a framework: React
      ✔️ Select a variant: TypeScript

    > cd <project name>
    > pnpm i
    ```

1. 起動時のポートを変更する場合は`vite.config.ts`を以下のように修正する

    ```diff
      import { defineConfig } from 'vite';
      import react from '@vitejs/plugin-react';

      // <https://vitejs.dev/config/>
      export default defineConfig({
    +   server: {
    +   port: <任意のポート番号>,
    + },
      plugins: [react()],
      });
    ```

1. プロジェクトの実行

    ```sh
    > pnpm dev
      VITE v5.2.0  ready in 85 ms

    ➜  Local:   http://localhost:8080/
    ➜  Network: use --host to expose
    ➜  press h + enter to show help
    ```

## GitHub Pagesへの公開

GitHub Pagesへの公開はブランチのディレクトリ指定とGitHub Actionsによるデプロイの2通りある。  
今回は静的ホスティングのビルドやデータの作成をローカルで行うことが多いため、  
ブランチのディレクトリ指定で公開する。(GitHub Actionsでの公開方法も[後述](#)する)  

### ブランチのディレクトリ指定での公開方法

1. 公開用ディレクトリの作成
GitHub Pagesに公開するには`<root dir>`または`docs`にindex.htmlが存在する必要がある。  
今回はビルド時に`dist`ディレクトリをコピーして`docs`ディレクトリを作成する。

    ```diff
      "scripts": {
        "dev": "vite",
        "build": "tsc && vite build",
    +   "pages": "rm -rf docs && cp -r dist docs",
        "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
        "preview": "vite preview"
      },
    ```

1. ビルド

    ```sh
    > pnpm build
    > pnpm pages
    ```

1. 