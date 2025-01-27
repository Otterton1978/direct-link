---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# IBM Cloud Direct Link Connect のアンケート
{: #ibm-cloud-direct-link-connect-questionnaire}

{{site.data.keyword.cloud}} Direct Link Connect をご注文いただき、ありがとうございます。 ご注文の最後に、追加情報を収集させてください。 アンケート・プロセス中、いつでもエンジニアとお話いただけます。 アンケートは、完了後、IBM のクラウド設計エンジニアリング・チームによって確認され、実装のために特別なネットワーク・サービスにエスカレートされます。

## 以下について確認して同意してください。

1. 各 Direct Link 接続に固有の注文が必要です。 複数の接続が必要な場合は、接続ごとに別個の Direct Link の注文をオープンしてください。

2. Direct Link Connect サービスに関する料金には、IBM Cloud インフラストラクチャーでのサービス終端のコストが含まれます。

 * インフラストラクチャー・サービスは事前に課金され、注文が受け入られると開始します。ただし、IBM Cloud Direct Link の性質のため、Direct Link サービスの課金は、IBM Cloud との Border Gateway Protocol (BGP) セッションの開始時、またはサービス・キーがお客様に提供されてから 30 日後に開始します。

 * 請求処理が停止するのは、以下の後です。
   * お客様が回線の削除を要求し、**かつ**
   * Connect プロバイダーまたはネットワーク・サービス・プロバイダーで回線がプロビジョン解除される。
  * 詳しくは、リンク [https://www.ibm.com/support/customer/zz/en/selectcountrylang.html](https://www.ibm.com/support/customer/zz/en/selectcountrylang.html) にある「Cloud Services Agreement」の**セクション 5『Charges』**を参照してください。 例えば、米国内のお客様の場合は、[このクラウド・サービス契約文書](https://www.ibm.com/support/customer/csol/contractexplorer/cloud/csa/us-en)をご覧いただけます。
  * あるいは、Direct Link サービスがオフになって機能しなくなることが通知された場合に、お客様に対する請求処理が停止することがあります。

3. Direct Link サービスを注文することで、お客様のリモート・ネットワークから PoP (Point of Presence) サービスへの到達、および Exchange プロバイダーに到達するために PoP 施設内で必要な相互接続に関連したすべての料金は、お客様の負担となります。 また、お客様 (またはお客様のプロバイダー) は、IBM Cloud へのバーチャル・サーキットの購入も負担することになります。 ご使用のプロバイダーで PoP にルーターまたはその他のデバイスが物理的に配置されている必要がある場合、その機器の配置に関するコストも負担することになります。 ネットワークまたは PoP プロバイダーが Direct Link Connect に到達でき、関連コストの総額を見積もってもらえることを確認してください。

4. IBM Cloud は、ネットワーク POP 内にあるお客様の機器はコロケーションしません。 ご使用のプロバイダーと連携して、IBM Cloud PoP が存在しているのと同じ施設に何らかの装置を配置する必要があるかどうかを判別する必要があります。

5. Direct Link Exchange サービスは、リンクと、その終端になる IBM Cloud ルーターの両方が Single Point of Failure (SPOF) になるような方法で提供されます。 Direct Link Connect サービスを介して冗長性を実現する場合、リンクの終端を 2 つの別個の IBM Cloud ネットワーク PoP にするか、2 次ルーターのある Direct Link Connect ロケーションへの 2 つの接続を注文する必要があります。

6. IBM Cloud サービス・ネットワークは、リモート・ネットワークから直接アクセス可能ではありません。 将来これが変更された場合、通知いたします。

7. IBM Cloud は、お客様が IBM Cloud バックボーンを介してリモート・サイト間でトラフィックをバックホールすることを許可しません。 Direct Link Connect 製品は、ご使用のリモート・ネットワークが IBM Cloud インフラストラクチャーと非公開通信できるようにすることを目的としています。

8. 回線が Direct Link Connect PoP に到達したことを確認した後、ご使用の Connect プロバイダーで注文し、関連するすべての情報を Cloud Exchange プロバイダーおよび IBM Cloud に提供する必要があります。 Equinix プロバイダーの場合、標準的なデプロイメント時間は数時間かかることがあります。 IBM Cloud Direct Link Connect オファリングの標準的なデプロイメント時間は、完了までに 5 日から 10 日かかります。

9. IBM Cloud Direct Link Connect では、IBM Cloud ネットワーク側で VRF (Virtual Routing and Forwarding) インスタンスを使用する必要があります。 これにより、お客様はリモート・ネットワークで使用するための独自のリモート IP アドレスを定義できます。ただし、10.x.x.x ネットワークを使用できる場合でも、IBM Cloud 内のホストおよび IBM Cloud サービス・ネットワーク (10.0.0.0/14、10.198.0.0/15、および 10.200.0.0/14) とオーバーラップすることはできないことに留意してください。 VRF へのアカウントの移行には、各 VLAN が新規構成にマイグレーションされる間、プライベート・ネットワークを短時間停止する必要があります。特別なネットワーク・サービス・チームがお客様と連携して、このアクティビティーの期間を定義いたします。 特別なネットワーク・サービス・チームは、通常、CST (米国中部標準時) で月曜日から金曜日の 8 時から 5 時まで支援が可能です。 この期間外のアクティベーション・アクティビティーについては、チケットを介して要求し、エンジニアの支援が可能かどうかの事前承認が必要です。

10. VRF は IBM Cloud SSL、PPTP、および IPSEC VPN の各サービスと互換性があるわけではありません。 代替手段として、サーバーの管理のために Direct Link 自体を使用したり、さまざまなタイプの VPN を使用して構成可能な独自の VPN ソリューション (Vyatta など) を実行したりすることができます。 VRF へのマイグレーション後、SSL VPN は通常、アクセス対象のコンピュートと同じ DC ロケーションに対する VPN 接続が確立されると機能しますが、グローバルなアクセスは許可されません。

11. IBM Cloud Direct Link Connect では、お客様のリモート・ネットワークへの経路を実装するために BGP を必要とします。Direct Link サービスがデプロイ済みの場合、IBM Cloud は、アカウントに割り当てられているすべてのプライベート・サブネットを通知します。IBM Cloud は、お客様のリモート BGP ピアへの通知に対して、カスタム・フィルター、AS-Path プリベンド、およびカスタム・ローカル・プリファレンスを実装することはありません。IBM Cloud は、IBM Cloud で受信した通知に対してフィルターを実装することはありません。お客様が、お客様の終端ルーターから IBM Cloud との間の通知を適切に管理する必要があります。

## その他の質問

* **IBM Cloud Direct Link Connect 接続に関する_お客様の場所_ の料金を認知しており、受け入れますか?**

* **IBM Cloud は、リモート・ネットワークを IBM Cloud プライベート・ネットワークに通知するように BGP を構成するために、プライベート ASN をお客様に割り当てます。 これを受け入れることができますか? あるいは、独自のパブリック ASN を使用しますか?**

* **IBM Cloud への冗長接続をセットアップするために、ECMP とともに BGP MultiPath を構成する必要がありますか?** 

    _「はい」の場合は、もう一方の接続のチケット ID を記載してください。 チケット番号: ____________ (ECMP は、同じ IBM Cloud XCR 上の 2 つのセッションでのみプロビジョンできるので注意してください。  ECMP が必要な場合、両方の Direct Link の宛先を同じルーター上にする必要があります)。

* **ローカル・ルーティング・アクセスが必要ですか、それともグローバル・ルーティング・アクセスが必要ですか?**

    _ローカル・ルーティングを選択するお客様は、Direct Link を注文した PoP からサービスが提供されるデータ・センター間でのみトラフィックを渡すことができます。 Direct Link を注文した PoP の外部でトラフィックを渡す必要があるお客様は、グローバル・ルーティング・オプションを追加する必要があります。_

* **_お客様の場所_ の月額料金および下記の超過料金を含む、グローバル・ルーティングの料金に同意しますか?**

    _ローカル・ルーティングには、PoP に直接接続されたすべてのデータ・センターへのアクセスが含まれ、無制限の発着信トラフィックが提供されます。 グローバル・ルーティングは、すべての IBM Cloud のデータ・センターをグローバルに含むようにアクセスを拡張します。 帯域幅は、サービスでトラフィックに課金できる場合に課金されます。 帯域幅の課金が発生した場合、以下の表に示すように、お客様の市場の料金に基づいて月次に課金されます。_


### グローバル・ルーティングの料金

| 着信グローバル・ルーティング | 発信グローバル・ルーティング |
|---|---|
| 無料 | 1、2、または 5 Gbps 回線 - 10 TB の無料帯域幅 |
| 無料 | 10 Gbps 回線 - 50 TB の無料帯域幅 |


| 帯域幅超過料金 |
|---|
| 市場 1: $0.05/GB |
| 市場 2: $0.10/GB |
| 市場 3: $0.15/GB |
