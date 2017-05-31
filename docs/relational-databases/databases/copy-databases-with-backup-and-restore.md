---
title: Kopieren von Datenbanken durch Sichern und Wiederherstellen | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/15/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], back up and restore
- restoring databases [SQL Server], previous SQL Server versions
- database restores [SQL Server], copying databases
- restoring databases [SQL Server], onto another server instance
- restoring [SQL Server], onto another server instance
- backing up databases [SQL Server], copying databases
- database backups [SQL Server], copying databases
ms.assetid: b93e9701-72a0-408e-958c-dc196872c040
caps.latest.revision: 61
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aa3c7efcaa066953595525819686c612b5a9aee5
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="copy-databases-with-backup-and-restore"></a>Kopieren von Datenbanken durch Sichern und Wiederherstellen
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie eine neue Datenbank erstellen, indem Sie die Sicherung einer Benutzerdatenbank wiederherstellen, die mithilfe von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder einer höheren Version erstellt wurde. Sicherungen der **master**-, **model** - und **msdb** -Datenbank, die mit einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt wurden, können von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]nicht wiederhergestellt werden. Außerdem können [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Sicherungen nicht mit einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wiederhergestellt werden.  
  
>**WICHTIG!** SQL Server 2016 verwendet im Vergleich zu früheren Versionen einen anderen Standardpfad. Daher muss zur Wiederherstellung von Sicherungen einer Datenbank, die im Standardverzeichnis früherer Versionen erstellt wurden, die MOVE-Option verwendet werden. Informationen zum neuen Standardpfad finden Sie unter [File Locations for Default and Named Instances of SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md). Weitere Informationen zum Verschieben von Datenbankdateien finden Sie weiter unten in diesem Thema unter "Verschieben der Datenbankdateien".  
  
## <a name="general-steps-for-using-backup-and-restore-to-copy-a-database"></a>Allgemeine Schritte zum Verwenden der Sicherung und Wiederherstellung zum Kopieren einer Datenbank  
 Wenn Sie durch Sichern und Wiederherstellen eine Datenbank in eine andere Instanz von SQL Server kopieren, kann es sich beim Quell- und Zielcomputer um eine beliebige Plattform handeln, auf der SQL Server ausgeführt wird.  
  
 Dies sind die allgemeinen Schritte:  
  
1.  Sichern Sie die Quelldatenbank, die in einer Instanz von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höher vorhanden sein kann. Der Computer, auf dem diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, ist der **Quellcomputer**.  
  
2.  Stellen Sie auf dem Computer, auf den Sie die Datenbank kopieren möchten (der **Zielcomputer**), eine Verbindung mit der Instanz von SQL Server her, in der Sie die Datenbank wiederherstellen möchten. Erstellen Sie bei Bedarf in der **Zielserverinstanz** dieselben Sicherungsmedien, die zum Sichern der **Quelldatenbanken** verwendet werden.  
  
3.  Stellen Sie die Sicherung der **Quelldatenbank** auf dem **Zielserver** wieder her. Durch das Wiederherstellen der Datenbank werden automatisch alle Datenbankdateien erstellt.  
  
Einige zusätzliche Aspekte, die diesen Vorgang beeinflussen können:
  
## <a name="before-you-restore-database-files"></a>Vor dem Wiederherstellen der Datenbankdateien  
 Beim Wiederherstellen einer Datenbank werden automatisch die Datenbankdateien erstellt, die für die wiederherzustellende Datenbank benötigt werden. Standardmäßig verwenden die von SQL Server während des Wiederherstellungsvorgangs erstellten Dateien dieselben Namen und Pfade wie die Sicherungsdateien aus der Originaldatenbank auf dem Quellcomputer.  
  
 Wenn Sie die Datenbank wiederherstellen, können Sie bei Bedarf die Gerätezuordnung, Dateinamen oder den Pfad für die wiederherzustellende Datenbank angeben (optional). 
 
 Dies kann in den folgenden Situationen erforderlich sein:  
  
-   Die Verzeichnisstruktur oder Laufwerkzuordnung, die von der Datenbank auf dem ursprünglichen Computer verwendet wurde, ist auf dem anderen Computer nicht vorhanden. Vielleicht enthält die Sicherung zum Beispiel eine Datei, die standardmäßig auf Laufwerk E wiederhergestellt werden soll, doch auf dem Zielcomputer ist kein Laufwerk mit dem Buchstaben E vorhanden.  
  
-   Am Zielort ist möglicherweise nicht genügend Speicherplatz vorhanden.  
  
-   Sie verwenden erneut einen Datenbanknamen, der am Wiederherstellungsziel bereits vorhanden ist, und wenn eine der Dateien den gleichen Namen wie eine Datenbankdatei im Sicherungssatz erhält, bestehen folgende Möglichkeiten:  
  
    -   Wenn die vorhandene Datenbankdatei überschrieben werden kann, wird sie überschrieben (dies würde sich nicht auf eine Datei auswirken, die zu einem anderen Datenbanknamen gehört).  
  
    -   Wenn die vorhandene Datei nicht überschrieben werden kann, würde ein Wiederherstellungsfehler auftreten.  
  
 Um Fehler und Unannehmlichkeiten zu vermeiden, können Sie vor dem Wiederherstellungsvorgang anhand der [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) -Verlaufstabelle die Datenbank und die Protokolldateien in der Sicherung ermitteln, die Sie wiederherstellen möchten.  
  
## <a name="moving-the-database-files"></a>Verschieben der Datenbankdateien  
 Wenn die Dateien in der Datenbanksicherung auf dem Zielcomputer nicht wiederhergestellt werden können, ist es notwendig, die Dateien während des Wiederherstellens an einen neuen Standort zu verschieben. Beispiel:  
  
-   Sie möchten eine Datenbank aus Sicherungen wiederherstellen, die am Standardspeicherort der früheren Version erstellt wurden.  
  
-   Aus Kapazitätsgründen kann es notwendig sein, einige Datenbankdateien der Sicherung auf einem anderen Laufwerk wiederherzustellen. Dieser Fall kann häufiger eintreten, da die meisten Computer in einem Unternehmen nicht die gleiche Anzahl und Größe der Datenträgerlaufwerke oder identische Softwarekonfigurationen aufweisen.  
  
-   Für Testzwecke kann es notwendig sein, eine Kopie einer vorhandenen Datenbank auf demselben Computer zu erstellen. In diesem Fall sind die Datenbankdateien für die Originaldatenbank bereits vorhanden. Deshalb müssen andere Dateinamen angegeben werden, wenn die Datenbankkopie während des Wiederherstellungsvorgangs erstellt wird.  
  
 Weitere Informationen finden Sie weiter unten in diesem Thema unter "So stellen Sie Dateien oder Dateigruppen an einem neuen Speicherort wieder her".  
  
## <a name="changing-the-database-name"></a>Ändern des Datenbanknamens  
 Der Name der Datenbank kann beim Wiederherstellen auf dem Zielcomputer geändert werden, ohne zuerst die Datenbank erstellen zu müssen und dann anschließend den Namen manuell zu ändern. So kann es sich beispielsweise als notwendig erweisen, den Datenbanknamen von **Sales** in **SalesCopy** zu ändern, um anzuzeigen, dass es sich um die Kopie einer Datenbank handelt.  
  
 Der beim Wiederherstellen einer Datenbank explizit bereitgestellte Name wird automatisch als neuer Datenbankname verwendet. Da der Datenbankname noch nicht vorhanden ist, wird ein neuer Name mithilfe der Dateien in der Sicherung erstellt.  
  
## <a name="when-upgrading-a-database-by-using-restore"></a>Beim Aktualisieren einer Datenbank mithilfe einer Wiederherstellung  
 Beim Wiederherstellen von Sicherungen einer früheren Version ist es hilfreich, vorher zu wissen, ob der Pfad (Laufwerk und Verzeichnis) jedes Volltextkatalogs in einer Sicherung auf dem Zielcomputer vorhanden ist. Zum Auflisten der logischen und physischen Namen (Pfad und Dateiname) jeder Datei in einer Sicherung, einschließlich der Katalogdateien, verwenden Sie eine RESTORE FILELISTONLY FROM *<Sicherungsmedium>*-Anweisung. Weitere Informationen finden Sie unter [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).  
  
 Falls auf dem Zielcomputer nicht der gleiche Pfad vorhanden ist, haben Sie zwei Möglichkeiten:  
  
-   Erstellen Sie die entsprechende Laufwerk/Verzeichnis-Zuordnung auf dem Zielcomputer.  
  
-   Verschieben Sie die Katalogdateien während des Wiederherstellungsvorgangs an einen neuen Speicherort, indem Sie die WITH MOVE-Klausel in der RESTORE DATABASE-Anweisung verwenden. Weitere Informationen finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)nicht wiederhergestellt werden.  
  
 Informationen zu Alternativen zum Upgrade von Volltextindizes finden Sie unter [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md).  
  
