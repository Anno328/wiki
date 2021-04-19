# Server-Sent Events



## 概要

 Server-Sent Eventsとは

⇒Web サーバーがリアルタイムのデータをクライアントにプッシュするできるようにする標準





## 仕組み

サーバからイベントを受けとれるようにする組み込みのクラス `EventSource` を用いる。

`EventSource`リファレンス：https://developer.mozilla.org/ja/docs/Web/API/EventSource



### Websocketとの違い

| `WebSocket`                                                  | `EventSource`                          |
| :----------------------------------------------------------- | :------------------------------------- |
| 双方向: クライアントとサーバ両方がメッセージのやり取りをすることができます | 単方向: サーバのみがデータを送信します |
| バリナリデータとテキストデータ                               | テキストのみ                           |
| WebSocket プロトコル                                         | 通常の HTTP                            |

>`EventSource` は `WebSocket` ほど強力ではない、サーバと通信する方法です。なぜこれを使う必要があるのでしょう？主たる理由はより簡単だからです。多くのアプリケーションでは、`WebSocket` は少し強力すぎます。サーバからデータストリームを受信する必要のある、例えばチャットメッセージやマーケットプレイスなどが `EventSource` の得意なところです。また、`WebSocket` では手動で何らかの実装が必要な自動再接続もサポートしています。その上、新しいプロトコルではなく通常の HTTP です。
>
>https://ja.javascript.info/server-sent-events



## 実装

## クライアント側



```javascript
    // クライアントとサーバー間の通信チャネルを初期化するオブジェクトを生成
    this.eventSource = new EventSource("https://another-site.com/events");

    componentDidMount() {
      // onmessageでサーバからの通信を待ち受ける
      this.eventSource.onmessage = e =>
        // e.dataの中にサーバからのデータが含まれる。
        this.updateFlightState(JSON.parse(e.data));
    }

    // サーバからのデータに対して、何らかの処理をするメソッド
    updateFlightState(flightState) {
      let newData = this.state.data.map(item => {
        if (item.flight === flightState.flight) {
          item.state = flightState.state;
        }
        return item;
      });
      this.setState(Object.assign({}, { data: newData }));
    }

    // サーバとの接続を閉じる
    eventSource.close();


```





## サーバ側



```javascript
      // responseにヘッダを追加して、このセッションが常時接続であることをクライアントに伝える
      response.writeHead(200, {
        Connection: "keep-alive",
        "Content-Type": "text/event-stream",
        "Cache-Control": "no-cache",
        "Access-Control-Allow-Origin": "*"
      });

      // responseにデータを追加 
      response.write('data: {"flight": "I768", "state": "landing"}');
```





IEは未対応



## 参考

https://developer.mozilla.org/ja/docs/Web/API/EventSource

https://developer.mozilla.org/ja/docs/Web/API/Server-sent_events/Using_server-sent_events

https://ja.javascript.info/server-sent-events

https://auth0.com/blog/jp-developing-real-time-web-applications-with-server-sent-events/