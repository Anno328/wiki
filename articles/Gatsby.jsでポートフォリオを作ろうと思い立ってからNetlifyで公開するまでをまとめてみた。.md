# 背景
今流行っているGatyby.jsで自身のポートフォリオを作ってみたいなぁと思い立ち、
実際に作ってみたので、その流れをまとめてみました。

# この記事で得られるもの

- Gatsby.jsを最小構成でセットアップする方法

- GithubからNetlifyへのデプロイ方法

- ポートフォリオの画面イメージを練るプロセス



# 最終的な成果物
最終的に下記のポートフォリオを作成し、Netlifyで公開しました。
https://annos-portfolio.netlify.app/
![pic.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/e385cb92-b132-f255-657e-85e8be2b2c28.gif)

ソースコードは下記で公開してます。
https://github.com/Anno328/Portfolio

# 環境/前提
![<LABEL>-<MESSAGE>](https://img.shields.io/badge/node-14.15.0-<COLOR>) ![<LABEL>-<MESSAGE>](https://img.shields.io/badge/npm-6.14.8-<COLOR>) ![<LABEL>-<MESSAGE>](https://img.shields.io/badge/gatsby-2.26.1-<COLOR>)

- 上記ライブラリがインストールされていること。

- GitHub上にリポジトリがあること。

- Netlifyのアカウントがあること。

# 手順
## ポートフォリオの画面イメージを練る
デザインについては全くの素人なので、他人様が公開してくださっているポートフォリオをもとに画面イメージを練っていきます。
下記サイトが参考になりました。
https://codeburst.io/10-awesome-web-developer-portfolios-d266b32e6154

で、練った画面イメージは下記のようになりました。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/9fb61896-b478-3027-f28e-be7d013e03aa.png)
(青字でHeaderとか言ってるのは、コンポーネントです。)

## コンポーネント設計
次にコンポーネント設計をしていきます。
画面イメージができたので、画面をセクションに区切って、コンポーネントとして切り分けていきます。
そして、切り分けたコンポーネントの親子関係を図示していきます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/260b2032-e533-c66b-c5e9-0753576aefc1.png)
(手書きで超適当なのは大目に見てください・・)

## Gatsbyセットアップ
ここからGatybyのセットアップに入っていきます。

そもそもGatsby.jsってなんぞや？って方は下記をご覧ください。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/53a9d08c-967a-8e93-ae24-f3346db982f0.png)
https://www.gatsbyjs.com/

>Gatsby.jsはReactで作られた静的サイトジェネレーターです。内部的にGraphQLを用いてデータを取得し、markdownからHTMLを生成、などの処理を簡単に行うことができます。
>https://qiita.com/hppRC/items/00739eaf9ae7fc95c1ca

下記の公式チュートリアルに沿ってセットアップしていきます。
(公式チュートリアルは親切にもnpmやらgitやらのインストールから解説してくれてます。。インストール済みの方はすっ飛ばしてOKです。)
https://www.gatsbyjs.com/docs/tutorial/part-zero/#create-a-gatsby-site

### 1)npm initでアプリケーションの初期処理を行う。
任意のフォルダで下記を実施し、アプリケーションに必要な設定ファイル(package.json)を作成していきます。

```
npm init
```

コマンド実行後に指定が必要な各種項目については、下記サイトが参考になります。
https://techacademy.jp/magazine/16151

こだわりがなければエンターを押し続けてもらえればOKです。

### 2)gatsby-cliをインストールする。
1)で作成したフォルダに移動し、下記コマンドを実行することでgatsby-cliをインストールすることができます。

```
npm install -g gatsby-cli
```

gatsby-cliとは、Gatsby.jsアプリを作成したり、操作するために必要なライブラリです。
これをインストールすることで、gatsbyコマンドが使えるようになります。

### 3)Gatsbyサイトを作成する。
下記コマンドを実行し、Gatsbyサイトを作成します。
今回はチュートリアルに沿って、hello-worldスタータキットを用いて作成します。

