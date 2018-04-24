---
title: Konfigurieren von Always Encrypted mithilfe von PowerShell | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 57b85f77c6ad119495f1738aada84b069288cae5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configure-always-encrypted-using-powershell"></a>Konfigurieren von Always Encrypted mithilfe von PowerShell
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Das PowerShell-Modul für SQL Server namens „SqlServer“ stellt Cmdlets bereit, mit denen Sie [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) sowohl in Azure SQL-Datenbank als auch in SQL Server 2016 konfigurieren können.

Always Encrypted-Cmdlets im SqlServer-Modul arbeiten mit Schlüsseln oder sensiblen Daten. Daher ist es wichtig, dass Sie die Cmdlets auf einem sicheren Computer ausführen. Führen Sie die Cmdlets bei der Verwaltung von Always Encrypted von einem anderen Computer als dem Computer aus, er Ihre SQL Server-Instanz hostet.

Der primäre Zweck von Always Encrypted ist, sicherzustellen, dass verschlüsselte sensible Daten sicher sind, wenn das Datenbanksystem kompromittiert wird. Daher kann das Ausführen eines PowerShell-Skripts, das Schlüssel oder sensible Daten auf dem SQL Server-Computer verarbeitet, die Vorteile der Funktion einschränken oder zunichte machen. Weitere Empfehlungen zum Thema Sicherheit finden Sie unter [Security Considerations for Key Management](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)(Überlegungen zur Verwaltung von Schlüsseln).

