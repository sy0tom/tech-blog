# React + Vite で GitHub Pages にブログを公開する

React + Vite で GitHub Pages にブログを公開する方法を紹介します。

## 目次

1. [セットアップ](#セットアップ)

## セットアップ

- NodeJSのインストール

  ```sh
  > brew install nodenv
  > exec $SHELL -l
  > nodenv install --list
  > nodenv install 20.5.1
  > nodenv global 20.5.1
  ```

- パッケージマネージャのインストール

  ```sh
  > brew install pnpm
  > pnpm setup
  ```

- プロジェクトの作成

  ```sh
  > pnpm create vite
    ✔️ Project name: <project name>
    ✔️ Select a framework: React
    ✔️ Select a variant: TypeScript

  > cd <project name>
  > pnpm i
  ```

- 起動時のポートを変更する場合は`vite.config.ts`を以下のように修正する

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

- プロジェクトの実行

  ```sh
  > pnpm dev
    VITE v5.2.0  ready in 85 ms

  ➜  Local:   http://localhost:8080/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
  ```
