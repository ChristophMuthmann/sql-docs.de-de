---
title: Azure Active Directory | Microsoft Docs
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.suite: sql
ms.custom: 
ms.technology: drivers
ms.topic: article
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.workload: Inactive
ms.openlocfilehash: eb13c1a57c63ce013a3b546572994106b8b1ffc0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="connect-using-azure-active-directory-authentication"></a>Herstellen einer Verbindung mithilfe von Azure Active Directory-Authentifizierung
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis) (Azure AD) ist eine zentrale Benutzer-ID-Management-Technologie, die als Alternative zur arbeitet [SQL Server-Authentifizierung](../../connect/php/how-to-connect-using-sql-server-authentication.md). Azure AD ermöglicht Verbindungen mit Microsoft Azure SQL-Datenbank und SQL Data Warehouse mit verbundenen Identitäten in Azure AD mit einem Benutzernamen und Kennwort, integrierte Windows-Authentifizierung oder eine Azure AD-Zugriffstokens; die PHP-Treiber für SQL Server bieten teilweise Unterstützung für diese Funktionen.

Um Azure AD verwenden, verwenden die **Authentifizierung** Schlüsselwort. Die Werte, die **Authentifizierung** dauert auf, werden in der folgenden Tabelle erläutert.

|Schlüsselwort|Werte|Description|
|-|-|-|
|**Authentifizierung**|Nicht festgelegt ist (Standardeinstellung)|Der Authentifizierungsmodus durch andere Schlüsselwörter bestimmt. Weitere Informationen finden Sie unter [Connection Options](../../connect/php/connection-options.md). |
||`SqlPassword`|Authentifizierung direkt mit einer SQL Server-Instanz (die eine Azure-Instanz sein kann) mit einem Benutzernamen und Kennwort. Benutzername und Kennwort in die Verbindungszeichenfolge mithilfe übergeben werden müssen die **UID** und **PWD** Schlüsselwörter. |
||`ActiveDirectoryPassword`|Mit einer Azure Active Directory-Identität mit einem Benutzernamen und Kennwort zu authentifizieren. Benutzername und Kennwort in die Verbindungszeichenfolge mithilfe übergeben werden müssen die **UID** und **PWD** Schlüsselwörter. |

Die **Authentifizierung** Schlüsselwort wirkt sich auf die verbindungssicherheitseinstellungen. Wenn sie in der Verbindungszeichenfolge aus, und klicken Sie dann in der Standardeinstellung festgelegt ist die **Encrypt** Schlüsselwort ist auf "true", damit die Clientanforderung Verschlüsselung wird festgelegt. Das Serverzertifikat wird darüber hinaus unabhängig von der verschlüsselungseinstellung überprüft werden, es sei denn, **"TrustServerCertificate"** festgelegt ist auf "true". Dies wird unterschieden, aus der alten und weniger sichere, Login-Methode, in dem das Serverzertifikat nicht überprüft wird, wenn die Verschlüsselung in der Verbindungszeichenfolge explizit angefordert wird.

Stellen Sie sicher, dass Sie installiert haben, vor der Verwendung von Azure AD mit der PHP-Treibern für SQL Server unter Windows, die [Microsoft Online Services-Anmeldeassistent](https://www.microsoft.com/download/details.aspx?id=41950) (nicht für Linux und MacOS erforderlich).

#### <a name="limitations"></a>Einschränkungen

Unter Windows, die zugrunde liegenden ODBC-Treiber unterstützt einen größeren Mehrwert für die **Authentifizierung** Schlüsselwort **ActiveDirectoryIntegrated**, aber die PHP-Treiber unterstützen diesen Wert auf jeder Plattform und daher auch Azure AD-Token-basierter Authentifizierung nicht unterstützt.

## <a name="example"></a>Beispiel

Im folgende Beispiel wird gezeigt, wie für die verbindungsherstellung **SqlPassword** und **ActiveDirectoryPassword**.

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = array( "UID"=>$myusername, "PWD"=>$mypassword, "Authentication"=>'SqlPassword' );

    $conn = sqlsrv_connect( $serverName, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=SqlPassword.\n";
        sqlsrv_close( $conn );
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = array( "Database"=>$azureDatabase, "UID"=>$azureUsername, "PWD"=>$azurePassword,
                             "Authentication"=>'ActiveDirectoryPassword' );

    $conn = sqlsrv_connect( $azureServer, $connectionInfo );
    if( $conn === false )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( sqlsrv_errors() );
    }
    else
    {
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        sqlsrv_close( $conn );
    }

    ?>
```

Im folgende Beispiel wird die genauso wie oben mit dem PDO_SQLSRV-Treiber.

```php
    <?php
    // First connect to a local SQL Server instance by setting Authentication to SqlPassword
    $serverName = "myserver.mydomain";

    $connectionInfo = "Database = $databaseName; Authentication = SqlPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $serverName ; $connectionInfo", $myusername, $mypassword );
        echo "Connected successfully with Authentication=SqlPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=SqlPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    // Now connect to an Azure SQL database by setting Authentication to ActiveDirectoryPassword
    $azureServer = "myazureserver.database.windows.net";
    $azureDatabase = "myazuredatabase";
    $azureUsername = "myuid";
    $azurePassword = "mypassword";
    $connectionInfo = "Database = $azureDatabase; Authentication = ActiveDirectoryPassword;";

    try
    {
        $conn = new PDO( "sqlsrv:server = $azureServer ; $connectionInfo", $azureUsername, $azurePassword );
        echo "Connected successfully with Authentication=ActiveDirectoryPassword.\n";
        $conn = null;
    }
    catch( PDOException $e )
    {
        echo "Could not connect with Authentication=ActiveDirectoryPassword.\n";
        print_r( $e->getMessage() );
        echo "\n";
    }

    ?>
```
## <a name="see-also"></a>Siehe auch  
[Mithilfe von Azure Active Directory mit dem ODBC-Treiber](https://docs.microsoft.com/en-us/sql/connect/odbc/using-azure-active-directory)
