---
title: "Transparente datenverschlüsselung für Parallel Datawarehouse"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Transparente datenverschlüsselung (TDE) führt in Echtzeit e/a-Verschlüsselung und Entschlüsselung von Daten und Transaktionsprotokolldateien und die speziellen PDW-Protokolldateien."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: b82ad21d-09dd-43dd-8fab-bcf2c8c3ac6d
caps.latest.revision: "22"
ms.openlocfilehash: 6c96bd67d9a935756b8353999f6c778134d2ed57
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="transparent-data-encryption"></a>Transparente Datenverschlüsselung
Sie können verschiedene Vorsichtsmaßnahmen treffen, um eine Datenbank abzusichern, beispielsweise ein sicheres System entwerfen, vertrauliche Datenbestände verschlüsseln oder eine Firewall für die Datenbankserver einrichten. Wenn jedoch physische Medien (etwa Laufwerke oder Sicherungsbänder) gestohlen werden, muss ein böswilliger Benutzer die Datenbank einfach nur wieder herstellen und kann dann die Daten durchsuchen. Eine Lösung dieses Problems besteht darin, die sensiblen Daten in der Datenbank zu verschlüsseln, und den für die Verschlüsselung der Daten verwendeten Schlüssel mit einem Zertifikat zu schützen. Dadurch kann niemand die Daten verwenden, der nicht im Besitz der Schlüssel ist. Diese Art des Schutzes muss jedoch im Voraus geplant werden.  
  
*Transparente datenverschlüsselung* (TDE) führt in Echtzeit e/a-Verschlüsselung und Entschlüsselung von Daten und Transaktionsprotokolldateien und spezielle PDW-Protokolldateien. Die Verschlüsselung verwendet einen Verschlüsselungsschlüssel für die Datenbank (Database Encryption Key, DEK), der in der Datenbankstartseite gespeichert wird, damit er während der Wiederherstellung verfügbar ist. Der DEK ist ein symmetrischer Schlüssel mit einem Zertifikat in der master-Datenbank von SQL Server-PDW gespeicherten gesichert. TDE schützt die "ruhenden" Daten, also die Daten- und die Protokolldateien. Sie entspricht den in vielen Branchen etablierten Gesetzen, Bestimmungen und Richtlinien. Dadurch können Softwareentwickler Daten mithilfe der AES- und 3DES-Verschlüsselungsalgorithmen verschlüsseln, ohne vorhandene Anwendungen ändern zu müssen.  
  
> [!IMPORTANT]  
> TDE stellt keine Verschlüsselung für Daten, die zwischen dem Client und dem PDW Wegstrecke bereit. Weitere Informationen zum Verschlüsseln von Daten zwischen dem Client und SQL Server PDW finden Sie unter [bereitstellen ein Zertifikats](provision-certificate.md).  
>   
> TDE werden keine Daten verschlüsselt, während sie verschoben werden oder wird verwendet. Interner Datenverkehr zwischen PDW-Komponenten in der SQL Server PDW ist nicht verschlüsselt. Daten, die temporär im Arbeitsspeicher gespeichert werden nicht verschlüsselt. Zur Minderung dieses Risikos können steuern Sie physischen Zugriff und Verbindungen mit SQL Server-PDW.  
  
Nachdem sie gesichert wurde, kann die Datenbank mit dem richtigen Zertifikat wiederhergestellt werden.  
  
> [!NOTE]  
> Wenn Sie ein Zertifikat für TDE erstellen, sollten Sie sofort es, zusammen mit den zugehörigen privaten Schlüssel sichern. Sollte das Zertifikat einmal nicht mehr verfügbar sein, oder sollten Sie die Datenbank auf einem anderen Server wiederherstellen oder anfügen müssen, müssen Sie über Sicherungen sowohl des Zertifikats als auch des privaten Schlüssels verfügen, da Sie andernfalls die Datenbank nicht öffnen können. Das zum Verschlüsseln verwendete Zertifikat sollte beibehalten werden, selbst wenn TDE für die Datenbank nicht mehr aktiviert ist. Selbst wenn die Datenbank nicht verschlüsselt ist, können Teile des Transaktionsprotokolls nach wie vor geschützt sein. Für bestimmte Vorgänge wird das Zertifikat ggf. weiterhin benötigt, bis eine vollständige Sicherung der Datenbank ausgeführt wurde. Ein abgelaufenes Zertifikat kann immer noch verwendet werden, um Daten mit TDE zu verschlüsseln und zu entschlüsseln.  
  
