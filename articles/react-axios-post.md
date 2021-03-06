--- title: "React axiosを使ってPOSTメソッドにヘッダーをつけてリクエストする"

emoji: "👻" 

type: "tech" 

topics: ["React","axios"] 

published: **false**  ---



## axios

ざっくり説明するとnodeからHTTPリクエストを送るためのライブラリです。
https://www.npmjs.com/package/axios

詳しい説明や使い方は、下記リンクを参照ください。
https://qiita.com/reoisym/items/245e3cdedc194a9f4062

今回は、axiosのなかでも、POSTメソッドにヘッダーをつけてリクエストする方法を紹介します。

## コード

```tsx:sample.tsx
import axios from "axios";


export function HttpAccess(): any {
  //リクエストに付加するヘッダーの定義
  const headers = {
            'Content-Type': 'application/json',
            'any-header': '付加したいヘッダー'
  }

  axios.post(url, data, {headers: headers});

}
```

上記の方法で、POSTメソッドにヘッダーをつけてリクエストすることができます。

参考になれば幸いです！