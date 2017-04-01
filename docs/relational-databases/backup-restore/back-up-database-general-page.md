---
title: "Datenbank sichern (Seite Allgemein) | Microsoft Docs"
ms.custom: ""
ms.date: "07/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.backupdatabase.general.f1"
ms.assetid: 5c344dfd-1ad3-41cc-98cd-732973b4a162
caps.latest.revision: 64
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 64
---
# Datenbank sichern (Seite Allgemein)
  Verwenden Sie im Dialogfeld **Datenbank sichern** die Seite **Allgemein** , um die Einstellungen für einen Sicherungsvorgang der Datenbank anzuzeigen und zu ändern.  
  
 Weitere Informationen zu grundlegenden Sicherungskonzepten finden Sie unter [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
> [!NOTE]  
>  Wenn Sie eine Sicherungsaufgabe mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angeben, können Sie das entsprechende [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md)-Skript generieren, indem Sie auf die Schaltfläche **Skript** klicken und anschließend ein Ziel für das Skript auswählen.  
  
 **So verwenden Sie SQL Server Management Studio zum Erstellen einer Sicherung**  
  
-   [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
    > [!IMPORTANT]  
    >  Sie können einen Datenbank-Wartungsplan definieren, um Datenbanksicherungen zu erstellen. Weitere Informationen über [Datenbank-Wartungspläne](http://msdn.microsoft.com/library/ms187658.aspx) finden Sie in der [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] -Onlinedokumentation.  
  
 **So erstellen Sie eine Teilsicherung**  
  
-   Für eine Teilsicherung müssen Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md)-Anweisung mit der Option PARTIAL verwenden.  
  
## Optionen  
  
### Quelle  
 Mithilfe der Optionen des Bereichs **Quelle** werden die Datenbank identifiziert und der Sicherungstyp und die Sicherungskomponente für den Sicherungsvorgang angegeben.  
  
 **Datenbank**  
 Wählen Sie die zu sichernde Datenbank aus.  
  
 **Wiederherstellungsmodell**  
 Zeigt das Wiederherstellungsmodell (SIMPLE, FULL oder BULK_LOGGED) für die ausgewählte Datenbank an.  
  
 **Sicherungstyp**  
 Wählen Sie den Sicherungstyp aus, der für die angegebene Datenbank ausgeführt werden soll.  
  
|Sicherungstyp|Verfügbar für|Einschränkungen|  
|-----------------|-------------------|------------------|  
|Full|Datenbanken, Dateien und Dateigruppen|Bei der **master** -Datenbank sind nur vollständige Sicherungen möglich.<br /><br /> Beim einfachen Wiederherstellungsmodell sind Datei- und Dateigruppensicherungen nur für schreibgeschützte Dateigruppen verfügbar.|  
|Differenziell|Datenbanken, Dateien und Dateigruppen|Beim einfachen Wiederherstellungsmodell sind Datei- und Dateigruppensicherungen nur für schreibgeschützte Dateigruppen verfügbar.|  
|Transaktionsprotokoll|Transaktionsprotokolle|Transaktionsprotokollsicherungen sind beim einfachen Wiederherstellungsmodell nicht verfügbar.|  
  
 **Kopiesicherung**  
 Wählen Sie diese Option aus, um eine Kopiesicherung zu erstellen. Eine *Kopiesicherung* ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherung, die unabhängig von der Sequenz von herkömmlichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherungen erstellt wird. Weitere Informationen finden Sie unter [Kopiesicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
> [!NOTE]  
>  Wenn die Option **Differenziell** aktiviert ist, können Sie keine Kopiesicherung erstellen.  
  
 **Sicherungskomponente**  
 Wählen Sie die zu sichernde Datenbankkomponente aus. Wenn in der Liste **Sicherungstyp** der Eintrag **Transaktionsprotokoll** ausgewählt wird, ist diese Option nicht aktiviert.  
  
 Wählen Sie eines der folgenden Optionsfelder aus:  
  
|||  
|-|-|  
|**Datenbank**|Gibt an, dass die gesamte Datenbank gesichert werden soll.|  
|**Dateien und Dateigruppen**|Gibt an, dass die angegebenen Dateien und/oder Dateigruppen gesichert werden sollen.<br /><br /> Durch das Auswählen dieser Option wird das Dialogfeld **Dateien und Dateigruppen auswählen** geöffnet. Nach dem Auswählen der zu sichernden Dateigruppen oder Dateien und dem Klicken auf **OK**wird die Auswahl im Feld **Dateien und Dateigruppen** angezeigt.|  
  
### Ziel  
 Mit den Optionen des Bereichs **Ziel** können Sie den Typ des Sicherungsmediums für den Sicherungsvorgang angeben und ein vorhandenes logisches oder physisches Sicherungsmedium suchen.  
  
> [!NOTE]  
>  Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherungsmedien finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 **Sichern auf**  
 Wählen Sie einen der folgenden Medientypen aus, auf denen gesichert werden soll. Die ausgewählten Ziele werden in der Liste **Sichern auf** angezeigt.  
  
|||  
|-|-|  
|**Datenträger**|Sicherung auf einem Datenträger. Hierbei kann es sich um eine Systemdatei oder ein datenträgerbasiertes logisches Sicherungsmedium handeln, das für die Datenbank erstellt wurde. Die aktuell ausgewählten Datenträger werden in der Liste **Sichern auf** angezeigt. Sie können bis zu 64 Datenträger für den Sicherungsvorgang auswählen.|  
|**Band**|Sicherung auf einem Band. Hierbei kann es sich um ein lokales Bandlaufwerk oder ein bandbasiertes logisches Sicherungsmedium handeln, das für die Datenbank erstellt wurde. Die aktuell ausgewählten Bänder werden in der Liste **Sichern auf** angezeigt. Es können maximal 64 Werte angegeben werden. Wenn keine Bandmedien mit dem Server verbunden sind, ist diese Option deaktiviert. Die ausgewählten Bänder werden in der Liste **Sichern auf** aufgeführt.<br /><br /> Die Unterstützung für Bandsicherungsgeräte wird in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entfernt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.|  
|**URL**|Sicherung im Microsoft Azure-BLOB-Speicher|  
  
 Welche Optionen als Nächstes angezeigt werden, ist abhängig vom Typ des ausgewählten Ziels. Wenn Sie einen Datenträger oder ein Band auswählen, werden die folgenden Optionen angezeigt:  
  
 **Hinzufügen**  
 Fügt der Liste **Sichern auf** eine Datei oder ein Medium hinzu. Sie können auf 64 Medien gleichzeitig auf einem lokalen Datenträger oder Remotedatenträger sichern. Verwenden Sie den vollqualifizierten UNC-Namen (Universal Naming Convention), um eine Datei auf einem Remotedatenträger anzugeben. Weitere Informationen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
 
 
  
 **Entfernen**  
 Entfernt mindestens ein aktuell ausgewähltes Medium aus der Liste **Sichern auf**.  
  
 **Inhalt**  
Zeigt den Medieninhalt des ausgewählten Mediums an, sofern es vorhanden ist.  Die Schaltfläche führt keine Funktion aus, wenn eine **URL** angegeben ist. 
   
Dialogfeld **Sicherungsziel auswählen**: Das Dialogfeld **Sicherungsziel auswählen** wird angezeigt, nachdem Sie die Option **Hinzufügen** auswählen.   Welche Optionen angezeigt werden, ist abhängig vom Typ des ausgewählten Ziels. 

Wenn Sie **Datenträger** oder **Band** als Sicherungsziel auswählen, wird die folgende Option angezeigt.  

*
  **Dateiname**  
    Geben Sie den Namen der Sicherungsdatei an.

Wenn Sie eine **URL** als Sicherungsziel ausgewählt haben, werden die folgenden Optionen angezeigt:
*
  **Azure-Speichercontainer**  
  Der Name des Microsoft Azure-Speichercontainers, um die Sicherungsdateien zu speichern. 
   
*
  **Richtlinie für den gemeinsamen Zugriff:**  
  Geben Sie die SAS (Shared Access Signature) für einen manuell eingegebenen Container an.  Dieses Feld ist nicht verfügbar, wenn ein vorhandener Container ausgewählt wurde.
  
*
  **Sicherungsdatei:**  
  Name der Sicherungsdatei.

*
  **Neuer Container:**  
Wird verwendet, um einen vorhandenen Container zu registrieren, für den Sie keine SAS besitzen.  Weitere Informationen finden Sie unter [Herstellen einer Verbindung zu einem Microsoft Azure-Abonnement](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md).
  
## Siehe auch  
 [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Sichern von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Definieren eines logischen Sicherungsmediums für eine Datenträgerdatei &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  