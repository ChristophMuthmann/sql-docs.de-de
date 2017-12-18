---
title: "TDE: Bring Your Own Key (BYOK) – Azure SQL | Microsoft-Dokumentation"
description: "BYOK-Unterstützung (Bring Your Own Key) für Transparent Data Encryption (TDE) mit Azure Key Vault für SQL-Datenbank und Data Warehouse. TDE mit BYOK: Überblick, Funktionsweise, Überlegungen und Empfehlungen."
keywords: 
services: sql-database
documentationcenter: 
author: aliceku
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: aliceku
ms.openlocfilehash: 5a0b56974d85f63e3382f26b1388e7d30dfbd6f8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>Transparent Data Encryption mit Bring Your Own Key-Unterstützung für Azure SQL-Datenbank und Data Warehouse
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Die Unterstützung von BYOK für [Transparent Data Encryption (TDE)](transparent-data-encryption.md) erlaubt Ihnen, die Kontrolle über Ihre TDE-Verschlüsselungsschlüssel zu übernehmen und einzuschränken, wer auf diese zugreifen kann und zu welchem Zeitpunkt. [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), das cloudbasierte externe Schlüsselverwaltungssystem von Azure, ist der erste Schlüsselverwaltungsdienst, bei dem die BYOK-Unterstützung in TDE integriert ist. Mit BYOK ist der Datenbank-Verschlüsselungsschlüssel durch einen asymmetrischen Schlüssel geschützt, der in Key Vault gespeichert ist. Der asymmetrische Schlüssel ist auf Serverebene festgelegt und wird von allen Datenbanken unter diesem Server geerbt. 

Mit der BYOK-Unterstützung können Benutzer nun Schlüsselverwaltungsaufgaben steuern, einschließlich Schlüsselrotationen, Schlüsseltresorberechtigungen, das Löschen von Schlüsseln und Aktivieren der Überwachung/Berichterstellung auf allen Verschlüsselungsschlüsseln. Key Vault bietet eine zentrale Schlüsselverwaltung, nutzt die streng überwachten Hardwaresicherheitsmodule (HSMs) und ermöglicht die Trennung der Pflichten zwischen dem Verwalten von Schlüsseln und Daten, um gesetzliche Bestimmungen einzuhalten. 

TDE mit BYOK bietet folgende Vorteile:
- Erhöhte Transparenz und eine präzise Steuerung mit der Möglichkeit, die TDE-Schutzvorrichtung selbst zu verwalten   
- Zentrale Verwaltung der TDE-Verschlüsselungsschlüssel (zusammen mit anderen Schlüsseln und Geheimnissen, die in anderen Azure-Diensten verwendet werden) durch das Hosten derselben in Key Vault
- Trennung von Schlüsseln und Datenverwaltungsrollen innerhalb der Organisation, um die Trennung der Pflichten zu unterstützen
- Mehr Vertrauen von Ihren eigenen Kunden, da Key Vault so konzipiert ist, dass Microsoft keine Verschlüsselungsschlüssel sehen oder extrahieren kann. 
- Unterstützung für die Schlüsselrotation

> [!IMPORTANT]
> Für diejenigen, die die von einem Dienst verwaltete TDE verwenden und nun Key Vault verwenden möchten, wird TDE während des Wechselns zu einem Schlüssel in Key Vault beibehalten. Es gibt keine Ausfallzeiten oder eine erneute Verschlüsselung der Datenbankdateien. Das Wechseln von einem Schlüssel, der von einem Dienst verwaltet wird, zu einem Key Vault-Schlüssel erfordert eine erneute Verschlüsselung des Datenbank-Verschlüsselungsschlüssels. Dieser Vorgang erfolgt schnell und online.
>

## <a name="how-does-tde-with-byok-support-work"></a>Wie funktioniert TDE mit BYOK-Unterstützung?
 
