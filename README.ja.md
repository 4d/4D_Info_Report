[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_inforeport.json)](https://github.com/4d/4D_Info_Report/releases/latest/)[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)](<>)[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)<br>[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)](<>)[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)](<>)

# ツール 4D_Info_Report

![info_report](https://github.com/4d/4D_Info_Report/blob/main/images/4DIR.png)

## READMEの翻訳

-   [英語](README.md)
-   [フランス語](README.fr.md)
-   [ドイツ語](README.de.md)
-   [日本語](README.ja.md)
-   [スペイン語](README.es.md)

## このコンポーネントについて?

コンポーネント`4D_Info_Report`は多数の情報を提供します。

-   オペレーティング システム、コンピュータ、および 4D アプリケーションについて

-   データベース上: 構造、データ ファイル、サイズ、設定などの説明。

-   サーバーの実行中、メモリの変化、キャッシュの使用状況、接続されているユーザー、プロセスなど。

<br>

## このコンポーネントの使い方は?

**_手順 1:_**

> [!NOTE]
> バージョン 20 R6 以降を使用している場合

-   を作成します`dependencies.json`内のファイル`/Project/Sources/` folder

-   以下のテキストをコピーして、`dependencies.json`ファイル

```json
{
	"dependencies": {
		"4D_Info_Report": {
			"github": "4d/4D_Info_Report",
			"version": "latest"
		}
	}
}
```

-   4D プロジェクトを再度開いた後、コンポーネントは自動的にロードされます

> [!NOTE]
>
> -   コンポーネントは次のフォルダーに存在します。
>     -   ~/ライブラリ/キャッシュ/4D/依存関係/.github/4d/4D_Info_Report/ (Mac の場合)
>     -   ~\AppData\Local\4D\Dependency.github\4d\4D_Info_Report\ (Windows の場合)

**_手順 2:_**

フォルダーを作成する`Components`ストラクチャーまたはアプリケーションファイルの横にある (まだ存在しない場合)、アーカイブされていないコンポーネントをコピーし、4D または 4D Server を再起動します。

その後、共有メソッドを直接実行できます。`aa4D_NP_Report_Manage_Display`4Dリモートから。

コンポーネントのダイアログを使用すると、ストアド プロシージャを開始して、サーバー上で N 分ごとにレポートを作成できます。

この小さなコードをホスト データベースに実装することもできます。`On Server startup`メソッドを使用して、共有メソッドのいずれかを実行します (すべてのメソッドは次で始まります)`aa4D_`）：

<pre>
  <code class="4d">
    var $NP : Integer
    ARRAY TEXT($at_Components;0)
    COMPONENT LIST($at_Components)
    If(Find in array($at_Components;"4D_Info_Report@")>0)
      // to start the stored procedure creating report every 5 minutes
      $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
    End if
   </code>
</pre>

**_手順 3:_**

共有メソッドを使用してレポートを 1 つだけ作成できます`aa4D_NP_Util_CreateReport_Serv`。

作成したレポート（テキストファイル）は作成したフォルダーに保存されます`Folder_reports`データファイルの横にあります。

<pre>
  <code class="4d">
    var $NP : Integer
    ARRAY TEXT($at_Components;0)
    COMPONENT LIST($at_Components)
    If(Find in array($at_Components;"4D_Info_Report@")>0)
      // to create a single report in "Folder_reports" next to the Data file
      $NP:=New process("aa4D_NP_Util_CreateReport_Serv";0;"$4DIR_NP")
    End if
    </code>
</pre>

<br>

## レポートを分析するにはどうすればよいですか?

これらのレポートを分析できます。

-   を実行してリモート 4D から`aa4D_NP_Report_Export_Display`方法

-   シングルユーザー 4D からコンポーネントを開いて`File / Local reports compare`メニュー

<br>

## ダウンロード

-   コンポーネントの参照:[ChD_Info_Report_vch_80_Ref_v40.pdf](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_80_Ref_v40.pdf)

-   ホスト データベース (19) といくつかのホスト共有メソッドの例 (テスト用にコンポーネントを「コンポーネント」フォルダーに追加してください)[４Ｄ＿いんふぉ＿れぽｒｔ＿ほｓｔ＿Ｔ＿ｖ９＿１９。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_Host_T_v9_19.zip)

-   バージョン 4D 20 R5 のコンポーネント (Apple Silicon プロセッサー用にもコンパイル):[４Ｄ＿いんふぉ＿れぽｒｔー２０ーＲ５。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-R5.zip)

-   バージョン 4D 20 のコンポーネント (Apple Silicon プロセッサー用にもコンパイルされています):[4D_Info_Report-20-LTS.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-LTS.zip)

-   バージョン 4D 19 R6 のコンポーネント (Intel/AMD プロセッサー用にのみコンパイル):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿８１＿い＿１９Ｒ６。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_81_I_19R6.zip)

-   バージョン 4D 19 R6 のコンポーネント (Apple Silicon プロセッサー用にもコンパイルされています):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿８１＿いＳ＿１９Ｒ６。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_81_IS_19R6.zip)

-   バージョン 4D 19 のコンポーネント (Intel/AMD プロセッサ用にのみコンパイル):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿８１＿い＿１９。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_81_I_19.zip)

-   バージョン 4D 19 のコンポーネント (Apple Silicon プロセッサー用にもコンパイルされています):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿８１＿いＳ＿１９。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_81_IS_19.zip)

<br>

## アーカイブ

-   バージョン 4D v18 のコンポーネント:[4D_Info_Report_v4_65_v18.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_65_v18.zip)

-   バージョン 4D v17 のコンポーネント (64 ビット用にのみコンパイル):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿３３＿６４ーびｔ＿ｖ１７。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_33_64-bit_v17.zip)

-   バージョン 4D v17 のコンポーネント (64 ビット用にもコンパイルされています):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿３３＿ｖ１７。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_33_v17.zip)

-   ホスト データベース (v17) といくつかのホスト共有メソッドの例 (テスト用に「コンポーネント」フォルダーにコンポーネントを追加してください:[４Ｄ＿いんふぉ＿れぽｒｔ＿ほｓｔ＿Ｔ＿ｖ８＿ｖ１７。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_Host_T_v8_v17.zip)

-   バージョン 4D v16 のコンポーネント (64 ビット用にもコンパイルされています):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿９ｒＺＣ＿ｖ１６＿れｖ３。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZC_v16_rev3.zip)

-   バージョン 4D v15 のコンポーネント (64 ビット用にもコンパイルされています):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿９ｒＺ８＿ｖ１５＿れｖ２。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

-   バージョン 4D v14 のコンポーネント (64 ビット用にもコンパイルされています):[4D_Info_Report_v4_9rZ2_v14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

-   バージョン 4D v13 のコンポーネント (64 ビット用にもコンパイルされています):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿９ｒＺ２＿ｖ１３＿れｖ１。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

-   バージョン 4D v12 のコンポーネント (64 ビット用にもコンパイルされています):[４Ｄ＿いんふぉ＿れぽｒｔ＿ｖ４＿９ｒＺ＿ｖ１２。じｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ_v12.zip)

-   ホスト データベース (v12) といくつかのホスト共有メソッドの例 (テスト用に「コンポーネント」フォルダーにコンポーネントを追加してください)[4D_Info_Report_Host_T_v6_v12.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_Host_T_v6_v12.zip)
