[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_inforeport.json)](https://github.com/4eDimension/4DIR/releases/latest/)[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)](<>)[![Downloads](https://img.shields.io/github/downloads/4eDimension/4DIR/total.svg)](https://GitHub.com/4eDimension/4DIR/releases/latest/)![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)<br>[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)](<>)[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)](<>)

# Herramienta 4D_Info_Report

![info_report](https://github.com/4eDimension/4DIR/blob/main/images/4DIR.png)

## Traducción LÉAME

-   [Inglés](README.md)
-   [Francés](README.fr.md)
-   [Alemán](README.de.md)
-   [japonés](README.ja.md)
-   [Español](README.es.md)

## ¿Sobre este componente?

el componente`4D_Info_Report`proporciona una gran cantidad de información:

-   sobre el sistema operativo, el ordenador y la aplicación 4D

-   sobre la base de datos: descripción de la estructura, archivo de datos, tamaño, configuración, etc.

-   mientras el servidor está en ejecución, variación de memoria, uso de caché, usuarios conectados, procesos, etc.

<br>

## ¿Cómo utilizar este componente?

**_Procedimiento n°1:_**

> [!NOTE]
> Si está utilizando la versión 20 R6 o superior

-   Crear un`dependencies.json`archivo en el`/Project/Sources/`carpeta

-   Copie y pegue el texto a continuación en el`dependencies.json`archivo

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

-   El componente se cargará automáticamente después de volver a abrir su proyecto 4D.

> [!NOTE]
>
> -   El componente estará presente en la carpeta:
>     -   ~/Library/Caches/4D/Dependencies/.github/4eDimension/4DIR/ (en Mac)
>     -   ~\\AppData\\Local\\4D\\Dependencies.github\\4eDimension\\4DIR\\ (en Windows)

**_Procedimiento n°2:_**

Crear una carpeta`Components`junto al archivo de estructura o aplicación (si aún no existe), copie el componente no archivado y reinicie su 4D o 4D Server.

Luego puedes ejecutar directamente el método compartido:`aa4D_NP_Report_Manage_Display`desde 4D Remoto.

Un cuadro de diálogo del componente le permitirá iniciar el procedimiento almacenado para crear informes cada N minutos en el servidor.

También puedes implementar en tu base de datos Host, este pequeño código en tu`On Server startup`método para ejecutar cualquiera de los métodos compartidos (todos comienzan con`aa4D_`):

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

**_Procedimiento n°3:_**

Puede crear un solo informe utilizando el método compartido`aa4D_NP_Util_CreateReport_Serv`.

Los informes creados (archivos de texto) se almacenan en una carpeta creada.`Folder_reports`al lado del archivo de datos.

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

## ¿Cómo analizar informes?

Puedes analizar estos informes:

-   desde un 4D remoto ejecutando el`aa4D_NP_Report_Export_Display`método

-   desde un 4D de un solo usuario abriendo el componente y haciendo clic en el`File / Local reports compare`menú

<br>

## Descargar

-   referencia del componente:[ChD_Info_Report_vch_80_Ref_v40.pdf](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_80_Ref_v40.pdf)

-   base de datos de host (19) con algunos ejemplos de métodos compartidos de host (agregue el componente en la carpeta "Componentes" para su prueba:[4D_Info_Report_Host_T_v9_19.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_Host_T_v9_19.zip)

-   componente para la versión 4D 20 R5 (también compilado para el procesador Apple Silicon):[4D_Info_Report-20-R5.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report-20-R5.zip)

-   componente para la versión 4D 20 (también compilado para el procesador Apple Silicon):[4D_Info_Report-20-LTS.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report-20-LTS.zip)

-   componente para la versión 4D 19 R6 (sólo compilado para procesador Intel/AMD):[4D_Info_Report_v4_81_I_19R6.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_81_I_19R6.zip)

-   componente para la versión 4D 19 R6 (también compilado para el procesador Apple Silicon):[4D_Info_Report_v4_81_IS_19R6.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_81_IS_19R6.zip)

-   componente para la versión 4D 19 (sólo compilado para procesador Intel/AMD):[4D_Info_Report_v4_81_I_19.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_81_I_19.zip)

-   componente para la versión 4D 19 (también compilado para el procesador Apple Silicon):[4D_Info_Report_v4_81_IS_19.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_81_IS_19.zip)

<br>

## Archivo

-   componente para la versión 4D v18:[4D_Info_Report_v4_65_v18.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_65_v18.zip)

-   componente para la versión 4D v17 (sólo compilado para 64 bits):[4D_Info_Report_v4_33_64-bit_v17.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_33_64-bit_v17.zip)

-   componente para la versión 4D v17 (también compilado para 64 bits):[4D_Info_Report_v4_33_v17.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_33_v17.zip)

-   base de datos de host (v17) con algunos ejemplos de métodos compartidos de host (agregue el componente en la carpeta "Componentes" para su prueba:[4D_Info_Report_Host_T_v8_v17.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_Host_T_v8_v17.zip)

-   componente para la versión 4D v16 (también compilado para 64 bits):[4D_Info_Report_v4_9rZC_v16_rev3.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_9rZC_v16_rev3.zip)

-   componente para la versión 4D v15 (también compilado para 64 bits):[4D_Info_Report_v4_9rZ8_v15_rev2.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

-   componente para la versión 4D v14 (también compilado para 64 bits):[4D_Info_Report_v4_9rZ2_v14_rev1.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

-   componente para la versión 4D v13 (también compilado para 64 bits):[4D_Info_Report_v4_9rZ2_v13_rev1.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

-   componente para la versión 4D v12 (también compilado para 64 bits):[4D_Info_Report_v4_9rZ_v12.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_v4_9rZ_v12.zip)

-   base de datos de host (v12) con algunos ejemplos de métodos compartidos de host (agregue el componente en la carpeta "Componentes" para su prueba:[4D_Info_Report_Host_T_v6_v12.zip](https://github.com/4eDimension/4DIR/releases/latest/download/4D_Info_Report_Host_T_v6_v12.zip)
