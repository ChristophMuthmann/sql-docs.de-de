---
title: Transparente Datenverschlüsselung für Azure SQL-Datenbank und Data Warehouse | Microsoft-Dokumentation
description: Eine Übersicht über die transparente Datenverschlüsselung für SQL-Datenbank und Data Warehouse. Das Dokument behandelt die Vorteile sowie die Optionen für die Konfiguration, einschließlich der von einem Dienst verwalteten transparenten Datenverschlüsselung und Bring Your Own Key.
keywords: ''
author: becczhang
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.component: security
ms.custom: ''
ms.workload: On Demand
ms.tgt_pltfrm: ''
ms.topic: article
ms.date: 04/10/2018
ms.author: rebeccaz
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: fd5186e4a069b76108ad0c8cd4e91497e618a195
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="transparent-data-encryption-for-sql-database-and-data-warehouse"></a>Transparente Datenverschlüsselung für SQL-Datenbank und Data Warehouse
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Die transparente Datenverschlüsselung unterstützt Maßnahmen zum Schutz von Azure SQL-Datenbank und Azure Data Warehouse vor schädlichen Aktivitäten. Sie führt die Verschlüsselung und Entschlüsselung der Datenbank sowie der ihr zugeordneten Sicherheitskopien und der Transaktionsprotokolle in Ruhephasen in Echtzeit durch, ohne Änderungen an der Anwendung zu erfordern.

Die transparente Datenverschlüsselung verschlüsselt den Speicher einer gesamten Datenbank mithilfe eines symmetrischen Schlüssels, der als Verschlüsselungsschlüssel für die Datenbank bezeichnet wird. Dieser Verschlüsselungsschlüssel für die Datenbank wird durch die Schutzvorrichtung der transparenten Datenverschlüsselung geschützt. Bei dieser Schutzvorrichtung handelt es sich entweder um ein von einem Dienst verwaltetes Zertifikat (von einem Dienst verwaltete transparente Datenverschlüsselung) oder um einen asymmetrischen Schlüssel, der in Azure Key Vault (Bring Your Own Key) gespeichert ist. Sie legen die Schutzvorrichtung für die transparente Datenverschlüsselung auf Serverebene fest. 

Beim Datenbankstart wird der Verschlüsselungsschlüssel der verschlüsselten Datenbank entschlüsselt und dann für die Entschlüsselung und erneute Verschlüsselung der Datenbankdateien im Prozess der SQL Server-Datenbank-Engine verwendet. Die transparente Datenverschlüsselung führt die E/A-Verschlüsselung und -Entschlüsselung der Daten auf Seitenebene durch. Jede Seite wird entschlüsselt, wenn sie in den Speicher gelesen wird, und dann verschlüsselt, bevor sie auf den Datenträger geschrieben wird. Eine allgemeine Beschreibung der transparenten Datenverschlüsselung finden Sie unter [Transparente Datenverschlüsselung](transparent-data-encryption.md).

