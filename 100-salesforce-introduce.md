# はじめての Salesforce【エンジニア向け】

社内の基幹システムを Salesforce に統合することになったので、業務で得られた知見をアウトプットする。
本記事は Salesforce 超初心者向けとする。

## Salesforce とは

Salesforce は所謂ローコードツールのひとつで、ざっくり言うとプログラマでなくてもWebアプリケーションが作れるというもの。
世界でもっとも売れているクラウド型のSFA/CRM（営業支援・顧客管理）プラットフォームである。
提供するのは米セールスフォース・ドットコム社で、B2B最大手の[SaaS](https://qiita.com/tags/saas)企業。若い企業だが時価総額はトヨタ自動車を超える。[Heroku](https://qiita.com/tags/heroku)を傘下に収める。[Slack](https://qiita.com/tags/slack)を約3兆円で買収[^1]することでも話題になった。
Microsoft365にAzure、AWS等、他のプラットフォームにもサービスコネクタ（連携API）が豊富に用意されているので、業務アプリケーション寄りエンジニア（AE）でなくても名前くらいは聞いたことがあると思う。
![salesforce連携](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/236222/5b512497-5321-a445-70ad-d81b9263cf40.png)

[^1]: [Salesforce が Slack 買収の最終契約を締結](https://slack.com/intl/ja-jp/blog/news/salesforce-signs-definitive-agreement-to-acquire-slack)

## エンジニアからみた Salesforce
エンジニアなら、やはり開発言語は気になるところ。
**Java** を易しくしたような`Apex`、そして、**SQL** と **ORM** を足したような`SOQL`という専用言語を使うらしい。ユーザーインターフェースは`Visualforce`というHTML類似のマークアップ言語で定義する。いずれも、標準のカスタマイズでは実現できない要件に限り用いることになるが、フロントエンドエンジニアならその専門領域を存分に発揮できるだろう。

`Apex`はサーバサイドのプログラムだが`Visualforce`と合わせることで **Servlet/JSP** ライクに使える。

```apex:Apex
class Example {
    public String greet() {
        return 'Hello, world !';
    }
}
```

```apex:Visualforce
<apex:page>
    <h1>Example</h1>
    <p>
        <apex:outputText value="{! 'Hello, world !' }"/>
    </p>
</apex:page>
```

勿論 JavaScript を含められるので、React や Vue.js を載せることもできるが、Lightning Component フレームワークを使うのが Salesforce 的には推奨のようだ。

開発環境はブラウザ内で完結するが、Salesforce CLI を使うと、Visual Studio Code と連携できる。

作成したアドオンやコンポーネント、ビジネスアプリケーションは、Salesforce が提供する企業向けアプリマーケット AppExchange で公開（販売）できる。

## Salesforce を構成する主なプロダクト
Salesforce の利用料金は、プロダクトとエディション、サポートプランによって決まる。
主なプロダクトは次の通り。

### Sales Cloud
SFAに特化。営業・マーケティングを主な対象業務とする。
商談管理、Chatter（チャター）と呼ばれる社内SNS、レポート作成、ダッシュボード機能がある。

### Service Cloud
カスタマーサポートに特化。コンタクトセンター・カスタマーサービス・フィールドサービスを主な対象業務とする。
サービス契約、ナレッジ、チャット機能がある。

営業の最前線に Sales Cloud、アフターサポートに Service Cloud という棲み分けであるが、近年はその差が曖昧になってきているようだ。

### Salesforce Platform（Lightning Platform）
Salesforce から、上記 Sales Cloud、Service Cloud の機能を除いたもの。旧 Force.com。
つまり、ローコードで独自アプリケーションを開発できるPaaS環境である。
CRMオブジェクト（テーブル）は無いが、独自のカスタムオブジェクトを作成できる。
コストを抑えて小さく始めたい人向き。

### Experience Cloud（Community Cloud）
企業やユーザー同士のコミュニティサイト、FAQの機能を提供する。
このようなサイトを運営する場合、ゲストユーザのアクセス権限を適切に設定しておかないと、148万件の企業・個人情報流出事例[^2] [^3] のようになる。肝に銘じることが賢明だ。

<font color="red">2021/2/18追記</font> ゲストユーザ問題については、[こちらの記事](https://qiita.com/tonnuts/items/212b4b3121c3d2915190)がとても丁寧に纏められていたので、併せて参照されると良いと思う。
[^2]: [クラウド型営業管理システムへの社外の第三者によるアクセスについて](https://corp.rakuten.co.jp/news/update/2020/1225_01.html)
[^3]: [当社一部製品をご利用のお客様におけるゲストユーザに対する共有に関する設定について](https://www.salesforce.com/jp/company/news-press/press-releases/2020/12/201225)

## 略語
コミュニティなどの書き言葉では次の略語が一般的。他にもあるかもしれない。

SF ▶ Salesforce
VF ▶ Visualforce
LEX ▶ Lightning Experience
SFDC ▶ セールスフォース・ドットコム

## 学習方法
まずは Trailhead から始めるのが良いと思う。

### Trailhead
Salesforce が提供する無償のオンライン学習プログラム。
お題クリアでポイントやバッジ獲得。ゲーム感覚で楽しく学べるよう工夫されている。
ランクがあり、スキルの証明にも使える。
https://trailhead.salesforce.com/ja

### Trailmix
誰もが作成できる学習コンテンツのコレクション。カスタムカリキュラム。
https://trailhead.salesforce.com/ja/trailmixes

取り敢えず次がオススメ。

- [まずはやるべき Trailhead：簡単カスタマイズ編](https://trailhead.salesforce.com/ja/users/welcome4/trailmixes/mazuyaru-mix)
- [Salesforceの開発をはじめる](https://trailhead.salesforce.com/ja/users/00550000007HqDdAAK/trailmixes/start-develop)

### Trailblazer
ユーザーコミュニティである。
https://trailblazers.salesforce.com

次のグループがオススメ。グループ名で検索し、参加すると良い。

- 質問広場～初心者から上級者まで～ 日本
- Japan Trailhead (日本)

活発かつ紳士的な交流が行われている。
なお、trailblazerとは先駆者という意味であるが、セールスフォース・ドットコム創業者で会長兼CEOのマーク・ベニオフ氏による同名の本もある。
本の内容については [中田敦彦のYouTube大学](https://www.youtube.com/watch?v=BZ-MQiuPPI4) でザックリ解説してくれている。これはこれで面白いのでオススメ。

### YouTubeチャンネル

- [Salesforce Developers Japan](https://www.youtube.com/user/salesforcedevjp)

### もくもく会
オンラインだけではモチベーションが保てないって人には、もくもく会のオフラインイベントに足を運んでみるのがオススメ。

- [Salesforce DG ルーキー会](https://sfdgr.connpass.com)

## Salesforce の認定資格
Salesforce 認定資格は、基本資格と上位資格で構成され、基本資格に合格すると上位資格を受験できる。
試験区分は多岐に渡るが、エンジニアなら、開発者／アーキテクトに分類される試験が候補になる。
どの試験も実務経験がないと合格するのは難しいと言われている。合格率は非公開。受験料は20,000円から。

## 本記事の開発環境

|分類         |分類名                |備考 |
|:------------|:-------------------|:----|
|プロダクト    |Sales Cloud         |営業支援プロダクト   |
|エディション  |Enterprise Edition  |定価：18,000円/ユーザ/月（年間契約）  |
|アドオン      |なし                |機能強化アプリなど   |
|サポートプラン |Premier            |いつでもエキスパートの支援を得ることができる  |
|UI           |Lightning Experience |従前のUIを Salesforce Classic という  |

プロダクトとエディションは [Salesforceライセンスの「きほんのき」まとめ](https://qiita.com/OKeiDev/items/aff6b1f66f9c57cb9423) が分かり易い。

## 標準オブジェクトとカスタムオブジェクト
**標準オブジェクト**は、Salesforce組織がデフォルトで持っているオブジェクト。取引先、取引先責任者、商談などはすべて標準オブジェクトである。
**カスタムオブジェクト**は、ユーザが作成するもので、会社や業種固有の情報を保存するオブジェクトである。

オブジェクトは、オブジェクトマネージャやスキーマビルダーで確認できるが、非表示のオブジェクトもある。すべての標準オブジェクトは、[SOAP API 開発者ガイド](https://developer.salesforce.com/docs/atlas.ja-jp.api.meta/api/sforce_api_objects_list.htm)で確認できる。

[公式サイトのER図](https://developer.salesforce.com/docs/atlas.ja-jp.api.meta/api/sforce_api_erd_majors.htm)を簡略化（**概念データモデル**への置き換え）してみた。
![Salesforce ER図](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/236222/2fb68488-e2b9-e8a7-6f7c-5932aa35dc6e.png)
各オブジェクトの用途は、[Salesforce 標準オブジェクト早見表](https://qiita.com/na0AaooQ/items/c2678f5e809923fa9fb5) が分かり易い。
オブジェクトを作ると、対応するバリデーション付き入力フォーム（CRUD操作画面）やレポートの標準形を自動で作ってくれる。超簡単！

アクセス権限や共有ルールの制約を考慮すると、最低限の設計、つまり、**業務フロー図とER図くらいは真面目に書いておかないと厳しい**と感じた。

なお、独自項目の表現方法として、標準オブジェクトにカスタム項目を追加する方法、カスタムオブジェクトから標準オブジェクトにリレーションを張る方法とがあるが、後者は複雑になり易いので、基本、前者で作るらしい（業務にも因るだろうけども）。

## 使ってみよう
### アカウントの作成
１つのアカウントを複数のユーザで使い回すことは禁止されている。
システム管理者アカウントでログインし、何はともあれ自分専用のアカウントを用意しよう。

1. 歯車のアイコンから [設定] をクリック。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/236222/7d1a387c-28b8-2edd-638f-ca27fec11271.png)

2. 管理 ▶ ユーザ ▶ 新規ユーザ をクリック。（クイック検索に「ユーザ」と入力しても良い）
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/236222/8847693a-7e27-2128-1536-419650075a6c.png)

3. 必要情報を入力。
ユーザ名は、メールアドレスの形式にする必要があるが、実際のメールアドレスでなくても構わない。
メールアドレスが全ての Salesforce 組織内でユニークなら、そのメールアドレスを使用できる。
ユーザライセンスによって、そのユーザで利用可能なプロファイルが決まる。
最初は、Salesforceユーザライセンス ＋ システム管理者プロファイルで良いと思う。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/236222/13a529af-ef98-c533-6a98-23db40936932.png)

## わかったこと
エンジニアであれば、Trailhead をひと通りこなすだけでも十分に理解できると分かった。