![Authentifizierung des Servers für Key Vault](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

Wenn TDE dafür konfiguriert wird, einen Schlüssel von Key Vault zu verwenden, sendet der Server einen Datenbank-Verschlüsselungsschlüssel für jede TDE-aktivierte Datenbank an Key Vault, um eine *Schlüssel packen*-Anforderung durchzuführen. Key Vault gibt den verschlüsselten Datenbank-Verschlüsselungsschlüssel zurück, der in der Benutzerdatenbank gespeichert ist. 

Beachten Sie, dass **ein Schlüssel, sobald er in Key Vault gespeichert ist, Key Vault nie verlässt**. Ein in einem Hardwaresicherheitsmodul (HSM) gespeicherter Schlüssel in Key Vault verlässt nie die HSM-Sicherheitsgrenze. Der Server kann Anforderungen für Schlüsselvorgänge nur an das Schlüsselmaterial der TDE-Schutzvorrichtung innerhalb von Key Vault senden. Der Key Vault-Administrator ist dazu berechtigt, die Key Vault-Berechtigungen für den Server jederzeit aufzuheben. In diesem Fall werden alle Verbindungen zum Server abgeschnitten. 

## <a name="considerations"></a>Weitere Überlegungen

Das Verwenden von TDE mit BYOK bietet Ihnen sowohl zusätzliche Aufgaben für die Schlüsselverwaltung als auch die zugehörigen Kosten für das Verwenden des Schlüsseltresors selbst. Diese Überlegungen werden in den nächsten zwei Abschnitten erläutert.

### <a name="key-management-responsibilities"></a>Aufgaben bei der Schlüsselverwaltung

Das Übernehmen der Verwaltung für Verschlüsselungsschlüssel von den Ressourcen einer Anwendung ist eine wichtige Aufgabe. Indem Sie TDE mit BYOK über Key Vault verwenden, können Sie von folgenden Aufgaben bei der Schlüsselverwaltung ausgehen:
- **Schlüsselrotationen:** Die TDE-Schutzvorrichtungen sollten gemäß der internen Richtlinien oder Kompatibilitätsanforderungen rotiert werden. Schlüsselrotationen können über den Schlüsseltresor der TDE-Schutzvorrichtung durchgeführt werden.  
- **Schlüsseltresorberechtigungen**: Berechtigungen innerhalb von Key Vault werden über einen Schlüsseltresor und auf Serverebene bereitgestellt. Die Berechtigung eines Servers für einen Schlüsseltresor kann jederzeit aufgehoben werden, indem die Zugriffsrichtlinien des Schlüsseltresors verwendet werden.
- **Löschen von Schlüsseln**: Schlüssel können von Key Vault und SQL Server für zusätzliche Sicherheit oder zur Einhaltung der Kompatibilitätsanforderungen gelöscht werden.
- **Überwachung/Berichterstellung auf allen Verschlüsselungsschlüsseln**: Key Vault stellt Protokolle bereit, die leicht in andere Tools für Sicherheitsinformationen und Ereignisverwaltung (SIEM) eingefügt werden können. Operations Management Suite (OMS) [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) ist ein Beispieldienst, der bereits integriert ist.

### <a name="pricing-considerations"></a>Überlegungen zu Preisen 

TDE mit BYOK-Unterstützung ist eine Sicherheitsfunktion, die in Azure SQL-Datenbank und Data Warehouse ohne zusätzliche Gebühren integriert ist. Es gibt jedoch mit der Nutzung von Key Vault verbundene Kosten. Key Vault-Vorgänge, die vom Server durchgeführt werden, werden als normale Vorgänge in Ihrem Tresor berechnet. Dabei werden die [Preise](https://azure.microsoft.com/pricing/details/key-vault/) von Key Vault befolgt. Der Server sendet Anforderungen an Key Vault für die folgenden Ereignisse:
- Neustarts von SQL-Instanzen
- Schlüsselrollover
- Alle sechs Stunden, um zu überprüfen, ob irgendwelche Änderungen an den Berechtigungen des Servers für den Schlüsseltresor vorgenommen wurden

## <a name="important-warnings"></a>Wichtige Warnungen

### <a name="loss-of-access-to-keys"></a>Verlust des Zugriffs auf Schlüssel

Sobald ein Server keine Verbindung mehr zur TDE-Schutzvorrichtung hat (entweder durch entfernte Key Vault-Berechtigungen oder einen gelöschten Schlüssel), **werden alle Verbindungen zu den verschlüsselten Datenbanken auf dem Server blockiert, und diese Datenbanken werden offline geschaltet und innerhalb von 24 Stunden gelöscht**. Auf alte Sicherungen, die mit dem nicht verfügbaren Schlüsseln verschlüsselt sind, kann nicht mehr zugegriffen werden. Wenn die Möglichkeit besteht, dass ein Schlüssel kompromittiert ist (z.B. durch unautorisierten Zugriff auf den Schlüssel durch einen Dienst oder Benutzer), sollte dieser Schlüssel gemäß den Richtlinien unter [Entfernen einer TDE-Schutzvorrichtung (Transparent Data Encryption) mithilfe von PowerShell](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) gelöscht werden. Die Datenbanken müssen gelöscht werden, bevor eine aktive TDE-Schutzvorrichtung gelöscht wird, um einen möglichen Datenverlust von bis zu zehn Minuten zu verhindern.  

### <a name="expired-keys"></a>Abgelaufene Schlüssel

Da die Verfügbarkeit der TDE-Schutzvorrichtung sich direkt auf die Verfügbarkeit der Datenbank auswirkt, kann ein Schlüssel mit Ablaufdatum nicht zu einem SQL-Server hinzugefügt werden. Wenn ein Schlüssel bereits als TDE-Schutzvorrichtung für einen Server verwendet wird und dieser später mit einem Ablaufdatum in Azure Key Vault konfiguriert wird, **haben die verschlüsselten Datenbanken keinen Zugriff mehr auf ihre TDE-Schutzvorrichtung und werden innerhalb von 24 Stunden gelöscht, sobald der Schlüssel abgelaufen ist**.

### <a name="deleted-server-identities"></a>Gelöschte Serveridentitäten 

Der Zugriff eines Servers auf Key Vault wird durch die eindeutige AAD-Identität (Azure Active Directory) des Servers verwaltet. Deshalb verliert der Server den Zugriff auf seine Schlüsseltresore, wenn seine Identität aus AAD gelöscht wird. Dies hat zur Folge, dass **alle Verbindungen zu den verschlüsselten Datenbanken auf dem Server blockiert und diese Datenbanken offline geschaltet und innerhalb von 24 Stunden gelöscht werden**.

## <a name="limitations"></a>Einschränkungen

Schlüsseltresore, die für TDE verwendet werden, müssen sich im selben AAD-Mandanten wie die SQL-Datenbank oder der Data Warehouse-Server befinden. Mandantenübergreifende Interaktionen von Schlüsseltresoren und Servern werden nicht unterstützt. Eine Ressource, die mit einem Schlüssel von Key Vault verschlüsselt wird, kann nicht über Azure-Abonnements verschoben werden. Das Verschieben der Ressource über Abonnements unterbricht die notwendigen Zugriffssteuerungen von Key Vault, die TDE mit BYOK ermöglicht haben. Wenn eine Ressource auf ein anderes Abonnement verschoben werden muss, ändern Sie den TDE-Modus von BYOK zu [Vom Dienst verwaltete TDE](transparent-data-encryption-azure-sql.md). 

Eindeutige TDE-Schutzvorrichtungen für Datenbanken oder Data Warehouse werden nicht unterstützt. Die TDE-Schutzvorrichtung ist auf Serverebene festgelegt und wird von allen Ressourcen auf dem Server geerbt. 

## <a name="guidelines-for-managing-encrypted-databases"></a>Richtlinien zum Verwalten von verschlüsselte Datenbanken

### <a name="high-availability-and-disaster-recovery"></a>Hochverfügbarkeit und Notfallwiederherstellung
  
Es gibt zwei Möglichkeiten, wie die Georeplikation für Server mithilfe von Key Vault konfiguriert werden kann: 

- **Separater Schlüsseltresor**: Jeder Server hat Zugriff auf einen separaten Schlüsseltresor (idealerweise jeweils innerhalb seiner eigenen Azure-Region). Dabei handelt es sich um die empfohlene Konfiguration, da jeder Server über seine eigene Kopie der TDE-Schutzvorrichtung für die verschlüsselten, georeplizierten Datenbanken verfügt. Wenn die Azure-Regionen eines Servers offline geschaltet werden, können die anderen Server weiterhin auf die georeplizierten Datenbanken zugreifen.   

- **Freigegebener Schlüsseltresor**: Alle Server verwenden denselben Schlüsseltresor. Diese Konfiguration ist leichter einzurichten, aber wenn die Azure-Region, in der sich der Schlüsseltresor befindet, offline geschaltet wird, kann kein Server mehr die verschlüsselten georeplizierten Datenbanken oder seine eigenen verschlüsselten Datenbanken lesen. 
 
Verwenden Sie zum Einstieg das Cmdlet [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey), um den Key Vault-Schlüssel jedes Servers zu den anderen Servern im Link der Georeplikation hinzuzufügen.  
(Beispiel für eine Schlüssel-ID von Key Vault: *https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h*)

   ```powershell
   <# Include the version guid in the KeyId #>
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

>[!NOTE]
>Die kombinierte Zeichenlänge des Schlüsseltresornamens und des Schlüsselnamens darf nicht über 94 Zeichen hinausgehen.
>

Befolgen Sie die Schritte in [Active geo-replication overview (Übersicht über die aktive Georeplikation)](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview), um die aktive Georeplikation mit diesen Servern zu konfigurieren und ein Failover auszulösen.  

### <a name="backup-and-restore"></a>Sichern und Wiederherstellen

Sobald eine Datenbank mit TDE und einem Schlüssel von Key Vault verschlüsselt ist, werden alle generierten Sicherungen ebenfalls mit derselben TDE-Schutzvorrichtung verschlüsselt.

Versichern Sie sich zum Wiederherstellen einer Sicherung, die mit einer TDE-Schutzvorrichtung von Key Vault verschlüsselt ist, dass sich das Schlüsselmaterial noch im ursprünglichen Tresor unter dem ursprünglichen Schlüsselnamen befindet. Wenn die TDE-Schutzvorrichtung für eine Datenbank geändert wird, werden alte Sicherungen von Datenbanken **nicht** für das Verwenden der neuesten TDE-Schutzvorrichtung aktualisiert. Deshalb empfehlen wir, dass Sie ältere Versionen der TDE-Schlüsselvorrichtung in Key Vault beibehalten, sodass Datenbanksicherungen wiederhergestellt werden können. 

Wenn ein Schlüssel, der möglicherweise für das Wiederherstellen einer Sicherung benötigt wird, sich nicht mehr in seinem ursprünglichen Schlüsseltresor befindet, wird die folgende Fehlermeldung zurückgegeben: "Target server <Servername> does not have access to all AKV Uris created between <Timestamp #1> and <Timestamp #2>. Please retry operation after restoring all AKV Uris." (Zielserver hat keinen Zugriff auf alle AKV-URIs, die zwischen <Zeitstempel #1> und <Zeitstempel #2> erstellt wurden. Bitte wiederholen Sie den Vorgang nach der Wiederherstellung aller AKV-URIs ).

Führen Sie zur Umgehung dieses Fehlers das Cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) aus, um die Liste der Key Vault-Schlüssel zurückzugeben, die dem Server hinzugefügt wurden. Versichern Sie sich, dass der Zielserver für die Sicherung auf all diese Schlüssel zugreifen kann, um sicherzustellen, dass alle Sicherungen wiederhergestellt werden können.

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
Weitere Informationen zum Wiederherstellen von Sicherungen für SQL-Datenbank finden Sie unter [Recover an Azure SQL database (Wiederherstellen von Azure SQL-Datenbank)](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups). Weitere Informationen zum Wiederherstellen von Sicherungen für SQL Data Warehouse finden Sie unter [Recover an Azure SQL Data Warehouse (Wiederherstellen von Azure SQL Data Warehouse)](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview).

## <a name="best-practices"></a>Bewährte Methoden

### <a name="key-management"></a>Schlüsselverwaltung 

Es wird Folgendes empfohlen, um die schnelle Wiederherstellung von Schlüsseln sicherzustellen und den Zugriff auf Ihre Daten außerhalb von Azure zu ermöglichen:
- Erstellen Sie Ihren Verschlüsselungsschlüssel lokal auf einem lokalen HSM-Gerät. (Stellen Sie sicher, dass dies ein asymmetrischer RSA-2048-Schlüssel ist, damit er in Azure Key Vault gespeichert werden kann.)
- Importieren Sie die Datei für den Verschlüsselungsschlüssel (PFX, BYOK oder BACKUP) in Azure Key Vault. Erwägen Sie die Verwendung eines Schlüsseltresors mit aktiviertem [vorläufigen Löschen](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete) für Wiederherstellungsschutz bei versehentlichem Löschen von Schlüsseln.
- Bevor Sie den Schlüssel zum ersten Mal in Azure Key Vault verwenden, erstellen Sie eine Azure Key Vault-Schlüsselsicherung. Erhalten Sie weitere Informationen zum Befehl [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) .
- Sobald Änderungen am Schlüssel vorgenommen werden (z.B. durch Hinzufügen von ACLs, Tags oder Schlüsselattributen), müssen Sie sicherstellen, dass Sie eine weitere Azure Key Vault-Schlüsselsicherung erstellen.
- **Behalten Sie frühere Versionen des Schlüssels** im Schlüsseltresor während eines Schlüsselrollovers bei, sodass Datenbanksicherungen wiederhergestellt werden können. 

Für Produktionsszenarios wird dringend empfohlen, zuerst den TDE-Verschlüsselungsschlüssel lokal zu erstellen und den asymmetrischen Schlüssel zu importieren, da der Administrator dann den Schlüssel in einem Schlüsselhinterlegungssystem hinterlegen kann. Wenn der asymmetrische Schlüssel in Azure Key Vault erstellt wird, kann er nicht hinterlegt werden, da der private Schlüssel nie den Tresor verlassen kann. Schlüssel zum Schützen wichtiger Daten sollten hinterlegt werden. Der Verlust eines asymmetrischen Schlüssels führt dazu, dass Daten dauerhaft nicht wiederhergestellt werden können.

### <a name="pre-configuration-for-replicated-databases"></a>Vorkonfiguration für replizierte Datenbanken

Wenn eine verschlüsselte Datenbank auf einen anderen Server repliziert werden soll, versichern Sie sich, dass der Server Zugriff auf eine Kopie des Key Vault-Schlüsselmaterials hat, das für den anderen Server verwendet wird, **bevor** Sie die Datenbank verschieben oder replizieren.  

Es wird empfohlen, dass jeder Server Zugriff auf das Key Vault-Schlüsselmaterial hat, das für den anderen Server verwendet wird. Dies wird in einem separaten Schlüsseltresor gespeichert (idealerweise jeweils innerhalb derselben Azure-Region wie der Server). Bei diesem Setup verfügt jeder Server über seine eigene Kopie der TDE-Schutzvorrichtung für die verschlüsselten, georeplizierten Datenbanken. Wenn die Azure-Region eines Servers offline geschaltet wird, können die anderen Server weiterhin auf die replizierten Datenbanken zugreifen.

## <a name="next-steps"></a>Nächste Schritte

- Erste Schritte mit der Bring Your Own Key-Unterstützung für TDE: [Turn on TDE using your own key from Key Vault using PowerShell (Aktivieren von TDE für das Verwenden Ihres eigenen Schlüssels von Key Vault mithilfe von PowerShell)](transparent-data-encryption-byok-azure-sql-configure.md)
- Erfahren Sie, wie Sie die TDE-Schutzvorrichtung eines Servers rotieren können, damit dieser den Sicherheitsrichtlinien entspricht: [Rotieren einer Transparent Data Encryption-Schutzvorrichtung (TDE) mithilfe von PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md).
- Im Fall eines Sicherheitsvorfalls erfahren Sie unter [Entfernen einer TDE-Schutzvorrichtung (Transparent Data Encryption) mithilfe von PowerShell](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md), wie Sie eine möglicherweise kompromittierte TDE-Schutzvorrichtung entfernen können. 