## <a name="database-ownership"></a>Datenbankbesitz  
 Wenn eine Datenbank auf einem anderen Computer wiederhergestellt wird, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldename oder der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Benutzer, der den Wiederherstellungsvorgang initiiert, automatisch zum Besitzer der neuen Datenbank. Nach dem Wiederherstellen der Datenbank kann der Systemadministrator oder der neue Datenbankbesitzer den Datenbankbesitz ändern. Verwenden Sie Kennwörter für Medien- oder Sicherungssätze, um das unbefugte Wiederherstellen einer Datenbank zu verhindern.  
  
## <a name="managing-metadata-when-restoring-to-another-server-instance"></a>Verwalten von Metadaten beim Wiederherstellen auf einer anderen Serverinstanz  
 Wenn Sie eine Datenbank auf einer anderen Serverinstanz wiederherstellen, müssen Sie möglicherweise einige oder alle Metadaten, wie Anmeldenamen und Aufträge, für die Datenbank auf der anderen Serverinstanz erneut erstellen, um für Konsistenz für Benutzer und Anwendungen zu sorgen. Weitere Informationen finden Sie unter [Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
 **Anzeigen der Daten und Protokolldateien in einem Sicherungssatz**  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
 **Wiederherstellen von Dateien und Dateigruppen an einem neuen Speicherort**  
  
-   [Wiederherstellen von Dateien an einem neuen Speicherort &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **Wiederherstellen von Dateien und Dateigruppen über vorhandene Dateien**  
  
-   [Wiederherstellen von Dateien und Dateigruppen über vorhandene Dateien &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
 **Wiederherstellen einer Datenbank mit einem neuen Namen**  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **Neustarten eines unterbrochenen Wiederherstellungsvorgangs**  
  
-   [Neustarten eines unterbrochenen Wiederherstellungsvorgangs Operation &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
 **Ändern des Datenbankbesitzers**  
  
-   [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)  
  
 **Kopieren einer Datenbank mithilfe von SQL Server Management Objects (SMO)**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadFileList%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.RelocateFiles%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReplaceDatabase%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
## <a name="see-also"></a>Siehe auch  
 [Kopieren von Datenbanken auf andere Server](../../relational-databases/databases/copy-databases-to-other-servers.md)   
 [File Locations for Default and Named Instances of SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  

