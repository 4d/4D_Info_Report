[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_4dir.json)](https://github.com/4d/4D_Info_Report/releases/latest/)
[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)]()
[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)
![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)
![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)
<br>
[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)]()
[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)]()

![info_report](https://raw.githubusercontent.com/4d/4D_Info_Report/main/images/4DIR.png)

-   [英語](README.md)
-   [フランス語](README.fr.md)
-   [ドイツ語](README.de.md)
-   [日本語](README.ja.md)
-   [スペイン語](README.es.md)

# コンポーネントについて

コンポーネント`4D_Info_Report`はアプリケーションの検査と診断に役立つ情報を収集するためのツールです。

- オペレーティングシステム・コンピューター・4Dアプリケーションの情報

- ストラクチャ・データファイル・データベース設定の情報

- メモリ・キャッシュ・接続ユーザー数・プロセス数の遷移

<br>

# コンポーネントをインストールするには

下記いずれかの方法でコンポーネントをインストールすることができます。

* ① オート: 「プロジェクト依存関係」ツールを使用する（[4D 20 R6](https://blog.4d.com/ja/integrate-4d-components-directly-from-github/)以降）

* ② マニュアル: プロジェクトの`Components`フォルダーに4D_Info_Reportコンポーネントをコピーする（すべてのバージョン）

**_① 自動_**

> 4D 20 R6以降が対象です。

- `/Project/Sources/`フォルダー内に`dependencies.json`ファイルを作成する

- `dependencies.json`ファイルに下記のテキストを転写する

```json
{
	"dependencies": {
		"4D_Info_Report": {
			"github": "4d/4D_Info_Report",
			"version": "4d"
		}
	}
}
```

- 4Dまたは4D Serverを再起動すると，プロジェクト起動と同時にコンポーネントがダウンロードされます。

>   コンポーネントは自動的に下記のフォルダーにダウンロードされます。
>   -   ~/Library/Cache/4D/Dependencies/.github/4d/4D_Info_Report/ (Mac)
>   -   ~\AppData\Local\4D\Dependency\\.github\4d\4D_Info_Report\ (Windows)

* 後述するいずれかの方法でコンポーネントにレポートを出力させることができます。

**_② マニュアル_**

> すべての4Dバージョンが対象です。

* 使用中の4Dバージョンに対応するコンポーネント（本記事の`ダウンロード`または`過去バージョン`を参照）をダウンロードする

* プロジェクトと同階層に`Components`フォルダーを作成する

* ダウンロードして展開したコンポーネントを`Components`フォルダーにコピーする

* 4Dまたは4D Serverを再起動する

* 後述するいずれかの方法でコンポーネントにレポートを出力させることができます。

# コンポーネントを使用するには

下記いずれかのタイミングでコンポーネントにレポートを出力させることができます。

* ❶ n分毎にレポートを作成する
* ❷ 1回だけレポートを作成する

> レポートはデータファイルと同階層に作成される`Folder_reports`に標準テキスト形式で出力されます。

どちらの場合も，下記いずれかの構成を選ぶことができます。

* ホストプロジェクトのソースコードを変更しない場合: コンポーネントの共有メソッドを`マニュアル`操作で実行し，サーバー側に常駐プロセスのストアドプロシージャーを開始します。ホストプロジェクトのソースコードを変更しないで済みます。たとえば，コンパイル版のアプリケーションをデプロイしている場合，再コンパイルしなくても良いので便利です。一方，サーバーアプリケーションを再起動するたびに，再度ストアドプロシージャーを開始しなければならない，という手間が生じます。

* ホストプロジェクトのソースコードを変更する場合: サーバー起動後，自動的にストアドプロシージャーを開始するようなコードをホストプロジェクトに追加します。メリットとして，人手を介さず自動的にレポートが出力されるので便利です。

> それぞれの方法には，メリットとデメリットがあるので，事情や必要に合わせて適切なほうを選択してください。 
 
**_❶ n分毎にレポートを作成する_**

**_ホストプロジェクトのソースコードを変更しない場合:_**

* クライアントで`aa4D_NP_Report_Manage_Display`共有メソッドを実行する

* N分毎にサーバー上でレポートを作成するストアドプロシージャを起動するためのダイアログ画面が表示されます。

**_ホストプロジェクトのソースコードを変更する場合:_**

* ホストプロジェクトの`On Server Startup`データベースメソッドに下記のサンプルコードをコピー＆ペーストする

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // 5分毎にサーバー上でレポートを作成するストアドプロシージャを起動する
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

**_❷ 1回だけレポートを作成する_**

**_ホストプロジェクトのソースコードを変更しない場合:_**

* `aa4D_NP_Util_CreateReport_Serv`共有メソッドを実行する

**_ホストプロジェクトのソースコードを変更する場合:_**

* ホストプロジェクトに下記のサンプルコードをコピー＆ペーストする

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // データファイルと同階層の"Folder_reports"に1回だけレポートを作成する
  $NP:=New process("aa4D_NP_Util_CreateReport_Serv";0;"$4DIR_NP")
End if
```

<br>

# レポートを解析するには

下記いずれかのレポートを解析することができます。

- クライアントで`aa4D_NP_Report_Export_Display`共有メソッドを実行する

- 直接コンポーネントを起動して`ファイル / Local reports compare`メニューを実行する

<br>

# ダウンロード

- リファレンス : [4D_Info_Report_v4_90_Ref_v42.pdf](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_Ref_v42.pdf)

- 4D 19ホストデータベースと共有メソッドの例題（*Components* フォルダーにコンポーネントをインストールしてください）: [4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v9_19.zip)

- 4D 20 R10コンポーネント（Intel/AMD, Apple Silicon）: [4D_Info_Report_v4_95_1_20R10.zip](https://github.com/4d/4D_Info_Report/releases/download/4.95.1/4D_Info_Report_v4_95_1_20R10.zip)

- 4D 20 LTS コンポーネント（Intel/AMD, Apple Silicon）: [4D_Info_Report_v4_95_1_20.zip](https://github.com/4d/4D_Info_Report/releases/download/4.95.1/4D_Info_Report_v4_95_1_20.zip)

- 4D 19 R6コンポーネント（Intel/AMD）: [4D_Info_Report_v4_83_I_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19R6.zip)

- 4D 19 R6コンポーネント（Intel/AMD, Apple Silicon）: [4D_Info_Report_v4_83_IS_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19R6.zip)

- 4D 19コンポーネント（Intel/AMD）: [4D_Info_Report_v4_90_2_I_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_2_I_19.zip)

- 4D 19コンポーネント（Intel/AMD, Apple Silicon）: [4D_Info_Report_v4_90_2_IS_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_2_IS_19.zip)

<br>

# 過去バージョン

- 4D 18コンポーネント : [4D_Info_Report_v4_90_2_18.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_90_2_v18.zip)

- 4D 17コンポーネント（64ビット）: [4D_Info_Report_v4_33_64-bit_17.zipｐ](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_64-bit_v17.zip)

- 4D 17コンポーネント（32/64ビット）: [4D_Info_Report_v4_33_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_v17.zip)

- 4D 17ホストデータベースと共有メソッドの例題（*Components* フォルダーにコンポーネントをインストールしてください）: [4D_Info_Report_Host_T_v8_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v8_v17.zip)

- 4D 16コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZC_16_rev3.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZC_v16_rev3.zip)

- 4D 15コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZ8_15_rev2.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

- 4D 14コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZ2_14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

- 4D 13コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZ2_13_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

- 4D 12コンポーネント（32/64ビット）: [4D_Info_Report_v4_9rZ_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ_v12.zip)

- 4D 12ホストデータベースと共有メソッドの例題（*Components* フォルダーにコンポーネントをインストールしてください）: [4D_Info_Report_Host_T_v6_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v6_v12.zip)