```
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

### 4)サーバを起動して、ページが表示されることを確認する。
3)で作成しhello-worldフォルダに移動し、サーバを起動するコマンドをたたきます。

```
cd hello-world
gatsby develop
```

これでサーバが立ち上がりました。

実際に確認するために、ブラウザから下記URLにアクセスします。
http://localhost:8000/

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/747ffd6e-9ff6-5aaf-be2c-3411dc456cd6.png)

上記画面が表示されればOKです。
セットアップは完了です！

## 実装

ここからは実装です。

このトピックについては本記事で詳しく説明することはしないのですが、基本的にはコンポーネント設計をもとに作成していきます。

コードは下記で公開しているので、よかったら参照してみてください。
https://github.com/Anno328/Portfolio

## GitHubのリポジトリへコードをpush
ここまでで出来上がったソースコードをGitHubの任意のリポジトリにpushします。

リポジトリがない方は、下記を参考に作成しましょう。
https://qiita.com/sodaihirai/items/caf8d39d314fa53db4db


## Netlifyへデプロイ
準備ができたので、GitHubとNetlifyを連携させて、デプロイしていきます。

そもそもNetlifyってなんぞや？って方は下記をご覧ください。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/36abe5ce-1b26-7bb6-6127-e5cbfebed203.png)
https://www.netlify.com/

>静的コンテンツのホスティングサービス。
>使い勝手の良いUIと、簡単な手順で公開までできるのがめっちゃよい。
>GitHub / GitLab / Bitbucket のリポジトリと連携して、pushやmergeなどがあったらNetlifyCIがビルドやデプロイをしてくれる感じになっている。
>https://qiita.com/sugo/items/2ee64887d682b0dae635

### Netlifyにログインする。
下記にアクセスし、ログインします。
https://www.netlify.com/

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/332651bd-7312-229e-736f-d7d0a7826e03.png)

### GitHubと連携
次に、「New site from Git」を押下し、GitHubの任意のリポジトリと連携します。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/46d916c1-ffc1-dfb7-7787-3ef6039b167d.png)

Create a new site で「GitHub」を選択します。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/de907b25-8d04-5734-5b9d-74a6230f879d.png)

任意のリポジトリを選択します。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/bd9c286b-cd95-e7c5-7204-6dd34048fda4.png)

ビルド対象のブランチ・ビルドコマンド・ビルド結果のパスを入力し、「Deploy site」を押下します。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/8c863544-e3af-8028-4a37-c157050f7c9a.png)
これでGitHubとの連携は完了です！

ビルドが完了したら、下記URLよりデプロイしたサイトを確認することができます。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/ebf1f538-568f-7c85-3563-933e59c78f00.png)


参考：https://qiita.com/suin/items/743fe6252ad8af425c5e#%E6%BA%96%E5%82%992-netlify%E3%81%A7%E3%82%B5%E3%82%A4%E3%83%88%E3%82%92%E4%BD%9C%E3%82%8B

# まとめ
Gatsby.jsでポートフォリオを作ろうと思い立ってからNetlifyで公開するまでの手順
1. 他人様のポートフォリオを参考にし、画面イメージを練る
2. 画面イメージをもとに、コンポーネント設計をする。
3. 設計をもとに、実装する。
4. 出来上がったソースコードをGitHubにpushする。
5. GitHubとNetlifyを連携し、Netlifyにデプロイする。


# 所感
Gatsby.jsで作ってみたはいいものの、あまりGatsbyであることのメリットを活かせていない気がしています。。
(imageとかもGatsbyのプラグインじゃなくてimgタグで埋めこんでしまっている。)
そもそも静的にサイトをGenerateしてないしね！

もはやGatsbyというか、ただのReactベースになってしまったので、もっとプラグインとか活用してしけたらいいなと思います。


やっぱりブログとか記事を増やしていきたいサービスに向いてるのかなと思いました。
ただサーバ勝手に作ってくれたり、静的コンテンツいい感じにまとめてくれたり、その辺の恩恵にあやかれるのは強いですね。


あとNetlifyへのデプロイが楽すぎて感動しました...！
地味に特定ブランチにpushした時の自動デプロイトリガーもいつの間にか設定してあったので、今度ちゃんと調べてみようと思います。