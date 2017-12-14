---
title: Sicherungsmedien (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tape backup devices, about tape backup devices
- backup devices [SQL Server]
- disk backup devices [SQL Server]
- database backups [SQL Server], backup devices
- logical devices [SQL Server]
- backup devices [SQL Server], about backup devices
- backing up [SQL Server], backup devices
- removable media [SQL Server]
- network shares [SQL Server]
- backups [SQL Server], backup devices
- tape backup devices
- physical devices [SQL Server]
- backing up databases [SQL Server], backup devices
- devices [SQL Server]
ms.assetid: 35a8e100-3ff2-4844-a5da-dd088c43cba4
caps.latest.revision: "93"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8efae7715dcb9d5b182360e074f87cc5c7b2f067
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="backup-devices-sql-server"></a>Sicherungsmedien (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Während eines Sicherungsvorgangs in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank werden die gesicherten Daten (die *Sicherung*) auf ein physisches Sicherungsmedium geschrieben. Dieses physische Sicherungsmedium wird initialisiert, wenn die erste Sicherung in einem Mediensatz darauf geschrieben wird. Die Sicherungen auf einem Satz von einem oder mehreren Sicherungsmedien bilden einen einzelnen Mediensatz.  
   
##  <a name="TermsAndDefinitions"></a> Begriffe und Definitionen  
 Sicherungsdatenträger  
 Eine Festplatte oder ein anderes Datenträgerspeichermedium, die bzw. das eine oder mehrere Sicherungsdateien enthält. Eine Sicherungsdatei ist eine reguläre Betriebssystemdatei.  
  
 Mediensatz  
 Eine geordnete Auflistung von Sicherungsmedien (Bänder oder Dateien auf Datenträgern), für die ein fester Typ sowie eine feste Anzahl von Sicherungsmedien verwendet wird. Weitere Informationen über Mediensätze finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
 Physisches Sicherungsmedium  
 Entweder ein Bandlaufwerk oder eine vom Betriebssystem bereitgestellte Datei auf dem Datenträger. Eine Sicherung kann auf 1 bis 64 Sicherungsmedien geschrieben werden. Wenn für eine Sicherung mehrere Sicherungsmedien benötigt werden, müssen diese ohne Ausnahme demselben Medientyp angehören (Datenträger oder Band).  
  
 SQL Server-Sicherungen können nicht nur auf einen Datenträger oder ein Band geschrieben werden, sondern auch in den Windows Azure-BLOB-Speicherdienst.  
 
  
##  <a name="DiskBackups"></a> Verwenden von Datenträgersicherungsmedien  
  
 Wenn sich eine Datenträgerdatei füllt, während bei einem Sicherungsvorgang dem Mediensatz eine Sicherung hinzugefügt wird, kann die Sicherungsvorgang nicht bis zum Ende ausgeführt werden. Die maximale Größe einer Sicherungsdatei wird durch den freien Speicherplatz auf dem Datenträgermedium bestimmt. Die geeignete Größe für ein Datenträgersicherungsmedium hängt daher von der Größe Ihrer Sicherungen ab.  
  
 Ein Datenträgersicherungsmedium kann ein einfacher Datenträger sein, z. B. ein ATA-Laufwerk. Alternativ kann auch ein im laufenden Betrieb austauschbares Datenträgerlaufwerk verwendet werden, das den Vorteil hat, dass Sie auf transparente Weise einen vollen Datenträger gegen einen leeren austauschen können. Ein Sicherungsdatenträger kann ein lokaler Datenträger auf dem Server oder ein als Netzwerkressource freigegebener Remotedatenträger sein. Informationen zum Verwenden eines Remotedatenträgers finden Sie unter [Sichern in eine Datei auf einer Netzwerkfreigabe](#NetworkShare)weiter unten in diesem Thema.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verwaltungstools bieten eine hohe Flexibilität beim Verwalten von Datenträgersicherungsmedien, da sie automatisch einen zeitgestempelten Dateinamen für die Datei auf dem Datenträger generieren.  
  
> **WICHTIG!** Als Sicherungsdatenträger sollte ein anderer Datenträger als für die Datenbankdaten und Protokolldatenträger verwendet werden. Nur so kann sichergestellt werden, dass Sie auch dann auf die Sicherungen zugreifen können, wenn die Daten- oder Protokolldatenträger ausfallen. 
>
>Wenn sich Datenbankdateien und Sicherungsdateien auf demselben Medium befinden und ein Fehler auftritt, stehen die Datenbank und die Sicherungen nicht mehr zur Verfügung. Wenn Sie die Daten und die Sicherungen auf separaten Medien speichern, wird auch die E/A-Leistung für die produktive Nutzung der Datenbank sowie für das Schreiben von Sicherungen optimiert.
  
##  <a name="BackupFileUsingPhysicalName"></a> Angeben einer Sicherungsdatei unter Verwendung des physischen Namens (Transact-SQL)  
 Die grundlegende [BACKUP](../../t-sql/statements/backup-transact-sql.md) -Syntax zum Angeben einer Sicherungsdatei mithilfe des Namens des physischen Mediums lautet wie folgt:  
  
 BACKUP DATABASE *Name der Datenbank*  
  
 TO DISK **=** { **'***Name des physischen Sicherungsmediums***'** | **@***physical_backup_device_name_var* }  
  
 Beispiel:  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';  
GO  
```  
  
 Die grundlegende Syntax zum Angeben eines physischen Datenträgermediums in einer [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) -Anweisung lautet:  
  
 RESTORE { DATABASE | LOG } *Name der Datenbank*  
  
 FROM DISK **=** { **'***Name des physischen Sicherungsmediums***'** | **@***physical_backup_device_name_var* }  
  
 Beispiel:  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';   
```  
  
  
##  <a name="BackupFileDiskPath"></a> Angeben des Dateipfads für die Datenträgersicherung 
 Wenn Sie eine Sicherungsdatei angeben, sollten Sie den vollständigen Pfad und den Dateinamen angeben. Wenn Sie beim Sichern der Datei nur den Dateinamen oder einen relativen Pfad angeben, wird die Sicherungsdatei im Standardsicherungsverzeichnis gespeichert. Das Standardsicherungsverzeichnis lautet „C:\Programme\Microsoft SQL Server\MSSQL.*n*\MSSQL\Backup“, wobei mit *n* die Nummer der Serverinstanz angegeben wird. Das Standardsicherungsverzeichnis für die Standardserverinstanz lautet daher „C:\Programme\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup“.  
  
 Für eine eindeutige Zuordnung (insbesondere in Skripts) empfiehlt sich die explizite Angabe des Pfads für das Sicherungsverzeichnis in allen DISK-Klauseln. Wenn Sie den Abfrage-Editor verwenden, ist dieser Aspekt weniger wichtig. In diesem Fall, wenn Sie sicherstellen können, dass sich die Sicherungsdatei im Standardsicherungsverzeichnis befindet, können Sie die Pfadangabe in der DISK-Klausel auslassen. Beispielsweise wird die `BACKUP` -Datenbank mithilfe der folgenden [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Anweisung im Standardsicherungsverzeichnis gesichert.  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = ’AdventureWorks2012.bak’;  
GO  
```  
  
> **HINWEIS:** Der Standardspeicherort wird im **BackupDirectory** -Registrierungsschlüssel unter **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.n\MSSQLServer**gespeichert.  
  
   
###  <a name="NetworkShare"></a> Sichern in einer Netzwerkfreigabedatei  
 Damit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf eine Datei auf einem Remotedatenträger zugreifen kann, muss das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto Zugriff auf die Netzwerkfreigabe haben. Dazu gehören auch Berechtigungen, die erforderlich sind, damit Sicherungsvorgänge auf die Netzwerkfreigabe schreiben und Wiederherstellungsvorgänge die Sicherungsdaten auf der Netzwerkfreigabe lesen können. Die Verfügbarkeit von Netzlaufwerken und Berechtigungen hängt von dem Kontext ab, in dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird:  
  
-   Zum Sichern eines Netzlaufwerks, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Kontext eines Domänenbenutzerkontos ausgeführt wird, muss das freigegebene Laufwerk in der Sitzung, in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, als Netzlaufwerk zugeordnet sein. Wenn Sie Sqlservr.exe über die Befehlszeile starten, werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sämtliche Netzlaufwerke angezeigt, die Sie in Ihrer Anmeldesitzung zugeordnet haben.  
  
-   Wenn Sie Sqlservr.exe als Dienst ausführen, wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einer separaten Sitzung ausgeführt, die nicht mit Ihrer Anmeldesitzung in Zusammenhang steht. Die Sitzung, in der ein Dienst ausgeführt wird, kann über eigene zugeordnete Laufwerke verfügen (obwohl das normalerweise nicht der Fall ist).  
  
-   Sie können eine Verbindung mit dem Netzwerkdienstkonto herstellen, indem Sie statt eines Domänenbenutzers das Computerkonto verwenden. Damit Sicherungen von bestimmten Computern auf ein freigegebenes Laufwerk zulässig sind, müssen Sie den Computerkonten entsprechende Zugriffsberechtigungen erteilen. Solange der Sqlservr.exe-Prozess, der die Sicherung schreibt, Zugriff hat, spielt es keine Rolle, ob der Benutzer, der den BACKUP-Befehl sendet, ebenfalls Zugriff hat.  
  
    > **WICHTIG!** Da es bei Vorliegen von Netzwerkfehlern beim Sichern von Daten über ein Netzwerk zu Störungen kommen kann, sollten Sie bei Verwendung eines Remotedatenträgers den Sicherungsvorgang am Ende überprüfen. Weitere Informationen finden Sie unter [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
## <a name="specify-a-universal-naming-convention-unc-name"></a>Angeben eines UNC-Namen (Universal Naming Convention)  
 Zum Angeben einer Netzwerkfreigabe in einem Sicherungs- oder Wiederherstellungsbefehl verwenden Sie den vollqualifizierten UNC-Namen der Datei für das Sicherungsmedium. Ein UNC-Name weist das Format **\\\\***Systemname***\\***ShareName***\\***Path***\\***FileName*.  
  
 Beispiel:  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = '\\BackupSystem\BackupDisk1\AW_backups\AdventureWorksData.Bak';  
GO  
```  
  
 
##  <a name="TapeDevices"></a> Verwenden von Bandgeräten  
  
> **HINWEIS:** Die Unterstützung für Bandsicherungsgeräte wird in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entfernt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.  
   
 Zum Sichern von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten auf Band ist mindestens ein Bandlaufwerk erforderlich, das vom [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Betriebssystem unterstützt wird. Verwenden Sie für diese Laufwerke nur die vom Hersteller des Laufwerks empfohlenen Bänder. Weitere Informationen zum Installieren eines Bandlaufwerks finden Sie in der Dokumentation zum Windows-Betriebssystem.  
  
 Wenn ein Bandlaufwerk verwendet wird, kann ein Sicherungsvorgang ein Band füllen und mit einem anderen Band fortfahren. Jedes Band enthält einen Medienheader. Das erste verwendete Medium wird als *Anfangsband*bezeichnet. Jedes darauf folgende Band wird als *Anschlussband* bezeichnet und verfügt über eine Mediensequenznummer (aufsteigend). Ein Mediensatz, der beispielsweise vier Bandmedien zugewiesen ist, enthält mindestens vier Anfangsbänder (und, bei Bedarf für die Datenbank vier weitere Reihen mit Anschlussbändern). Wenn Sie einen Sicherungssatz anfügen, müssen Sie das letzte Band in der Reihe einlegen. Wenn das letzte Band nicht eingelegt wurde, wird der Scanvorgang von [!INCLUDE[ssDE](../../includes/ssde-md.md)] bis zum Ende des eingelegten Bands fortgesetzt, woraufhin Sie das Band wechseln müssen. Legen Sie zu diesem Zeitpunkt das letzte Band ein.  
  
 Bandsicherungsmedien werden wie Datenträgermedien verwendet. Es gelten folgende Ausnahmen:  
  
-   Das Bandmedium muss physisch mit dem Computer verbunden sein, auf dem eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt wird. Das Sichern auf Remotebandmedien wird nicht unterstützt.  
  
-   Wenn ein Bandsicherungsmedium während des Sicherungsvorgangs gefüllt wird, jedoch noch weitere Daten geschrieben werden müssen, fordert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Einlegen eines neues Bands auf, und setzt danach den Sicherungsvorgang fort.  
  
##  <a name="BackupTapeUsingPhysicalName"></a> Angeben eines Sicherungsbands unter Verwendung des physischen Namens (Transact-SQL)  
 Die grundlegende [BACKUP](../../t-sql/statements/backup-transact-sql.md) -Syntax zum Angeben eines Sicherungsbands mithilfe des physischen Gerätenamens des Bandlaufwerks lautet wie folgt:  
  
 BACKUP { DATABASE | LOG } *Name der Datenbank*  
  
 TO TAPE **=** { **'***Name des physischen Sicherungsmediums***'** | **@***physical_backup_device_name_var* }  
  
 Beispiel:  
  
```  
BACKUP LOG AdventureWorks2012   
   TO TAPE = '\\.\tape0';  
GO  
```  
  
 Die grundlegende Syntax zum Angeben eines physischen Bandmediums in einer [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) -Anweisung lautet:  
  
 RESTORE { DATABASE | LOG } *Name der Datenbank*  
  
 FROM TAPE **=** { **'***Name des physischen Sicherungsmediums***'** | **@***physical_backup_device_name_var* }  
  
###  <a name="TapeOptions"></a> Bandspezifische BACKUP- und RESTORE-Optionen (Transact-SQL)  
 Zur Vereinfachung der Bandverwaltung bietet die BACKUP-Anweisung die folgenden bandspezifischen Optionen:  
  
-   { NOUNLOAD | **UNLOAD** }  
  
     Sie können steuern, ob ein Sicherungsband nach einem Sicherungs- oder Wiederherstellungsvorgang automatisch aus dem Bandlaufwerk ausgeworfen werden soll. UNLOAD/NOUNLOAD ist eine Sitzungseinstellung, die für die Dauer der Sitzung oder bis zur Angabe der alternativen Einstellung persistent gespeichert wird.  
  
-   { **REWIND** | NOREWIND }  
  
     Sie können steuern, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach dem Sicherungs- oder Wiederherstellungsvorgang das Band offen hält oder das Band, wenn es voll ist, freigibt und zurückspult. Standardmäßig wird das Band zurückgespult (REWIND).  
  
> **HINWEIS:** Weitere Informationen zur Syntax und den Argumenten von BACKUP finden Sie unter [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md). Weitere Informationen zur Syntax und den Argumenten von RESTORE finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) und [RESTORE-Argumente &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
###  <a name="OpenTapes"></a> Verwalten von offenen Bändern  
 Führen Sie eine Abfrage auf die dynamische Verwaltungssicht [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) aus, um eine Liste der offenen Bandmedien und den Status von Einbindungsanforderungen anzuzeigen. In dieser Sicht werden alle offenen Bänder angezeigt. Dies umfasst auch die gerade verwendeten Bänder, die sich bis zum nächsten BACKUP- oder RESTORE-Vorgang vorübergehend im Leerlauf befinden.  
  
 Wenn ein Band versehentlich offen geblieben ist, kann es am schnellsten mithilfe des folgenden Befehls freigegeben werden: RESTORE REWINDONLY FROM TAPE **=***Name des Sicherungsmediums*. Weitere Informationen finden Sie unter [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md).  
  
  
## <a name="using-the-windows-azure-blob-storage-service"></a>Verwenden des Windows Azure-BLOB-Speicherdiensts  
 SQL Server-Sicherungen können in den Windows Azure-BLOB-Speicherdienst geschrieben werden.  Weitere Informationen zum Verwenden von Microsoft Azure Blob Storage für Sicherungen finden Sie unter [SQL Server-Sicherung und -Wiederherstellung mit Microsoft Azure Blob Storage](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
##  <a name="LogicalBackupDevice"></a> Verwenden eines logischen Sicherungsmediums  
 Ein *logisches Sicherungsmedium* ist ein optionaler, benutzerdefinierter Name, der auf ein bestimmtes, physisches Sicherungsmedium (Datenträgerdatei oder Bandlaufwerk) verweist. Ein logisches Sicherungsmedium gibt Ihnen beim Verweisen auf das entsprechende physische Sicherungsmedium die Möglichkeit zur Dereferenzierung.  
  
 Zum Definieren eines logischen Sicherungsmediums muss einem physischen Medium ein logischer Name zugeordnet werden. Beispielsweise kann ein logisches Medium (AdventureWorksBackups) so definiert werden, dass es auf die Datei „Z:\SQLServerBackups\AdventureWorks2012.bak“ oder das Bandlaufwerk „ \\\\.\tape0“ verweist. In Sicherungs- und Wiederherstellungsbefehlen kann dann AdventureWorksBackups anstelle von DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' or TAPE = '\\\\.\tape0' als Sicherungsmedium angegeben werden.  
  
 Der Name des logischen Mediums muss innerhalb der logischen Sicherungsmedien auf der Serverinstanz eindeutig sein. Sie können sich die vorhandenen logischen Mediennamen anzeigen lassen, indem Sie eine Abfrage für die [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) -Katalogsicht ausführen. In dieser Sicht wird der Name des logischen Sicherungsmediums angezeigt, und es wird der Typ und der physische Dateiname oder der Pfad des entsprechenden physischen Sicherungsmediums angegeben.  
  
 Nachdem ein logisches Sicherungsmedium definiert wurde, können Sie in einem BACKUP- oder RESTORE-Befehl das logische Sicherungsmedium angeben, statt den physischen Namen des Sicherungsmediums zu verwenden. Beispielsweise wird die `AdventureWorks2012` -Datenbank mit der folgenden Anweisung auf dem logischen Sicherungsmedium `AdventureWorksBackups` gesichert.  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups;  
GO  
```  
  
> **HINWEIS:** In jeder BACKUP- oder RESTORE-Anweisung kann wahlweise der logische Name des Sicherungsmediums oder der Name des entsprechenden physischen Sicherungsmediums angegeben werden.  
  
 Die Verwendung eines logischen Sicherungsmediums ist einfacher, da kein langer Pfad angegeben werden muss. Die Verwendung eines logischen Sicherungsmediums kann hilfreich sein, wenn Sie vorhaben, eine Reihe von Sicherungen auf denselben Pfad oder auf dasselbe Bandmedium zu schreiben. Logische Sicherungsmedien sind besonders nützlich zum Identifizieren von Bandsicherungsmedien.  
  
 Es kann ein Sicherungsskript geschrieben werden, um ein bestimmtes logisches Sicherungsmedium zu verwenden. Damit können Sie zu einem neuen physischen Sicherungsmedium wechseln, ohne dass ein Update des Skripts erforderlich ist. Für diesen Wechsel sind die folgenden Schritte erforderlich:  
  
1.  Löschen des ursprünglichen logischen Sicherungsmediums.  
  
2.  Definieren eines neuen logischen Sicherungsmediums, für das der Name des ursprünglichen logischen Sicherungsmediums verwendet wird, für das jedoch eine Zuordnung zu einem anderen physischen Sicherungsmedium erfolgt. Logische Sicherungsmedien sind besonders nützlich zum Identifizieren von Bandsicherungsmedien.  
  
  
##  <a name="MirroredMediaSets"></a> Gespiegelte Sicherungsmediensätze  
 Die Spiegelung von Sicherungsmediensätzen mindert die Auswirkungen von Funktionsstörungen bei Sicherungsmedien. Diese Funktionsstörungen sind besonders schwerwiegend, da Sicherungen im Hinblick auf den Verlust von Daten die letzte Schutzmaßnahme darstellen. Mit zunehmendem Umfang einer Datenbank nimmt auch die Wahrscheinlichkeit für einen Fehler bei einem Sicherungsgerät oder -medium zu, in dessen Folge eine Sicherung schließlich nicht mehr wiederhergestellt werden kann. Aufgrund der mit der Spiegelung von Sicherungsmedien bereitgestellten Redundanz für das physische Sicherungsmedium erhöht sich die Zuverlässigkeit von Sicherungen. Weitere Informationen finden Sie unter [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md).  
  
> **HINWEIS:** Gespiegelte Sicherungsmediensätze werden nur in [!INCLUDE[ssEnterpriseEd2005](../../includes/ssenterpriseed2005-md.md)] und höheren Versionen unterstützt.  
  
  
##  <a name="Archiving"></a> Archivieren von SQL Server-Sicherungen  
 Datenträgersicherungen sollten mithilfe eines Hilfsprogramms für die Dateisystemsicherung archiviert und die Archive außerhalb des Standorts aufbewahrt werden. Das Verwenden eines Datenträgers hat den Vorteil, dass Sie die archivierten Sicherungen über das Netzwerk auf einen Datenträger außerhalb des Standorts schreiben können. Der Windows Azure-BLOB-Speicherdienst kann als externe Archivierungsfunktion genutzt werden.  Sie können entweder die Datenträgersicherungen hochladen, oder Sie können die Sicherungen direkt in den Windows Azure-BLOB-Speicherdienst schreiben.  
  
 Eine weitere verbreitete Archivierungsmethode besteht darin, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherungen auf einen lokalen Sicherungsdatenträger zu schreiben, auf Band zu archivieren und die Bänder außerhalb des Standorts aufzubewahren.  

  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So geben Sie ein Datenträgermedium an (SQL Server Management Studio)**  
  
-   [Angeben eines Datenträgers oder ein Bands als Sicherungsziel &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **So geben Sie ein Bandmedium an (SQL Server Management Studio)**  
  
-   [Angeben eines Datenträgers oder ein Bands als Sicherungsziel &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **So definieren Sie ein logisches Sicherungsmedium**  
  
-   [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)  
  
-   [Definieren eines logischen Sicherungsmediums für eine Datenträgerdatei &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.BackupDevice> (SMO)  
  
 **So verwenden Sie ein logisches Sicherungsmedium**  
  
-   [Angeben eines Datenträgers oder ein Bands als Sicherungsziel &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Wiederherstellung einer Sicherung von einem Medium &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 **So zeigen Sie Informationen zu Sicherungsmedien an**  
  
-   [Sicherungsverlauf und Headerinformationen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
-   [Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Anzeigen der Inhalte eines Sicherungsbands oder einer -datei &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
 **So löschen Sie ein logisches Sicherungsmedium**  
  
-   [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)  
  
-   [Löschen eines Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server, Sicherungsmedium-Objekt](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [sys.dm_io_backup_tapes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)   
 [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  
