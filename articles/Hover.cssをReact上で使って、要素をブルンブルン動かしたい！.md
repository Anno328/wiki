--- title: "Hover.cssをReact上で使って、要素をブルンブルン動かしたい！"

emoji: "😳" 

type: "tech" 

topics: ["React","css","Hover.css"] 

published: **false**  ---



## はじめに

タイトル通り、Reactで生成した要素にホバーアクションを実装してブルンブルン動かしたくなったのでやってみました。

## 開発環境
VsCode
npm 6.12.1

## セットアップ
###Hover.cssのインストール
何パターンか方法があるらしいですが、今回はGithubからソースファイルを引っ張ってきてローカルに保存する方法でやってきます。

https://github.com/IanLunn/Hover
上記サイトのcssフォルダ配下にある`hover-min.css`をダウンロードして、ローカルの適当なフォルダに配置します。

###hover-min.cssを上位のスタイルファイルでインポート
プロジェクトの上位のスタイルファイルで、保存した`hover-min.css`をimportします。

```
@import url("hover-min.css");
```

###classをつける
これでHover.cssを使える状態になったので、ブルンブルンさせたい要素に対してクラスをつけてあげます。

```
    <div className="hvr-grow">
```

## 動作確認
サーバを起動して確認してみましょう。
![screen.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/73d17605-0c6b-da1e-c862-678affc72e88.gif)

## 終わりに
楽ちんですね。