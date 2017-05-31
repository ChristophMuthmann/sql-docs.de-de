---
title: "Datenbank sichern (Seite „Medienoptionen“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- swb.backupdatabase.mediaoptions.f1
- sql13.swb.backupdatabase.mediaoptions.f1
ms.assetid: eff36228-710c-4ed5-9af5-95859575dc0f
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7e1fd480768d75f33793f7260eb2652a25c1cc77
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="back-up-database-media-options-page"></a>Datenbank sichern (Seite 'Medienoptionen')
  Auf der Seite  **Medienoptionen** des Dialogfelds **Datenbank sichern** können Sie Medienoptionen zur Sicherung der Datenbank anzeigen oder ändern.  
  
 **So erstellen Sie eine Sicherung mithilfe von SQL Server Management Studio**  
  
-   [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  Sie können einen Datenbank-Wartungsplan definieren, um Datenbanksicherungen zu erstellen. Weitere Informationen finden Sie unter [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md) und [Verwenden des Wartungsplanungs-Assistenten](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
> [!NOTE]  
>  Wenn Sie eine Sicherungsaufgabe mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]angeben, können Sie das entsprechende [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) -Skript generieren, indem Sie auf die Schaltfläche **Skript** klicken und anschließend ein Ziel für das Skript auswählen.  
  
## <a name="options"></a>Optionen  
  
### <a name="overwrite-media"></a>Medium überschreiben  
 Mit den Optionen des Bereichs **Medium überschreiben** kann gesteuert werden, wie die Sicherung auf das Medium geschrieben wird. Wenn Sie im Dialogfeld Datenbank sichern auf der Seite Allgemein die Option URL (Windows Azure-Speicher) als Sicherungsziel auswählen, sind die Optionen im Abschnitt Medium überschreiben deaktiviert. Sie können eine Sicherung mithilfe der Transact-SQL-Anweisung **BACKUP TO URL. WITH FORMAT** überschreiben. Weitere Informationen finden Sie unter [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
 Nur die Option **Auf neuen Mediensatz sichern und alle vorhandenen Sicherungssätze löschen** wird mit Verschlüsselungsoptionen unterstützt. Wenn Sie die Optionen im Abschnitt **Auf vorhandenen Mediensatz sichern** auswählen, werden die Verschlüsselungsoptionen auf der Seite **Sicherungsoptionen** deaktiviert.  
  
> [!NOTE]  
>  Informationen über Mediensätze finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)ausgeführt wird.  
  
 **Auf vorhandenen Mediensatz sichern**  
 Sichert eine Datenbank auf einen vorhandenen Mediensatz. Durch Auswahl dieser Option werden drei weitere Optionen aktiviert.  
  
 Wählen Sie eine der folgenden Optionen aus:  
  
 **An vorhandenen Sicherungssatz anfügen**  
 Fügt den Sicherungssatz unter Beibehaltung vorheriger Sicherungen an den vorhandenen Mediensatz an.  
  
 **Alle vorhandenen Sicherungssätze überschreiben**  
 Ersetzt alle vorherigen Sicherungen auf dem vorhandenen Mediensatz durch die aktuelle Sicherung.  
  
 **Mediensatznamen und Ablaufzeit des Sicherungssatzes überprüfen**  
 Legen Sie optional beim Sichern auf einen vorhandenen Mediensatz fest, dass während des Sicherungsvorgangs der Name und das Ablaufdatum der Sicherungssätze überprüft werden.  
  
 **Mediensatzname**  
 Wenn **Mediensatznamen und Ablaufzeit des Sicherungssatzes überprüfen** ausgewählt ist, geben Sie optional den Namen des Mediensatzes an, der für diesen Sicherungsvorgang verwendet werden soll.  
  
 **Auf neuen Mediensatz sichern und alle vorhandenen Sicherungssätze löschen**  
 Mit dieser Option erstellen Sie einen neuen Mediensatz, wobei die vorherigen Sicherungssätze gelöscht werden.  
  
 Durch Auswählen dieser Option werden die folgenden Optionen aktiviert:  
  
 **Name für neuen Mediensatz**  
 Geben Sie optional einen neuen Namen für den Mediensatz ein.  
  
 **Beschreibung für neuen Mediensatz**  
 Geben Sie optional eine aussagekräftige Beschreibung für den neuen Mediensatz ein. Die Beschreibung sollte genau genug sein, um den Inhalt akkurat zu vermitteln.  
  
### <a name="reliability"></a>Zuverlässigkeit  
 Mit den Optionen des Bereichs **Transaktionsprotokoll** wird die Fehlerverwaltung durch den Sicherungsvorgang gesteuert.  
  
 **Sicherung nach dem Abschluss überprüfen**  
 Überprüft, ob der Sicherungssatz vollständig ist und alle Volumes lesbar sind.  
  
 **Vor dem Schreiben auf die Medien Prüfsumme bilden**  
 Überprüft vor dem Schreiben auf die Sicherungsmedien die Prüfsummen. Das Auswählen dieser Option entspricht der Angabe der Option CHECKSUM in der BACKUP-Anweisung von [!INCLUDE[tsql](../../includes/tsql-md.md)]. Durch Auswahl dieser Option kann die Arbeitsauslastung erhöht und der Sicherungsdurchsatz des Sicherungsvorgangs verringert werden. Weitere Informationen zu Sicherungsprüfsummen finden Sie unter [Mögliche Medienfehler während der Sicherung und Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 **Bei Fehler fortsetzen**  
 Der Sicherungsvorgang wird auch nach Auftreten eines oder mehrerer Fehler fortgesetzt.  
  
### <a name="transaction-log"></a>Transaktionsprotokoll  
 Mit den Optionen des Bereichs **Transaktionsprotokoll** wird das Verhalten einer Transaktionsprotokollsicherung gesteuert. Diese Optionen sind nur beim vollständigen Wiederherstellungsmodell oder beim massenprotokollierten Wiederherstellungsmodell relevant. Sie sind nur aktiviert, wenn im Dialogfeld **Datenbank sichern** auf der Seite **Allgemein** im Feld [Sicherungstyp](../../relational-databases/backup-restore/back-up-database-general-page.md) die Option **Transaktionsprotokoll** ausgewählt ist.  
  
> [!NOTE]  
>  Informationen zu Transaktionsprotokollsicherungen finden Sie unter [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 **Transaktionsprotokoll abschneiden**  
 Das Transaktionsprotokoll wird gesichert und abgeschnitten, um Protokollspeicherplatz freizugeben. Die Datenbank bleibt dabei online. Diese Option ist die Standardeinstellung.  
  
 **Protokollfragment sichern und Datenbank im Wiederherstellungsstatus belassen**  
 Das Protokollfragment wird gesichert und die Datenbank im Wiederherstellungsstatus belassen. Diese Option erstellt eine *Sicherung des Protokollfragments*. Dabei werden Protokolle gesichert, die bisher (vom aktiven Protokoll) noch nicht gesichert wurden, i.d.R. als Vorbereitung für die Wiederherstellung einer Datenbank. Die Datenbank steht Benutzern erst wieder zur Verfügung, wenn sie vollständig wiederhergestellt ist.  
  
 Das Auswählen dieser Option entspricht der Angabe von WITH NO_TRUNCATE und NORECOVERY in einer [BACKUP](../../t-sql/statements/backup-transact-sql.md)-Anweisung ([!INCLUDE[tsql](../../includes/tsql-md.md)]). Weitere Informationen finden Sie unter [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
### <a name="tape-drive"></a>Bandlaufwerk  
 Mit den Optionen des Bereichs **Bandlaufwerk** wird die Bandverwaltung während des Sicherungsvorgangs gesteuert. Diese Optionen sind nur aktiviert, wenn im Dialogfeld **Datenbank sichern** auf der Seite **Allgemein** im Feld [Ziel](../../relational-databases/backup-restore/back-up-database-general-page.md) die Option **Band** ausgewählt ist.  
  
> [!NOTE]  
>  Weitere Informationen zum Verwenden von Bandmedien finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 **Band nach dem Sichern entladen**  
 Nach Abschluss der Sicherung wird das Band entladen.  
  
 **Band vor dem Entladen zurückspulen**  
 Das Band wird vor dem Entladen freigegeben und zurückgespult. Diese Option ist nur aktiviert, wenn **Band nach dem Sichern entladen** ausgewählt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [Sichern von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [Sichern des Transaktionsprotokolls bei beschädigter Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