SQL Server kann bei der Ausführung auf einem virtuellen Azure-Computer auch einen asymmetrischen Schlüssel aus Key Vault verwenden. Die Konfigurationsschritte unterscheiden sich von der Verwendung eines asymmetrischen Schlüssels in SQL-Datenbank. Weitere Informationen finden Sie unter [Erweiterbare Schlüsselverwaltung mit Azure Key Vault (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md).

## <a name="service-managed-transparent-data-encryption"></a>Transparente Datenverschlüsselung (von einem Dienst verwaltet)

In Azure sieht die Standardeinstellung für die transparente Datenverschlüsselung so aus, dass der Verschlüsselungsschlüssel der Datenbank durch ein integriertes Serverzertifikat geschützt ist. Das integrierte Serverzertifikat ist für jeden Server eindeutig. Wenn sich eine Datenbank in einer Georeplikationsbeziehung befindet, werden die primäre und die sekundäre Geodatenbank vom übergeordneten Serverschlüssel der primären Datenbank geschützt. Wenn zwei Datenbanken mit dem gleichen Server verbunden sind, verwenden sie das gleiche integrierte Zertifikat. Microsoft tauscht diese Zertifikate mindestens alle 90 Tage automatisch untereinander.

Microsoft verschiebt und verwaltet auch die Schlüssel nahtlos, die für die Georeplikation und Wiederherstellung benötigt werden. 

> [!IMPORTANT]
> Alle neu erstellten SQL-Datenbanken werden standardmäßig mithilfe der von einem Dienst verwalteten transparenten Datenverschlüsselung verschlüsselt. Datenbanken, die schon vor Mai 2017 vorhanden waren, und Datenbanken, die durch Wiederherstellung, Georeplikation und Datenbankkopie erstellt wurden, werden standardmäßig nicht verschlüsselt.
>

## <a name="bring-your-own-key"></a>Bring Your Own Key

Durch die Bring Your Own Key-Unterstützung können Sie Ihre Schlüssel für die transparente Datenverschlüsselung verwalten und steuern, wer zu welchem Zeitpunkt auf diese zugreifen kann. Key Vault, das cloudbasierte externe Schlüsselverwaltungssystem von Azure, ist der erste Schlüsselverwaltungsdienst, der in die transparente Datenverschlüsselung mit Bring Your Own Key-Unterstützung integriert ist. Durch die Bring Your Own Key-Unterstützung ist der Verschlüsselungsschlüssel der Datenbank durch einen asymmetrischen Schlüssel geschützt, der in Key Vault gespeichert ist. Der asymmetrische Schlüssel verlässt Key Vault nie. Sobald der Server Berechtigungen für einen Schlüsseltresor besitzt, sendet er grundlegende Anforderungen für Schlüsselvorgänge über Key Vault an den Schlüsseltresor. Der asymmetrische Schlüssel ist auf Serverebene festgelegt und wird von allen Datenbanken unter diesem Server geerbt.

Durch die Bring Your Own Key-Unterstützung können Sie die Aufgaben der Schlüsselverwaltung steuern, z.B. Schlüsselrotationen und Schlüsseltresorberechtigungen. Sie können ebenfalls Schlüssel löschen sowie die Überwachung und Berichterstellung für alle Verschlüsselungsschlüssel aktivieren. Key Vault bietet eine zentrale Schlüsselverwaltung und verwendet stark überwachte Hardwaresicherheitsmodule. Key Vault unterstützt die Trennung der Verwaltung von Schlüsseln und Daten, um gesetzliche Bestimmungen zu erfüllen. Weitere Informationen zu Key Vault finden Sie in der [Dokumentation zu Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).

Weitere Informationen zur transparenten Datenverschlüsselung mit Bring Your Own Key-Unterstützung für SQL-Datenbank und Data Warehouse finden Sie unter [Transparent data encryption with Bring Your Own Key support (Transparente Datenverschlüsselung mit Bring Your Own Key-Unterstützung)](transparent-data-encryption-byok-azure-sql.md).

Weitere Informationen zur Verwendung der transparenten Datenverschlüsselung mit Bring Your Own Key-Unterstützung beginnen möchten finden Sie in diesem Leitfaden zur Vorgehensweise [Turn on transparent data encryption by using your own key from Key Vault by using PowerShell (Aktivieren der transparenten Datenverschlüsselung mithilfe Ihres eigenen Schlüssels aus Key Vault mit PowerShell)](transparent-data-encryption-byok-azure-sql-configure.md).

## <a name="move-a-transparent-data-encryption-protected-database"></a>Verschieben einer durch die transparente Datenverschlüsselung gesicherte Datenbank

Für Vorgänge in Azure müssen Datenbanken nicht entschlüsselt werden. Die Einstellungen der transparenten Datenverschlüsselung für die Quelldatenbank oder die primäre Datenbank werden transparent an das Ziel vererbt. Folgende Vorgänge sind enthalten:
- Geowiederherstellung
- Self-Service-Point-In-Time-Wiederherstellung
- Wiederherstellung einer gelöschten Datenbank
- Aktive Georeplikation
- Erstellung einer Datenbankkopie

Wenn Sie eine Datenbank exportieren, die mit der transparenten Datenverschlüsselung gesichert ist, werden die exportierten Inhalte der Datenbank nicht verschlüsselt. Diese exportierten Inhalte werden in unverschlüsselten BACPAC-Dateien gespeichert. Achten Sie darauf, die BACPAC-Dateien entsprechend zu schützen, und aktivieren Sie die transparente Datenverschlüsselung, nachdem der Import der neuen Datenbank abgeschlossen ist.

Wenn die BACPAC-Datei z.B. von einer lokalen Instanz von SQL Server exportiert wird, erfolgt keine automatische Verschlüsselung des importierten Inhalts der neuen Datenbank. Wenn die BACPAC-Datei auf eine lokale Instanz von SQL Server exportiert wird, erfolgt ebenfalls keine automatische Verschlüsselung der neuen Datenbank.

Eine Ausnahme besteht im Exportieren nach und aus SQL-Datenbank. Die transparente Datenverschlüsselung ist in der neuen Datenbank aktiviert, die BACPAC-Datei ist jedoch nicht verschlüsselt.

## <a name="manage-transparent-data-encryption-in-the-azure-portal"></a>Verwalten der transparenten Datenverschlüsselung im Azure-Portal

Sie müssen eine Verbindung als Azure-Besitzer, Azure-Mitwirkender oder SQL-Sicherheitsmanager herstellen, um die transparente Datenverschlüsselung über das Azure-Portal zu konfigurieren. 

Die transparente Datenverschlüsselung wird auf Datenbankebene festgelegt. Besuchen Sie das [Azure-Portal](https://portal.azure.com), und melden Sie sich mit Ihrem Azure-Administrator- oder Mitwirkendenkonto an, um die transparente Datenverschlüsselung auf einer Datenbank zu aktivieren. Suchen Sie die Einstellungen für die transparente Datenverschlüsselung in Ihrer Benutzerdatenbank. Standardmäßig wird die von einem Dienst verwaltete transparente Datenverschlüsselung verwendet. Für den Server, der die Datenbank enthält, wird automatisch ein Zertifikat für die transparente Datenverschlüsselung generiert. 

![Transparente Datenverschlüsselung (von einem Dienst verwaltet)](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

Der Hauptschlüssel für die transparente Datenverschlüsselung, der auch als Schutzvorrichtung für die transparente Datenverschlüsselung bezeichnet wird, wird auf Serverebene festgelegt. Verwenden Sie die Einstellungen für die transparente Datenverschlüsselung auf Ihrem Server, um diese mit Bring Your Own Key-Unterstützung zu verwenden und Ihre Datenbank mit einem Schlüssel von Key Vault zu schützen. 

![Transparente Datenverschlüsselung mit Bring Your Own Key-Unterstützung](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="manage-transparent-data-encryption-by-using-powershell"></a>Verwalten der transparenten Datenverschlüsselung mithilfe von PowerShell

Sie müssen eine Verbindung als Azure-Besitzer, Azure-Mitwirkender oder SQL-Sicherheitsmanager herstellen, um die transparente Datenverschlüsselung über PowerShell zu konfigurieren. 

| Cmdlet | Description |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |Aktiviert oder deaktiviert die transparente Datenverschlüsselung für eine Datenbank|
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |Ruft den Status der transparenten Datenverschlüsselung für eine Datenbank ab |
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption-Activity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |Überprüft den Verschlüsselungsfortschritt für eine Datenbank |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |Fügt einer Instanz von SQL Server einen Key Vault-Schlüssel hinzu |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |Ruft die Key Vault-Schlüssel für eine Instanz von SQL Server ab  |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |Legt die Schutzvorrichtung der transparenten Datenverschlüsselung für eine Instanz von SQL Server fest |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |Ruft die Schutzvorrichtung für die transparente Datenverschlüsselung ab |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |Entfernt einen Key Vault-Schlüssel aus einer Instanz von SQL Server |
|  | |

## <a name="manage-transparent-data-encryption-by-using-transact-sql"></a>Verwalten der transparenten Datenverschlüsselung mithilfe von Transact-SQL

Stellen Sie eine Verbindung mit der Datenbank mithilfe eines Kontos her, das ein Administratorkonto oder ein Mitglied der Rolle **dbmanager** in der Masterdatenbank ist.

| Befehl | Description |
| --- | --- |
| [ALTER DATABASE (Azure SQL-Datenbank)](/sql/t-sql/statements/alter-database-azure-sql-database) | Durch SET ENCRYPTION ON/OFF wird eine Datenbank verschlüsselt oder entschlüsselt |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |Gibt Informationen über den Verschlüsselungsstatus einer Datenbank und die ihr zugeordneten Verschlüsselungsschlüssel zurück |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |Gibt Informationen über den Verschlüsselungsstatus jedes Data Warehouse-Knotens und die ihm zugeordneten Verschlüsselungsschlüssel der Datenbank zurück | 
|  | |

Sie können die Schutzvorrichtung der transparenten Datenverschlüsselung mithilfe von Transact-SQL nicht durch einen Schlüssel von Key Vault ersetzen. Verwenden Sie PowerShell oder das Azure-Portal.

## <a name="manage-transparent-data-encryption-by-using-the-rest-api"></a>Verwalten der transparenten Datenverschlüsselung mithilfe der REST-API
 
Sie müssen eine Verbindung als Azure-Besitzer, Azure-Mitwirkender oder SQL-Sicherheitsmanager herstellen, um die transparente Datenverschlüsselung über die REST-API zu konfigurieren. 

| Befehl | Description |
| --- | --- |
|[Server erstellen oder aktualisieren](/rest/api/sql/servers/createorupdate)|Fügt eine Azure Active Directory-Identität zu einer Instanz von SQL Server hinzu, die für den Zugriff auf Key Vault verwendet wird|
|[Serverschlüssel erstellen oder aktualisieren](/rest/api/sql/serverkeys/createorupdate)|Fügt einer Instanz von SQL Server einen Key Vault-Schlüssel hinzu|
|[Serverschlüssel entfernen](/rest/api/sql/serverkeys/delete)|Entfernt einen Key Vault-Schlüssel aus einer Instanz von SQL Server|
|[Serverschlüssel abrufen](/rest/api/sql/serverkeys/get)|Ruft einen bestimmten Key Vault-Schlüssel aus einer Instanz von SQL Server ab|
|[Serverschlüssel nach Server auflisten](/rest/api/sql/serverkeys/listbyserver)|Ruft die Key Vault-Schlüssel für eine Instanz von SQL Server ab |
|[Transparent Data Encryption-Schutzvorrichtung erstellen oder aktualisieren](/rest/api/sql/encryptionprotectors/createorupdate)|Legt die Schutzvorrichtung der transparenten Datenverschlüsselung für eine Instanz von SQL Server fest|
|[Transparent Data Encryption-Schutzvorrichtung abrufen](/rest/api/sql/encryptionprotectors/get)|Ruft die Schutzvorrichtung der transparenten Datenverschlüsselung für eine Instanz von SQL Server ab|
|[Transparent Data Encryption-Schutzvorrichtung nach Server auflisten](/rest/api/sql/encryptionprotectors/listbyserver)|Ruft die Schutzvorrichtungen der transparenten Datenverschlüsselung für eine Instanz von SQL Server ab |
|[Transparent Data Encryption-Konfiguration erstellen oder aktualisieren](/rest/api/sql/transparentdataencryptions/createorupdate)|Aktiviert oder deaktiviert die transparente Datenverschlüsselung für eine Datenbank|
|[Transparent Data Encryption-Konfiguration abrufen](/rest/api/sql/transparentdataencryptions/get)|Ruft die Konfiguration der transparenten Datenverschlüsselung für eine Datenbank ab|
|[Ergebnisse der Transparent Data Encryption-Konfiguration auflisten](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|Ruft das Verschlüsselungsergebnis für eine Datenbank ab|

## <a name="next-steps"></a>Nächste Schritte

- Eine allgemeine Beschreibung der transparenten Datenverschlüsselung finden Sie unter [Transparente Datenverschlüsselung](transparent-data-encryption.md).
- Weitere Informationen zur transparenten Datenverschlüsselung mit Bring Your Own Key-Unterstützung für SQL-Datenbank und Data Warehouse finden Sie unter [Transparent data encryption with Bring Your Own Key support (Transparente Datenverschlüsselung mit Bring Your Own Key-Unterstützung)](transparent-data-encryption-byok-azure-sql.md).
- Weitere Informationen zur Verwendung der transparenten Datenverschlüsselung mit Bring Your Own Key-Unterstützung finden Sie in folgendem Leitfaden zur Vorgehensweise: [Turn on transparent data encryption by using your own key from Key Vault by using PowerShell (Aktivieren der transparenten Datenverschlüsselung mithilfe Ihres eigenen Schlüssels aus Key Vault mit PowerShell)](transparent-data-encryption-byok-azure-sql-configure.md).
- Weitere Informationen zu Key Vault finden Sie in der [Key Vault-Dokumentation](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).
