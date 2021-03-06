## この記事について
今話題になってるらしいCSSフレームワークの「Tailwindcss」をReactで使ってみるためのまとめ。

##そもそもTailwindって
CSSフレームワークの一つです。
下のGifを見ればわかりやすいと思いますが、要素に対してclassを指定することでスタイルを適用できます。
https://tailwindcss.com/
![screen.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/fc45e921-3a98-0de4-ae6f-3605445134e3.gif)

## 開発環境
- VsCode
- create-react-appした状態
- npm 6.12.1

## インストール手順
###パッケージインストール
対象プロジェクトのpackage.jsonがあるフォルダで下記コマンドを実行。

```
npm install -D tailwindcss@npm:@tailwindcss/postcss7-compat @tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
```

```
npm install postcss-cli autoprefixer --save-dev
or
yarn add postcss-cli autoprefixer --save-dev
```

###styles.css作成
tailwindcssのいろいろをインポートした.cssファイルを作成します。

```styles.css
@tailwind base;

@tailwind components;

@tailwind utilities;
```

###package.jsonにビルド用のスクリプトを作成し実行

```package.json
"scripts": {
    "start": "react-scripts start",
    "build:tailwind":"tailwind build src/styles.css -o src/tailwind.css",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
```

```
npm run-script build:tailwind
```

そうすると、tailwind.cssが作成される。

###buildされたtailwind.cssを任意のファイルでインポート

```index.js
import './tailwind.css';
```

##動作確認
任意のコンポーネントに下記コードを張り付けて、正常にスタイルが適用されてるか確認します。

```App.js
import React from "react";

function App() {
  return (
    <div className="App">
      <div class="max-w-sm rounded overflow-hidden shadow-lg">
        <img
          class="w-full"
          src="https://source.unsplash.com/random/1600x900/"
          alt="Sunset in the mountains"
        ></img>
        <div class="px-6 py-4">
          <div class="font-bold text-xl mb-2">The Coldest Sunset</div>
          <p class="text-gray-700 text-base">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit.
            Voluptatibus quia, nulla! Maiores et perferendis eaque,
            exercitationem praesentium nihil.
          </p>
        </div>
        <div class="px-6 py-4">
          <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">
            #photography
          </span>
          <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2">
            #travel
          </span>
          <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700">
            #winter
          </span>
        </div>
      </div>
    </div>
  );
}

export default App;
```

こんな感じになってたら成功です。
（画像はrandomでunsplashAPIから取ってきてるので変わってるはずです。）
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/502798/61a3e193-9c4a-7e92-12c5-2a6cb657f4a1.png)

##最後に
bootstrapはなんも考えなくても適当にクラスつけてれば、いい感じのスタイルにできてたのに比べて、tailwindcssはしっかりCSS理解してクラスつけないとうまくいかんなーって所感です。
tailwindcss自体もうちょい勉強せんとなーって思いました。

また細かいtaiwindcssの使い方は記事にまとめます。

##参考記事
https://blog.logrocket.com/create-react-app-and-tailwindcss/
https://qiita.com/zzzzz/items/68461080515ec1012980