Links zu einzelnen Artikeln über Cmdlets finden Sie [unten auf dieser Seite](#aecmdletreference).

## <a name="prerequisites"></a>Voraussetzungen

Installieren Sie das [SqlServer-Modul](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/sqlserver) auf einem sicheren Computer, der NICHT der Hostcomputer Ihrer SQL Server-Instanz ist. Das Modul kann direkt aus dem PowerShell-Katalog installiert werden.  In den [Downloadanweisungen](../../../ssms/download-sql-server-ps-module.md) finden Sie weitere Informationen.


## <a name="importsqlservermodule"></a> Importieren des SqlServer-Moduls 

So laden Sie das SqlServer-Modul:

1.  Verwenden Sie das Cmdlet **Set-ExecutionPolicy** , um die entsprechende Skriptausführungsrichtlinie festzulegen.
2.  Verwenden Sie das Cmdlet **Import-Module** zum Importieren des SqlServer-Moduls.

In diesem Beispiel wird das SqlServer-Modul geladen.

```
# Import the SQL Server Module.  
Import-Module "SqlServer" 
```

## <a name="connectingtodatabase"></a> Herstellen einer Verbindung mit einer Datenbank

Einige der Always Encrypted-Cmdlets arbeiten mit Daten oder Metadaten in der Datenbank und erfordern, dass Sie zuerst eine Verbindung mit der Datenbank herstellen. Es werden zwei Methoden empfohlen, um bei der Konfiguration von Always Encrypted mithilfe des SqlServer-Moduls eine Verbindung mit einer Datenbank herzustellen: 
1. Verbinden mithilfe von SQL Server PowerShell
2. Verbinden mithilfe von SQL Server Management Objects (SMO)

### <a name="using-sql-server-powershell"></a>SQL Server PowerShell

Diese Methode funktioniert nur für SQL Server, d.h. dass sie in Azure SQL-Datenbank nicht unterstützt wird.

Sie können mit SQL Server PowerShell in den Pfaden navigieren, indem Sie Windows PowerShell-Aliase ähnlich den Befehlen verwenden, die Sie normalerweise zum Navigieren in den Dateisystempfaden verwenden. Nachdem Sie zu der Zielinstanz und der Datenbank navigiert sind, richten sich die nachfolgenden Cmdlets an diese Datenbank, wie im folgenden Beispiel gezeigt:

```
# Import the SqlServer module.
Import-Module "SqlServer"
# Navigate to the database in the remote instance.
cd SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
# List column master keys in the above database.
Get-SqlColumnMasterKey
```

 
Alternativ können Sie einen Datenbankpfad mithilfe des allgemeinen **Path** -Parameters angeben, statt zur Datenbank zu navigieren.


```
# Import the SqlServer module.
Import-Module "SqlServer" 
# List column master keys for the specified database.
Get-SqlColumnMasterKey -Path SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
```
 
### <a name="using-smo"></a>Mithilfe von SQL Server Management Objects (SMO)

Diese Methode funktioniert sowohl für Azure SQL-Datenbank als auch für SQL Server.
Mit SMO können Sie ein Objekt der [Database-Klasse](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.database.aspx)erstellen und es anschließend mithilfe des **InputObject** -Parameters eines Cmdlets übergeben, das eine Verbindung mit der Datenbank herstellt.


```
# Import the SqlServer module
Import-Module "SqlServer"  

# Connect to your database (Azure SQL database).
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName] 

# List column master keys for the specified database.
Get-SqlColumnMasterKey -InputObject $database
```


Alternativ könnten Sie es auch pipegetrennt übergeben:


```
$database | Get-SqlColumnMasterKey
```

## <a name="always-encrypted-tasks-using-powershell"></a>Always Encrypted-Tasks mithilfe von PowerShell

- [Konfigurieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md) 
- [Rotieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Konfigurieren der Spaltenverschlüsselung mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md)


##  <a name="aecmdletreference"></a> Referenz zu Always Encrypted-Cmdlets

Die folgenden PowerShell-Cmdlets sind für Always Encrypted verfügbar:

|CMDLET |Description
|:---|:---
|**[Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)**   |Führt die Azure-Authentifizierung aus und ruft ein Authentifizierungstoken ab.
|**[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)**   |Fügt einen neuen verschlüsselten Wert für ein vorhandenes Spaltenverschlüsselungsschlüssel-Objekt in der Datenbank hinzu.
|**[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)**   |Schließt die Rotation eines Spaltenhauptschlüssels ab.
|**[Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)** |Gibt alle in der Datenbank definierten Spaltenverschlüsselungsschlüssel-Objekte zurück, oder gibt ein Spaltenverschlüsselungsschlüssel-Objekt mit dem angegebenen Namen zurück.
|**[Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey)** |Gibt die in der Datenbank definierten Spaltenhauptschlüssel-Objekte zurück, oder gibt ein Spaltenhauptschlüssel-Objekt mit dem angegebenen Namen zurück.
|**[Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation)**   |Initiiert die Rotation eines Spaltenhauptschlüssels.
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)**   |Erstellt ein SqlColumnMasterKeySettings-Objekt, das einen asymmetrischen Schlüssel beschreibt, der in Azure Key Vault gespeichert ist.
|**[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)**   |Erstellt ein SqlColumnMasterKeySettings-Objekt, das einen asymmetrischen Schlüssel beschreibt, der in einem Schlüsselspeicher gespeichert ist, der die Cryptography Next Generation-API (CNG) unterstützt.
|**[New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)** |Erstellt ein neues Spaltenverschlüsselungsschlüssel-Objekt in der Datenbank
|**[New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)** |Erstellt den verschlüsselten Wert eines Spaltenverschlüsselungsschlüssels.
|**[New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings)**   |Erstellt ein SqlColumnEncryptionSettings-Objekt, das Informationen über die Verschlüsselung einer einzelnen Spalte kapselt, einschließlich Spaltenverschlüsselungsschlüssel und Verschlüsselungstyp
|**[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)** |Erstellt ein Spaltenhauptschlüssel-Objekt in der Datenbank
|**[New-SqlColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkeysettings)**|Erstellt ein SqlColumnMasterKeySettings-Objekt für einen Spaltenhauptschlüssel mit dem angegebenen Anbieter und Schlüsselpfad
|**[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)**   |Erstellt ein SqlColumnMasterKeySettings-Objekt, das einen asymmetrischen Schlüssel beschreibt, das in einem Schlüsselspeicher mit einem Kryptografiedienstanbieter (cryptography service provider; CSP) gespeichert ist, der die Kryptografie-API (CAPI) unterstützt.
|**[Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey)**   |Entfernt das Spaltenverschlüsselungsschlüssel-Objekt aus der Datenbank.
|**[Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)** |Entfernt einen verschlüsselten Wert für ein vorhandenes Spaltenverschlüsselungsschlüssel-Objekt aus der Datenbank.
|**[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)**   |Entfernt das Spaltenhauptschlüssel-Objekt aus der Datenbank.
|**[Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)**   |Verschlüsselt, entschlüsselt oder verschlüsselt angegebene Spalten in der Datenbank erneut.



## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Always Encrypted (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Overview of Key Management for Always Encrypted (Übersicht über die Schlüsselverwaltung für Always Encrypted)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Verwenden von Always Encrypted mit .NET Framework-Datenanbieter für SQL Server:](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [Konfigurieren von Always Encrypted mithilfe von SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)


