# PUSHERとは



## 概要

PUSHER(https://pusher.com/)

リアルタイムアプリケーションを構築するためのAPIを提供するSaaS

⇒Websocketのコネクションの管理をしてくれる。

![image-20210422142845765](C:\Users\annor\AppData\Roaming\Typora\typora-user-images\image-20210422142845765.png)



![image-20210422142803793](C:\Users\annor\AppData\Roaming\Typora\typora-user-images\image-20210422142803793.png)(コネクションの維持はPUSHERに任せるため、サーバレスアーキテクチャでもWebsocketが利用可能)



## プライス



Freeプランだと、下記を提供している。

- 200,000リクエスト/日
- 最大同時接続数100コネクション

![image-20210422143046659](C:\Users\annor\AppData\Roaming\Typora\typora-user-images\image-20210422143046659.png)

https://pusher.com/channels/pricing



## 実装



ドキュメント⇒https://pusher.com/docs/channels



### アカウント登録

下記にアクセスし、Sign upからアカウント登録を行う。

PUSHER(https://pusher.com/)

![image-20210422142845765](C:\Users\annor\AppData\Roaming\Typora\typora-user-images\image-20210422142845765.png)

ダッシュボードからアプリを作成し、APIキーを取得する。

![スクリーンショット 2021-04-22 143419](C:\Users\annor\Desktop\スクリーンショット 2021-04-22 143419.png)



### サーバ側実装

ライブラリインストール

```
npm i pusher
```



```typescript

    const Pusher = require('pusher');
    
    // pusherオブジェクト作成
    const pusher = new Pusher({
      appId: APP_ID,
      key: PUSHER_API_KEY,
      secret: PUSHER_API_SECRET,
      cluster: PUSHER_API_CLUSTER,
    });
    
    // pusherイベントをトリガー
    // 指定したチャネルとイベント名をsubscribe()している箇所に、pushが到達する。
    pusher.trigger('my-channel', 'my-event', { message: 'hello world' });
```




### クライアント側実装

ライブラリインストール

```
npm i pusher-js
```



```typescript
import Pusher from 'pusher-js';

  // pusherオブジェクト作成
  const pusher = new Pusher(PUSHER_API_KEY, {
    cluster: PUSHER_API_CLUSTER,
  });

  // pushを受け取るためのチャネルを作成。
  const channel = pusher.subscribe('my-channel');

  // 指定したイベント名で作成されたトリガーが実行したとき、pushを受け取る。
  channel.bind('my-event', (data: any) => {
    console.log(data);
  });
```

