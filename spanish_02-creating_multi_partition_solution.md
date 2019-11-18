# Crear una solución de varias particiones con Azure Cosmos DB

En este laboratorio, creará varios contenedores de Azure Cosmos DB. Algunos de los contenedores serán ilimitados y configurados con una clave de partición, mientras que otros serán de tamaño fijo. Luego utilizará la API de SQL y el SDK de .NET para consultar contenedores específicos utilizando una sola clave de partición o en varias claves de partición.

## Inicie sesión en Azure Portal

1. En una nueva ventana, inicie sesión en ** Azure Portal ** (<http://portal.azure.com>).

1. Una vez que haya iniciado sesión, es posible que se le solicite iniciar un recorrido por el portal de Azure. Puede omitir este paso de manera segura.

## Preparar

> Antes de comenzar este laboratorio, deberá crear una base de datos y una colección de Azure Cosmos DB que usará en todo el laboratorio. El SDK de .NET requiere credenciales para conectarse a su cuenta de Azure Cosmos DB. Recopilará y almacenará estas credenciales para usar en todo el laboratorio.

### Recuperar credenciales de cuenta

1. En el lado izquierdo del portal, haga clic en el enlace ** Grupos de recursos **.

    ! [Grupos de recursos] (https://raw.githubusercontent.com/CosmosDB/labs/master/dotnet/media/02-resource_groups.jpg)

1. En la hoja ** Grupos de recursos **, ubique y seleccione el ** cosmosgroup-lab ** * Grupo de recursos *.

    ! [Grupo de recursos de laboratorio] (../ media / 02-lab_resource_group.jpg)

1. En la hoja ** cosmosgroup-lab **, seleccione la cuenta ** Azure Cosmos DB ** que creó recientemente.

    ! [Recurso Cosmos] (../ media / 02-cosmos_resource.jpg)

1. En la hoja ** Azure Cosmos DB **, busque la sección ** Configuración ** y haga clic en el enlace ** Teclas **.

    ! [Panel de teclas] (../ media / 02-keys_pane.jpg)

1. En el panel ** Keys **, registre los valores en los campos ** CONNECTION STRING **, ** URI ** y ** PRIMARY KEY **. Utilizará estos valores más adelante en esta práctica de laboratorio.

    ! [Credenciales] (../ media / 02-keys.jpg)

## Crear contenedores con .NET SDK

> Comenzará utilizando .NET SDK para crear contenedores de tamaño fijo e ilimitados para usar en el laboratorio.

### Crear un proyecto de .NET Core

1. En su máquina local, cree una nueva carpeta que se utilizará para contener el contenido de su proyecto .NET Core.

1. En la nueva carpeta, haga clic derecho en la carpeta y seleccione la opción de menú ** Abrir con código **.

    ! [Abrir con Visual Studio Code] (../ media / 02-open_with_code.jpg)

    > Alternativamente, puede ejecutar un símbolo del sistema en su directorio actual y ejecutar el comando `` código ''.

1. En la ventana de Visual Studio Code que aparece, haga clic con el botón derecho en el panel ** Explorer ** y seleccione la opción de menú ** Abrir en el símbolo del sistema **.

    ! [Abrir en el símbolo del sistema] (../ media / 02-open_command_prompt.jpg)

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

    > Este comando agregará el paquete [Microsoft.Azure.DocumentDB.Core] (../media/https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/) NuGet como una dependencia del proyecto. Las instrucciones de laboratorio se probaron con la versión `` 1.9.1 '' de este paquete NuGet.

1. En el panel de terminales, ingrese y ejecute el siguiente comando:

    `` `sh
    dotnet add package Bogus - versión 22.0.8
    `` `

    > Este comando agregará el paquete NuGet [Bogus] (../media/https://www.nuget.org/packages/Bogus/) como una dependencia del proyecto. Esta biblioteca nos permitirá generar rápidamente datos de prueba usando una sintaxis fluida y un código mínimo. Utilizaremos esta biblioteca para generar documentos de prueba para cargar en nuestra instancia de Azure Cosmos DB. Las instrucciones de laboratorio se probaron con la versión `` 22.0.8 '' de este paquete NuGet.

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

    ! [Archivos de proyecto] (../ media / 02-project_files.jpg)

1. Haga doble clic en el enlace ** [nombre de carpeta] .csproj ** en el panel ** Explorer ** para abrir el archivo en el editor.

1. Ahora agregaremos un nuevo elemento XML ** PropertyGroup ** a la configuración del proyecto dentro del elemento ** Proyecto **. Para agregar un nuevo ** PropertyGroup **, inserte las siguientes líneas de código debajo de la línea que dice `` <Project Sdk = "Microsoft.NET.Sdk"> ``:

    `` `xml
    <Grupo de propiedades>
        <LangVersion> última </LangVersion>
    </PropertyGroup>
