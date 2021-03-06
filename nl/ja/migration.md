---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-20"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# {{site.data.keyword.Bluemix_notm}} へのデータのマイグレーション
{: #migration}

ローカル・ネットワーク上またはオブジェクト・ストア内 (Amazon S3 または {{site.data.keyword.Bluemix_notm}} Object Storage) にある、区切り文字で区切られた形式 (CSV または TXT) のデータ・ファイルから {{site.data.keyword.dashdblong}} にデータをロードできます。 オンプレミス・システムからデータをマイグレーションすることもできます。
{: shortdesc}

## オブジェクト・ストアからのデータのロード
{: #cos}

Amazon S3 からデータをロードするには、以下のいずれかの方法を選択します。
  * {{site.data.keyword.dashdbshort_notm}} Web コンソール。 **「ロード (Load)」 > 「Amazon S3」**。 
  * 外部のテーブルから直接。 次に、SQL ステートメントの例を示します。

    ```
    INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
      (CCSID 1208 s3('s3.amazonaws.com', 
      '<S3-access-key-ID>',
      '<S3-secret-access-key>', 
      '<my_bucket>'
         )
      )      
    ```

外部表を使用して、{{site.data.keyword.Bluemix_notm}} Object Storage から直接データをロードする場合、以下のサンプル SQL ステートメントを使用できます。

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**注:** {{site.data.keyword.Bluemix_notm}} Object Storage の場合、HMAC 資格情報を作成するために、新規サービス資格情報を作成する際、*「インラインの構成パラメーターの追加」*フィールドに {"HMAC:true"} を指定してください。

{{site.data.keyword.Bluemix_notm}} Object Storage からのデータのロードに関するガイド付きデモについては、[{{site.data.keyword.dashdblong}} guided demo: Explore data loading ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:new_window} を参照してください。

## オンプレミス・システムからのデータのマイグレーション
{: #onprem}

オンプレミス・システムからデータをマイグレーションするには、データ・セットのサイズに応じて、以下のいずれかの方式を選択します。
* 25 TB 未満のデータ: [IBM Lift](#lift)
* 25 TB 以上のデータ: [{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift は、表 1 にリストされている各種データ・ソースから {{site.data.keyword.Bluemix_notm}} にデータをマイグレーションするときに無料で使用できるアプリケーションです。 

| {{site.data.keyword.Bluemix_notm}} 上のターゲット DB | データ・ソース |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle データベース |
|                              | Microsoft SQL Server |
|                              | CSV ファイル・フォーマット |
{: caption="表 1. マイグレーションのデータ・ソース" caption-side="top"}

Lift のダウンロードとインストールについては、[Download Lift ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://lift.ng.bluemix.net/#download){:new_window} を参照してください。

Lift を使用してデータを {{site.data.keyword.Bluemix_notm}} にマイグレーションする方法に関するステップバイステップの説明については、[{{site.data.keyword.dashdblong}} へのデータ・マイグレーション ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://lift.ng.bluemix.net/#docs){:new_window}を参照してください。

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service (MDMS) を使用して、大規模な (約 25 TB 以上) IBM PureData Systems for Analytics (Netezza) データベースから、{{site.data.keyword.Bluemix_notm}} 上の完全管理された {{site.data.keyword.dashdblong}} データベースにデータをマイグレーションできます。

MDMS は、テラバイト単位からペタバイト単位までのデータを {{site.data.keyword.Bluemix_notm}} に物理的に転送するための高速かつシンプルで安全な方法を提供します。 MDMS は、120 TB の使用可能な記憶容量を備えたモバイル・ストレージ・デバイスです。 このデバイスによって、高いコスト、長い転送時間、セキュリティー上の懸念など、転送に関わる一般的な課題を単一サービスですべて克服できます。

![Mass Data Migration Service デバイスの表示](images/mdms.svg)

MDMS デバイスについて詳しくは、以下を参照してください。 
- [{{site.data.keyword.Bluemix_notm}} 大量データ・マイグレーションの概説](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}。

MDMS デバイスを使用した IBM PureData System for Analytics (Netezza) データベースから {{site.data.keyword.dashdblong}} データベースへのデータのマイグレーションについて詳しくは、以下を参照してください。 
- [IBM PureData System for Analytics (Netezza) からのマイグレーション](/docs/services/Db2whc/pda_db2whc_mdms.html){:new_window}。

## チュートリアル: Migrating data from on-premises relational databases
{: #tutorial}

このチュートリアルでは、オンプレミスのリレーショナル・データベースから、ビジネス・アナリティクス・アプリケーション用の {{site.data.keyword.dashdbshort_notm}} へのデータのマイグレーション方法を示します。 

[Hybrid data warehousing with {{site.data.keyword.dashdbshort_notm}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:new_window}

