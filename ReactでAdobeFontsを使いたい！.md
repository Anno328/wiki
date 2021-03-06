## はじめに
ReactでAdobeFontsを使うためにまとめました。
最終的にこんな感じになります。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/1fdf3c74-2e2b-fffd-2559-6df7ea7683b5.png)

###そもそもAdobeFontsって？
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/d2e1f213-03ea-744f-04df-fc428bef52c7.png)
https://fonts.adobe.com/

豊富なフォントの中からお気に入りのフォントをサクッと探して、手軽に適用できる素晴らしいWebフォントサービスです。


## 開発環境
VsCode
npm 6.12.1

## セットアップ
###Adobeアカウント作成
https://fonts.adobe.com/
上記サイトへアクセスして、アカウントを作成しましょう。

###AdobeFontsからお気に入りのフォントを見つけて、プロジェクトに追加する
次に、お気に入りのフォントを見つけましょう。
見つけたら、下画像にマークしてあるコードアイコンを押します。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/71263cda-9431-cc81-d9b5-327e2e00a01c.png)

ウィンドウが出てくるので、プロジェクトを新規作成し、保存ボタンを押下しましょう。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/fff5b320-3e7a-93f5-f6dc-d8efd350de36.png)

すると、Webサイトからフォントを読み込むためのLinkタグとCssが表示されます。
これでAdobeFonts側の準備は完了です。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/0402e801-589e-ba4b-6376-bba585914425.png)

###Reactプロジェクトからフォントを読み込み、適用する。
先ほど確認したLinkタグをコンポーネントの`return()`内に配置します。

```ShopPage.js
import React from "react";
import "./ShopPage.css";

export function ShopPage() {
  return (
    <div className="ShopPage">
      <link rel="stylesheet" href="https://use.typekit.net/wrq6syh.css"></link>
      <div className="top-title-background w-screen bg-red-800 text-white p-4">
        <div className="flex">
          <div className="w-1/2">
            <p className="-mb-8">Shop</p>
            <p className="-mb-8">Sample</p>
            <p className="-mb-8">Page</p>
          </div>
          <div className="discription w-1/2 h-auto">
            <p>some discription some discription some discription</p>
            <p>some discription some discription some discription</p>
            <p>some discription some discription some discription</p>
            <p>some discription some discription some discription</p>
            <p>some discription some discription some discription</p>
            <p>some discription some discription some discription</p>
            <p>some discription some discription some discription</p>
          </div>
        </div>
      </div>
      <div className="intro">
        <h1>Introduction</h1>
      </div>
    </div>
  );
}
```

次にCssを適用します。

```ShopPage.css
.top-title-background {
  height: 25rem;
  font-family: bungee, sans-serif;
  font-weight: 400;
  font-style: normal;
  font-size: 6rem;
}

.discription {
    font-family: fira-sans,sans-serif;
    font-weight: 400;
    font-style: normal;
    font-size: 1.2rem;
}

body{
    background-color: #e7e7b8;
}

h1{
  font-family: bungee, sans-serif;
  font-weight: 200;
  font-style: normal;
  font-size: 2.5rem;
}
```

## 動作確認
これで完了です。
サーバを立てて確認してみましょう。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/1fdf3c74-2e2b-fffd-2559-6df7ea7683b5.png)
こんな感じになります。

## 終わりに
webフォントってめちゃめちゃ便利ですね。
ただローカルで開発する場合、ネット環境がないとフォントを読み込めないネックですけど。