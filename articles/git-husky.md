--- title: "Gitコマンドの前に特定の処理を挟む方法"

emoji: "🧐" 

type: "tech" 

topics: ["Git","husky"] 

published: **false**  ---



# はじめに

Gitを使ってる際に、コミット前に静的チェックを実施するためにあれこれ調べたので、記事にまとめました。

# この記事で得られること
- Gitコマンドの前に特定の処理を挟む方法

# 最終的な成果物
package.jsonに下記を指定することで、git commit前に静的チェック(lint)を実行できる。

```package.json
  "husky": {
    "hooks": {
      "pre-commit": "npm run lint"
    }
  },
```


# 環境/前提
![<LABEL>-<MESSAGE>](https://img.shields.io/badge/node-14.15.0-<COLOR>) ![<LABEL>-<MESSAGE>](https://img.shields.io/badge/npm-6.14.8-<COLOR>) ![<LABEL>-<MESSAGE>](https://img.shields.io/badge/git-2.29.2-<COLOR>)

- 上記ライブラリがインストールされていること。

# Gitのコマンドを検知する仕組み
最初に、Gitのコマンドを検知する仕組みについて紹介します。

Gitには、Gitの特定アクションを検知してカスタムスクリプトを叩く仕組みである「Gitフック」が提供されています。
この「Gitフック」を利用することで、gitコマンド実行時に処理を割り込ませることができます。

https://git-scm.com/book/ja/v2/Git-のカスタマイズ-Git-フック 

Gフックの例

| フック             | タイミング                                                   |
| :----------------- | :----------------------------------------------------------- |
| pre-commit         | コミットメッセージが入力される前に実行                       |
| prepare-commit-msg | コミットメッセージエディターが起動する直前、デフォルトメッセージが生成された直後に実行 |
| post-commit        | コミットプロセスが全て完了した後                             |

# Gフックを利用したnpmパッケージ
Gフックを利用して、特定処理を挟むサポートをしてくれるパッケージは主に下記があります。
・GHooks(https://github.com/ghooks-org/ghooks)
・Husky(https://github.com/typicode/husky#readme)
・Pre-Commit(https://github.com/observing/pre-commit)

パッケージを比較してみると、Huskyが最も人気がありアップデート頻度も高いので、Huskyで実装していきます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/ce0e5a31-5529-d41b-e5aa-d77851464bed.png)
https://www.npmtrends.com/git-hooks-vs-husky-vs-pre-commit

# 手順
## huskeyのインストール

下記コマンドを実行し、huskeyをインストールする。

```
npm install husky --save-dev
```

参考
https://typicode.github.io/husky/#/?id=manual

## package.jsonに、Gフックとコマンドを設定

下記のように、package.jsonに"husky"の設定を追記すればOKです。

例：git commit前にnpm run lintを実行する。

```package.json
  "husky": {
    "hooks": {
      "pre-commit": "npm run lint"
    }
  },
```


# まとめ

huskyを使えば、簡単に任意のコマンドをGitの特定アクション前後に挟むことができます。