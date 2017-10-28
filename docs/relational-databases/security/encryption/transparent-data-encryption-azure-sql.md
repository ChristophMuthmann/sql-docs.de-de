---
title: "TDE für Azure SQL-Datenbank und Data Warehouse | Microsoft Docs"
description: "Eine Übersicht über Transparent Data Encryption für SQL-Datenbank und Data Warehouse. Das Dokument behandelt die Vorteile sowie die Optionen für die Konfiguration, einschließlich die vom Dienst verwaltete TDE-Technologie und Bring Your Own Key."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: 35c94a39989fda76ea023588b2d7a3aa4e463262
ms.contentlocale: de-de
ms.lasthandoff: 09/05/2017

---


# <a name="transparent-data-encryption-for-azure-sql-database-and-data-warehouse"></a>Transparent Data Encryption für Azure SQL-Datenbank und Data Warehouse

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Transparent Data Encryption (TDE) unterstützt Maßnahmen zum Schutz von Azure SQL-Datenbank und Data Warehouse vor bösartigen Aktivitäten, indem die Technologie die Verschlüsselung und Entschlüsselung der Datenbank in Echtzeit sowie der ihr zugeordneten Sicherheitskopien und der Transaktionsprotokolle in Ruhephasen vornimmt, ohne Änderungen an der Anwendung zu erfordern.

TDE verschlüsselt den Speicher einer gesamten Datenbank mithilfe eines symmetrischen Schlüssels, der als Verschlüsselungsschlüssel für die Datenbank (DEK) bezeichnet wird. Dieser Verschlüsselungsschlüssel für die Datenbank wird durch die TDE-Schutzvorrichtung geschützt, die entweder ein vom Dienst verwaltetes Zertifikat („Vom Dienst verwaltete TDE“) oder ein asymmetrischer Schlüssel sein kann, der in Azure Key Vault („Bring Your Own Key“) gespeichert ist. Die TDE-Schutzvorrichtung ist auf Serverebene festgelegt. 

Beim Datenbankstart wird der verschlüsselte DEK entschlüsselt und dann für die Entschlüsselung und erneute Verschlüsselung der Datenbankdateien im SQL Engine-Prozess verwendet. Die TDE führt die E/A-Verschlüsselung und -Entschlüsselung der Daten und auf Seitenebene durch. Jede Seite wird entschlüsselt, wenn sie in den Speicher gelesen wird und verschlüsselt, bevor Sie auf den Datenträger geschrieben wird. Eine allgemeine Beschreibung von TDE finden Sie unter [Transparente Datenverschlüsselung (TDE)](transparent-data-encryption.md).

