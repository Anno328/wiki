# はじめに
create-react-appでアプリを作成すると、なんだかいつの間にか設定されているwebpackが何者なのか気になったのでまとめてみました。

# この記事で得られること
webpackがどんな役割でどんな機能なのかわかる。
webpackを使うと何がうれしいのかわかる。
webpackってなんだっけ？て時に概要が5分でわかる。

# webpack概要
ウェブコンテンツに必要なファイル(モジュール)を、1つのファイルにまとめる(バンドル)モジュールバンドラー
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/43bdb8ef-bd1b-3e98-b506-b45dd7bc9c3a.png)


# webpackを使うと何がうれしい？
## ファイル取得のリクエスト数を削減できる
ファイルが1つになることでブラウザが読み込むファイル数が減り、ファイル取得に伴うリクエスト回数も減ることで、Webページの表示速度を向上させることができます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/2690631e-3fea-a389-0ab7-7cb78e35274c.png)
ファイルが複数必要だと、各リクエストごとにオーバヘッドがかかってしまいます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/3cc43209-04c2-8ab5-fdb9-78e94fa1090f.png)
ファイルが1つであれば、1回分のオーバヘッドで済みます。

##  モジュール方式で開発できる
モジュールが複数のファイルに分割されている場合でも、バンドルする際に依存関係も考慮してバンドルするため、開発者は依存関係を意識せずモジュールを利用できるようになります。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/a82db087-ff82-e51e-3f52-745a823dde64.png)


# webpackの機能
## ローダー
webpackはデフォルトではjsファイルとjsonファイルを対象としてます。
ローダーを使うことで、css等の他の拡張子のファイルも扱うことができるようになります。

## コード圧縮
実行モードがproductionの場合、ブラウザのコンテンツロード時間を短くするために、バンドル時にファイルを圧縮してくれます。
開発時はブラウザ上でデバッグをするために実行モードをdevelopmentに設定し、静的コンテンツを公開する際は実行モードをproductionに設定しましょう。


## サーバ構築
webpack-dev-serverというライブラリを使用すると、ウェブサーバを構築することができます。
下記コマンドでサーバを起動できます。

```
webpack serve
```

## ファイル変更検知
ファイルを変更するたびにビルドを実行するのは面倒です。
サーバを起動する際に --watchオプションを付けることで、ファイルの変更を検知し、自動的にビルドを行ってくれます。

# webpackの設定
webpackの設定にはwebpack.config.jsを利用します。
最小構成であれば、下記のようになります。

```webpack.config.js
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
  },
};
```

各プロパティについて説明します。

## mode
webpackの実行モードを指定します。
developmentを指定すると、ソースマップを有効にでき、
productionを指定すると、コードの圧縮を行います。

https://webpack.js.org/configuration/mode/

## entry
バンドルの構築を開始する場所を指定します。
webpackはここで指定されたファイルから、依存関係を解決していきます。

https://webpack.js.org/concepts/#entry

## output
バンドルしたファイルをどこに生成するのか(path)と、
バンドル結果ファイル名(filename)を指定します。

https://webpack.js.org/concepts/#output

## loader
ローダを使ってcss等をバンドルするには、下記のように設定します。

先に必要なローダをインストールします。

```
npm i -D style-loader css-loader
```
style-loaderは<link>タグにCSSを展開するライブラリです。
css-loaderはCSSをJSにバンドルするライブラリです。


```webpack.config.js
module.exports = {
  module: {
    rules: [{
      test: /\.css/,
      use: [
        'style-loader',
        { loader: 'css-loader', options: {url: false}},
      ],
    },]
  }
};
```

rulesプロパティ内で、対象ファイル(test)と、使用するローダ(use)を指定します。

https://webpack.js.org/concepts/#loaders

# (おまけ)実装例

## webpack * babel
必要なライブラリのインストール

```
npm install -D babel-loader @babel/core @babel/preset-env
```

```webpack.config.js
module.exports = {
  entry: "./src/index.js",
  module: {
    rules: [
      {
        test: /\.js$/,
        use: [
          {
            loader: "babel-loader",
            options: {
              presets: [
                "@babel/preset-env",
              ],
            },
          },
        ],
      },
    ],
  },
  target: ["web", "es5"],
};
```

>※プリセット「@babel/preset-env」は「ECMAScript 5/6/7 compatibility tables」に基づきターゲットブラウザを指定できたりとさまざまな機能が提供されています。たとえば、ターゲットブラウザがSafari 10だけでよければ、ES5まで落として変換する必要はなく、ES2015(ES6)をターゲットにすれば良いということになります。
>webpack 5からtarget: ["web", "es5"]プロパティーの設定が必要になりました。これを設定しないとIE 11でバンドル後のJavaScriptファイルが動作しなくなります（アロー関数などES2015の記法がIE11で認識しないため、実行時エラーとなります）。
>https://ics.media/entry/16028/

## webpack * typescript
必要なライブラリのインストール

```
npm install -D typescript ts-loader
```

```tsconfig.json
{
  "compilerOptions": {
    "sourceMap": true,
    "target": "es5",
    "module": "es2015"
  }
}
```

>とくにmoduleにes2015を指定するのが重要です。これを指定しないと、TypeScriptコードのimport文とexport文がコンパイラによってCommonJSとして変換されるため、webpackによるTree Shaking（未使用のimportを静的解析によって振り落とす機能）のメリットが得られません。Tree Shakingの効果を得るためには明示的にES Modulesをコンパイルオプションで指定します。
>https://ics.media/entry/16329/


```webpack.config.js
module.exports = {
  entry: './src/main.ts',
  module: {
    rules: [
      {
        test: /\.ts$/,
        use: 'ts-loader',
      },
    ],
  },
  resolve: {
    extensions: [
      '.ts', '.js',
    ],
  },
};
```

resolveはバンドル対象のファイルの拡張子を表します。
これを指定してあげることで、import時にファイル名に拡張子を記載する必要がなくなります。


# 参考
https://webpack.js.org/
https://zenn.dev/yuri/books/4391b9280f823061932c/viewer/772ea55a74179ab617d1
https://ics.media/entry/12140/
https://ics.media/entry/16028/
https://ics.media/entry/16329/
https://qiita.com/soarflat/items/28bf799f7e0335b68186