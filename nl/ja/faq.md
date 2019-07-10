---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-31"

keywords: FAQ, faqs, limit, resource, vNIC, VSI, PGW, console, VRF, bandwidth, COS, egress, load balancer

subcollection: vpc-on-classic

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}
{:faq: data-hd-content-type='faq'}


# FAQ
{: #faqs}

## VPC を他の IBM Cloud ワークロードに接続できますか?  
{: #faq-0}
{:faq}

はい。各地域の 1 つの VPC から {{site.data.keyword.cloud}} クラシック・インフラストラクチャーへのアクセスをセットアップできます。詳しくは、[クラシック・インフラストラクチャーへのアクセスのセットアップ](/docs/vpc-on-classic?topic=vpc-on-classic-setting-up-access-to-your-classic-infrastructure-from-vpc)を参照してください。

## VPC 名の文字数の上限はいくつですか。
{: #faq-1}
{:faq}

現在、上限は 100 文字です。 この上限を超えると、内部エラー・メッセージが表示される場合があります。

## いずれかの VPC リソース名の先頭に数字を使用できますか。
{: #faq-2}
{:faq}

いいえ。名前に数字を含めることはできますが、先頭は英字でなければなりません。

## 名前に使用できる文字について制限はありますか。
{: #faq-3}
{:faq}

はい。UI では、連続する二重ダッシュ、下線、およびピリオドを VSI 名の一部として使用することは禁止されています。

## 浮動 IP のみを使用して、サブネットなしで VSI を作成できますか。
{: #faq-9}
{:faq}

いいえ。

## VSI を複数の VPC に接続できますか。
{: #faq-10}
{:faq}

いいえ。

## VPC 内でサブネットを作成した後に、そのサブネットのサイズを変更できますか。
{: #faq-11}
{:faq}

いいえ。

## VPC から COS へのトラフィックについて、出口帯域幅の料金は発生しますか。
{: #faq-17}
{:faq}

ADN エンドポイントを使用して VPC から COS に接続している場合は、出口帯域幅の料金は発生しませんが、この場合でも API 呼び出しの料金は適用されます。

 ## VPC 用の VPN をセットアップする際にサブネットを指定する必要があるのはなぜですか。また、何を指定すればよいですか。
{: #faq-16}
{:faq}

VPN ゲートウェイをセットアップする際は、サブネットを指定する必要があります。そうすることで、その VPN ゲートウェイは VPN サービスに必要な IP アドレスを取得できます。 サブネットを指定することで、VPN トラフィックの処理方法を継続的に制御できるとともに、VPN を利用するリソースにより近い場所を指定する柔軟性が得られます。 このようにして、待ち時間を短縮してパフォーマンスを高めることができます。

## 自身のロード・バランサー・インスタンスがデプロイされる場所をどのようにして知ることができますか。
{: #faq-18}
{:faq}

選択されたサブネットによって、VPC ロード・バランサーがデプロイされる場所が決定されます。 VPC ロード・バランサーはリージョンのリソースです。 最適な方法は、特定のリージョンで複数の異なるゾーンから複数のサブネットを選択することで、冗長性を高めることです。


## VPC 内で浮動 IP を割り当てるときに、お客様は VSI の vNIC を指定する必要がある、というのは正しいですか。
{: #faq-4}
{:faq}

はい。具体的には、それはサーバーの 1 次ネットワーク・インターフェースである必要があります。

ただし、ネットワーキング領域で API にアドレス・リソースを追加した場合は、インターフェースではなくそのアドレスに対する浮動 IP の関連付けを変更することは十分にあり得ます。

## VPC 内の仮想サーバー・インスタンス上の vNIC に浮動 IP とプライベート IP の両方を割り当てることはできますか。
{: #faq-5}
{:faq}
 
はい。

## VPC 用の IBM Cloud コンソール UI では、各サブネットをパブリック・ゲートウェイ (PGW) に接続するか PGW から切り離すための「切り替えスイッチ」が用意されています。誰が PGW を作成しますか。 お客様が UI でサブネットを PGW に接続しようとするときに、PGW は使用可能な状態になっていますか。
{: #faq-6}
{:faq}

PGW は API を通じて明示的に作成される必要があります。API を使用するには、サブネットが特定のパブリック・ゲートウェイに明示的に関連付けられている必要があるからです。

## 例えば、VPC 内の VSI1 が vNIC1 のみを備えており、vNIC1 はサブネット 1 に接続されているとします。 サブネット 1 はパブリック・ゲートウェイ (PGW) に接続されています。 この場合でも、お客様は VSI1 に浮動 IP を割り当てることはできますか。
{: #faq-7}
{:faq}

はい。パブリック・ゲートウェイに接続されたサブネット上にサーバーを配置できるとともに、そのサーバーに浮動 IP を割り当てることもできます。 VSI への浮動 IP の割り当ては、サブネットに接続されたパブリック・ゲートウェイが存在するかどうかには関係ありません。VSI に割り当てられた浮動 IP は、サブネットに接続されたパブリック・ゲートウェイより優先されます。

## 現在使用している VPC 内では、VSI1 は vNIC1 と vNIC2 という 2 つの vNIC を備えています。 これら 2 つの vNIC を同じサブネットに接続できますか。
{: #faq-8}
{:faq}
 
はい。同じサーバー上の複数のネットワーク・インターフェースを同じサブネットに接続することは制限されていません。 ただし、単一 VSI 上の複数の NIC はサポートされていません。

## 1 つの VPC についてゾーンあたり 1 つのパブリック・ゲートウェイしか存在してはいけないという制限は、どのようにして強制されますか。
{: #faq-13}
{: faq}

この制限は VPC API によって強制されます。

## PGW の作成時に、浮動 IP を手動で予約する必要がありますか。それとも浮動 IP はシステム側で自動的に予約されますか。 すべての浮動 IP を照会したときに、その浮動 IP は表示されますか。
{: #faq-12}
{: #faq}

既存の浮動 IP が指定されていない場合は、API によってパブリック・ゲートウェイとともに浮動 IP が自動的に作成されます。そして、その浮動 IP は照会時のリストに表示されます。


## VRF によって、ユーザーの他のネットワーキング機能とユーザーのサブネットはどのような影響を受けますか。
{: #faq-14}
{:faq}

VLAN および VRF に関する注意事項:

* VRF 環境では、アカウント間の VLAN スパンニングは許可されません。
* IPSec VPN サービスは制限されます。

VRF は SSL や PPTP VPN アクセスを防ぎませんが、動作が変化します。VRF がない場合、1 つの VPN 接続で、アカウント上のすべてのサーバーを確認するのに十分です。 VRF がある場合、VPN に関連付けられている市場のリソースのみにアクセスできます。 したがって、DAL VPN に接続した場合は、DAL サーバーにしか接続できません。
{: note}

## `instance-network-interface-floating-ip-add` サブコマンドを VPC 内で使用するための正しい方法はどのようなものですか。 浮動 IP アドレスを事前に作成または割り当てますか。
{: #faq-15}
{:faq}

 まず浮動 IP を割り当ててから、インターフェースの浮動 IP の `add` コマンドで浮動 IP アドレスを指定する必要があります。

 例: `ibmcloud is floating-ip-reserve FLOATING_IP_NAME (--zone ZONE | --nic NIC_ID)`。 ゾーンを指定します。