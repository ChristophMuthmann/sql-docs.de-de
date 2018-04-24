---
title: SQL Server-URL-Sicherung – bewährte Methoden und Problembehandlung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 305b5c00edd3f1a2549bbfaa6080d1fd37aa4103
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>SQL Server-URL-Sicherung – bewährte Methoden und Problembehandlung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden bewährte Methoden und Tipps zur Problembehandlung beschrieben, die sich auf SQL Server-Sicherungs- und Wiederherstellungsvorgänge im Windows Azure-BLOB-Dienst beziehen.  
  
 Weitere Informationen zur Verwendung des Windows Azure-BLOB-Speicherdiensts für SQL Server-Sicherungs- oder -Wiederherstellungsvorgänge finden Sie unter:  
  
-   [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Lernprogramm: SQL Server-Sicherung und -Wiederherstellung im Windows Azure-BLOB-Speicherdienst](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a>Verwalten von Sicherungen  
 Die folgende Liste enthält allgemeine Empfehlungen zur Verwaltung von Sicherungen:  
  
-   Für jede Sicherung sollte ein eindeutiger Dateiname verwendet werden, um zu verhindern, dass BLOBs versehentlich überschrieben werden.  
  
-   Beim Erstellen eines Containers wird empfohlen, die Zugriffsebene auf **Privat**festzulegen, sodass der Lese- oder Schreibzugriff auf Blobs im Container nur Benutzern oder Konten mit den erforderlichen Authentifizierungsinformationen gestattet ist.  
  
-   Um Übertragungskosten zwischen Regionen zu vermeiden, verwenden Sie für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf einem virtuellen Windows Azure-Computer ausgeführt wird, ein Speicherkonto, das derselben Region wie der virtuelle Computer angehört. Wenn Sie innerhalb einer Region bleiben, erzielen Sie darüber hinaus optimale Leistung bei Sicherungs- und Wiederherstellungsvorgängen.  
  
-   Eine fehlerhafte Sicherungsaktivität kann dazu führen, dass eine Sicherungsdatei unbrauchbar wird. Es wird empfohlen, regelmäßig nach fehlerhaften Sicherungen zu suchen und die BLOB-Dateien zu löschen. Weitere Informationen hierzu finden Sie unter [Löschen von Sicherungsblobdateien aktiver Lease](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
-   Wenn Sie die Sicherung mit der `WITH COMPRESSION`-Option durchführen, können Sie die Speicherkosten und Speichertransaktionskosten minimieren. Darüber hinaus verkürzt die Option die Dauer des Sicherungsvorgangs.  

- Legen Sie die Argumente `MAXTRANSFERSIZE` und `BLOCKSIZE` wie in dem Artikel [SQL Server-Sicherung über URLs](./sql-server-backup-to-url.md) empfohlen fest.
  
## <a name="handling-large-files"></a>Behandlung großer Dateien  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherungsvorgänge verwenden mehrere Threads, um die Datenübertragung an die Windows Azure-BLOB-Speicherdienste zu optimieren.  Die Leistung hängt jedoch von verschiedenen Faktoren ab wie der Bandbreite des unabhängigen Softwareherstellers (ISV) und der Größe der Datenbank. Wenn Sie beabsichtigen, große Datenbanken oder Dateigruppen von einer lokalen SQL Server-Datenbank zu sichern, sollten Sie zunächst den Durchsatz testen. Die [SLA zum Speicher](http://azure.microsoft.com/support/legal/sla/storage/v1_0/) von Azure bietet maximale Verarbeitungszeiten für Blobs, die Sie als Ausgangspunkt verwenden können.  
  
-   Die Verwendung der im Abschnitt [Verwalten von Sicherungen](##managing-backups) empfohlenen `WITH COMPRESSION`-Option ist besonders beim Sichern umfangreicher Dateien von Bedeutung.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>Problembehandlung bei Sicherungs- oder Wiederherstellungsvorgängen über URLs  
 Im Folgenden finden Sie einige schnelle Lösungen zur Behandlung von Sicherungs- und Wiederherstellungsfehlern im Windows Azure-BLOB-Speicherdienst.  
  
 Zur Vermeidung von Fehlern, die durch nicht unterstützte Optionen oder Einschränkungen verursacht werden, informieren Sie sich anhand der Liste im Artikel [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage-Dienst](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) über die Möglichkeiten und Grenzen von BACKUP- und RESTORE-Befehlen.  
  
 **Authentifizierungsfehler:**  
  
-   `WITH CREDENTIAL` ist eine neue Option, die für Sicherungs- oder Wiederherstellungsvorgänge im Windows Azure-BLOB-Speicherdienst erforderlich ist. In Zusammenhang mit Anmeldeinformationen können folgende Fehler auftreten:  
  
     Die im **BACKUP** -Befehl oder **RESTORE** -Befehl angegebenen Anmeldeinformationen sind nicht vorhanden. Um dieses Problem zu vermeiden, können Sie T-SQL-Anweisungen zum Erstellen von Anmeldeinformationen einschließen, falls in der BACKUP-Anweisung keine Anmeldeinformationen enthalten sind. Beachten Sie das folgende Anwendungsbeispiel:  
  
    ```sql  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
    ```  
  
-   Die Anmeldeinformationen sind zwar vorhanden, aber das Anmeldekonto zum Ausführen des Sicherungsbefehls verfügt über keine Berechtigung für den Zugriff auf die Anmeldeinformationen. Verwenden Sie ein Anmeldekonto aus der **db_backupoperator** -Rolle mit Berechtigungen für ***Beliebige Anmeldeinformationen ändern*** .  
  
-   Überprüfen Sie den Namen des Speicherkontos und die Schlüsselwerte. Die in den Anmeldeinformationen gespeicherten Informationen müssen den Eigenschaftswerten des Windows Azure-Speicherkontos entsprechen, das Sie für Sicherungs- und Wiederherstellungsvorgänge verwenden.  
  
 **Sicherungsfehler:**  
  
-   Parallele Sicherungen im selben Blob führen dazu, dass bei einer der Sicherungen die Meldung **Fehler beim Initialisieren** ausgegeben wird.  
  
-   Verwenden Sie die folgenden Fehlerprotokolle, die Ihnen die Problembehandlung bei Sicherungsfehlern erleichtern:  
  
    -   Legen Sie das Ablaufverfolgungsflag 3051 wie folgt fest, um die Protokollierung in einem bestimmten Fehlerprotokoll zu aktivieren:  
  
        `BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log`, wenn `\<action>` einer der folgenden Typen ist:  
  
        -   **DB**  
        -   **FILELISTONLY**  
        -   **LABELONLY**  
        -   **HEADERONLY**  
        -   **VERIFYONLY**  
  
    -   Ebenso erhalten Sie Informationen, wenn Sie im Windows-Ereignisprotokoll in den Anwendungsprotokollen nach dem Namen `SQLBackupToUrl` suchen.  
  
-   Bei der Wiederherstellung von einer komprimierten Sicherung kann eine Fehlermeldung mit etwa folgendem Wortlaut angezeigt werden:  
  
    -   `SqlException 3284 occurred. Severity: 16 State: 5  
        Message Filemark on device 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak' is not aligned.           Reissue the Restore statement with the same block size used to create the backupset: '65536' looks like a possible value.`  
  
        Um diesen Fehler zu beheben, führen Sie die **BACKUP** -Anweisung erneut aus, und geben Sie dabei **BLOCKSIZE = 65536** an.  
  
-   Sicherungsfehler aufgrund von BLOBs, die über eine aktive Leasedauer verfügen: Fehlerhafte Sicherungsaktivitäten können dazu führen, dass BLOBs eine aktive Leasedauer aufweisen.  
  
     Wenn die BACKUP-Anweisung erneut ausgeführt wird, kann ein Sicherungsvorgang einen Fehler mit etwa folgendem Wortlaut verursachen:  
  
     `Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (412) There is currently a lease on the blob and no lease ID was specified in the request.`  
  
     Wenn versucht wird, eine RESTORE-Anweisung für eine BLOB-Sicherungsdatei mit aktiver Leasedauer auszuführen, wird eine Fehlermeldung mit etwa folgendem Wortlaut angezeigt:  
  
     `Exception Message: The remote server returned an error: (409) Conflict..`  
  
     Wenn dieser Fehler auftritt, müssen die BLOB-Dateien gelöscht werden. Weitere Informationen zu diesem Szenario und Lösungsvorschläge finden Sie unter [Löschen von Sicherungsblobdateien mit aktiver Lease](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
## <a name="proxy-errors"></a>Proxyfehler  
 Wenn Sie über Proxyserver auf das Internet zugreifen, können folgende Probleme auftreten:  
  
 **Durch Proxyserver gedrosselte Verbindungen:**  
  
 Proxyserver können über Einstellungen verfügen, die die Anzahl der Verbindungen pro Minute begrenzen. Der URL-Sicherungsprozess ist ein Multithreadprozess und kann diese Begrenzung folglich überschreiten. In diesem Fall wird die Verbindung vom Proxyserver abgebrochen. Um das Problem zu beheben, ändern Sie die Proxyeinstellungen, damit der Proxy von SQL Server nicht verwendet wird. Im Folgenden einige Beispiele für Fehlertypen oder -meldungen, die im Fehlerprotokoll angezeigt werden können:  
  
```
Write on "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak" failed: Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
```
A nonrecoverable I/O error occurred on file "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Error could not be gathered from Remote Endpoint.  
  
Msg 3013, Level 16, State 1, Line 2  
  
BACKUP DATABASE is terminating abnormally.  
```

```
BackupIoRequest::ReportIoError: write failure on backup device http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak'. Operating system error Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
Wenn Sie die ausführliche Protokollierung mit Ablaufverfolgungsflag 3051 aktivieren, können auch folgende Meldungen in den Protokollen angezeigt werden:  
  
`HTTP status code 502, HTTP Status Message Proxy Error (The number of HTTP requests per minute exceeded the configured limit. Contact your ISA Server administrator.) ` 
  
 **Standardproxyeinstellungen wurden nicht abgerufen:**  
  
Teilweise werden die Standardeinstellungen nicht übernommen, wodurch ähnliche Proxyauthentifizierungsfehler wie die untenstehend aufgeführten entstehen:
 
 `A nonrecoverable I/O error occurred on file "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (407)* **Proxy Authentication Required.`  
  
Um dieses Problem zu beheben, erstellen Sie mithilfe folgender Schritte eine Konfigurationsdatei, durch die beim URL-Sicherungsprozess die Standardproxyeinstellungen verwendet werden können:  
  
1.  Erstellen Sie eine Konfigurationsdatei mit dem Namen `BackuptoURL.exe.config` und folgendem XML-Inhalt:  
  
    ```xml  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
    ```  
  
2.  Speichern Sie die Konfigurationsdatei im Ordner „Binn“ der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz. Beispiel: Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Computer auf Laufwerk C installiert ist, legen Sie die Konfigurationsdatei im Ordner `C:\Program Files\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\Binn` ab.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Wiederherstellen von in Microsoft Azure gespeicherten Sicherungen](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)
  
