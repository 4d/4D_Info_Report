[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_inforeport.json)](https://github.com/4d/4D_Info_Report/releases/latest/)[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)](<>)[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)<br>[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)](<>)[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)](<>)

# 4D_Info_Report ツール

![info_report](https://github.com/4d/4D_Info_Report/blob/main/images/4DIR.png)

## 各言語のREADME

-   [英語](README.md)
-   [フランス語](README.fr.md)
-   [ドイツ語](README.de.md)
-   [日本語](README.ja.md)
-   [スペイン語](README.es.md)

## コンポーネントの用途

コンポーネント`4D_Info_Report`はアプリケーションの検査と診断に役立つ情報を収集するためのツールです。

- オペレーティングシステム・コンピュータ・4Dアプリケーションの情報

- ストラクチャ・データファイル・データベース設定の情報

- サーバー運用中におけるメモリ・キャッシュ・接続ユーザー数・プロセス数の遷移

<br>

## コンポーネントを使用する

**_方法 1:_**

> [!情報]
> 4D 20 R6以降が対象です。

- `/Project/Sources/`フォルダー内に`dependencies.json`ファイルを作成する

- `dependencies.json`ファイルに下記のテキストを転写する

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

- プロジェクトを再起動する

> [!情報]
>
> -   コンポーネントは自動的に下記のフォルダーにダウンロードされます。
>     -   ~/Library/Cache/4D/dependencies/.github/4d/4D_Info_Report/ (Mac)
>     -   ~\AppData\Local\4D\Dependency\\.github\4d\4D_Info_Report\ (Windows)

**_方法 2:_**

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

**_方法 3:_**

`aa4D_NP_Util_CreateReport_Serv`共有メソッドを実行することにより，レポートを1個だけ作成することができます。

データファイルと同階層の`Folder_reports`フォルダーに標準テキスト形式のレポートファイルが出力されます。

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

## レポートを解析する

下記いずれかのレポートを解析することができます。

- クライアントで`aa4D_NP_Report_Export_Display`共有メソッドを実行する

- 直接コンポーネントを起動して`ファイル / Local reports compare`メニューを実行する

<br>

## ダウンロード

- リファレンス: [ChD_Info_Report_vch_80_Ref_v40.pdf](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_80_Ref_v40.pdf)

- 4D 19ホストデータベースと共有メソッドの例題（*Components* フォルダーにコンポーネントをインストールしてください）: [4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_Host_T_v9_19.zip)

- 4D 20 R5コンポーネント（Intel/AMD, Apple Silicon）: [4D_Info_Report-20-R5.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-R5.zip)

- 4D 20コンポーネント（Intel/AMD, Apple Silicon）: [4D_Info_Report-20-LTS.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report-20-LTS.zip)

- 4D 19 R6コンポーネント（Intel/AMD）: [4D_Info_Report_v4_81_I_19R6.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_81_I_19R6.zip)

- 4D 19 R6コンポーネント（Intel/AMD, Apple Silicon）: [4D_Info_Report_v4_81_IS_19R6.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_81_IS_19R6.zip)

- 4D 19コンポーネント（Intel/AMD）: [4D_Info_Report_v4_81_I_19.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_81_I_19.zip)

- 4D 19コンポーネント（Intel/AMD, Apple Silicon）: [4D_Info_Report_v4_81_IS_19.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_81_IS_19.zip)

<br>

## 過去バージョン

- 4D v18コンポーネント: [4D_Info_Report_v4_65_v18.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_65_v18.zip)

- 4D v17コンポーネント（64ビット）: [4D_Info_Report_v4_33_64-bit_v17.zipｐ](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_33_64-bit_v17.zip)

- 4D v17コンポーネント（32/64ビット）: [4D_Info_Report_v4_33_v17.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_33_v17.zip)

- 4D v17ホストデータベースと共有メソッドの例題（*Components* フォルダーにコンポーネントをインストールしてください）: [4D_Info_Report_Host_T_v8_v17.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_Host_T_v8_v17.zip)

- 4D v16コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZC_v16_rev3.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZC_v16_rev3.zip)

- 4D v15コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZ8_v15_rev2.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

- 4D v14コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZ2_v14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

- 4D v13コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZ2_v13_rev1.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

- 4D v12コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZ_v12.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_v4_9rZ_v12.zip)

- 4D v12ホストデータベースと共有メソッドの例題（*Components* フォルダーにコンポーネントをインストールしてください）: [4D_Info_Report_Host_T_v6_v12.zip](https://github.com/4d/4D_Info_Report/releases/latest/download/4D_Info_Report_Host_T_v6_v12.zip)
