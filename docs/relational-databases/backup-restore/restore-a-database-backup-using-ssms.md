---
title: Wiederherstellen einer Datenbanksicherung (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.locatebackupfileazure.f1
- sql13.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
caps.latest.revision: 79
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0d09693778fa9382d40dfb02f0c3fb4b212f86ed
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="restore-a-database-backup-using-ssms"></a>Restore a Database Backup Using SSMS
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird erläutert, wie eine vollständige Datenbanksicherung mit SQL Server Management Studio wiederhergestellt wird.    
       
### <a name="important"></a>Wichtig!    
Bevor eine Datenbank im vollständigen oder im massenprotokollierten Wiederherstellungsmodell wiederhergestellt werden kann, muss möglicherweise das Protokoll der aktiven Transaktion (als [Protokollfragment](https://msdn.microsoft.com/library/ms179314.aspx)bezeichnet) gesichert werden. Weitere Informationen finden Sie unter [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)bezeichnet) gesichert werden.  

Berücksichtigen Sie beim Wiederherstellen einer Datenbank aus einer anderen Instanz die Informationen unter [Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).   
    
Um eine verschlüsselte Datenbank wiederherzustellen, benötigen Sie Zugriff auf das Zertifikat oder den asymmetrischen Schlüssel, der zum Verschlüsseln der Datenbank verwendet wurde. Ohne das Zertifikat oder den asymmetrischen Schlüssel können Sie die Datenbank nicht wiederherstellen. Sie müssen das zum Verschlüsseln des Datenbankverschlüsselungsschlüssels verwendete Zertifikat so lange aufbewahren, wie die Sicherung gespeichert werden muss. Weitere Informationen finden Sie unter [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).    
    
Wenn Sie eine Datenbank einer älteren Version nach [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]wiederherstellen, wird diese Datenbank automatisch auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]aktualisiert.   
  
In der Regel ist die Datenbank sofort verfügbar. Wenn eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank Volltextindizes aufweist, werden diese beim Upgrade entweder importiert, zurückgesetzt oder neu erstellt, je nach der Einstellung der Servereigenschaft **Volltextupgrade-Option** . Wenn Sie die Upgradeoption auf **Importieren** oder **Neu erstellen**festlegen, sind die Volltextindizes während des Upgrades nicht verfügbar. Je nach Menge der indizierten Daten kann der Importvorgang mehrere Stunden dauern; die Neuerstellung dauert sogar bis zu zehnmal länger.     
    
Wenn die Upgradeoption auf **Importieren**festgelegt und kein Volltextkatalog verfügbar ist, werden die zugehörigen Volltextindizes neu erstellt. Informationen zum Anzeigen oder Ändern der Einstellung der Eigenschaft **Volltextupgrade-Option** finden Sie unter [Verwalten und Überwachen der Volltextsuche auf einer Serverinstanz](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).    

Informationen zur SQL Server-Wiederherstellung aus dem Microsoft Azure-BLOB-Speicherdienst finden Sie unter [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure-BLOB-Speicherdienst](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).

## <a name="examples"></a>Beispiele
    
### <a name="a-restore-a-full-database-backup"></a>**A. Wiederherstellen einer vollständigen Datenbanksicherung**    
    
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
    
2.  Klicken Sie mit der rechten Maustaste auf **Datenbanken** , und wählen Sie **Datenbank wiederherstellen**aus.    
    
3.  Legen Sie Quelle und Speicherort der wiederherzustellenden Sicherungssätze auf der Seite **Allgemein** mithilfe des Abschnitts **Quelle** fest. Wählen Sie eine der folgenden Optionen aus:    
    
    -   **Datenbank**    
    
         Wählen Sie die wiederherzustellende Datenbank aus der Dropdownliste aus. Die Liste enthält nur Datenbanken, die entsprechend dem Sicherungsverlauf von **msdb** gesichert wurden.    
    
    > **HINWEIS:** Wenn die Sicherung von einem anderen Server abgerufen wird, verfügt der Zielserver über keine Sicherungsverlaufsinformationen für die angegebene Datenbank. Wählen Sie in diesem Fall **Sicherungsmedium** aus, um die wiederherzustellende Datei oder das Medium manuell anzugeben. 
    
    -   **Sicherungsmedium**    
    
         Klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um das Dialogfeld **Sicherungsmedien auswählen** zu öffnen. 
         
        -   Dialogfeld**Sicherungsmedien auswählen**   
        
            **Sicherungsmedientyp**  
         Wählen Sie einen Medientyp aus der Dropdownliste **Sicherungsmedientyp** aus.  Hinweis: Die Option **Band** ist nur verfügbar, wenn ein Bandlaufwerk auf dem Computer bereitgestellt ist. Die Option **Sicherungsmedium** wird nur angezeigt, wenn mindestens ein Sicherungsmedium vorhanden ist.

            **Hinzufügen**  
            Abhängig vom Medientyp, den Sie in der Dropdownliste **Sicherungsmedientyp** ausgewählt haben, wird durch das Klicken auf **Hinzufügen** eines der folgenden Dialogfelder geöffnet. (Ist die Liste im Listenfeld **Sicherungsmedien** voll, ist die Schaltfläche **Hinzufügen** nicht verfügbar.)

            |Medientyp|Dialogfeld|Beschreibung|    
            |----------------|----------------|-----------------|    
            |**File**|**Sicherungsdatei suchen**|In diesem Dialogfeld können Sie eine lokale Datei aus der Struktur auswählen oder eine Remotedatei mithilfe des vollqualifizierten UNC-Namens (Universal Naming Convention) angeben. Weitere Informationen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|    
            |**Sicherungsmedium**|**Sicherungsmedium auswählen**|In diesem Dialogfeld können Sie aus einer Liste logischer Sicherungsmedien auswählen, die auf der Serverinstanz definiert sind.|    
            |**Band**|**Sicherungsband auswählen**|In diesem Dialogfeld können Sie aus einer Liste der Bandlaufwerke auswählen, die physisch mit dem Computer verbunden sind, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt wird.|    
            |**URL**|**Speicherort der Sicherungsdatei auswählen**|In diesem Dialogfeld können Sie vorhandene SQL Server-Anmeldeinformationen/Azure-Speichercontainer auswählen, einen neuen Azure-Speichercontainer mit einer Shared Access Signature (SAS) erstellen oder eine SAS und SQL Server-Anmeldeinformationen für einen vorhandenen Speichercontainer generieren.  Siehe auch [Herstellen einer Verbindung zu einem Microsoft Azure-Abonnement](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)|  
         
             **Entfernen**    
             Entfernt eine oder mehrere ausgewählte Dateien, Bänder oder logische Sicherungsmedien.    
                 
             **Inhalt**    
            Zeigt den Medieninhalt von ausgewählten Dateien, Bändern oder logischen Sicherungsmedien an.  Diese Schaltfläche funktioniert möglicherweise nicht, wenn der Medientyp **URL**ist.  

             **Sicherungsmedien**   
             Listet die ausgewählten Medien auf.
    
             Klicken Sie nach dem Hinzufügen der gewünschten Medien zum Listenfeld **Sicherungsmedien** auf **OK** , um zur Seite **Allgemein** zurückzukehren.    
    
         Wählen Sie im Listenfeld **Quelle: Sicherungsmedium: Datenbank** den Namen der Datenbank aus, die wiederhergestellt werden soll.    
    
        > **Hinweis:** Diese Liste ist nur verfügbar, wenn **Sicherungsmedium** ausgewählt wird. Nur Datenbanken mit Sicherungen auf dem ausgewählten Medium stehen zur Verfügung.    
     
4.  Im Abschnitt **Ziel** wird das Feld **Datenbank** automatisch mit dem Namen der Datenbank aufgefüllt, die wiederhergestellt werden soll. Geben Sie zum Ändern des Datenbanknamens den neuen Namen ins Feld **Datenbank** ein.    
    
5.  Übernehmen Sie im Feld **Wiederherstellen in** den Standardwert **Bis zur zuletzt erstellten Sicherung** , oder klicken Sie auf **Zeitachse** , um auf das Dialogfeld **Sicherungszeitachse** zuzugreifen und darin manuell einen Zeitpunkt zum Beenden des Wiederherstellungsvorgangs auszuwählen. Weitere Informationen zum Festlegen eines bestimmten Zeitpunkts finden Sie unter [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md).    
    
6.  Wählen Sie im Raster **Wiederherzustellende Sicherungssätze** die wiederherzustellenden Sicherungen aus. Mit diesem Raster werden die Sicherungen angezeigt, die für den angegebenen Speicherort verfügbar sind. Standardmäßig wird ein Wiederherstellungsplan vorgeschlagen. Sie können die Auswahl im Raster ändern, um den vorgeschlagenen Wiederherstellungsplan zu überschreiben. Die Auswahl von Sicherungen, die von der Wiederherstellung einer früheren Sicherung abhängig sind, wird automatisch aufgehoben, wenn die Auswahl der früheren Sicherung aufgehoben wird. Weitere Informationen zu den Spalten des Rasters **Wiederherzustellende Sicherungssätze** finden Sie unter [Datenbank wiederherstellen &#40;Seite „Allgemein“&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)bezeichnet) gesichert werden.    
    
7.  Klicken Sie optional im Bereich **Seite auswählen** auf **Dateien** , um auf das Dialogfeld **Dateien** zuzugreifen. Hier können Sie die Datenbank an einem neuen Ort wiederherstellen, indem Sie für die einzelnen Dateien im Raster **Datenbankdateien wiederherstellen als** ein neues Wiederherstellungsziel angeben. Weitere Informationen zu diesem Raster finden Sie unter [Datenbank wiederherstellen &#40;Seite „Dateien“&#41;](../../relational-databases/backup-restore/restore-database-files-page.md).    
    
8. Zum Anzeigen oder Auswählen der erweiterten Optionen können Sie auf der Seite **Optionen** im Bereich **Wiederherstellungsoptionen** die folgenden für Ihre Situation zutreffenden Optionen auswählen:    
    
    1.  **WITH** -Optionen (nicht erforderlich):    
    
        -   **Vorhandene Datenbank überschreiben (WITH REPLACE)**    
    
        -   **Replikationseinstellungen beibehalten (WITH KEEP_REPLICATION)**    
    
        -   **Zugriff auf die wiederhergestellte Datenbank einschränken (WITH RESTRICTED_USER)**    
    
    2.  Aktivieren Sie eine Option für das Feld **Wiederherstellungsstatus** . In diesem Feld wird der Status der Datenbank nach dem Wiederherstellungsvorgang bestimmt.    
    
        -   **RESTORE WITH RECOVERY** ist das Standardverhalten, das die Datenbank betriebsbereit belässt, indem für Transaktionen ohne Commit ein Rollback ausgeführt wird. Zusätzliche Transaktionsprotokolle können nicht wiederhergestellt werden. Wählen Sie diese Option nur aus, wenn Sie alle benötigten Sicherungen jetzt wiederherstellen möchten.    
    
        -   **RESTORE WITH NORECOVERY** belässt die Datenbank nicht betriebsbereit und führt kein Rollback für Transaktionen ohne Commit aus. Zusätzliche Transaktionsprotokolle können wiederhergestellt werden. Die Datenbank kann erst verwendet werden, wenn sie wiederhergestellt wurde.    
    
        -   **RESTORE WITH STANDBY** belässt die Datenbank im schreibgeschützten Modus. Diese Option macht Transaktionen rückgängig, für die noch kein Commit ausgeführt wurde, speichert die Umkehraktionen aber in einer Standbydatei, damit die Auswirkungen der Wiederherstellung rückgängig gemacht werden können.    
    
    3.  **Protokollfragment vor der Wiederherstellung sichern.** Nicht für alle Wiederherstellungsszenarien ist eine Sicherung des Protokollfragments erforderlich.  Weitere Informationen finden Sie unter **Szenarien, die eine Sicherung des Protokollfragments erfordern** aus [Protokollfragmentsicherungen (SQL Server).](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)
    
    4.  Bei Wiederherstellungsvorgängen treten möglicherweise Fehler auf, wenn aktive Verbindungen zur Datenbank bestehen. Aktivieren Sie die Option **Bestehende Verbindungen schließen** , um sicherzustellen, dass alle aktiven Verbindungen zwischen [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] und der Datenbank geschlossen werden. Durch die Aktivierung dieses Kontrollkästchens wechselt die Datenbank in einen Einzelbenutzermodus, bevor Wiederherstellungsvorgänge ausgeführt werden. Außerdem wird dadurch die Datenbank auf einen Multibenutzermodus festgelegt, wenn der Vorgang abgeschlossen ist.    
    
    5.  Wählen Sie **Bestätigung vor Wiederherstellen jeder einzelnen Sicherung** aus, wenn Sie zwischen jedem Wiederherstellungsvorgang zur Bestätigung aufgefordert werden möchten. Dies ist in der Regel nur bei großen Datenbanken und bei der gewünschten Überwachung des Status des Wiederherstellungsvorgangs erforderlich.    
    
     Weitere Informationen zu diesen Wiederherstellungsoptionen finden Sie unter [Datenbank wiederherstellen &#40;Seite „Optionen“&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)bezeichnet) gesichert werden.    
    
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="b-restore-an-earlier-disk-backup-over-an-existing-database"></a>**B. Wiederherstellen einer früheren Datenträgersicherung über eine vorhandene Datenbank**    
Im folgenden Beispiel wird eine frühere Datenträgersicherung von `Sales` wiederhergestellt und dabei die vorhandene `Sales` -Datenbank überschrieben.

1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
    
2.  Klicken Sie mit der rechten Maustaste auf **Datenbanken** , und wählen Sie **Datenbank wiederherstellen**aus.  

3.  Wählen Sie auf der Seite **Allgemein** im Abschnitt **Quelle** die Option **Gerät** aus.

4.  Klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um das Dialogfeld **Sicherungsmedien auswählen** zu öffnen. Klicken Sie auf **Hinzufügen** , und navigieren Sie Ihrer Sicherung.  Nachdem Sie Ihre Datenträgersicherungsdatei(en) ausgewählt haben, klicken Sie auf **OK** .

5.  Klicken Sie auf **OK** , um zur Seite **Allgemein** zurückzukehren.

6.  Klicken Sie im Abschnitt **Seite auswählen** auf **Optionen** .

7.  Aktivieren Sie im Abschnitt **Wiederherstellungsoptionen** die Option **Vorhandene Datenbank überschreiben (WITH REPLACE)**.

    > **Hinweis:** Wenn Sie diese Option nicht aktivieren, wird möglicherweise die folgende Fehlermeldung angezeigt: „System.Data.SqlClient.SqlError: Der Sicherungssatz enthält die Sicherung einer anderen Datenbank als der vorhandenen `Sales`-Datenbank“. (Microsoft.SqlServer.SmoExtended)“

8.  Deaktivieren Sie im Abschnitt **Sicherung des Protokollfragments** die Option **Protokollfragment vor der Wiederherstellung sichern**.

    > **HINWEIS:** Nicht für alle Wiederherstellungsszenarien ist eine Sicherung des Protokollfragments erforderlich. Sie benötigen keine Sicherung des Protokollfragments, wenn der Wiederherstellungspunkt in einer früheren Protokollsicherung enthalten ist. Eine Sicherung des Protokollfragments ist auch dann nicht erforderlich, wenn Sie eine Datenbank verschieben oder ersetzen (überschreiben) und sie nicht für einen Zeitpunkt nach der letzten Sicherung wiederherstellen müssen.  Weitere Informationen finden Sie unter [Protokollfragmentsicherungen (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).
Diese Option ist für Datenbanken im einfachen Wiederherstellungsmodell nicht verfügbar.

9.  Aktivieren Sie im Abschnitt **Serververbindungen** das Kontrollkästchen **Bestehende Verbindungen mit der Zieldatenbank schließen**.

    > **Hinweis:** Wenn Sie diese Option nicht aktivieren, wird möglicherweise die folgende Fehlermeldung angezeigt: „System.Data.SqlClient.SqlError: Der exklusive Zugriff auf die Datenbank ist nicht möglich, da die Datenbank gerade verwendet wird.“ (Microsoft.SqlServer.SmoExtended)“
    
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="c--restore-an-earlier-disk-backup-with-a-new-database-name-where-the-original-database-still-exists"></a>**C.  Wiederherstellen einer früheren Datenträgersicherung mit einem neuen Datenbanknamen unter Beibehaltung der ursprünglichen Datenbank**
Im folgenden Beispiel wird eine frühere Datenträgersicherung von `Sales` wiederhergestellt und dabei eine neue Datenbank mit dem Namen `SalesTest`erstellt.  Die ursprüngliche Datenbank `Sales`bleibt auf dem Server erhalten.

1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
    
2.  Klicken Sie mit der rechten Maustaste auf **Datenbanken** , und wählen Sie **Datenbank wiederherstellen**aus.  

3.  Wählen Sie auf der Seite **Allgemein** im Abschnitt **Quelle** die Option **Gerät** aus.

4.  Klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um das Dialogfeld **Sicherungsmedien auswählen** zu öffnen. Klicken Sie auf **Hinzufügen** , und navigieren Sie Ihrer Sicherung.  Nachdem Sie Ihre Datenträgersicherungsdatei(en) ausgewählt haben, klicken Sie auf **OK** .

5.  Klicken Sie auf **OK** , um zur Seite **Allgemein** zurückzukehren.

6.  Im Abschnitt **Ziel** wird das Feld **Datenbank** automatisch mit dem Namen der Datenbank aufgefüllt, die wiederhergestellt werden soll.  Geben Sie zum Ändern des Datenbanknamens den neuen Namen ins Feld **Datenbank** ein.

7.  Klicken Sie im Abschnitt **Seite auswählen** auf **Optionen** .

8.  Deaktivieren Sie im Abschnitt **Sicherung des Protokollfragments** die Option**Protokollfragment vor der Wiederherstellung sichern**.

    > **WICHTIG!** Wenn Sie diese Option nicht deaktivieren, wechselt die vorhandene `Sales`-Datenbank in den Status RESTORING.

9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

    > **Hinweis:** Sollte die folgende Fehlermeldung „System.Data.SqlClient.SqlError: Das Protokollfragment für die `Sales`-Datenbank wurde nicht gesichert“ angezeigt werden: Sichern Sie das Protokoll mit BACKUP LOG WITH NORECOVERY, falls es Daten enthält, die Sie nicht verlieren möchten. Verwenden Sie die WITH REPLACE- oder WITH STOPAT-Klausel der RESTORE-Anweisung, um den Inhalt des Protokolls zu überschreiben. (Microsoft.SqlServer.SmoExtended)“.  
angezeigt wird, haben Sie wahrscheinlich nicht den neuen Datenbanknamen aus Schritt 6 oben eingegeben.  Die Wiederherstellung verhindert normalerweise, dass eine Datenbank versehentlich durch eine andere Datenbank überschrieben wird.  Wenn die in einer RESTORE-Anweisung angegebene Datenbank bereits auf dem aktuellen Server vorhanden ist und sich die angegebene GUID der Datenbankfamilie von der im Sicherungssatz aufgezeichneten GUID der Datenbankfamilie unterscheidet, wird die Datenbank nicht wiederhergestellt. Dies ist ein wichtiges Sicherheitselement.

### <a name="d--restore-earlier-disk-backups-to-a-point-in-time"></a>**D.  Wiederherstellen früherer Datenträgersicherungen bis zu einem bestimmten Zeitpunkt**
Im folgenden Beispiel wird eine Datenbank in den am 30. Mai 2016 um 13:23:17 Uhr bestehenden Status wiederhergestellt und ein Wiederherstellungsvorgang gezeigt, der mehrere Protokollsicherungen umfasst.  Die Datenbank ist auf dem Server derzeit nicht vorhanden.

1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
    
2.  Klicken Sie mit der rechten Maustaste auf **Datenbanken** , und wählen Sie **Datenbank wiederherstellen**aus.  

3.  Wählen Sie auf der Seite **Allgemein** im Abschnitt **Quelle** die Option **Gerät** aus.

4.  Klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um das Dialogfeld **Sicherungsmedien auswählen** zu öffnen. Klicken Sie auf **Hinzufügen** , und navigieren Sie zu der vollständigen Sicherung und allen relevanten Transaktionsprotokollsicherungen.  Nachdem Sie Ihre Datenträgersicherungsdateien ausgewählt haben, klicken Sie auf **OK** .

5.  Klicken Sie auf **OK** , um zur Seite **Allgemein** zurückzukehren.

6.  Klicken Sie im Abschnitt **Ziel** auf **Zeitachse** , um auf das Dialogfeld **Sicherungszeitachse** zuzugreifen und darin manuell einen Zeitpunkt zum Beenden des Wiederherstellungsvorgangs auszuwählen.

7.  Wählen Sie **Bestimmtes Datum und bestimmte Uhrzeit**aus.
8.  Ändern Sie die Einstellung von **Zeitachsenintervall** im Dropdownfeld auf **Stunde** (optional).
9.  Verschieben Sie den Schieberegler auf die gewünschte Zeit.

10. Klicken Sie auf **OK** , um zur Seite „Allgemein“ zurückzukehren.

11. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="e--restore-a-backup-from-the-microsoft-azure-storage-service"></a>**E.  Wiederherstellen einer Sicherung aus dem Microsoft Azure-Speicherdienst**
#### <a name="common-steps"></a>**Allgemeine Schritte**
In den beiden folgenden Beispielen wird eine Wiederherstellung von `Sales` aus einer Sicherung ausgeführt, die sich im Microsoft Azure-Speicherdienst befindet.  Der Speicherkontoname lautet `mystorageaccount`.  Der Container heißt `myfirstcontainer`.  Aus Gründen der Übersichtlichkeit sind die ersten sechs Schritte hier einmal aufgelistet und alle Beispiele beginnen mit **Schritt 7**.
1.  Stellen Sie im ****Objekt-Explorer eine Verbindung mit einer Instanz des SQL Server-Datenbankmoduls her, und erweitern Sie dann diese Instanz.

2.  Klicken Sie mit der rechten Maustaste auf **Datenbanken** , und wählen Sie **Datenbank wiederherstellen**aus.

3.  Wählen Sie auf der Seite **Allgemein** im Abschnitt **Quelle** die Option **Gerät** aus.

4.  Klicken Sie auf die Schaltfläche zum Durchsuchen (...), um das Dialogfeld **Sicherungsmedien auswählen** zu öffnen.  
5.  Wählen Sie eine **URL** aus der Dropdownliste **Sicherungsmedientyp** aus.

6.  Klicken Sie auf **Hinzufügen** . Das Dialogfeld **Speicherort der Sicherungsdatei auswählen** wird geöffnet.

    #### <a name="e1---restore-a-striped-backup-over-an-existing-database-and-a-shared-access-signature-exists"></a>**E1.   Wiederherstellen einer Sicherung im Stripesetformat über eine vorhandene Datenbank; eine Shared Access Signature (SAS) ist vorhanden.**
    Eine gespeicherte Zugriffsrichtlinie wurde mit Lese-, Schreib-, Lösch- und Auflistungsrechten erstellt.  Eine SAS, die der gespeicherten Zugriffsrichtlinie zugeordnet ist, wurde für den Container `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`erstellt.  Die Schritte sind weitestgehend identisch, wenn bereits SQL Server-Anmeldeinformationen vorhanden sind.  Die Datenbank `Sales` ist auf dem Server bereits vorhanden.  Die Sicherungsdateien sind `Sales_stripe1of2_20160601.bak` und `Sales_stripe2of2_20160601.bak`.  
*  
    7.  Wählen Sie `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` aus dem **Azure-Speichercontainer aus:** über die Dropdown-Liste, wenn die SQL Server-Anmeldeinformationen bereits vorhanden sind, andernfalls geben Sie den Namen des Containers ( `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`) manuell ein.
    
    8.  Geben Sie die SAS im **Shared Access Signature:** -Feld für Rich-Text ein.
       9.   Klicken Sie auf **OK** . Das Dialogfeld **Sicherungsdatei in Microsoft Azure suchen** wird geöffnet.
    10. Erweitern Sie **Container** , und navigieren Sie zu `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`.
    
    11. Halten Sie STRG gedrückt, und wählen Sie die Dateien `Sales_stripe1of2_20160601.bak` und `Sales_stripe2of2_20160601.bak`aus.
    12. Klicken Sie auf **OK**.
    13. Klicken Sie auf **OK** , um zur Seite **Allgemein** zurückzukehren.
    14. Klicken Sie im Abschnitt **Seite auswählen** auf **Optionen** .
    15. Aktivieren Sie im Abschnitt **Wiederherstellungsoptionen** die Option **Vorhandene Datenbank überschreiben (WITH REPLACE)**.
    16. Deaktivieren Sie im Abschnitt **Sicherung des Protokollfragments** die Option **Protokollfragment vor der Wiederherstellung sichern.**.
    17. Aktivieren Sie im Abschnitt **Serververbindungen** das Kontrollkästchen **Bestehende Verbindungen mit der Zieldatenbank schließen**.
    18. Klicken Sie auf **OK**.

    #### <a name="e2---a-shared-access-signature-does-not-exist"></a>**E2.   Es ist keine Shared Access Signature (SAS) vorhanden.**
    In diesem Beispiel ist die Datenbank `Sales` auf dem Server derzeit nicht vorhanden.
    7.  Klicken Sie auf **Hinzufügen** . Das Dialogfeld **Verbindung mit einen Microsoft Abonnement herstellen** wird geöffnet.  
    
    8.  Füllen Sie das Dialogfeld **Verbindung mit einen Microsoft Abonnement herstellen** aus, und klicken Sie dann auf **OK** um zum Dialogfeld **Speicherort der Sicherungsdatei auswählen** zurückzukehren.  Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einen Microsoft Abonnement](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) .
    9.  Klicken Sie im Dialogfeld **Speicherort der Sicherungsdatei auswählen** auf **OK** . Das Dialogfeld **Sicherungsdatei in Microsoft Azure suchen** wird geöffnet.
    10. Erweitern Sie **Container** , und navigieren Sie zu `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`.
    11. Wählen Sie die Sicherungsdatei aus, und klicken Sie dann auf **OK**.
    12. Klicken Sie auf **OK** , um zur Seite **Allgemein** zurückzukehren.
    13. Klicken Sie auf **OK**.

#### <a name="f---restore-local-backup-to-microsoft-azure-storage-url"></a>**F.   Wiederherstellen einer lokalen Sicherung in Microsoft Azure-Speicher (URL)**
Die Datenbank `Sales` wird aus einer Sicherung unter `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` im Microsoft Azure-Speichercontainer `E:\MSSQL\BAK`wiederhergestellt.  Die SQL Server-Anmeldeinformationen für den Azure-Container wurden bereits erstellt.  SQL Server-Anmeldeinformationen für den Zielcontainer müssen bereits vorhanden sein, da sie durch den **Wiederherstellungstask** nicht erstellt werden können.  Die Datenbank `Sales` ist auf dem Server derzeit nicht vorhanden.
1.  Stellen Sie im ****Objekt-Explorer eine Verbindung mit einer Instanz des SQL Server-Datenbankmoduls her, und erweitern Sie dann diese Instanz.

2.  Klicken Sie mit der rechten Maustaste auf **Datenbanken** , und wählen Sie **Datenbank wiederherstellen**aus.
3.  Wählen Sie auf der Seite **Allgemein** im Abschnitt **Quelle** die Option **Gerät** aus.
4.  Klicken Sie auf die Schaltfläche zum Durchsuchen (...), um das Dialogfeld **Sicherungsmedien auswählen** zu öffnen.  
5.  Wählen Sie eine **Datei** aus der Dropdownliste **Sicherungsmedientyp** aus.
6.  Klicken Sie auf **Hinzufügen** . Das Dialogfeld **Sicherungsdatei suchen** wird geöffnet.
7.  Navigieren Sie zu `E:\MSSQL\BAK`, wählen Sie die Sicherungsdatei aus, und klicken Sie dann auf **OK**.
8.  Klicken Sie auf **OK** , um zur Seite **Allgemein** zurückzukehren.
9.  Klicken Sie im Fensterbereich **Seite auswählen** auf **Dateien** .
10. Aktivieren Sie das Kontrollkästchen **Alle Dateien verschieben in Ordner**.
11. Geben Sie den Container ( `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`) in die Textfelder für **Datendateiordner:** und **Protokolldateiordner:**ein.
12. Klicken Sie auf **OK**.


## <a name="see-also"></a>Siehe auch    
 [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)     
 [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)     
 [Wiederherstellen einer Datenbank an einem neuen Speicherort &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)     
 [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)     
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [Datenbank wiederherstellen &#40;Seite „Optionen“&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)     
 [Datenbank wiederherstellen &#40;Seite „Allgemein“&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)    
    
  

