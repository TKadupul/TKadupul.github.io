# Test_blog

date: 2026-04-28

> this is Test_Blog


# This is a Test page! But also something helpful！

# Conferences (and Journals)

中村研のResearch Areaは次のような範囲です:

* Data Communication Network
* Network Architecture
* Network Operation
* Network Virtualization
* Routing
* Network Protocols
* High Performance Networking
* The Internet
* Carrier Networks
* Data Center Networks
* Software Defined Networking and Network Function Virtualization (古い)
* Operating Systems (especially network subsystem)

以上のようなジャンルにおいて、論文を探す時に参考にするために、分野に関
連する国際会議や論文誌に関する情報をまとめます。


なお国際会議には、業界のコンセンサスとしてのランクがあります。最上位
(Tier 1と呼ばれる)のトップ会議は、非常に難易度が高く、採択率も低いです。
一方難しい会議ばかりでは分野が衰退してしまうので、それほど難易度が高く
ない(採択率の高い)会議もたくさんあります。必ずしも難しい会議に通った論
文が良い論文であるというわけではありませんが、既存研究をサーベイしたり、
近年の研究動向を知るためには、まずはトップ会議の方から眺めていくのがお
すすめです。


> [!TIP]
>
> 国際会議と論文誌の違い: 一般的に、国際会議で発表される論文は速報であ
> りまだ途中段階の研究成果、論文誌に掲載される論文は完成されたひとつの
> 研究成果、と言われることがあります。そのため、研究成果として国際会議
> 論文よりも論文誌を重視する姿勢が、理工系の多くの分野では一般的です。
>
> しかしComputer Scienceの分野は発展の速度が速く、査読に1年以上かかる
> 場合のある論文誌よりも、国際会議での発表が重要視される傾向があります。
> そのため国際会議の難易度も高めです。Networkの分野も同様で、論文誌も
> もちろん大事ですが、国際会議の論文を研究成果として重視しています。


## ネットワーク分野に関連する国際学会

