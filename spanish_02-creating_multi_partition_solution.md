# Crear un contenedor particionado con .NET SDK

En esta práctica de laboratorio, creará varios contenedores de Azure Cosmos DB con diferentes configuraciones y claves de partición. En laboratorios posteriores, utilizará la API de SQL y el SDK de .NET para consultar contenedores específicos utilizando una sola clave de partición o en varias claves de partición.

> Si aún no ha completado la configuración del contenido del laboratorio, consulte las instrucciones para la Configuración de la cuenta antes de comenzar este laboratorio.

## Crear contenedores con .NET SDK

> Comenzará utilizando .NET SDK para crear contenedores de tamaño fijo e ilimitados para usar en el laboratorio.

### Crear un proyecto de .NET Core

1. En su máquina local, cree una nueva carpeta que se utilizará para contener el contenido de su proyecto .NET Core.

1. En la nueva carpeta, haga clic derecho en la carpeta y seleccione la opción de menú ** Abrir con código **.

    <img src="/media/02-open_with_code.jpg">

    > Alternativamente, puede ejecutar un símbolo del sistema en su directorio actual y ejecutar el comando `` código ''.

1. En la ventana de Visual Studio Code que aparece, haga clic con el botón derecho en el panel ** Explorer ** y seleccione la opción de menú ** Abrir en el símbolo del sistema **.

    <img src="/media/02-open_command_prompt.jpg"> 

1. En el panel de terminal abierto, ingrese y ejecute el siguiente comando:

    `` `sh
    nueva consola dotnet --salida.
    `` `

    > Este comando creará un nuevo proyecto .NET Core 2.1. El proyecto será un proyecto de ** consola ** y el proyecto se creará en el actual directamente desde que usó la opción `` --output``.

1. Visual Studio Code probablemente le pedirá que instale varias extensiones relacionadas con el desarrollo ** .NET Core ** o ** Azure Cosmos DB **. Ninguna de estas extensiones es necesaria para completar los laboratorios.

1. En el panel de terminales, ingrese y ejecute el siguiente comando:

    `` `sh
    dotnet add package Microsoft.Azure.DocumentDB.Core --version 1.9.1
    `` `

    > Este comando agregará el paquete Microsoft.Azure.DocumentDB.Core NuGet como una dependencia del proyecto. Las instrucciones de laboratorio se probaron con la versión `` 1.9.1 '' de este paquete NuGet.

1. En el panel de terminales, ingrese y ejecute el siguiente comando:

    `` `sh
    dotnet add package Bogus - versión 22.0.8
    `` `

    > Este comando agregará el paquete NuGet Bogus como una dependencia del proyecto. Esta biblioteca nos permitirá generar rápidamente datos de prueba usando una sintaxis fluida y un código mínimo. Utilizaremos esta biblioteca para generar documentos de prueba para cargar en nuestra instancia de Azure Cosmos DB. Las instrucciones de laboratorio se probaron con la versión `` 22.0.8 '' de este paquete NuGet.

1. En el panel de terminales, ingrese y ejecute el siguiente comando:

    `` `sh
    restaurar dotnet
    `` `

    > Este comando restaurará todos los paquetes especificados como dependencias en el proyecto.

1. En el panel de terminales, ingrese y ejecute el siguiente comando:

    `` sh
    construcción dotnet
    `` `

    > Este comando construirá el proyecto.

1. Haga clic en el símbolo ** 🗙 ** para cerrar el panel de terminales.

1. Observe los archivos ** Program.cs ** y ** [nombre de carpeta] .csproj ** creados por .NET Core CLI.

    <img src="/media/02-project_files.jpg">

1. Haga doble clic en el enlace ** [nombre de carpeta] .csproj ** en el panel ** Explorer ** para abrir el archivo en el editor.

1. Ahora agregaremos un nuevo elemento XML ** PropertyGroup ** a la configuración del proyecto dentro del elemento ** Proyecto **. Para agregar un nuevo ** PropertyGroup **, inserte las siguientes líneas de código debajo de la línea que dice `` <Project Sdk = "Microsoft.NET.Sdk"> ``:
