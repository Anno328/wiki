[[_TOC_]]


# 概要
>Azure Data Factory は Azure のクラウド ETL サービスであり、スケールアウト サーバーレス データ統合およびデータ変換を実現します。

![image.png](/.attachments/image-96373ee7-aa6e-42d3-b823-24639a12329f.png)

---

# できること
>オンプレミスにあるデータ ストアやクラウド内のデータ ストアの間でデータをコピーできます。
>生データを大規模な予測と分析情報に変換して処理することができます。 

![image.png](/.attachments/image-b947d225-1f23-4ddd-ac78-838a7fad2944.png)
![image.png](/.attachments/image-9ab2490f-3b26-4324-b7ef-50409d2b2a9f.png)
---

# 料金体系
![image.png](/.attachments/image-72d84dfb-c4f9-4385-bce9-3919a29f06da.png)

従量課金体系。
パイプラインを作成する時、複数のアクティビティを紐づけることで、パイプラインの処理を行ってる。（yamlでいうとタスク）
そのアクティビティの実行回数で料金が決まる。

ちなみに、databaseからstorageへのコピーパイプラインは、1アクティビティだけで動いてる。

# 操作方法
DataFactoryのリソース画面に遷移して、「作成と監視」をクリック
![image.png](/.attachments/image-7535b029-9178-4e2f-b6a2-7d35adc40495.png)

![image.png](/.attachments/image-1c5d7c10-ec17-4002-8480-a3984faca212.png)
上記ページに遷移する。

Copy dataをクリックすると、コピーパイプラインを作成することが出来る。

![image.png](/.attachments/image-3d8556a5-4daf-4441-9326-97a3f19c0953.png)

左ペインの「Source」がコピー元。「Destination」がコピー先。

作成したパイプラインは、初期画面の左ペイン鉛筆タブで確認できる。

![image.png](/.attachments/image-cc7767dc-c7a3-4384-863c-b21fb95bdf15.png)

---

# 参考
https://docs.microsoft.com/ja-jp/azure/data-factory/
https://boxil.jp/mag/a2415/