**ACM**: Association for Computing Machinery、米国計算機科学学会、もっ
ぱらACMと呼ばれる。分野ごとに複数のSpecial Interest Group (SIG)という
グループに分かれており、SIGごとに国際会議を実施している。ACMで採録され
た論文は[ACM Digital Library](https://dl.acm.org/)に掲載される。ACMが
スポンサードする会議は採択率を一定以下に抑えることが条件となっている場
合があり、比較的難易度の高い会議が多い。


**IEEE**: Institute of Electrical and Electronics Engineers、米国電気
電子学会、だが、もっぱらIEEEと呼ばれる。標準化団体でもある。IEEEの会議
で採択された論文は[IEEE
Xplore](https://ieeexplore.ieee.org/Xplore/home.jsp)に掲載される。ACM
と比べると、難易度の高いものから低いものまで幅広い会議を開催している。


**USENIX**: もともとはUnix User Groupという、UNIX OSのユーザグループ
が起源。実装系や実践系の論文が主で、会議の数は少なく、それぞれの会議は
その分野のトップ会議となっている。


## ネットワーク分野の著名な国際会議

国際会議はどれも基本的に年に一度開催されます。下記に記載されているURL
はある年の会議のURLになっています。検索すれば最新や過去の会議のWeb
Pageも見つかるので、URLは参考までに。

またここに記載されている会議は、ネットワークに関連する分野のごく一部で
す。他にも多くの会議が実施されています。トップ会議ほどトピックが幅広い
傾向があります(Network系ならなんでもOK、OSならなんでもOKなど)。


- **SIGCOMM** https://www.sigcomm.org/events/sigcomm-conference ACMの
  Data Communicationに関するSIGであるSIGCOMMの名前を冠したフラッグシッ
  プ会議。名実ともにネットワーク分野のトップ会議。ざっくり分野の動向を
  知りたいときや、どんな研究トピックが盛り上がっているのかを知りたいと
  きはまずは最近のSIGCOMMのプログラムを眺めてみるとよいです。

- **CoNEXT** https://conferences.sigcomm.org/co-next/2025/#!/home
  SIGCOMMに次ぐ、SIGCOMM系列のトップ会議。

- **NSDI** https://www.usenix.org/conference/nsdi25 USENIX主催のネット
  ワークとシステムに関するトップ会議。USENIX系なので実装に主眼を置いた
  論文がメイン。

- **IMC** https://conferences.sigcomm.org/imc/2024/ ACM SIGCOMM主催の
  インターネットに関する計測系のトップ会議。

- **PAM** https://pam2024.cs.northwestern.edu/ IMCを運営しているコミュ
  ニティが主催している、計測系のTier 2会議。

- **HotNets** https://conferences.sigcomm.org/hotnets/2024/ ACM
  SIGCOMM主催の特殊なワークショップ。この分野における今後の大きな研究
  テーマを提示するような論文が採択される。研究テーマに迷っているときは
  眺めてみるのも一興。

- **HotOS** https://sigops.org/s/conferences/hotos/2025/ HotNetsのOS版。

- **INFOCOM** https://infocom2024.ieee-infocom.org/ IEEEのネットワーク
  系のトップ会議。一度に採録される論文数が多く、玉石混交とも言われる。
  理論系が多め。
  
- **ICNP** https://icnp24.cs.ucr.edu/ IEEEのネットワーク系のトップ会議
  の一つで、International Conference on Network Protocolsの名前の通り、
  Network Protocolにフォーカスした会議。
  
- **NOMS** https://noms2024.ieee-noms.org/ IEEEのネットワーク運用にフォー
  カスしたトップ会議。
  
- **CNSM** https://cnsm-conf.org/2024/ IEEEのネットワーク・サービスの
  管理や運用手法が主眼の会議。

- **OSDI** https://www.usenix.org/conference/osdi25 USENIX主催の
   Operating Systemに関するトップ会議。OSがメインで、OSのネットワーク
   関連のトピックもよく登場する。

- **SOSP** https://sigops.org/s/conferences/sosp/2024/ ACM SIGOPS主催
  のOperating Systemに関するトップ会議。昔はOSDIと隔年開催だったが、最
  近毎年開催になった。

- **EuroSys** https://www.eurosys.org/ SIGOPS主催のOS/System系のトップ会議。
  理論だけでなく実装にも主眼を置いた論文が多い。

- **ASPLOS** https://www.asplos-conference.org/ SIGOPSとSIGPLAN主催の
  トップ会議。OSを中心に、プログラミングにもフォーカスを当てた会議。



### 少し分野外シリーズ

* **ISCA** https://iscaconf.org/isca2025/ HPC系のコンピュータアーキテ
  クチャに関する会議。スパコン系の会議は、スパコンを使った計算(科学計
  算)については分野外ですが、スパコンそのもののOSやNetworkの仕組みや効
  率化に関する論文は参考になる時があります。


* **SC** https://sc24.supercomputing.org/program/proceedings-archives/
  Supercomputing Conferenceの名前の通りスパコンの会議。企業による展示
  会がメインだが、論文投稿と発表もある。展示会場にはSCinetと呼ばれるデモンストレーション
  ネットワークが構築され、HPC系のネットワークを使った[デモが行われる](https://sc24.supercomputing.org/scinet/network-research-exhibition/)。

  
* **VLDB** https://vldb.org/2024/ ACM SIGMOD主催のデータベースに関する
  トップ会議。データベースを載せるOSにまで踏み込んだ研究にときおり出会
  う。
  
* **SIGMETRICS** https://www.sigmetrics.org/sigmetrics2024/ ACM
  SIGMETRICSのトップ会議。SIGMETRICSはコンピュータの性能の評価と計測の
  SIGなので、論文も緻密な実験と評価が参考になるものが多い。たまたま目
  にしたOSの性能計測ネタ論文がSIGMETRICSのものだったりする。



## 論文誌

論文誌は多くの出版社から発行されています。昨今ハゲタカジャーナルといっ
た問題もあるので、基本的にはACMかIEEEの発行する雑誌の論文を参照するこ
と。次いでSpringer、ぎりぎりElsevier、といった感覚です。

ネットワーク分野のトップ論文誌は、[IEEE/ACM Transactions on
Network](https://ieeexplore.ieee.org/xpl/RecentIssue.jsp?punumber=90)
(通称ToN)です。

その他 [IEEE Transactions on Network and Service
Management](https://ieeexplore.ieee.org/xpl/RecentIssue.jsp?punumber=4275028)
(通称TNSM) の論文を見かけることが多いです。


論文を探すときは、基本的には国際会議のプログラムを眺めるか、トピックに
よってGoogle Scholarを検索することがほとんどです。論文誌から論文を探す
ことはめったにないので、あまり気にする必要はありません。質の低い論文を
つかまないために、発行元がACMかIEEE、Springerか、ぎりぎりElsevier、と
いうことだけ意識しておいてください。



## 国内学会

日本国内で関連する学会は次の二つです:

- 情報処理学会 (IPSJ): https://www.ipsj.or.jp/
- 電子情報通信学会 (IEICE): https://www.ieice.org/jpn_r/

それぞれの学会では、分野ごとに「研究会」と呼ばれる小グループを構成して
おり、研究会ごとに、年に4,5回ほど研究発表の場(n月研究会などと呼ばれる)
を開催しています。


ネットワーク分野で関わるのは次の研究会です:

- 情報処理学会 インターネットと運用技術研究会(IOT) https://www.iot.ipsj.or.jp/
- 電子情報通信学会 インターネットアーキテクチャ研究会(IA) https://www.ieice.org/cs/ia/jpn/doku.php


国際会議論文は、論文を投稿し、査読され、査読を通過した論文だけが発表さ
れ電子図書館に掲載される査読付き論文と呼ばれるものです。一方国内研究会
では、論文(予稿と呼ばれる)は投稿しますが、査読はありません。論文を投稿
すれば発表することができます。

EEISを修了するためには、すくなくとも一度は学外で研究成果を発表しなけれ
ばなりません。そういう意味でも国内研究会がもっとも身近な発表の場となり
ます。


