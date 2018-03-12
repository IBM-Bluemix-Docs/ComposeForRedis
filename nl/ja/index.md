---

copyright:
  years: 2016,2018
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.composeForRedis}} の概要
{: #about-compose-for-redis}

Redis は、オープン・ソースでインメモリー型のキー/値ストアです。 Redis には値として、単純なストリング、ハッシュ、リスト、セットを格納したり、強力なビットマップ、hyperloglog、地理空間インデックスを格納したりできます。 Redis は、アプリケーション・キャッシュまたは高速応答用データ・ストアに向いています。 {{site.data.keyword.composeForRedis_full}} で提供する構成は、高可用性とディスク上での永続性のために事前調整されており、追加のセキュリティー機能によってすべてがロックダウンされます。
{:shortdesc}

**注:** 2016 年 9 月 14 日より前にプロビジョンされた、現在もアクティブな Compose サービス・インスタンスは引き続き使用可能で、[https://www.compose.com/](https://www.compose.com) から直接アクセスできます。 その時点以降にプロビジョンされた Compose サービス・インスタンスは、{{site.data.keyword.cloud}} アカウント内で直接アクセスして使用されます。

## {{site.data.keyword.composeForRedis}} サービス・インスタンスの作成

{{site.data.keyword.composeForRedis}} サービスは、{{site.data.keyword.cloud_notm}} カタログの [{{site.data.keyword.composeForRedis}} ページ](https://console.{DomainName}/catalog/services/compose-for-redis/)から作成できます。

サービス名、およびサービスをプロビジョンする地域、組織、スペースを選択します。 **「データベースのバージョンの選択 (Select a database version)」**フィールドを使用して、データベースの使用できるバージョンを選択できます。

TLS /SSL 暗号化を選択するためのドロップダウンがあります。暗号化は、デフォルトでは **True** に設定されています。**False** を選択すると、サービスが暗号化なしでプロビジョンされます。これは、ドライバーが暗号化を処理できない場合に使用できますが、暗号化されないトラフィックにはリスクが潜んでいる可能性があることを意識しておく必要があります。 

{{site.data.keyword.composeForRedis}} インスタンスをプロビジョンするときには、*標準*プランか*エンタープライズ*・プランを選択できます。 *エンタープライズ*・プランでは、{{site.data.keyword.composeForRedis}} インスタンスを利用可能な {{site.data.keyword.composeEnterprise}} クラスターにプロビジョンできます。 {{site.data.keyword.composeEnterprise}} は、企業コンプライアンスで要求されるセキュリティーと分離を提供し、専用ネットワーキングを使用してデプロイ済みデータベースのパフォーマンスを確保します。 詳しくは、[Compose Enterprise 文書](../ComposeEnterprise/index.html)を参照してください。

## {{site.data.keyword.composeForRedis}} の管理

サービス・ダッシュボードからサービスを管理できます。 ダッシュボードには {{site.data.keyword.cloud_notm}} Compose データベースとそれへの接続方法に関する情報が示されます。 また、以下の操作を行うこともできます。
- バックアップを管理する
- サービスに割り振るリソースを増やす
- サービス・パスワードを変更する
- ホワイトリストを使用してデータベースへのアクセスを制限する。 
詳しくは、[設定](./dashboard-settings.html)を参照してください。

## {{site.data.keyword.composeForRedis}} への接続

サービスに接続するには、サービスと一緒に作成された資格情報を使用するか、サービス・ダッシュボードの*「概要」*タブに表示される接続ストリングとコマンド・ラインを使用します。

## {{site.data.keyword.composeForRedis}} への {{site.data.keyword.cloud_notm}} アプリケーションの接続

{{site.data.keyword.cloud_notm}} アプリケーションをサービスに接続するには、サービスと一緒に作成された資格情報を使用します。 {{site.data.keyword.cloud_notm}} アプリケーションを {{site.data.keyword.composeForRedis}} サービスに接続する方法については、[{{site.data.keyword.cloud_notm}} アプリケーションの接続](./connecting-bluemix-app.html)を参照してください。

## {{site.data.keyword.cloud_notm}}

 外からの {{site.data.keyword.composeForRedis}} への接続{{site.data.keyword.composeForRedis}} に {{site.data.keyword.cloud_notm}} の外部から接続するには、提供された接続ストリングまたはコマンド・ラインを使用します。 接続方法については、[外部アプリケーションの接続](./connecting-external.html)を参照してください。