Die Verschlüsselung der Datenbankdatei wird auf Seitenebene ausgeführt. In einer verschlüsselten Datenbank werden die Seiten verschlüsselt, bevor Sie auf den Datenträger geschrieben werden, und entschlüsselt, wenn sie in den Arbeitsspeicher gelesen werden. TDE erhöht nicht die Größe einer verschlüsselten Datenbank.  
  
Die folgende Abbildung zeigt die Hierarchie der Schlüssel für die TDE-Verschlüsselung:  
  
![Zeigt die Hierarchie, die in diesem Thema beschrieben. ] (media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>Verwenden die transparente datenverschlüsselung  
Führen Sie folgende Schritte aus, um TDE zu verwenden: Die ersten drei Schritte sind nur einmal ausgeführt werden, bei der Vorbereitung von SQL Server PDW um TDE zu unterstützen.  
  
1.  Erstellen Sie einen Hauptschlüssel in der master-Datenbank.  
  
2.  Verwendung **sp_pdw_database_encryption aktiviert werden** zum Aktivieren von TDE in SQL Server-PDW. Dieser Vorgang ändert die temporären Datenbanken, um sicherzustellen, dass den Schutz für zukünftige temporäre Daten und schlägt fehl, wenn versucht wird, wenn aktive Sitzungen, die temporäre Tabellen weisen vorhanden sind. **sp_pdw_database_encryption aktiviert werden** datenmaskierung in PDW Systemprotokolle Benutzer aktiviert. (Weitere Informationen zu Benutzer datenmaskierung in PDW-Systemprotokolle, finden Sie unter [Sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md).)  
  
3.  Verwendung [Sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) Anmeldeinformationen zu erstellen, können zu authentifizieren und Schreiben auf die Freigabe, in dem die Sicherung des Zertifikats gespeichert. Wenn die Anmeldeinformationen für den gewünschten Server bereits vorhanden sind, kann die vorhandene Anmeldeinformationen verwendet werden.  
  
4.  Erstellen Sie in der master-Datenbank ein Zertifikat mit dem Hauptschlüssel geschützt.  
  
5.  Sichern Sie das Zertifikat für die Speicherfreigabe.  
  
6.  Erstellen Sie in der Benutzerdatenbank einen Datenbankverschlüsselungsschlüssel, und schützen Sie, indem Sie das Zertifikat, das in der master-Datenbank gespeichert ist.  
  
7.  Verwenden der `ALTER DATABASE` Anweisung, um die Datenbank mit TDE zu verschlüsseln.  
  
Das folgende Beispiel veranschaulicht das Verschlüsseln der `AdventureWorksPDW2012` Datenbank mit einem Zertifikat namens `MyServerCert`, in SQL Server PDW erstellt.  
  
**Erstens: Aktivieren von TDE in SQLServer PDW.** Dies muss nur einmal.  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
-- Add a credential that can write to the share  
-- A credential created for a backup can be used if you wish  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
**Zweite: Erstellen Sie und Sichern Sie ein Zertifikat in der master-Datenbank.** Dies ist nur einmal erforderlich. Sie können jeweils ein Zertifikat für jede Datenbank (empfohlen), oder Sie können mehrere Datenbanken mit einem Zertifikat schützen.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
GO  
  
-- Back up the certificate with private key  
BACKUP CERTIFICATE MyServerCert   
    TO FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'  
    WITH PRIVATE KEY   
    (   
        FILE = '\\SECURE_SERVER\cert\MyServerCert.key',  
        ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>'   
    )   
GO  
```  
  
**Letzte: Erstellen Sie den DEK und verwenden Sie ALTER DATABASE, um eine Benutzerdatenbank zu verschlüsseln.** Dieser Vorgang wird für jede Datenbank wiederholt, die durch TDE geschützt ist.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
  
ALTER DATABASE AdventureWorksPDW2012 SET ENCRYPTION ON;  
GO  
```  
  
Die Verschlüsselung und Entschlüsselung Vorgänge werden von SQL Server in Hintergrundthreads geplant. Sie können den Status dieser Vorgänge mithilfe der in der Liste weiter unten in diesem Thema genannten Katalogsichten und dynamischen Verwaltungssichten anzeigen.  
  
> [!CAUTION]  
> Sicherungsdateien von Datenbanken, für die TDE aktiviert wurde, werden ebenfalls mithilfe des Verschlüsselungsschlüssels für die Datenbank verschlüsselt. Darum muss bei der Wiederherstellung dieser Sicherungen das Zertifikat, das zum Verschlüsseln des Verschlüsselungsschlüssels für die Datenbank verwendet wurde, verfügbar sein. Dies bedeutet, dass Sie zusätzlich zur Sicherung der Datenbank auch Sicherungskopien der Serverzertifikate aufbewahren müssen, um einem Datenverlust vorzubeugen. Ist das Zertifikat nicht mehr verfügbar, kann es zu einem Datenverlust kommen.  
  
## <a name="commands-and-functions"></a>Befehle und Funktionen  
Die für TDE verwendeten Zertifikate müssen mithilfe des Datenbank-Hauptschlüssels verschlüsselt sein, damit sie von den folgenden Anweisungen akzeptiert werden.  
  
Die folgende Tabelle bietet Links und Erläuterungen zu den Befehlen und Funktionen von TDE.  
  
|Befehl oder Funktion|Zweck|  
|-----------------------|-----------|  
|[ERSTELLEN SIE DATENBANK-VERSCHLÜSSELUNGSSCHLÜSSEL](../t-sql/statements/create-database-encryption-key-transact-sql.md)|Erstellt einen Schlüssel, der verwendet wird, um eine Datenbank zu verschlüsseln.|  
|[ALTER DATABASE ENCRYPTION KEY](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Ändert den Schlüssel, der verwendet wird, um eine Datenbank zu verschlüsseln.|  
|[DROP DATABASE ENCRYPTION KEY](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Entfernt den Schlüssel, der verwendet wurde, um eine Datenbank zu verschlüsseln.|  
|[ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md)|Erklärt die **ALTER DATABASE** -Option, mit der TDE aktiviert wird.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Katalogsichten und dynamische Verwaltungssichten  
In der folgenden Tabelle werden die Katalogsichten und die dynamischen Verwaltungssichten von TDE erläutert.  
  
|Katalogsicht oder dynamische Verwaltungssicht|Zweck|  
|-------------------------------------------|-----------|  
|[sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Katalogsicht, die Datenbankinformationen anzeigt.|  
|[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Katalogsicht, die die Zertifikate in einer Datenbank anzeigt.|  
|[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|Dynamische Ansicht "Verwaltung", die Informationen für jeden Knoten, die in einer Datenbank und den Status der Verschlüsselung einer Datenbank verwendeten Verschlüsselungsschlüsseln bereitstellt.|  
  
## <a name="permissions"></a>Berechtigungen  
Jede Funktion und jeder Befehl von TDE erfordert bestimmte Berechtigungen, die in den zuvor gezeigten Tabellen beschrieben wurden.  
  
Zum Anzeigen der Metadaten, die Beziehung zu TDE ist die `CONTROL SERVER` Berechtigung.  
  
## <a name="considerations"></a>Weitere Überlegungen  
Während eine erneute Verschlüsselungsprüfung für einen Datenbankverschlüsselungsvorgang ausgeführt wird, sind Wartungsvorgänge für die Datenbank deaktiviert.  
  
Sie finden den Status der Verschlüsselung für die Datenbank mithilfe der **sys.dm_pdw_nodes_database_encryption_keys** -verwaltungssicht. Weitere Informationen finden Sie unter der *Katalogsichten und dynamische Verwaltungssichten* weiter oben in diesem Thema).  
  
### <a name="restrictions"></a>Restrictions  
Die folgenden Vorgänge sind nicht zulässig, während die `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, oder `ALTER DATABASE...SET ENCRYPTION` Anweisungen.  
  
-   Löschen der Datenbank.  
  
-   Mithilfe einer `ALTER DATABASE` Befehl.  
  
-   Starten Sie eine datenbanksicherung.  
  
-   Starten Sie eine Wiederherstellung der Datenbank.  
  
Die folgenden Vorgänge oder Bedingungen verhindern die `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, oder `ALTER DATABASE...SET ENCRYPTION` Anweisungen.  
  
-   Ein `ALTER DATABASE` -Befehl wird ausgeführt.  
  
-   Eine Datensicherung wird ausgeführt.  
  
Beim Erstellen von Datenbankdateien ist die sofortige Dateiinitialisierung nicht verfügbar, wenn TDE aktiviert ist.  
  
### <a name="areas-not-protected-by-tde"></a>Bereiche, die nicht durch TDE geschützt.  
TDE schützt die externe Tabellen nicht.  
  
TDE schützt nicht diagnosesitzungen. Benutzer sollten Sie vorsichtig sein, nicht für Abfragen mit sensible Parameter während diagnosesitzungen verwendet werden. Diagnosesitzungen, die vertraulichen Informationen offenlegen sollten gelöscht werden, sobald sie nicht mehr benötigt werden.  
  
Durch TDE geschützte Daten werden entschlüsselt, wenn im SQL Server PDW-Speicher abgelegt. Speicherabbilder werden erstellt, wenn bestimmte Probleme auf dem Gerät auftreten. Dump-Dateien stellen den Inhalt des Arbeitsspeichers zum Zeitpunkt der Darstellung Problem, und sensible Daten in unverschlüsselter Form enthalten. Der Inhalt des Speicherabbilder sollten überprüft werden, bevor sie mit anderen gemeinsam genutzt werden.  
  
Der master-Datenbank ist nicht mit TDE geschützt. Obwohl der master-Datenbank keine Benutzerdaten enthält, enthält er Informationen wie z. B. Anmeldenamen.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>Transparente Datenverschlüsselung und Transaktionsprotokolle  
Aktivieren einer Datenbank mit TDE ist die Wirkung unwiderrufliche des verbleibenden Teils des virtuellen Transaktionsprotokolls auf der nächste virtuelles Transaktionsprotokoll erzwungen. Dies gewährleistet, dass in den Transaktionsprotokollen kein Klartext verbleibt, nachdem die Datenbank für die Verschlüsselung eingerichtet wurde. Sie finden den Status der Verschlüsselungsstatus der Log-Datei auf jedem Knoten PDW durch Anzeigen der `encryption_state` Spalte in der `sys.dm_pdw_nodes_database_encryption_keys` anzeigen, wie in diesem Beispiel:  
  
```sql  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
           ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
Alle vor einer Änderung des Datenbank-Verschlüsselungsschlüssels in das Transaktionsprotokoll geschriebenen Daten werden mithilfe des vorherigen Verschlüsselungsschlüssels für die Datenbank verschlüsselt.  
  
### <a name="pdw-activity-logs"></a>PDW-Aktivitätsprotokolle  
SQL Server PDW verwaltet einen Satz von Protokollen, die für die Problembehandlung bei vorgesehen. (Beachten Sie dies nicht das Transaktionsprotokoll, das SQL Server-Fehlerprotokoll oder im Windows-Ereignisprotokoll ist.) Diese PDW Aktivitätsprotokolle können vollständige Anweisungen in Klartext enthalten, von die einige Benutzerdaten enthalten kann. Typische Beispiele dafür sind **einfügen** und **UPDATE** Anweisungen. Maskieren von Benutzerdaten kann werden explizit aktiviert oder deaktiviert mit **Sp_pdw_log_user_data_masking**. Aktivieren der Verschlüsselung für SQL Server PDW automatisch aktiviert das Maskieren von Benutzerdaten in PDW Aktivitätsprotokolle um sie zu schützen. **Sp_pdw_log_user_data_masking** kann auch verwendet werden, um Anweisungen zu maskieren, wenn TDE nicht verwenden, aber, wird nicht empfohlen, da es die Fähigkeit des Microsoft-Support-Team, Analysieren von Problemen erheblich reduziert wird.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparente Datenverschlüsselung und die tempdb-Systemdatenbank  
Die Tempdb-Systemdatenbank wird verschlüsselt, wenn Verschlüsselung aktiviert ist, indem Sie mithilfe von [sp_pdw_database_encryption aktiviert werden](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md). Dies ist erforderlich, bevor eine beliebige Datenbank TDE verwenden kann. Dies kann eine Auswirkung auf die Leistung unverschlüsselter Datenbanken auf derselben Instanz von SQL Server PDW haben.  
  
## <a name="key-management"></a>Schlüsselverwaltung  
Die Datenbank-Verschlüsselungsschlüssels (DEK) ist durch die Zertifikate in der master-Datenbank gespeicherten geschützt. Diese Zertifikate werden von Datenbank-Hauptschlüssels (DMK) der master-Datenbank geschützt. Der Datenbank-Hauptschlüssel muss mit dem Diensthauptschlüssel (SMK) geschützt werden, um für TDE verwendet werden.  
  
Das System kann die Schlüssel zugreifen, ohne Benutzereingriff (z. B. die Angabe eines Kennworts). Wenn das Zertifikat nicht verfügbar ist, wird das System ausgegeben, Fehler erläutert wird, dass der DEK nicht entschlüsselt werden kann, bis das richtige Zertifikat verfügbar ist.  
  
Beim Verschieben einer Datenbank von einer Anwendung in eine andere das Zertifikat zum Schützen der "DEK muss zuerst auf dem Zielserver wiederhergestellt werden. Anschließend kann die Datenbank wie gewohnt wiederhergestellt. Weitere Informationen finden Sie in der standardmäßigen SQL Server-Dokumentation unter [Verschieben einer TDE-geschützten Datenbank auf einen anderen SQL Server](http://technet.microsoft.com/library/ff773063.aspx).  
  
Zertifikate zum Verschlüsseln von DEKs sollte beibehalten werden, solange es werden datenbanksicherungen, die diese verwenden. Sicherungen des Zertifikats müssen dem privaten Schlüssel des Zertifikats enthalten, da ohne den privaten Schlüssel ein Zertifikats für die Wiederherstellung der Datenbank verwendet werden kann. Diese Zertifikat private Key-Sicherungen werden in einer separaten Datei gespeichert, geschützt durch ein Kennwort, die für die Zertifikat-Wiederherstellung bereitgestellt werden müssen.  
  
## <a name="restoring-the-master-database"></a>Wiederherstellen der master-Datenbank  
Der master-Datenbank kann wiederhergestellt werden, mithilfe von **DWConfig**, als Teil der Wiederherstellung im Notfall.  
  
-   Wenn der Knoten "Zugriffssteuerung" nicht geändert hat, handelt es sich, wenn der master-Datenbank auf der gleichen und unverändert Appliance wiederhergestellt wird, von dem die Sicherung der master-Datenbank erstellt wurde, der Datenbank-Hauptschlüssel und alle Zertifikate lesbar, ohne dass weitere Aktionen werden.  
  
-   Wenn der master-Datenbank auf einer anderen Appliance wiederhergestellt wird oder der Steuerelementknoten seit der Sicherung der master-Datenbank geändert wurde, werden zusätzliche Schritte erforderlich werden, um Datenbank-Hauptschlüssels erneut generieren.  
  
    1.  Öffnen Sie die Datenbank-Hauptschlüssel:  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  Fügen Sie die Verschlüsselung von SMK hinzu:  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  Neustart des Geräts an.  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>Aktualisieren und Ersetzen von virtuellen Computern  
Wenn ein Datenbank-Hauptschlüssel auf dem Gerät vorhanden für die Aktualisierung oder Ersetzen von VM ausgeführt wurde ist, muss die Datenbank-Hauptschlüssels ein Kennwort als Parameter angegeben werden.  
  
Beispiel für die Upgradeaktion. Ersetzen Sie `**********` durch Ihr Kennwort Datenbank-Hauptschlüssel.  
  
`setup.exe /Action=ProvisionUpgrade … DMKPassword='**********'  `  
  
Beispiel für die Aktion zum virtueller Maschinen ersetzen.  
  
`setup.exe /Action=ReplaceVM … DMKPassword='**********'  `  
  
Während des Upgrades wird bei einer Benutzerdatenbank wird verschlüsselt, und das Kennwort des Datenbank-Hauptschlüssel nicht angegeben wird, die Upgradeaktion fehl. Während ersetzen Wenn das richtige Kennwort nicht angegeben wird, wenn ein Datenbank-Hauptschlüssel vorhanden ist, überspringt der Vorgang den Datenbank-Hauptschlüssel Wiederherstellungsschritt. Am Ende der Replace-VM-Aktion werden die andere Schritte ausgeführt werden, jedoch die Aktion Fehler am Ende meldet, um anzugeben, dass zusätzliche Schritte erforderlich sind. In den Setupprotokollen (befindet sich im **\ProgramData\Microsoft\Microsoft SQL Server Parallel Data Warehouse\100\Logs\Setup\\< Zeitstempel > \Detail-Setup**), wird die folgende Warnung angezeigt, in der Nähe des.  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!  `
  
Führen Sie diese Anweisungen in PDW manuell, und starten Sie Appliance nach, die eine Wiederherstellung der Datenbank-Hauptschlüssel neu:  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
Verwenden Sie die Schritte in der **wiederherstellen den master-Datenbank** Absatz zum Wiederherstellen der Datenbank, und starten Sie das Gerät neu.  
  
Wenn der Datenbank-Hauptschlüssel vorhanden, bevor Sie waren jedoch nicht nach der Aktion wiederhergestellt wurde, wird die folgende Fehlermeldung angezeigt wird ausgelöst, wenn eine Datenbank abgefragt wird.  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>Leistungsauswirkungen  
Auswirkungen auf die Leistung von TDE ist mit dem Typ des vorhandenen Daten, wie er gespeichert wird und den Typ der arbeitsauslastung Aktivität in der SQL Server-PDW unterschiedlich. Wenn TDE-Schutz, wird der e/a der lesen und Entschlüsseln von Daten oder verschlüsseln und dann das Schreiben von Daten ist eine CPU-intensive Aktivität und hat weitere Auswirkung, wenn andere CPU-intensiven Aktivitäten zur gleichen Zeit auftreten. Da die TDE verschlüsselt `tempdb`, TDE kann beeinträchtigt die Leistung von Datenbanken, die nicht verschlüsselt sind. Um eine genaue Vorstellung der Leistung zu erhalten, sollten Sie das gesamte System mit Ihren Daten und Abfragen Aktivitäten testen.  
  
## <a name="related-content"></a>Verwandte Inhalte  
Die folgenden Links enthalten allgemeine Informationen zum Verwalten von Verschlüsselung in SQL Server. Diese Themen helfen Ihnen zu verstehen, SQL Server-Verschlüsselung, aber diese Themen keine Informationen, die spezifisch für SQL Server PDW und es werden Funktionen, die in SQL Server PDW nicht vorhanden sind.  
  
-   [SQL Server-Verschlüsselung](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [Verschlüsselungshierarchie](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [Verschlüsselungsschlüssel für SQL Server und Datenbank](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>Siehe auch  
[ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md)  
[ERSTELLEN VON HAUPTSCHLÜSSEL](../t-sql/statements/create-master-key-transact-sql.md)  
[ERSTELLEN SIE DATENBANK-VERSCHLÜSSELUNGSSCHLÜSSEL](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
