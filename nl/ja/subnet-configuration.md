---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-02-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# IBM Cloud Direct Link の構成
{ #configure-ibm-cloud-direct-link}

IBM Cloud Direct Link 接続が確立されたら、この資料に示されている手順に従ってサブネットを構成し、IBM Cloud と相互作用できるようにします。

一般に、IBM Cloud Direct Link 接続を機能させるには、基本的なネットワーク構成ステップをいくつか実行し、その後で BGP (Border Gateway Protocol) をセットアップする必要があります。 セットアップ・プロセス時に、IBM 技術員がお客様と協力して、ネットワークに必要な VRF (Virtual Routing Function) 機能を使用できるようにします。

## 基本ネットワーク構成

1. 標準 RFC1918 専用アドレス・スペースを使用して、リモート・ネットワークを定義します。 
 * 新しい環境の場合は、10.0.0.0/8 スペースを使用**しない**ことをお勧めします。 
 * 既存の環境で 10.0.0.0/8 を使用している場合は、より詳細なアセスメントを取得して、{{site.data.keyword.BluSoftlayer_notm}} サービス・ネットワーク、またはアカウントに既に割り当てられているネットワークとの競合がないようにすることをお勧めします。

2. {{site.data.keyword.BluSoftlayer_notm}} のスタッフが、各接続に /31 または /30 を割り当て、{{site.data.keyword.BluSoftlayer_notm}} 相互接続ルーター (XCR) インフラストラクチャーにインターフェース IP アドレスを構成します。  

3. 提供された IP アドレスを使用して、顧客側エッジ・ルーター (CER) 上のインターフェースを構成します。これは、{{site.data.keyword.BluSoftlayer_notm}} XCR IP を {{site.data.keyword.BluSoftlayer_notm}} 宛てのすべてのトラフィックのネクスト・ホップとして使用するだけです。 

4. リターン・トラフィックの場合、{{site.data.keyword.BluSoftlayer_notm}} は、BGP を介して通知されたとおり、リモート・ネットワークを宛先とするすべてのトラフィックのネクスト・ホップとして、割り当てられた CER IP を使用します。

## BGP の構成

ご使用の環境とルート情報を交換するには、{{site.data.keyword.BluSoftlayer_notm}} では BGP が構成されている必要があります。  

1. **ASN**: {{site.data.keyword.BluSoftlayer_notm}} は、それぞれのお客様が使用するためのプライベート ASN を割り当てます。 代わりに、独自のパブリック ASN を使用することもできます。 発注時に、どちらを使用するかを指定できます。 割り当てられたプライベート ASN は、実装プロセス中に提供されます。

2. **VRF**: {{site.data.keyword.BluSoftlayer_notm}} は、VRF を使用して、お客様のアカウントに割り当てられた特定のプライベート・サブネットを通知します。  お客様は、{{site.data.keyword.BluSoftlayer_notm}} プライベート・ネットワークから到達できるようにしたいリモート・ネットワークを通知する必要があります。 以下のネットワークは、フィルター操作で除外され、受け入れられません。0.0.0.0、10.0.0.0/14、10.198.0.0/15、10.200.0.0/14、169.254.0.0/16、224.0.0.0/4。 IBM Cloud ネットワークとの間の通知の管理は、お客様の責任で行っていただきます。 (VRF についての詳細は、次のセクションで説明します。)

3. **ECMP**: サポートされるロケーションで冗長性を構築することを選択したお客様の場合、{{site.data.keyword.BluSoftlayer_notm}} は ECMP (equal-cost multipath) の実装をサポートし、2 つのリンク間のロード・バランシングと冗長性を提供します。 この ECMP のセットアップは、注文時に指定してください。

## IBM Cloud Direct Link の BGP 仕様 

BGP 仕様は以下のとおりです。

上記のセクションに記載されているように、BGP は、Direct Link 経由のルーティングを管理するために必須です。 Direct Link を注文したアカウントは、VRF 環境にマイグレーションされます。

**VLANS および VRF に関する注意:**
 * VRF 環境では、アカウント間の VLAN スパンニングは許可されません。 
 * IPSEC VPN サービスは制限されます。 
 
**注:** VRF は SSL や PPTP VPN アクセスを防ぎませんが、動作が変化します。 VRF がない場合、1 つの VPN 接続で、アカウント上のすべてのサーバーを確認するのに十分です。 VRF がある場合、VPN に関連付けられている市場のリソースのみにアクセスできます。 したがって、DAL VPN に接続した場合は、DAL サーバーにしか接続できません。

IBM Cloud ASN は、パブリック・サービスおよびプライベート・サービスの場合、**13884** です。 
 * 注文する際のお客様のデフォルト ASN は **64999** ですが、お客様の要求に応じてデフォルトを変更できます。 
 * オプションとして、4201000000 から 4201064511 の 4 バイトのプライベート ASN をサポートできます。
 * IP VPN などのレイヤー 3 サービスとともに Direct Link Connect を使用する場合、IBM Cloud は Direct Link Connect プロバイダーの ASN を使用して BGP を確立します。
   
**IP 割り当てに対する厳密な制限:**
 * 10.x.x.x ネットワークを使用した場合でも、IBM Cloud 内のホストや IBM Cloud サービス・ネットワーク (`10.0.0.0/14`、`10.198.0.0/15`、および  `10.200.0.0/14` を占めるもの) とのオーバーラップを作成できません。  

 * 範囲 `169.254.0.0/16` および `224.0.0.0/4` は、フェデレーテッド・システムで許可されず、IBM サーバーによって拒否されます。

**推奨、デフォルト、および制限:**

 * トンネリング (つまり、GRE) がサポートされ、IP オーバーラップが問題になった場合に推奨されます。
 * BGP タイマーのデフォルトは `Keepalive:30`、`Holdtime:60` です。
 * 認証は、デフォルトでは有効になっていません。
 * BGP BFD は、デフォルトでは有効になっていません。
 * 最大受信 (お客様からプロバイダーへの) プレフィックス制限は、1 VRF 当たり 200 です。

## 冗長性と多様性

IBM Cloud Direct Link は多様性を提供します。お客様は BGP スキーマを通じて冗長性を実装する責任があります。

冗長性のために ECMP を選択した場合、両方の BGP セッションは同じ XCR に存在する必要があるため、ルーターの多様性は無くなり、ルーターに障害が発生した場合にリスクにさらされます。 レイヤー 3 の冗長性は得られますが、ルーターの多様性は失われます。

## VRF の使用に関する詳細

IBM Cloud Direct Link ソリューションを使用するすべてのアカウントは、VRF にマイグレーションする必要があります。 お客様は、VRF を使用して、自己定義されたリモート・ネットワークへの使用可能な経路を通知します。 この構成は、{{site.data.keyword.BluSoftlayer_notm}} ネットワーク上で自己定義 IP アドレスを使用することを許可するものではありません。

VRF へのマイグレーションは、セットアップ・プロセス中に実行されます。 このために、短い停止時間 (複数の VLAN またはロケーションを持つ大規模なアカウントの場合は最大 30 分) が必要になります。バックエンド・ネットワーク VLAN は、VRF に移行されている間、相互の接続が失われます。 VRF のマイグレーションのスケジュールは、実装担当の技術員とともに決定します。

VRF では、アカウントの「VLAN スパンニング」オプション (すべてのアカウント間 VLAN スパンニング機能を含む) が除去されます。これは、トラフィックを管理するためにゲートウェイ・アプライアンスが導入されていない限り、すべての VLAN が通信できるためです。 VRF では {{site.data.keyword.BluSoftlayer_notm}} VPN サービスを使用する機能も制限されます。VRF は {{site.data.keyword.BluSoftlayer_notm}} SSL、PPTP、および IPSec VPN の各サービスと互換性がないためです。   

代替方法の 1 つは、IBM Cloud Direct Link オファリング自体を使用してサーバーを管理するか、別のタイプの VPN を使用して構成できる独自の VPN ソリューション (Vyatta など) を実行することです。 VRF へのマイグレーション後、計算 VM が稼働しているデータ・センターと同じ場所に VPN 接続が行われた場合、通常 SSL VPN は機能しますが、グローバルなアクセスは許可しません。

## Direct Link での BYOIP および NAT の使用
IBM Cloud  Direct Link は、プライベート・ネットワークに BYOIP を提供しません。 そのため、{{site.data.keyword.BluSoftlayer_notm}} が割り当てたものではない宛先 IP アドレスを持つトラフィックはドロップされます。 ただし、お客様は、GRE、IPSec、または VXLAN を使用して、リモート・ネットワークと {{site.data.keyword.BluSoftlayer_notm}} ネットワーク間のトラフィックをカプセル化することができます。  

最も一般的には、BYOIP 環境は、ネットワーク・ゲートウェイ (Vyatta) または VMWare NSX デプロイメントの有効範囲内に実装されます。 この構成では、お客様は {{site.data.keyword.BluSoftlayer_notm}} サイドの任意の望ましい IP スペースを使用し、トンネル経由でルーティングしてリモート・ネットワークに戻すことができます。 この構成は、{{site.data.keyword.BluSoftlayer_notm}} から独立して、お客様が管理してサポートする必要があります。 さらに、この構成では、{{site.data.keyword.BluSoftlayer_notm}} がサービスに使用中の 10.x.x.x ブロックをお客様が割り当てた場合、{{site.data.keyword.BluSoftlayer_notm}} サービス・ネットワークの接続を切断するおそれがあります。 

また、このソリューションでは、{{site.data.keyword.BluSoftlayer_notm}} サービス・ネットワークおよびリモート・ネットワークへの接続を必要としている各ホストに 2 つの IP アドレスが割り当てられている必要があります。1 つは IBM 10.x.x.x ブロックから割り当てられ、もう 1 つはリモート・ネットワークから割り当てられていなければなりません。 静的ルートをホスト上にセットアップし、トラフィックが適切にルーティングされるようにする必要があります。 {{site.data.keyword.BluSoftlayer_notm}} ホスト (BYOIP) 上に直接 IP スペースを割り当て、それを本質的に {{site.data.keyword.BluSoftlayer_notm}} ネットワーク上にルーティング可能にすることはできません。 この機能を実装する唯一の方法は前述のとおりですが、これは {{site.data.keyword.BluSoftlayer_notm}} によってサポートされていません。

あるいは、お客様は、リモート・エッジ・ルーター上に構成された NAT テーブルで、使用するリモート・ネットワーク・ブロックを割り当てることがよくあります。 この構成では、お客様は、両方のネットワークに必要な変更を制限できると同時に、両方のネットワークと互換性のあるネットワーク・アドレス・スペースにトラフィックを変換することができます。


