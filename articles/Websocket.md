# Websocket





## Websocketとは

Webにおいて、サーバとクライアントの双方向通信を実現するためのプロトコル。



詳しくは↓

https://www.slideshare.net/mawarimichi/websocketwebrtc



## Websocketが生まれた背景

従来のWebの用途は、HTTPプロトコルを用いた文書共有が主だった。

この時の処理の流れは、クライアントからサーバに対してリクエストを投げ、そのレスポンスとしてサーバが応答する。(サーバからクライアント方向の通信はリクエストに対するレスポンスしか送信できない。)

![スクリーンショット 2021-04-15 101312](スクリーンショット 2021-04-15 101312.png)



それがSNSやチャットアプリの登場により、「リアルタイムなやり取り」が求められるようになった。

しかし、HTTPプロトコルではサーバからクライアントへの通信をサポートしておらず、ポーリング※という実装で無理くりHTTPプロトコルで実装していた。

※細切れのリクエストを 10 秒間隔などでサーバに送ってレスポンスを促す仕組み。



上記の実装だと、無駄なリクエストが何度も走る・反応時間に限界があるなどの問題が発生する。



その問題に対処するためにWebsocketが生まれた。



Websocketを使うと、↓みたいなサーバ⇒クライアント方向の通信が可能になる。

![スクリーンショット 2021-04-15 101746](スクリーンショット 2021-04-15 101746.png)

## Websocketの仕組み

Websocketは下記の手順で通信を行う。

1. クライアント⇔サーバ間のコネクション確立
2. 確立したコネクション上で双方向でデータをやり取りする



### クライアント⇔サーバ間のコネクション確立

Websocketのコネクション確立は、HTTPプロトコルに相乗りして行われる。



↓Websocketを用いたクライアントからサーバへのリクエスト例

```
GET /resource HTTP/1.1
Host: example.com
Upgrade: websocket
Connection: upgrade
Sec-WebSocket-Version: 13
Sec-WebSocket-Key: E4WSEcseoWr4csPLS2QJHA==
```

WebsocketはHTTPプロトコルに相乗りしたプロトコルのため、HTTPプロトコルとしてみても問題ないようなリクエストになっている。



特徴として、下記のヘッダが追加されている。

- Upgread
- Connection
- Sec-WebSocket-Version
- Sec-Websocket-Key



サーバは上記のヘッダを確認して、通信がWebsocketであることを確認する。



その後、Sec-Websocket-Keyを元に新たな値を生成し、Sec-WebSocket-Acceptヘッダに付与してレスポンスを投げる。

↓Websocketを用いたサーバからクライアントへのレスポンス例

```
HTTP/1.1 101 OK
Upgrade: websocket
Connection: upgrade
Sec-WebSocket-Accept: 7eQChgCtQMnVILefJAO6dK5JwPc=
```



上記のレスポンスをクライアントが受け取ることで、クライアント⇔サーバ間のコネクションが確立される。

そのコネクションを使って、双方向でデータをやり取りできるようになる。



## 実装



### パッケージ検討

nodeでwebsocketを扱うためのライブラリは、代表的なもので下記がある。

- socket.io

- websocket

- (react-use-websocket)



npm trendsで比較。(https://www.npmtrends.com/react-use-websocket-vs-socket.io-vs-websocket)![スクリーンショット 2021-04-15 104344](スクリーンショット 2021-04-15 104344.png)



Downlad数・star数・アップデート頻度的に「socket.io」を使うのが無難っぽい。



### socket.ioを用いた実装

socket.io⇒https://www.npmjs.com/package/socket.io

ドキュメント⇒https://socket.io/docs/v4/

チュートリアル⇒https://github.com/socketio/chat-example

#### クライアント側(React)

```javascript
      var socket = io();

      //サーバへリクエストを送る。
      socket.emit('chat message', input.value);

      //サーバからのemit()をキャッチする。
      socket.on('chat message', function(msg) {
        var item = document.createElement('li');
        item.textContent = msg;
        messages.appendChild(item);
        window.scrollTo(0, document.body.scrollHeight);
      });
```

どのタイミングでコネクション張るかは要検討。

(サーバの指定とかどうやるか調査)



#### サーバ側(Express)

```javascript
// socket.ioを読み込み
const io = require('socket.io')(http);

// socket.ioのミドルウェア。
// クライアントからのsocket.onを用いたリクエストをキャッチする。
io.on('connection', (socket) => {
  // クライアントのsocket.on('chat message',~)をキャッチする。
  socket.on('chat message', msg => {
    //クライアントにpushする。
    io.emit('chat message', msg);
  });
});
```

app.tsとかに記述する？







## 懸念

- 確立されたWebsocketのコネクションがいつまで生きてるか。
- 同時接続可能な限界はどのくらいか。(何かしらの制御が必要？)
- ↓めっちゃたくさんの端末とコネクション張ってる時のサーバ負荷

![スクリーンショット 2021-04-16 100654](スクリーンショット 2021-04-16 100654.png)

https://www.slideshare.net/mawarimichi/websocketwebrtc



**⇒実装して検証してみる。**

　**最悪ポーリングでの対応も検討する。**

(https://developer.mozilla.org/ja/docs/Web/API/WindowOrWorkerGlobalScope/setInterval)



## 参考

https://docs.microsoft.com/ja-jp/archive/msdn-magazine/2012/december/windows-8-networking-windows-8-and-the-websocket-protocol

https://www.silex.jp/blog/wireless/2016/10/websocket.html

https://qiita.com/chihiro/items/9d280704c6eff8603389

https://www.slideshare.net/mawarimichi/websocketwebrtc

https://qiita.com/eri/items/24360c6f75d0a23796c4

https://qiita.com/south37/items/6f92d4268fe676347160

http://wild-data-chase.com/index.php/2019/03/17/post-630/#outline__1