SQL Server kann bei der Ausführung auf einem virtuellen Azure-Computer auch einen asymmetrischen Schlüssel aus Key Vault verwenden. Die Konfigurationsschritte unterscheiden sich von der Verwendung eines asymmetrischen Schlüssels in Azure SQL-Datenbank. Weitere Informationen finden Sie im Thema [Erweiterbare Schlüsselverwaltung mit Azure Key Vault (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md).

## <a name="service-managed-tde"></a>Vom Dienst verwaltete TDE

In Azure sieht die Standardeinstellung für TDE so aus, dass der Datenbank-Verschlüsselungsschlüssel durch ein integriertes Serverzertifikat geschützt ist. Das integrierte Serverzertifikat ist für jeden Server eindeutig. Wenn sich eine Datenbank in einer Georeplikationsbeziehung befindet, werden die primäre und die sekundäre Geodatenbank vom übergeordneten Serverschlüssel der primären Datenbank geschützt. Wenn zwei Datenbanken mit dem gleichen Server verbunden sind, verwenden sie das gleiche integrierte Zertifikat. Microsoft tauscht diese Zertifikate mindestens alle 90 Tage automatisch untereinander.

Microsoft verschiebt und verwaltet auch nahtlos die Schlüssel, die für die Georeplikation und Wiederherstellung benötigt werden. 

> [!IMPORTANT]
> Alle neu erstellten SQL-Datenbanken werden standardmäßig mithilfe der vom Dienst verwalteten TDE verschlüsselt. Datenbanken, die schon vor Mai 2017 existiert haben, und Datenbanken, die durch Wiederherstellung, Georeplikation und Datenbankkopie erstellt wurden, werden nicht standardmäßig verschlüsselt.
>

## <a name="bring-your-own-key"></a>Bring Your Own Key

Die Unterstützung von Bring Your Own Key (BYOK) erlaubt dem Benutzer, Kontrolle über seine TDE-Verschlüsselungsschlüssel zu übernehmen und darüber, wer auf diese zugreifen kann und zu welchem Zeitpunkt. Azure Key Vault (AKV), das cloudbasierte externe Schlüsselverwaltungssystem von Azure, ist der erste Schlüsselverwaltungsdienst, der in TDE mit BYOK-Unterstützung integriert ist. Mit BYOK ist der Datenbankverschlüsselungsschlüssel durch einen asymmetrischen Schlüssel geschützt, der in AKV gespeichert ist. Der asymmetrische Schlüssel verlässt Key Vault nie. Sobald der Server Berechtigungen für einen Schlüsseltresor besitzt, sendet er grundlegende Schlüsselvorgangsanforderungen über den Key Vault-Dienst an den Schlüsseltresor. Der asymmetrische Schlüssel ist auf Serverebene festgelegt und wird von allen Datenbanken unter diesem Server geerbt. Mit der BYOK-Unterstützung können Benutzer nun Schlüsselverwaltungsaufgaben steuern, einschließlich Schlüsselrotationen, Schlüsseltresorberechtigungen, das Löschen von Schlüsseln und Aktivieren der Überwachung/Berichterstellung auf allen Verschlüsselungsschlüsseln. Key Vault bietet eine zentrale Schlüsselverwaltung, nutzt die streng überwachten Hardwaresicherheitsmodule (HSMs) und stuft die Trennung der Verwaltung von Schlüsseln und Daten höher, damit die rechtliche Kompatibilität eingehalten werden kann. Weitere Informationen über Key Vault finden Sie auf der [Dokumentationsseite für Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).

Weitere Informationen über TDE mit BYOK-Unterstützung für Azure SQL-Datenbank und Data Warehouse finden Sie unter [Transparent Data Encryption with Bring Your Own Key support (Transparent Data Encryption mit Bring Your Own Key-Unterstützung)](transparent-data-encryption-byok-azure-sql.md).

Wenn Sie mit der Verwendung von TDE mit BYOK-Unterstützung beginnen möchten, sehen Sie sich den Leitfaden zur Vorgehensweise, [Turn on Transparent Data Encryption using your own key from Key Vault Using PowerShell (Aktivieren von Transparent Data Encryption mithilfe Ihres eigenen Schlüssels aus Key Vault mit PowerShell)](transparent-data-encryption-byok-azure-sql-configure.md), an.

## <a name="moving-a-tde-protected-database"></a>Verschieben einer TDE-geschützten Datenbank

Für Vorgänge in Azure brauchen Datenbanken nicht entschlüsselt zu werden. Die TDE-Einstellungen für die Quelldatenbank oder die primäre Datenbank werden transparent an das Ziel vererbt. Dazu gehören auch Vorgänge, die dieses beinhalten:
- Geowiederherstellung
- Self-Service-Point-In-Time-Wiederherstellung
- Wiederherstellung einer gelöschten Datenbank
- Aktive Georeplikation
- Erstellen einer Datenbankkopie

Wenn Sie eine TDE-geschützte Datenbank exportieren, wird der exportierte Inhalt der Datenbank nicht verschlüsselt. Diese exportierten Inhalte werden in unverschlüsselten BACPAC-Dateien gespeichert. Achten Sie darauf, die BACPAC-Dateien in geeigneter Weise zu schützen und TDE zu aktivieren, sobald der Import der neuen Datenbank abgeschlossen ist.

Wenn die BACPAC-Datei z.B. von einem lokalen SQL-Server exportiert wird, erfolgt keine automatische Verschlüsselung des importierten Inhalts der neuen Datenbank. Wenn die BACPAC-Datei auf einen lokalen SQL-Server exportiert wird, erfolgt ebenfalls keine automatische Verschlüsselung der neuen Datenbank.

Eine Ausnahme ist das Exportieren zu und aus Azure SQL-Datenbank. TDE ist in der neuen Datenbank aktiviert, jedoch ist die BACPAC-Datei selbst noch nicht verschlüsselt.

## <a name="managing-transparent-data-encryption-in-the-azure-portal"></a>Verwalten von Transparent Data Encryption im Azure-Portal

Um TDE über das Azure-Portal zu konfigurieren, müssen Sie als Azure-Besitzer, Azure-Mitwirkender oder SQL-Sicherheitsmanager verbunden sein. 

Transparent Data Encryption wird auf Datenbankebene festgelegt. Um TDE auf einer Datenbank zu aktivieren, besuchen Sie das [Azure-Portal](https://portal.azure.com), und melden Sie sich mit Ihrem Azure-Administrator- oder Mitwirkendenkonto an. Suchen Sie die TDE-Einstellungen in Ihrer Benutzerdatenbank. Standardmäßig wird die vom Dienst verwaltete TDE verwendet, und ein TDE-Zertifikat wird automatisch für den Server erstellt, der die Datenbank enthält. 

![vom Dienst verwaltete TDE](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

Der TDE-Hauptschlüssel, der auch als *TDE-Schutzvorrichtung* bezeichnet wird, wird auf Serverebene festgelegt. Besuchen Sie die TDE-Einstellungen in Ihrem Server, um TDE mit der Bring Your Own Key-Unterstützung zu verwenden und um Ihre Datenbanken mit einem Schlüssel aus Azure Key Vault zu schützen. 

![TDE mit BYOK-Unterstützung](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="managing-transparent-data-encryption-using-powershell"></a>Verwalten von Transparent Data Encryption mithilfe von PowerShell

Um TDE über PowerShell zu konfigurieren, müssen Sie als Azure-Besitzer, Azure-Mitwirkender oder SQL-Sicherheitsmanager verbunden sein. 

| Cmdlet | Description |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |Aktiviert oder deaktiviert TDE für eine Datenbank|
| [Get-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |Ruft den TDE-Status für eine Datenbank ab |
| [Get-AzureRmSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |Überprüft den Verschlüsselungsfortschritt für eine Datenbank |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |Fügt einem SQL-Server einen Key Vault-Schlüssel hinzu |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |Ruft die Key Vault-Schlüssel eines SQL-Servers ab |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |Legt die TDE-Schutzvorrichtung für einen SQL-Server fest |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |Ruft die Transparent Data Encryption-Schutzvorrichtung ab |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |Entfernt einen Key Vault-Schlüssel aus einem SQL-Server |
|  | |

## <a name="managing-transparent-data-encryption-using-transact-sql"></a>Verwalten von Transparent Data Encryption mithilfe von Transact-SQL

Stellen Sie eine Verbindung mit der Datenbank mithilfe eines Kontos her, das ein Administratorkonto oder ein Mitglied der Rolle **dbmanager** in der Masterdatenbank ist.

| Befehl | Description |
| --- | --- |
| [ALTER DATABASE (Azure SQL-Datenbank)](/sql/t-sql/statements/alter-database-azure-sql-database) | Verwenden Sie „SET ENCRYPTION ON/OFF“, um eine Datenbank zu verschlüsseln oder zu entschlüsseln. |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |Gibt Informationen über den Verschlüsselungsstatus einer Datenbank und die ihr zugeordneten Verschlüsselungsschlüssel für die Datenbank zurück. |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |Gibt Informationen über den Verschlüsselungsstatus jedes Data Warehouse-Knotens und die ihm zugeordneten Verschlüsselungsschlüssel für die Datenbank zurück. | 
|  | |

Die TDE-Schutzvorrichtung kann nicht mithilfe von Transact-SQL auf einen Schlüssel aus Azure Key Vault geändert werden; verwenden Sie PowerShell oder das Azure-Portal.

## <a name="managing-transparent-data-encryption-using-rest-api"></a>Verwalten von Transparent Data Encryption mithilfe von REST API
 
Um TDE über REST-API zu konfigurieren, müssen Sie als Azure-Besitzer, Azure-Mitwirkender oder SQL-Sicherheitsmanager verbunden sein. 

| Befehl | Description |
| --- | --- |
|[Server erstellen oder aktualisieren](/rest/api/sql/servers/createorupdate)|Fügt einem SQL-Server eine AAD-Identität hinzu (wird verwendet, um Zugriff auf Key Vault zu gewähren)|
|[Serverschlüssel erstellen oder aktualisieren](/rest/api/sql/serverkeys/createorupdate)|Fügt einem SQL-Server einen Key Vault-Schlüssel hinzu|
|[Serverschlüssel entfernen](/rest/api/sql/serverkeys/delete)|Entfernt einen Key Vault-Schlüssel aus einem SQL-Server|
|[Serverschlüssel abrufen](/rest/api/sql/serverkeys/get)|Ruft einen bestimmten Key Vault-Schlüssel aus einem SQL-Server ab|
|[Serverschlüssel nach Server auflisten](/rest/api/sql/serverkeys/listbyserver)|Ruft die Key Vault-Schlüssel eines SQL-Servers ab|
|[Transparent Data Encryption-Schutzvorrichtung erstellen oder aktualisieren](/rest/api/sql/encryptionprotectors/createorupdate)|Legt die TDE-Schutzvorrichtung für einen SQL-Server fest|
|[Transparent Data Encryption-Schutzvorrichtung abrufen](/rest/api/sql/encryptionprotectors/get)|Ruft die TDE-Schutzvorrichtung für einen SQL-Server ab|
|[Transparent Data Encryption-Schutzvorrichtung nach Server auflisten](/rest/api/sql/encryptionprotectors/listbyserver)|Ruft die TDE-Schutzvorrichtung eines SQL-Servers auf|
|[Transparent Data Encryption-Konfiguration erstellen oder aktualisieren](/rest/api/sql/transparentdataencryptions/createorupdate)|Aktiviert oder deaktiviert TDE für eine Datenbank|
|[Transparent Data Encryption-Konfiguration abrufen](/rest/api/sql/transparentdataencryptions/get)|Ruft die TDE-Konfiguration für eine Datenbank ab.|
|[Ergebnisse der Transparent Data Encryption-Konfiguration auflisten](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|Ruft das Verschlüsselungsergebnis für eine Datenbank ab|

## <a name="next-steps"></a>Nächste Schritte

- Eine allgemeine Beschreibung von TDE finden Sie unter [Transparente Datenverschlüsselung (TDE)](transparent-data-encryption.md).

- Weitere Informationen über TDE mit BYOK-Unterstützung für Azure SQL-Datenbank und Data Warehouse finden Sie unter [Transparent Data Encryption with Bring Your Own Key support (Transparent Data Encryption mit Bring Your Own Key-Unterstützung)](transparent-data-encryption-byok-azure-sql.md).

- Wenn Sie mit der Verwendung von TDE mit BYOK-Unterstützung beginnen möchten, sehen Sie sich den Leitfaden zur Vorgehensweise, [Turn on Transparent Data Encryption using your own key from Key Vault Using PowerShell (Aktivieren von Transparent Data Encryption mithilfe Ihres eigenen Schlüssels aus Key Vault mit PowerShell)](transparent-data-encryption-byok-azure-sql-configure.md), an.

- Weitere Informationen zu Key Vault finden Sie auf den [Seiten der Key Vault-Dokumentation](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).

