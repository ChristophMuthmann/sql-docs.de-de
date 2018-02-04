---
title: Verwalten von SQLServer on Linux mit PowerShell | Microsoft Docs
description: "Dieses Thema enthält eine Übersicht über die Verwendung von PowerShell unter Windows mit SQL Server on Linux."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.workload: Inactive
ms.openlocfilehash: 0952e8ff950e6b440e963f3867ce74477334e74f
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Verwenden von PowerShell unter Windows zum Verwalten von SQLServer on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieses Thema enthält [SQL Server PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx) und führt Sie durch ein paar Beispiele zum mit SQL Server-2017 unter Linux verwenden. PowerShell-Unterstützung für SQL Server ist derzeit unter Windows verfügbar, damit Sie es verwenden können, wenn Sie einen Windows-Computer verfügen, der mit einer SQL Server-Remoteinstanz unter Linux eine Verbindung herstellen können.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Installieren Sie die neueste Version von SQL PowerShell unter Windows

[SQL PowerShell](https://msdn.microsoft.com/en-us/library/mt740629.aspx) unter Windows ist im Lieferumfang [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md). Bei der Arbeit mit SQL Server sollten Sie immer die neueste Version von SSMS und SQL PowerShell verwenden. Die neueste Version von SSMS wird laufend aktualisiert und optimiert und arbeitet zurzeit mit SQLServer 2017 on Linux. Zum Herunterladen und installieren Sie die neueste Version, finden Sie unter [Herunterladen von SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Um auf dem neuesten Stand zu bleiben, die neueste Version von SSMS werden Sie aufgefordert, wenn eine neue Version für den download verfügbaren vorhanden ist.

## <a name="before-you-begin"></a>Vorbereitungen

Lesen der [bekannte Probleme](sql-server-linux-release-notes.md) für SQLServer 2017 unter Linux.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>Starten Sie PowerShell, und importieren Sie die *Sqlserver* Modul

Beginnen wir mit PowerShell unter Windows wird gestartet. Öffnen einer *Eingabeaufforderung* auf Ihrem Windows-Computer, und geben **PowerShell** um eine neue Windows PowerShell-Sitzung zu starten.

```
PowerShell
```

SQL Server bietet ein Windows PowerShell-Modul, das mit dem Namen **SqlServer** , dass Sie zum Importieren von SQL Server-Komponenten (SQL Server-Anbieter und Cmdlets) in einem PowerShell-Umgebung oder dieses Skript verwenden können.

Kopieren Sie den unten stehenden Befehl an der PowerShell-Eingabeaufforderung Importieren der **SqlServer** -Modul in Ihrer aktuellen PowerShell-Sitzung:

```powershell
Import-Module SqlServer
```

Geben Sie den unten stehenden Befehl an der PowerShell-Eingabeaufforderung zu überprüfen, ob die **SqlServer** Modul ordnungsgemäß importiert wurde:

```powershell
Get-Module -Name SqlServer
```

PowerShell sollte etwa wie folgt anzeigen:

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     0.0        SqlServer
Manifest   20.0       SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>Herstellen einer Verbindung mit SQL Server und Abrufen der Serverinformationen

Wir verwenden von PowerShell unter Windows unter Linux die 2017 von SQL Server-Instanz herstellen und eine Reihe von Servereigenschaften anzuzeigen.

Kopieren Sie die nachfolgenden Befehle an der PowerShell-Eingabeaufforderung. Wenn Sie diese Befehle ausführen, sehen PowerShell:
- Anzeigen der *Windows PowerShell anmelden* Dialogfeld, das Sie zum Angeben der Anmeldeinformationen aufgefordert werden (*SQL-Benutzername* und *SQL-Kennwort*) zur Verbindung mit Ihrem SQL Server-2017 die Instanz unter Linux
- Laden Sie die SQL Server Management Objects (SMO)-assembly
- Erstellen Sie eine Instanz von der [Server](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.smo.server.aspx) Objekt
- Herstellen einer Verbindung mit der **Server** und einige Eigenschaften anzeigen

Denken Sie daran, ersetzen Sie  **\<Your_server_instance\>**  mit der IP-Adresse oder den Hostnamen Ihrer 2017 von SQL Server-Instanz unter Linux.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Load the SMO assembly and create a Server object
[System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SMO') | out-null
$server = New-Object ('Microsoft.SqlServer.Management.Smo.Server') $serverInstance

# Set credentials
$server.ConnectionContext.LoginSecure=$false
$server.ConnectionContext.set_Login($credential.UserName)
$server.ConnectionContext.set_SecurePassword($credential.Password)

# Connect to the Server and get a few properties
$server.Information | Select-Object Edition, HostPlatform, HostDistribution | Format-List
# done
```

PowerShell sollte ähnlich wie nachfolgend gezeigt Informationen anzuzeigen:

```
Edition          : Developer Edition (64-bit)
HostPlatform     : Linux
HostDistribution : Ubuntu
```
> [!NOTE]
> Wenn nichts für diese Werte angezeigt wird, konnte die Verbindung mit SQL Server-Zielinstanz wahrscheinlich nicht. Stellen Sie sicher, dass Sie dieselben Verbindungsinformationen für die Verbindung von SQL Server Management Studio verwenden können. Überprüfen Sie anschließend die [Empfehlungen zur Verbindungsproblembehandlung](sql-server-linux-troubleshooting-guide.md#connection).

## <a name="examine-sql-server-error-logs"></a>Überprüfen Sie die Fehlerprotokolle von SQL Server

Verwenden von PowerShell unter Windows Fehlerprotokolle untersuchen wir für Ihre 2017 von SQL Server-Instanz unter Linux verbinden. Wir verwenden ebenfalls die **Out GridView** -Cmdlet zum Anzeigen von Informationen aus den Fehler protokolliert, in einem Raster anzeigen.

Kopieren Sie die nachfolgenden Befehle an der PowerShell-Eingabeaufforderung. Sie möglicherweise einige Minuten ausgeführt. Diese Befehle führen die folgenden:
- Anzeigen der *Windows PowerShell anmelden* Dialogfeld, das Sie zum Angeben der Anmeldeinformationen aufgefordert werden (*SQL-Benutzername* und *SQL-Kennwort*) zur Verbindung mit Ihrem SQL Server-2017 die Instanz unter Linux
- Verwenden der **Get-SqlErrorLog** -Cmdlet zum Herstellen einer Verbindung mit der 2017 von SQL Server-Instanz unter Linux und Abrufen von Fehler protokolliert seit **gestern**
- Die Ausgabe an die **Out GridView** Cmdlet

Denken Sie daran, ersetzen Sie  **\<Your_server_instance\>**  mit der IP-Adresse oder den Hostnamen Ihrer 2017 von SQL Server-Instanz unter Linux.

```powershell
# Prompt for credentials to login into SQL Server
$serverInstance = "<your_server_instance>"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>Siehe auch
- [SQL Server-PowerShell](../relational-databases/scripting/sql-server-powershell.md)
