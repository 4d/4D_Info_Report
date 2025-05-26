[![Version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/release_4dir.json)](https://github.com/4d/4D_Info_Report/releases/latest/)
[![4D version](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/CGareau/dd2aa26e5b6c4152e80e7d3d09f2486a/raw/version_4dir.json)]()
[![Downloads](https://img.shields.io/github/downloads/4d/4D_Info_Report/total.svg)](https://GitHub.com/4d/4D_Info_Report/releases/latest/)
![maintenance-status](https://img.shields.io/badge/maintenance-actively--developed-brightgreen.svg)
![Maintainer](https://img.shields.io/badge/maintainer-ThomasSchlumberger-blue)
<br>
[![support mac](https://img.shields.io/badge/macOS-000000.svg?style=flat-square&logo=apple&labelColor=000000&logoColor=white)]()
[![support windows](https://img.shields.io/badge/windows-0078D6.svg?style=flat-square&logo=MODX&logoColor=white)]()

![info_report](https://raw.githubusercontent.com/4d/4D_Info_Report/main/images/4DIR.png)

* [Inglés](README.md)
* [Francés](README.fr.md)
* [Alemán](README.de.md)
* [Japonés](README.ja.md)
* [Español](README.es.md)

# ¿Sobre este componente?

el componente`4D_Info_Report`proporciona una gran cantidad de información:

* sobre el sistema operativo, el ordenador y la aplicación 4D

* sobre la base de datos: descripción de la estructura, archivo de datos, tamaño, configuración, etc.

* mientras el servidor está en ejecución, variación de memoria, uso de caché, usuarios conectados, procesos, etc.

<br>

# ¿Cómo se instala este componente?

Existen 2 formas de instalar este componente:
* 1/ Automáticamente: mediante el gestor de dependencias ([nueva funcionalidad 4D, disponible a partir de la versión 4D 20 R6](https://blog.4d.com/integrate-4d-components-directly-from-github/))
* 2/ Manualmente: copiando y pegando el componente 4D_Info_Report en la carpeta `Components' del proyecto 4D (funciona con todas las versiones de 4D)

**_1/ Automáticamente_**

> Este método requiere el uso de al menos la versión 20 R6 de 4D

* Crear un archivo `dependencies.json` en la carpeta `/Project/Sources/`

* Copie y pegue el texto siguiente en este archivo:

```json
{
	"dependencies": {
		"4D_Info_Report": {
			"github": "4d/4D_Info_Report",
			"tag": "20R8"
		}
	}
}
```

* Reinicie 4D o 4D Server, el componente se cargará automáticamente cuando se vuelva a abrir el proyecto 4D

> A título informativo, el componente se descargará en el archivo:
> * ~/Library/Caches/4D/Dependencies/.github/4d/4D_Info_Report/ (en Mac)
> * ~\AppData\Local\4D\Dependencies\\.github\4d\4D_Info_Report\ (en Windows)

* Siga una de las 2 maneras de utilizar el componente (véase el párrafo siguiente) para generar uno o varios informes

**_2/ Manual_**

> Este método funciona con todas las versiones de 4D

* Descargue la versión del componente correspondiente a su versión de 4D (consulte la sección `Descargar` o `Archivos` de este artículo)

* Cree una carpeta `Components` en la carpeta del proyecto 4D (si esta carpeta no existe)

* Copie el componente no archivado en esta carpeta `Components`

* Reiniciar 4D o 4D Server

* Siga una de las 2 formas de utilizar el componente que se indican a continuación para generar uno o varios informes

<br>

# ¿Cómo utilizar este componente?

Existen dos formas de utilizar este componente:
* 1/ Generar informes cada N minutos
* 2/ Generar un informe previa solicitud

> Los informes (archivos de texto) se crean en una nueva carpeta llamada `Carpeta_informes` junto al archivo de datos.

Puede utilizar el botón:
* Sin modificar el código de la base de datos anfitriona: Ejecute un método compartido del componente creando `manualmente' un procedimiento almacenado en el servidor. La ventaja es que no es necesario modificar el código de la base de datos anfitriona, lo que resulta especialmente útil si la aplicación se despliega en una versión compilada, ya que evita la recompilación. Sin embargo, la desventaja es que tiene que volver a ejecutar el método compartido después de cada reinicio del servidor 4D para que el procedimiento almacenado esté activo.
* Modificando el código en la base de datos host: Este método consiste en añadir código directamente en la base de datos host. Permite crear automáticamente el procedimiento almacenado cuando se inicia el servidor 4D, lo que es muy útil para generar informes de forma autónoma y sin intervención. Se trata de una solución "automatizada" en la que todo está listo en cuanto se inicia el servidor.

> Ambos enfoques tienen sus ventajas, dependiendo del contexto y de los requisitos de supervisión de la aplicación.

**_1/ Generar informes cada N minutos_**

**_Sin modificar el código anfitrión:_**

* Ejecuta el método compartido `aa4D_NP_Report_Manage_Display` de 4D Remote

* Un diálogo de componentes le permitirá iniciar el procedimiento almacenado para crear un informe cada N minutos en el servidor 4D

**_Mediante la modificación del código de la base de acogida:_**

* Copie y pegue el código de ejemplo siguiente en el método base `On server startup` de su base de datos host:

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to start the stored procedure creating report every 5 minutes
  $NP:=New process("aa4D_NP_Schedule_Reports_Server";0;"$4DIR_NP";5;0)
End if
```

**_2/ Generar un único informe_**

**_Sin modificar el código anfitrión:_**

* Crea un informe ejecutando el método compartido `aa4D_NP_Util_CreateReport_Serv`

**_Mediante la modificación del código de la base de acogida:_**

* Copie y pegue el código de ejemplo siguiente en la base de datos de su host:

```4d
var $NP : Integer
ARRAY TEXT($at_Components;0)
COMPONENT LIST($at_Components)
If(Find in array($at_Components;"4D_Info_Report@")>0)
  // to create a single report in "Folder_reports" next to the Data file
  $NP:=New process("aa4D_NP_Util_CreateReport_Serv";0;"$4DIR_NP")
End if
```

<br>

# ¿Cómo analizar informes?

Puedes analizar estos informes:

* desde un 4D remoto ejecutando el`aa4D_NP_Report_Export_Display`método

* desde un 4D de un solo usuario abriendo el componente y haciendo clic en el`File / Local reports compare`menú

<br>

# Descargar

* referencia del componente: [4D_Info_Report_v4_89_7_Ref_v41.pdf](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_89_7_Ref_v41.pdf)

* base de datos de host (4D 19) con algunos ejemplos de métodos compartidos de host (agregue el componente en la carpeta "Componentes" para su prueba): [4D_Info_Report_Host_T_v9_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v9_19.zip)

* componente para la versión 4D 20 R7 (también compilado para el procesador Apple Silicon): [4D_Info_Report_20R7](https://github.com/4d/4D_Info_Report/releases/latest/)

* componente para la versión 4D 20 LTS (también compilado para el procesador Apple Silicon): [4D_Info_Report_20](https://github.com/4d/4D_Info_Report/releases/latest/)

* componente para la versión 4D 19 R6 (sólo compilado para procesador Intel/AMD): [4D_Info_Report_v4_83_I_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19R6.zip)

* componente para la versión 4D 19 R6 (también compilado para el procesador Apple Silicon): [4D_Info_Report_v4_83_IS_19R6.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19R6.zip)

* componente para la versión 4D 19 (sólo compilado para procesador Intel/AMD): [4D_Info_Report_v4_83_I_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_I_19.zip)

* componente para la versión 4D 19 (también compilado para el procesador Apple Silicon): [4D_Info_Report_v4_83_IS_19.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_83_IS_19.zip)

<br>

# Archivo

* componente para la versión 4D 18: [4D_Info_Report_v4_65_18.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_65_v18.zip)

* componente para la versión 4D 17 (sólo compilado para 64 bits): [4D_Info_Report_v4_33_64-bit_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_64-bit_v17.zip)

* componente para la versión 4D 17 (también compilado para 64 bits): [4D_Info_Report_v4_33_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_33_v17.zip)

* base de datos de host (4D 17) con algunos ejemplos de métodos compartidos de host (agregue el componente en la carpeta "Componentes" para su prueba: [4D_Info_Report_Host_T_v8_17.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v8_v17.zip)

* componente para la versión 4D 16 (también compilado para 64 bits): [4D_Info_Report_v4_9rZC_16_rev3.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZC_v16_rev3.zip)

* componente para la versión 4D 15 (también compilado para 64 bits): [4D_Info_Report_v4_9rZ8_15_rev2.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ8_v15_rev2.zip)

* componente para la versión 4D 14 (también compilado para 64 bits): [4D_Info_Report_v4_9rZ2_14_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v14_rev1.zip)

* componente para la versión 4D 13 (también compilado para 64 bits): [4D_Info_Report_v4_9rZ2_13_rev1.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ2_v13_rev1.zip)

* componente para la versión 4D 12 (también compilado para 64 bits): [4D_Info_Report_v4_9rZ_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_v4_9rZ_v12.zip)

* base de datos de host (4D 12) con algunos ejemplos de métodos compartidos de host (agregue el componente en la carpeta "Componentes" para su prueba: [4D_Info_Report_Host_T_v6_12.zip](https://github.com/4d/4D_Info_Report/releases/download/archives/4D_Info_Report_Host_T_v6_v12.zip)
