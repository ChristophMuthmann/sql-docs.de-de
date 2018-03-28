---
title: 'TDE: Bring Your Own Key (BYOK) – Azure SQL | Microsoft-Dokumentation'
description: 'BYOK-Unterstützung (Bring Your Own Key) für Transparent Data Encryption (TDE) mit Azure Key Vault für SQL-Datenbank und Data Warehouse. TDE mit BYOK: Überblick, Funktionsweise, Überlegungen und Empfehlungen.'
keywords: ''
services: sql-database
documentationcenter: ''
author: aliceku
manager: craigg
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: ''
ms.devlang: na
ms.topic: article
ms.date: 03/16/2018
ms.author: aliceku
ms.openlocfilehash: ae89e8496ce8f2aec87d80e36ce7b48acfd6a8cf
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="transparent-data-encryption-with-bring-your-own-key-preview-support-for-azure-sql-database-and-data-warehouse"></a>Transparent Data Encryption mit Bring Your Own Key-Unterstützung (Vorschau) für Azure SQL-Datenbank und Data Warehouse
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

Mithilfe der Unterstützung von Bring Your Own Key (BYOK) für die [Transparent Data Encryption (TDE)](transparent-data-encryption.md) können Sie den Datenbank-Verschlüsselungsschlüssel (Database Encryption Key, DEK) mit einem dem asymmetrischen Schlüssel „TDE Protector“ verschlüsseln.  Der TDE Protector ist in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault) gespeichert. Dabei handelt es sich um das cloudbasierte Verwaltungssystem von externen Schlüsseln von Azure. Bei Azure Key Vault handelt es sich um den ersten Verwaltungsdienst für Schlüssel, in dem die Unterstützung von BYOK in TDE integriert ist. Der TDE-DEK ist auf der Startseite der Datenbank gespeichert und wird vom TDE Protector verschlüsselt und entschlüsselt. Der TDE Protector ist in Azure Key Vault gespeichert und bleibt auch dort erhalten. Wenn dem Server der Zugriff auf den Schlüsseltresor entzogen wird, können Datenbanken nicht entschlüsselt und im Speicher gelesen werden.  Der TDE Protector ist auf der Ebene des logischen Servers platziert und wird von allen Datenbanken geerbt, die diesem Server zugeordnet sind. 

Mit der BYOK-Unterstützung können Benutzer jetzt Schlüsselverwaltungsaufgaben steuern, einschließlich Schlüsselrotationen, Schlüsseltresorberechtigungen, Löschen von Schlüsseln und Aktivieren der Überwachung/Berichterstellung auf allen TDE Protectors, die die Funktionen von Azure Key Vault verwenden. Key Vault bietet eine zentrale Schlüsselverwaltung, nutzt die streng überwachten Hardwaresicherheitsmodule (HSMs) und ermöglicht die Trennung der Pflichten zwischen dem Verwalten von Schlüsseln und Daten, um gesetzliche Bestimmungen einzuhalten.  


TDE mit BYOK bietet folgende Vorteile:
- Erhöhte Transparenz und eine präzise Steuerung mit der Möglichkeit, die TDE-Schutzvorrichtung selbst zu verwalten   
- Zentrale Verwaltung des TDE-Protectors (zusammen mit anderen Schlüsseln und Geheimnissen, die in anderen Azure-Diensten verwendet werden) durch das Hosten in Key Vault
- Trennung von Schlüsseln und Datenverwaltungsverantwortlichkeiten innerhalb der Organisation, um die Trennung der Pflichten zu unterstützen
- Mehr Vertrauen von Ihren eigenen Kunden, da Key Vault so konzipiert ist, dass Microsoft keine Verschlüsselungsschlüssel sehen oder extrahieren kann. 
- Unterstützung für die Schlüsselrotation

> [!IMPORTANT]
> Für diejenigen, die die von einem Dienst verwaltete TDE verwenden und jetzt Key Vault verwenden möchten, wird TDE während des Wechselns zu einem Schlüssel in Key Vault beibehalten. Es gibt keine Downtime oder eine erneute Verschlüsselung der Datenbankdateien. Das Wechseln von einem Schlüssel, der von einem Dienst verwaltet wird, zu einem Key Vault-Schlüssel erfordert eine erneute Verschlüsselung des Datenbank-Verschlüsselungsschlüssels. Dieser Vorgang erfolgt schnell und online. 
>

## <a name="how-does-tde-with-byok-support-work"></a>Wie funktioniert TDE mit BYOK-Unterstützung?
 
![Authentifizierung des Servers für Key Vault](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

Wenn TDE dafür konfiguriert wird, einen TDE Protector von Key Vault zu verwenden, sendet der Server einen Datenbank-Verschlüsselungsschlüssel für jede TDE-aktivierte Datenbank an Key Vault, um eine „Schlüssel packen“-Anforderung durchzuführen. Key Vault gibt den verschlüsselten Datenbank-Verschlüsselungsschlüssel zurück, der in der Benutzerdatenbank gespeichert ist.  

>[!IMPORTANT]
>Beachten Sie, dass **TDE Protectors immer in Azure Key Vault verbleiben, wenn sie einmal dort gespeichert werden**. Der logische Server kann Anforderungen für Schlüsselvorgänge nur an das Schlüsselmaterial des TDE Protectors innerhalb von Key Vault senden und **greift niemals auf den TDE Protector zu oder speichert ihn zwischen**. Der Key Vault-Administrator ist dazu berechtigt, die Key Vault-Berechtigungen für den Server jederzeit aufzuheben. In diesem Fall werden alle Verbindungen zum Server getrennt. 
>


## <a name="guidelines-for-configuring-tde-with-byok"></a>Richtlinien für das Konfigurieren von TDE mit BYOK

### <a name="general-guidelines"></a>Allgemeine Richtlinien
- Vergewissern Sie sich, dass Azure Key Vault und Azure SQL-Datenbank in demselben Mandanten gespeichert werden.  Mandantenübergreifende Interaktionen von Key Vaults und Servern **werden nicht unterstützt**.
- Legen Sie fest, welche Abonnements für die erforderlichen Ressourcen verwendet werden sollen. Wenn Sie dem Server später anderen Abonnements zuweisen, ist ein erneutes Setup von TDE mit BYOK erforderlich.
- Beim Konfigurieren von TDE mit BYOK müssen Sie die Last berücksichtigen, die durch wiederholte wrap-/unwrap-Vorgänge im Schlüsseltresor entsteht. Ein Beispiel: Da alle Datenbanken, die einem logischen Server zugeordnet sind, den gleichen TDE Protector verwenden, löst ein Failover dieses Servers so viele Schlüsselvorgänge im Tresor aus, wie Datenbanken auf dem Server vorhanden sind. Basierend auf unseren Erfahrungen und den dokumentierten [Grenzwerten des Key Vault-Diensts](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-service-limits) empfehlen wir, einer Azure Key Vault-Instanz in einem einzelnen Abonnement höchstens 500 Standard- oder 200-Premium-Datenbanken zuzuordnen, um beim Zugriff auf den TDE Protector im Tresor eine konsistent hohe Verfügbarkeit sicherzustellen. 
- Empfehlung: Speichern Sie lokal eine Kopie des TDE Protectors.  Dafür benötigen Sie ein HSM-Gerät, um einen TDE Protector lokal zu erstellen, und ein Schlüsselhinterlegungssystem zum Speichern der lokalen Kopie des TDE Protectors.


### <a name="guidelines-for-configuring-azure-key-vault"></a>Richtlinien für das Konfigurieren von Azure Key Vault

- Verwenden Sie einen Schlüsseltresor, für den [vorläufiges Löschen](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete) aktiviert ist, um sich vor Datenverlusten zu schützen, falls der Schlüssel bzw. der Schlüsseltresor aus Versehen gelöscht wird:  
  - Vorläufig gelöschte Ressourcen bleiben für einen Zeitraum von 90 Tagen weiter gespeichert. In diesem Zeitraum können sie wiederhergestellt oder endgültig gelöscht werden.
  - Den Aktionen **Wiederherstellen** und **Endgültig löschen** sind über Zugriffsrichtlinien für den Schlüsseltresor eigene Berechtigungen zugewiesen. 
- Erteilen Sie dem logischen Server über dessen Azure AD-Identität (Azure Active Directory) Zugriff auf den Schlüsseltresor.  Wenn die Benutzeroberfläche des Portals verwendet wird, wird die Azure AD-Identität automatisch erstellt, und dem Server werden die Zugriffsberechtigungen für den Schlüsseltresor erteilt.  Wenn PowerShell verwendet wird, um TDE mit BYOK zu konfigurieren, muss die Azure AD-Identität erstellt werden. Außerdem sollte der Abschluss des Vorgangs überprüft werden. Wenn Sie PowerShell verwenden, finden Sie detaillierte Anweisungen unter [Konfigurieren von TDE mit BYOK](transparent-data-encryption-byok-azure-sql-configure.md).

  >[!NOTE]
  >Wenn die Azure AD-Identität über die Zugriffsrichtlinie des Schlüsseltresors **aus Versehen gelöscht wird oder die Serverberechtigungen widerrufen werden**, kann der Server nicht mehr auf den Schlüsseltresor zugreifen.
  >
  
- Aktivieren Sie die Überwachung und die Berichterstellung auf allen Verschlüsselungsschlüsseln: Key Vault stellt Protokolle bereit, die leicht in andere Tools für Sicherheitsinformationen und Ereignisverwaltung (SIEM) eingefügt werden können. Operations Management Suite (OMS) [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) ist ein Beispieldienst, der bereits integriert ist.
- Konfigurieren Sie alle logischen Server mit jeweils zwei Azure Key Vaults, die sich in verschiedenen Regionen befinden, um die Hochverfügbarkeit von verschlüsselten Datenbanken zu gewährleisten.


### <a name="guidelines-for-configuring-the-tde-protector-asymmetric-key-stored-in-azure-key-vault"></a>Richtlinien zum Konfigurieren des TDE Protectors (asymmetrischer Schlüssel), der in Azure Key Vault gespeichert ist

- Erstellen Sie Ihren Verschlüsselungsschlüssel lokal auf einem lokalen HSM-Gerät. Stellen Sie sicher, dass dies ein asymmetrischer RSA-2048-Schlüssel ist, damit er in Azure Key Vault gespeichert werden kann.
- Hinterlegen Sie den Schlüssel in einem Schlüsselhinterlegungssystem.  
- Importieren Sie die Datei für den Verschlüsselungsschlüssel (PFX, BYOK oder BACKUP) in Azure Key Vault. 
    

>[!NOTE] 
    >Wenn Sie einen Test durchführen möchten, können Sie einen Schlüssel mit Azure Key Vault erstellen. Dieser Schlüssel kann dann allerdings nicht hinterlegt werden, da der private Schlüssel immer im Schlüsseltresor verbleiben muss.  Sichern und hinterlegen Sie immer die Schlüssel, die zum Verschlüsseln von Produktionsdaten verwendet werden, da es zu nicht wiederherstellbaren Datenverlusten kommen kann, wenn der Schlüssel verloren gehen sollte (z.B. wenn er aus Versehen aus dem Schlüsseltresor gelöscht wird oder abläuft).
    >
    
- Verwenden Sie Schlüssel ohne Ablaufdatum und legen Sie niemals ein Ablaufdatum für einen Schlüssel fest, der bereits verwendet wird: **Sobald der Schlüssel abläuft, können die verschlüsselten Datenbanken nicht mehr auf ihre TDE Protectors zugreifen und werden innerhalb von 24 Stunden gelöscht.**
- Vergewissern Sie sich, das der Schlüssel aktiviert ist und die Berechtigungen hat, um die Vorgänge *Abrufen*, *Schlüssel packen* und *Schlüssel entpacken* durchzuführen.
- Bevor Sie den Schlüssel zum ersten Mal in Azure Key Vault verwenden, erstellen Sie eine Azure Key Vault-Schlüsselsicherung. Erhalten Sie weitere Informationen zum Befehl [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) .
- Erstellen Sie jedes Mal eine neue Sicherung, wenn Änderungen an dem Schlüssel vorgenommen werden – z.B. wenn ACLs, Tags oder Schlüsselattribute hinzugefügt werden.
- **Behalten Sie frühere Versionen des Schlüssels** im Schlüsseltresor, wenn Sie Schlüssel rotieren, damit Datenbanksicherungen wiederhergestellt werden können. Wenn der TDE Protector für eine Datenbank geändert wird, werden alte Sicherungen von Datenbanken **nicht** für das Verwenden des neuesten TDE Protectors aktualisiert.  Für jede Sicherung wird der TDE Protector benötigt, mit dem diese zum Zeitpunkt der Wiederherstellung erstellt wurde. Schlüsselrotationen können ausgeführt werden, indem Sie die Anweisungen unter [Rotieren einer Transparent Data Encryption-Schutzvorrichtung (TDE) mithilfe von PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md) befolgen.
- Behalten Sie alle zuvor benutzen Schlüssel in Azure Key Vault, wenn Sie zurück zu Schlüsseln wechseln, die von einem Dienst verwaltet werden.  Dadurch wird sichergestellt, dass Datenbankwiederherstellungen über die TDE Protectors, die in Azure Key Vault gespeichert sind, wiederhergestellt werden können.  TDE Protectors, die mit Azure Key Vault erstellt wurden, müssen so lange verwaltet werden, bis alle gespeicherten Sicherungen mit Schlüsseln erstellt worden sind, die von einem Dienst verwaltet werden.  
- Erstellen Sie wiederherstellbare Sicherungskopien dieser Schlüssel über [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1).
- Wenn Sie einen möglicherweise kompromittierten Schlüssel im Zusammenhang mit einem Sicherheitsproblem entfernen möchten, ohne dabei einen Datenverlust zu riskieren, führen Sie die Schritte unter [Entfernen einer TDE-Schutzvorrichtung (Transparent Data Encryption) mithilfe von PowerShell](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) aus.


## <a name="high-availability-geo-replication-and-backup--restore"></a>Hochverfügbarkeit, Georeplikation und Sichern bzw. Wiederherstellen

### <a name="high-availability-and-disaster-recovery"></a>Hochverfügbarkeit und Notfallwiederherstellung

Die Art und Weise, auf die Hochverfügbarkeit mit Azure Key Vault konfiguriert werden kann, ist davon abhängig, wie Ihre Datenbank und Ihr logischer Server konfiguriert sind. Im Folgenden werden die empfohlenen Konfigurationen für zwei unterschiedliche Fälle beschrieben.  Im ersten Fall handelt es sich um eine eigenständige Datenbank oder einen logischen Server, der ohne Georedundanz konfiguriert ist.  Im zweiten Fall handelt es sich um eine Datenbank oder einen logischen Server, der mit Failovergruppen oder Georedundanz konfiguriert ist. Dabei muss gewährleistet sein, das jede Kopie mit Georedundanz über einen lokalen Azur Key Vault innerhalb der Failovergruppe verfügt, damit die Geofailovers funktionieren können. Im ersten Fall wird empfohlen, den Server so zu konfigurieren, dass er zwei verschiedene Schlüsseltresore in zwei verschiedenen Regionen mit demselben Schlüsselmaterial verwendet, wenn Hochverfügbarkeit einer Datenbank und eines logischen Servers ohne konfigurierte Georedundanz erforderlich ist.  Dies können Sie tun, indem Sie einen TDE Protector erstellen, der den primären Schlüsseltresor verwendet, der sich in derselben Region wie der logische Server befindet und den Schlüssel in den Schlüsseltresor in einer anderen Azure-Region klonen, sodass der Server Zugriff auf einem zweiten Schlüsseltresor hat, wenn der primäre Schlüsseltresor ausfallen sollte, während die Datenbank weiter funktioniert. Verwenden Sie das Cmdlet „Backup-AzureKeyVaultKey“, um den Schlüssel aus dem primären Schlüsseltresor im verschlüsselten Format abzurufen und dann das Cmdlet „Restore-AzureKeyVaultKey“ zu verwenden und einen Schlüsseltresor in der zweiten Region anzugeben.


![Hochverfügbarkeit für einen einzelnen Server und fehlende Georedundanz](./media/transparent-data-encryption-byok-azure-sql/SingleServer_HA_Config.PNG)

Im zweiten Fall ist es erforderlich, redundante Azure Key Vaults anhand der vorhandenen SQL-Datenbank-Failovergruppen oder der Kopien der aktiven Georedundanz von Datenbanken zu konfigurieren, um die Hochverfügbarkeit der TDE Protectors in Azure Key Vault zu erhalten.  Jeder georeplizierte Server erfordert einen separaten Schlüsseltresor, der sich idealerweise in derselben Azure-Region befindet wie der Server. Wenn es in einer Region zu einem Ausfall kommen sollte, nach dem nicht mehr auf die primäre Datenbank zugegriffen werden kann und ein Failover ausgelöst wird, kann die sekundäre Datenbank einspringen und den sekundären Schlüsseltresor verwenden.  

![Failovergruppen und Georedundanz](./media/transparent-data-encryption-byok-azure-sql/Geo_DR_Config.PNG)

Wenn Sie sicherstellen wollen, dass ohne Einschränkungen während eines Failovers auf den TDE Protector in Azur Key Vault zugegriffen werden kann, muss dies konfiguriert werden, bevor eine Datenbank repliziert wird oder ein Failover auf einen sekundären Server ausgeführt wird. Sowohl der primäre als auch der sekundäre Server muss Kopien der TDE Protectors in allen anderen Azure Key Vaults speichern. Das bedeutet in diesem Fall, dass dieselben Schlüssel in beiden Schlüsseltresoren gespeichert werden.

Im Szenario der georedundanten Notfallwiederherstellung wird zur Sicherstellung von Redundanz eine sekundäre Datenbank mit einem sekundären Schlüsseltresor benötigt. Dabei werden maximal vier sekundäre Datenbanken unterstützt.  Nicht unterstützt wird das Verketten, also das Erstellen einer sekundären Datenbank für eine andere sekundäre Datenbank.  Bei der Ersteinrichtung bestätigt der Dienst, dass die Berechtigungen ordnungsgemäß für den primären und sekundären Schlüsseltresor konfiguriert sind.  Diese Berechtigungen müssen korrekt verwaltet und regelmäßig geprüft werden, sodass sichergestellt wird, dass diese aktiv sind.

>[!NOTE]
>Wenn die Identität des Servers einem primären und einem sekundären Server zugewiesen wird, muss diese zuerst dem sekundären Server zugewiesen werden.
>

Wenn Sie einen in einem Schlüsseltresor vorhandenen Schlüssel einem anderen Schlüsseltresor hinzufügen möchten, verwenden Sie das Cmdlet [Add-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey).

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

Führen Sie zur Umgehung dieses Fehlers das Cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) aus, um die Liste der Key Vault-Schlüssel zurückzugeben, die dem Server hinzugefügt wurden (wenn sie nicht bereits von einem Benutzer gelöscht wurden). Vergewissern Sie sich, dass der Zielserver für die Sicherung auf all diese Schlüssel zugreifen kann, um sicherzustellen, dass alle Sicherungen wiederhergestellt werden können.

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
Weitere Informationen zum Wiederherstellen von Sicherungen für SQL-Datenbank finden Sie unter [Recover an Azure SQL database (Wiederherstellen von Azure SQL-Datenbank)](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups). Weitere Informationen zum Wiederherstellen von Sicherungen für SQL Data Warehouse finden Sie unter [Recover an Azure SQL Data Warehouse (Wiederherstellen von Azure SQL Data Warehouse)](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview).


Weitere Überlegungen für gesicherte Protokolldateien: Gesicherte Protokolldateien sind weiterhin mit dem ursprünglichen TDE Encryptor verschlüsselt, auch wenn der TDE Protector rotiert wurde und die Datenbank jetzt einen neuen TDE Protector verwendet.  Zur Wiederherstellungszeit werden beide Schlüssel benötigt, um die Datenbank wiederherzustellen.  Wenn die Protokolldatei einen in Azure Key Vault gespeicherten TDE Protector verwendet, wird dieser Schlüssel zur Wiederherstellungszeit benötigt, auch wenn die Datenbank in der Zwischenzeit geändert wurde und jetzt eine per Dienst verwaltete TDE verwendet.


