---
title: RESTORE-Argumente (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/05/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE statement, arguments
- RESTORE statement
ms.assetid: 4bfe5734-3003-4165-afd4-b1131ea26e2b
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: db010db48a42113c147751021404ac0dbc29ecaf
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---arguments-transact-sql"></a>RESTORE-Anweisungen – Argumente (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden die Argumente, die in den Abschnitten über die Syntax der RESTORE {DATABASE|LOG}-Anweisung und der zugeordneten Gruppe der folgenden Hilfsanweisungen beschrieben werden, dokumentiert: RESTORE FILELISTONLY, RESTORE HEADERONLY, RESTORE LABELONLY, RESTORE REWINDONLY und RESTORE VERIFYONLY. Die meisten der Argumente werden nur von einer Untermenge dieser sechs Anweisungen unterstützt. Die Unterstützung für jedes Argument wird in der Beschreibung des Arguments angezeigt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
 Informationen zur Syntax finden Sie in den folgenden Themen:  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="arguments"></a>Argumente  
 DATABASE  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Gibt die Zieldatenbank an. Falls eine Liste mit Dateien oder Dateigruppen angegeben ist, werden nur diese Dateien und Dateigruppen wiederhergestellt.  
  
 Bei einer Datenbank, die das Modell der vollen oder massenprotokollierten Wiederherstellung verwendet, erfordert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in den meisten Fällen die Sicherung des Protokollfragments, bevor die Datenbank wiederhergestellt wird. Wenn eine Datenbank ohne vorherige Sicherung des Protokollfragments wiederhergestellt wird, tritt ein Fehler auf. Dies gilt nicht, wenn die RESTORE DATABASE-Anweisung die WITH REPLACE- oder die WITH STOPAT-Klausel enthält, in der eine Zeit oder Transaktion nach dem Ende der Datensicherung angegeben sein muss. Weitere Informationen zu Sicherungen des Protokollfragments finden Sie unter [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
 LOG  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Gibt an, dass eine Transaktionsprotokollsicherung auf diese Datenbank angewendet werden soll. Transaktionsprotokolle müssen in sequenzieller Reihenfolge ausgeführt werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft die gesicherten Transaktionsprotokolle, um sicherzustellen, dass die Transaktionen in der richtigen Reihenfolge in die richtige Datenbank geladen werden. Zur Anwendung mehrerer Transaktionsprotokolle verwenden Sie die Option NORECOVERY für alle Wiederherstellungsoperationen außer für die letzte.  
  
> [!NOTE]  
>  Üblicherweise handelt es sich bei dem zuletzt wiederhergestellten Protokoll um die Sicherung des Protokollfragments. Eine *Sicherung des Protokollfragments* ist eine Protokollsicherung, die unmittelbar vor dem Wiederherstellen einer Datenbank erstellt wurde. Dies erfolgt normalerweise nach dem Auftreten eines Datenbankfehlers. Durch das Erstellen einer Sicherung des Protokollfragments von der möglicherweise beschädigten Datenbank kann der Verlust von Arbeit verhindert werden, indem der noch nicht gesicherte Teil des Protokolls (Protokollfragment) erfasst wird. Weitere Informationen finden Sie unter [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
 Weitere Informationen finden Sie unter [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
 { *database_name* | **@***database_name_var*}  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Dies ist die Datenbank, in die das Protokoll oder die vollständige Datenbank wiederhergestellt wird. Wird das Argument in Form einer Variablen angegeben (**@***database_name_var*), kann dieser Name entweder als Zeichenfolgenkonstante (**@***database_name_var* = *database*_*name*) oder als Variable eines Zeichenfolgen-Datentyps (mit Ausnahme des Datentyps **ntext** oder **text**) angegeben werden.  
  
 \<file_or_filegroup_or_page> [ **,**...*n* ]  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Gibt den Namen einer logischen Datei oder Dateigruppe oder einer Seite an, die in eine RESTORE DATABASE- oder RESTORE LOG-Anweisung eingeschlossen werden soll. Sie können eine Liste mit Dateien oder Dateigruppen angeben.  
  
 Bei einer Datenbank, für die das einfache Wiederherstellungsmodell verwendet wird, sind die Optionen FILE und FILEGROUP nur dann zulässig, wenn die Zieldateien oder -dateigruppen schreibgeschützt sind oder wenn es sich um eine Wiederherstellung mit PARTIAL handelt (deren Ergebnis eine [veraltete Dateigruppe](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md) ist).  
  
 Bei einer Datenbank, für die das vollständige oder massenprotokollierte Wiederherstellungsmodell verwendet wird, müssen Sie nach der Verwendung von RESTORE DATABASE zum Wiederherstellen einer oder mehrerer Dateien, Dateigruppen und/oder Seiten normalerweise das Transaktionsprotokoll auf die Dateien anwenden, die die wiederhergestellten Daten enthalten. Durch die Anwendung des Protokolls wird die Konsistenz dieser Dateien mit dem Rest der Datenbank erreicht. Hierbei gelten die folgenden Ausnahmen:  
  
-   Wenn die Dateien, die wiederhergestellt werden, vor der letzten Sicherung schreibgeschützt waren, muss kein Transaktionsprotokoll angewendet werden. Sie werden von der RESTORE-Anweisung über diesen Sachverhalt informiert.  
  
-   Wenn die Sicherung die primäre Dateigruppe enthält und eine Teilwiederherstellung ausgeführt wird. In diesem Fall wird das Wiederherstellungsprotokoll nicht benötigt, da das Protokoll automatisch aus dem Sicherungssatz wiederhergestellt wird.  
  
FILE **=** { *logical_file_name_in_backup*| **@***logical_file_name_in_backup_var*}  
 Benennt eine Datei, die in die Wiederherstellung der Datenbank eingeschlossen werden soll.  
  
FILEGROUP **=** { *logical_filegroup_name* | **@***logical_filegroup_name_var* }  
 Benennt eine Dateigruppe, die in die Wiederherstellung der Datenbank eingeschlossen werden soll.  
  
 **Hinweis** FILEGROUP ist beim einfachen Wiederherstellungsmodell nur zulässig, wenn die angegebene Dateigruppe schreibgeschützt ist und es sich um eine Teilwiederherstellung handelt. Dies ist bei Verwendung von WITH PARTIAL der Fall. Alle nicht wiederhergestellten Dateigruppen mit Lese-/Schreibzugriff werden als veraltet markiert und können nachfolgend nicht mehr in der sich ergebenden Datenbank wiederhergestellt werden.  
  
READ_WRITE_FILEGROUPS  
 Wählt alle Dateigruppen mit Lese-/Schreibzugriff aus. Diese Option ist besonders hilfreich, wenn Sie schreibgeschützte Dateigruppen nach der Wiederherstellung von Dateigruppen mit Lese-/Schreibzugriff wiederherstellen möchten.  
  
PAGE = **'***file***:***page* [ **,**...*n* ]**'**  
 Gibt eine Liste mit mindestens einer Seite für eine Seitenwiederherstellung an. Diese wird nur für Datenbanken unterstützt, die das vollständige oder massenprotokollierte Wiederherstellungsmodell verwenden. Mit den Parametern werden folgende Werte angegeben:  
  
PAGE  
 Zeigt eine Liste mit mindestens einer Datei oder Seite an.  
  
 *file*  
 Die Datei-ID der Datei, die eine bestimmte wiederherzustellende Seite enthält.  
  
 *page*  
 Die Seiten-ID der in der Datei wiederherzustellenden Seite.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass mehrere Seiten angegeben werden können.  
  
 Die maximale Anzahl der Seiten, die in einer Wiederherstellungssequenz in einer einzigen Datei wiederhergestellt werden können, beträgt 1000. Wenn jedoch eine größere Anzahl von beschädigten Seiten in einer Datei vorhanden ist, sollten Sie die Wiederherstellung der gesamten Datei statt der Seiten in Betracht ziehen.  
  
> [!NOTE]  
>  Seitenwiederherstellungen werden nie wiederhergestellt.  
  
 Weitere Informationen zur Seitenwiederherstellung finden Sie unter [Wiederherstellung von Seiten &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md).  
  
 [ **,**...*n* ]  
 Ein Platzhalter, der anzeigt, dass mehrere Dateien, Dateigruppen und Seiten in einer durch Trennzeichen getrennten Liste angegeben werden können. Für die Anzahl gibt es keine Einschränkungen.  
  
FROM { \<backup_device> [ **,**...*n* ]| \<database_snapshot> } Gibt normalerweise die Sicherungsmedien an, von denen die Sicherung wiederhergestellt werden soll. Alternativ dazu können Sie in der FROM-Klausel einer RESTORE DATABASE-Anweisung auch den Namen einer Momentaufnahme angeben, auf den die Datenbank zurückgesetzt werden soll. In diesem Fall ist die WITH-Klausel nicht zulässig.  
  
 Falls die FROM-Klausel nicht angegeben wird, findet die Wiederherstellung einer Sicherung nicht statt. Stattdessen wird die Datenbank wiederhergestellt. Dies ermöglicht Ihnen die Wiederherstellung einer Datenbank, für die eine Dateiwiederherstellung mit der Option NORECOVERY durchgeführt wurde, oder das Wechseln zu einem Standbyserver. Falls die FROM-Klausel nicht angegeben wird, müssen NORECOVERY, RECOVERY oder STANDBY in der WITH-Klausel angegeben werden.  
  
 \<backup_device> [ **,**...*n* ] Gibt das logische oder physische Sicherungsmedium an, das für den Wiederherstellungsvorgang verwendet wird.  
  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md), [RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 \<backup_device>::= Gibt ein logisches oder physisches Sicherungsmedium an, das wie folgt für den Sicherungsvorgang verwendet werden soll:  
  
 { *logical_backup_device_name* | **@***logical_backup_device_name_var* } Der logische Name, der von **sp_addumpdevice** erstellten Sicherungsmedien, von denen die Datenbank wiederhergestellt wird. Der Name muss den Regeln für Bezeichner entsprechen. Bei der Angabe als Variable (**@***logical_backup_device_name_var*) kann der Name des Sicherungsmediums entweder als Zeichenfolgenkonstante (**@***logical_backup_device_name_var* = *logical_backup_device_name*) oder als Variable eines Zeichenfolgen-Datentyps (mit Ausnahme der Datentypen **ntext** oder **text**) angegeben werden.  
  
 {DISK | TAPE } **=** { **'***physical_backup_device_name***'** | **@***physical_backup_device_name_var* } Ermöglicht die Wiederherstellung von Sicherungen vom angegebenen Datenträger oder vom Bandmedium. Die Gerätetypen von Datenträgern und Bändern sollten durch die tatsächlichen Namen des Geräts angegeben werden (z.B. vollständiger Pfad und Dateiname): `DISK ='Z:\SQLServerBackups\AdventureWorks.bak'` oder `TAPE ='\\\\.\TAPE0'`. Bei der Angabe als Variable (**@***physical_backup_device_name_var*) kann der Name des Geräts entweder als Zeichenfolgenkonstante (**@***physical_backup_device_name_var* = '*physcial_backup_device_name*') oder als Variable eines Zeichenfolgen-Datentyps (mit Ausnahme der Datentypen **ntext** oder **text**) angegeben werden.  
  
 Wenn Sie einen Netzwerkserver mit einem UNC-Namen (der einen Computernamen enthalten muss) verwenden, geben Sie die Geräteart Datenträger (DISK) an. Weitere Informationen zur Verwendung von UNC-Namen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 Das Konto, unter dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, muss über Lesezugriff auf den Remotecomputer oder Netzwerkserver verfügen, damit ein RESTORE-Vorgang ausgeführt werden kann.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass in einer durch Trennzeichen getrennten Liste möglicherweise bis zu 64 Sicherungsmedien angegeben werden.  
  
 Ob für eine Wiederherstellungssequenz so viele Sicherungsmedien erforderlich sind, wie beim Erstellen des Mediensatzes verwendet wurden, zu dem die Sicherungen gehören, hängt davon ab, ob die Wiederherstellung offline oder online erfolgt:  
  
-   Bei der Offlinewiederherstellung kann eine Sicherung mit weniger Medien wiederhergestellt werden, als zum Erstellen der Sicherung erforderlich waren.  
  
-   Für eine Onlinewiederherstellung sind alle Sicherungsmedien der Sicherung erforderlich. Einer Wiederherstellungsversuch mit weniger Medien erzeugt einen Fehler.  
  
 Angenommen, eine Datenbank wurde auf vier Bandlaufwerken gesichert, die mit dem Server verbunden sind. Für eine Onlinewiederherstellung müssen vier Laufwerke mit dem Server verbunden sein. Bei einer Offlinewiederherstellung ist es möglich, die Sicherung auch dann wiederherzustellen, wenn weniger als vier Laufwerke mit dem Computer verbunden sind.  
  
> [!NOTE]  
>  Beim Wiederherstellen einer Sicherung von einem gespiegelten Mediensatz können Sie nur einen Spiegel für jede Medienfamilie angeben. Falls Fehler auftreten, kann das Vorhandensein der anderen Spiegel jedoch dazu beitragen, dass einige Wiederherstellungsprobleme schneller gelöst werden können. Sie können ein beschädigtes Medienvolume durch das entsprechende Volume eines anderen Spiegels ersetzen. Beachten Sie, dass Offlinewiederherstellungen auch mit einer geringeren Anzahl von Medien als Medienfamilien möglich sind; jede Familie wird jedoch nur einmal verarbeitet.  
  
\<database_snapshot>::=  
**Unterstützt durch:**  [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
DATABASE_SNAPSHOT **=***database_snapshot_name*  
 Stellt die Datenbank mit der Datenbankmomentaufnahme wieder her, die durch *database_snapshot_name* angegeben wurde. Die Option DATABASE_SNAPSHOT ist nur bei einer vollständigen Datenbankwiederherstellung verfügbar. Beim Zurücksetzen tritt die Datenbankmomentaufnahme an die Stelle der vollständigen Datenbanksicherung.  
  
 Für das Zurücksetzen ist es erforderlich, dass die angegebene Datenbankmomentaufnahme die einzige Momentaufnahme für die Datenbank ist. Während des Vorgangs werden die Datenbankmomentaufnahme und die Zieldatenbank als `In restore` markiert. Weitere Informationen finden Sie im Abschnitt „Hinweise“ unter [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md).  
  
### <a name="with-options"></a>WITH-Optionen  
 Gibt die Optionen an, die bei einem Wiederherstellungsvorgang verwendet werden sollen. Eine Zusammenfassung der Anweisungen und der jeweils verwendeten Option finden Sie im Abschnitt zur Zusammenfassung der Unterstützung für WITH-Optionen weiter unten in diesem Thema.  
  
> [!NOTE]  
>  Die WITH-Optionen sind hier in der gleichen Reihenfolge wie im Abschnitt „Syntax“ in [RESTORE {DATABASE|LOG}](../../t-sql/statements/restore-statements-transact-sql.md) organisiert.  
  
 PARTIAL  
 **Unterstützt durch:**  [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Gibt einen Teilwiederherstellungsvorgang an, bei dem die primäre Dateigruppe und alle angegebenen sekundären Dateigruppen wiederhergestellt werden. Die Option PARTIAL wählt implizit die primäre Dateigruppe aus; die Angabe FILEGROUP = 'PRIMARY' ist nicht erforderlich. Geben Sie die Dateigruppe explizit mithilfe der Option FILE oder der Option FILEGROUP an, um eine sekundäre Dateigruppe wiederherzustellen.  
  
 Die Option PARTIAL ist bei RESTORE LOG-Anweisungen nicht zulässig.  
  
 Durch die Option PARTIAL wird die Anfangsphase einer schrittweisen Wiederherstellung gestartet, wodurch es möglich ist, die verbleibenden Dateigruppen zu einem späteren Zeitpunkt wiederherzustellen. Weitere Informationen finden Sie unter [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).  
  
 [ **RECOVERY** | NORECOVERY | STANDBY ]  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 **RECOVERY**  
 Weist den Wiederherstellungsvorgang an, einen Rollback für jede Transaktion auszuführen, für die kein Commit ausgeführt wurde. Nach dem Wiederherstellungsprozess kann die Datenbank verwendet werden. Falls weder NORECOVERY noch RECOVERY noch STANDBY angegeben wird, ist RECOVERY die Standardeinstellung.  
  
 Falls nachfolgende RESTORE-Vorgänge (RESTORE LOG oder RESTORE DATABASE von differenzieller Sicherung) geplant sind, sollte stattdessen NORECOVERY oder STANDBY angegeben werden.  
  
 Wenn Sicherungssätze wiederhergestellt werden sollen, die mit einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt wurden, ist möglicherweise ein Datenbankupgrade erforderlich. Dieses Upgrade erfolgt automatisch, wenn WITH RECOVERY angegeben ist. Weitere Informationen finden Sie unter [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
> [!NOTE]  
>  Falls die FROM-Klausel nicht angegeben wird, müssen NORECOVERY, RECOVERY oder STANDBY in der WITH-Klausel angegeben werden.  
  
 NORECOVERY  
 Weist den Wiederherstellungsvorgang an, keinen Rollback für Transaktionen durchzuführen, für die kein Commit ausgeführt wurde. Wenn später ein weiteres Transaktionsprotokoll angewendet werden muss, sollten Sie entweder die Option NORECOVERY oder die Option STANDBY angeben. Falls weder NORECOVERY noch RECOVERY noch STANDBY angegeben wird, ist RECOVERY die Standardeinstellung. Beim Durchführen eines Offlinewiederherstellungsvorgangs mit der Option NORECOVERY kann die Datenbank nicht verwendet werden.  
  
 Wenn Sie eine Datenbanksicherung und ein oder mehrere Transaktionsprotokolle wiederherstellen oder wenn mehrere RESTORE-Anweisungen notwendig sind (z. B. wenn eine vollständige Datenbanksicherung und danach eine differenzielle Datenbanksicherung wiederhergestellt wird), muss die Option WITH NORECOVERY für alle RESTORE-Anweisungen angegeben werden. Dies gilt jedoch nicht für die letzte RESTORE-Anweisung. Eine bewährte Methode ist das Verwenden der Option WITH NORECOVERY für ALLE Anweisungen in einer aus mehreren Schritten bestehenden Wiederherstellungssequenz, bis der gewünschte Wiederherstellungspunkt erreicht ist. Danach verwenden Sie eine separate RESTORE WITH RECOVERY-Anweisung ausschließlich für die Wiederherstellung.  
  
 Bei Verwendung der Option NONRECOVERY mit einem Wiederherstellungsvorgang für Dateien oder Dateigruppen erzwingt die Option, dass die Datenbank nach dem Wiederherstellungsvorgang im Wiederherstellungsstatus bleibt. Dies ist in folgenden Situationen nützlich:  
  
-   Ein Wiederherstellungsskript wird ausgeführt, und das Protokoll soll immer angewendet werden.  
  
-   Eine Sequenz von Dateiwiederherstellungen wird verwendet, und die Datenbank soll nicht zwischen zwei der Wiederherstellungsvorgängen verwendet werden können.  
  
 In einigen Fällen bewirkt RESTORE WITH NORECOVERY einen Rollforward der Rollforwardgruppe, der weit genug reicht, um die Konsistenz mit der Datenbank zu erreichen. In diesen Fällen erfolgt kein Rollback, und die Daten bleiben offline, wie bei dieser Option zu erwarten ist. In [!INCLUDE[ssDE](../../includes/ssde-md.md)] wird jedoch eine Informationsmeldung ausgegeben, in der angegeben wird, dass eine Wiederherstellung der Rollforwardgruppe mit der Option RECOVERY jetzt möglich ist.  
  
STANDBY **=***standby_file_name*  
 Gibt eine Standbydatei an, die es ermöglicht, die Auswirkungen der Wiederherstellungen rückgängig zu machen. Die Option STANDBY ist nur bei Offlinewiederherstellungen (einschließlich Teilwiederherstellungen) zulässig. Bei Onlinewiederherstellungen darf diese Option nicht verwendet werden. Das Angeben der Option STANDBY bei einem Onlinewiederherstellungsvorgang bewirkt, dass der Wiederherstellungsvorgang einen Fehler erzeugt. STANDBY ist ebenfalls nicht zulässig, wenn ein Datenbankupgrade erforderlich ist.  
  
 Mithilfe der Standbydatei wird ein Vorab-Image (mithilfe der Kopie bei Schreibvorgang) für Seiten beibehalten, die während der Umkehrphase eines RESTORE WITH STANDBY-Vorgangs geändert werden. Die Standbydatei ermöglicht den schreibgeschützten Zugriff auf eine Datenbank zwischen Wiederherstellungen des Transaktionsprotokolls. Die Datei kann entweder bei betriebsbereitem Standbyserver oder in besonderen Wiederherstellungssituationen verwendet werden, in denen die Überprüfung der Datenbank zwischen Protokollwiederherstellungen sinnvoll ist. Nach einem RESTORE WITH STANDBY-Vorgang wird die Rückgängigdatei beim nächsten RESTORE-Vorgang automatisch gelöscht. Wenn diese Standbydatei vor dem nächsten RESTORE-Vorgang manuell gelöscht wird, muss die ganze Datenbank erneut wiederhergestellt werden. Während die Datenbank den STANDBY-Status aufweist, müssen Sie diese Standbydatei mit derselben Sorgfalt wie jede andere Datenbankdatei behandeln. Anders als andere Datenbankdateien wird diese Datei nur während aktiver Wiederherstellungsvorgänge von [!INCLUDE[ssDE](../../includes/ssde-md.md)] offen gehalten.  
  
 *standby_file_name* gibt eine Standbydatei an, deren Speicherort im Protokoll der Datenbank gespeichert ist. Wenn der angegebene Name von einer vorhandenen Datei verwendet wird, wird die Datei überschrieben. Andernfalls wird die Datei von [!INCLUDE[ssDE](../../includes/ssde-md.md)] erstellt.  
  
 Die Größenanforderung einer bestimmten Standbydatei hängt vom Umfang der Umkehraktionen ab, die sich im Verlauf der Wiederherstellung durch Transaktionen ergeben, für die kein Commit ausgeführt wurde.  
  
> [!IMPORTANT]  
>  Falls kein Speicherplatz mehr auf dem Datenträger mit der angegebenen Standbydatei verfügbar ist, wird der Wiederherstellungsvorgang beendet.  
  
 Einen Vergleich zwischen RECOVERY und NORECOVERY finden Sie im Abschnitt „Hinweise“ unter [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md).  
  
LOADHISTORY  
 **Unterstützt durch:**  [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 Gibt an, dass der Wiederherstellungsvorgang die Informationen in die Verlaufstabellen von **msdb** lädt. Mit der Option LOADHISTORY werden für den einzelnen Sicherungssatz, der überprüft wird, Informationen zu auf dem Mediensatz gespeicherten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherungen in die Sicherungs- und Wiederherstellungsverlaufstabellen in der **msdb**-Datenbank geladen. Weitere Informationen zu Verlaufstabellen finden Sie unter [Systemtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md).  
  
#### <a name="generalwithoptions--n-"></a>\<general_WITH_options> [ ,...n ]  
 Alle allgemeinen WITH-Optionen werden in der RESTORE DATABASE-Anweisung und der RESTORE LOG-Anweisung unterstützt. Einige dieser Optionen werden, wie unten angegeben, auch von einer oder mehreren Hilfsanweisungen unterstützt.  
  
##### <a name="restore-operation-options"></a>Optionen für den Wiederherstellungsvorgang  
 Diese Optionen beeinflussen das Verhalten des Wiederherstellungsvorgangs.  
  
MOVE **'***logical_file_name_in_backup***'** TO **'***operating_system_file_name***'** [ ...*n* ]  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 Gibt an, dass die Daten- oder Protokolldatei, deren logischer Name durch *logical_file_name_in_backup* angegeben wird, verschoben werden sollte, indem sie an dem durch *operating_system_file_name* angegebenen Speicherort wiederhergestellt wird. Der logische Dateiname einer Daten- oder Protokolldatei in einem Sicherungssatz entspricht ihrem logischen Namen in der Datenbank zum Zeitpunkt der Erstellung des Sicherungssatzes.  
  
*n* ist ein Platzhalter, der angibt, dass weitere MOVE-Anweisungen angegeben werden können. Geben Sie für jede logische Datei, die aus dem Sicherungssatz an einem neuen Speicherort wiederhergestellt werden soll, eine MOVE-Anweisung an. Die Datei *logical_file_name_in_backup* wird standardmäßig an ihrem ursprünglichen Speicherort wiederhergestellt.  
  
> [!NOTE]  
>  Mit RESTORE FILELISTONLY können Sie eine Liste abrufen, in der die logischen Dateien eines Sicherungssatzes aufgeführt sind.  
  
 Wenn eine RESTORE-Anweisung zum Verschieben einer Datenbank auf demselben Server oder zum Kopieren der Datenbank auf einen anderen Server verwendet wird, kann die Option MOVE notwendig sein, um die Datenbankdateien zu verschieben und Konflikte mit vorhandenen Dateien zu vermeiden.  
  
 Wenn die Option MOVE mit RESTORE LOG verwendet wird, kann sie nur zum Verschieben von Dateien verwendet werden, die während des Intervalls hinzugefügt wurden, das durch das wiederherzustellende Protokoll abgedeckt wird. Wenn die Protokollsicherung beispielsweise eine Dateihinzufügung für die Datei `file23` enthält, kann diese Datei mithilfe der Option MOVE in RESTORE LOG verschoben werden.  
  
 Bei Verwendung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Snapshotsicherung kann die MOVE-Option nur verwendet werden, um Dateien in ein Azure-Blob zu verschieben, der sich in demselben Konto befindet wie der ursprüngliche Blob. Die MOVE-Option kann nicht zur Wiederherstellung der Snapshotsicherung in einer lokalen Datei oder einem anderen Speicherkonto verwendet werden.  
  
 Wenn eine RESTORE VERIFYONLY-Anweisung verwendet wird, um eine Datenbank auf demselben Server zu verschieben oder um sie auf einen anderen Server zu kopieren, kann die Option MOVE notwendig sein. Sie wird verwendet, um zu überprüfen, ob ausreichend Speicherplatz auf dem Zielserver verfügbar ist und um potenzielle Konflikte mit vorhandenen Dateien zu identifizieren.  
  
 Weitere Informationen finden Sie unter [Kopieren von Datenbanken durch Sichern und Wiederherstellen](../../relational-databases/databases/copy-databases-with-backup-and-restore.md).  
  
CREDENTIAL  
 **Unterstützt durch:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
**Gilt für** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Wird nur verwendet, wenn eine Sicherung vom Microsoft Azure Blob-Speicherdienst wiederhergestellt wird.  
  
> [!NOTE]  
>  Bei [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 bis [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ist eine Wiederherstellung von einem einzelnen Gerät nur dann möglich, wenn Sie die Wiederherstellung über eine URL durchführen. Wenn Sie die Wiederherstellung über eine URL durchführen, müssen Sie [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658) und die SAS-Token (SAS = Shared Access Signature) verwenden, damit eine Wiederherstellung von mehreren Geräten möglich ist. Weitere Informationen finden Sie unter [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md) (Aktivieren einer von SQL Server verwalteten Sicherung für Microsoft Azure) und unter [Simplifying creation of SQL Credentials with Shared Access Signature ( SAS ) tokens on Azure Storage with Powershell](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx) (Vereinfachen der Erstellung von SQL-Anmeldeinformationen mit Shared Access Signature-Token in Azure Storage mit PowerShell).  
  
 REPLACE  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die angegebene Datenbank und die zugehörigen Dateien erstellen soll, auch wenn bereits eine andere Datenbank mit demselben Namen vorhanden ist. In einem solchen Fall wird die vorhandene Datenbank gelöscht. Wenn die Option REPLACE nicht angegeben ist, erfolgt eine Sicherheitsüberprüfung. Dadurch wird das versehentliche Überschreiben einer anderen Datenbank verhindert. Die Sicherheitsüberprüfung stellt sicher, dass die RESTORE DATABASE-Anweisung die Datenbank nicht auf dem aktuellen Server wiederherstellt, wenn beide der folgenden Bedingungen erfüllt sind:  
  
-   Die in der RESTORE-Anweisung angegebene Datenbank ist bereits auf dem aktuellen Server vorhanden.  
  
-   Der Datenbankname unterscheidet sich von dem im Sicherungssatz aufgezeichneten Datenbanknamen.  
  
 Durch die Angabe von REPLACE kann mit RESTORE außerdem eine vorhandene Datei überschrieben werden, deren Zugehörigkeit zu der Datenbank, die wiederhergestellt wird, nicht festgestellt werden kann. Normalerweise ist das Überschreiben vorhandener Dateien mit RESTORE nicht möglich. Auf dieselbe Weise kann WITH REPLACE auch in Verbindung mit RESTORE LOG verwendet werden.  
  
 Bei der Verwendung von REPLACE ist es außerdem nicht mehr notwendig, das Protokollfragment zu sichern, bevor die Datenbank wiederhergestellt wird.  
  
 Weitere Informationen zu den Auswirkungen der Verwendung der REPLACE-Option finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
RESTART  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen unterbrochenen Wiederherstellungsvorgang neu starten soll. RESTART startet den Wiederherstellungsvorgang an dem Punkt wieder neu, an dem er unterbrochen wurde.  
  
RESTRICTED_USER  
 **Unterstützt durch:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 Beschränkt den Zugriff auf die erneut wiederhergestellte Datenbank auf Mitglieder mit den Rollen **db_owner**, **dbcreator** oder **sysadmin**.  RESTRICTED_USER ersetzt die Option DBO_ONLY. DBO_ONLY wurde mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] eingestellt.  
  
 Verwenden Sie diese Option in Verbindung mit der Option RECOVERY.  
  
##### <a name="backup-set-options"></a>Sicherungssatzoptionen  
 Diese Optionen werden für den Sicherungssatz verwendet, der die wiederherzustellende Sicherung enthält.  
  
FILE **=**{ *backup_set_file_number* | **@***backup_set_file_number* }  
 **Unterstützt von:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Identifiziert den wiederherzustellenden Sicherungssatz. Wenn *backup_set_file_number* beispielsweise den Wert **1** besitzt, weist dies auf den ersten Sicherungssatz auf dem Sicherungsmedium hin. Wenn *backup_set_file_number* den Wert **2** besitzt, entspricht dies dem zweiten Sicherungssatz. Sie können die *backup_set_file_number* eines Sicherungssatzes mit der [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) -Anweisung abrufen.  
  
 Wenn dieses Argument nicht angegeben wird, gilt der Standardwert **1**. Eine Ausnahme stellt RESTORE HEADERONLY dar; hier werden alle Sicherungssätze im Mediensatz verarbeitet. Weitere Informationen finden Sie im Abschnitt zum Angeben eines Sicherungssatzes weiter unten in diesem Thema.  
  
> [!IMPORTANT]  
>  Diese FILE-Option steht in keinem Zusammenhang mit der FILE-Option für die Angabe einer Datenbankdatei, FILE **=** { *logical_file_name_in_backup* | **@***logical_file_name_in_backup_var* }.  
  
 PASSWORD  **=** { *password* | **@***password_variable* }  
 **Unterstützt von:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Gibt das Kennwort für den Sicherungssatz an. Das Kennwort für einen Sicherungssatz ist eine Zeichenfolge.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Wenn beim Erstellen des Sicherungssatzes ein Kennwort angegeben wurde, ist dieses Kennwort erforderlich, um einen Wiederherstellungsvorgang auf der Grundlage des Sicherungssatzes auszuführen. Die Angabe eines falschen Kennworts oder die Angabe eines Kennworts, wenn der Sicherungssatz nicht über ein Kennwort verfügt, stellt einen Fehler dar.  
  
> [!IMPORTANT]  
>  Dieses Kennwort bietet nur einen geringen Schutz für den Mediensatz. Weitere Informationen finden Sie im Abschnitt zu den Berechtigungen für die jeweilige Anweisung.  
  
##### <a name="media-set-options"></a>Mediensatzoptionen  
 Diese Optionen werden für den Mediensatz insgesamt verwendet.  
  
 MEDIANAME **=** { *media_name* | **@***media_name_variable*}  
 **Unterstützt durch:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Gibt den Mediennamen an. Falls der Medienname bereitgestellt wird, muss er mit dem Mediennamen auf den Sicherungsvolumes übereinstimmen. Andernfalls wird der Wiederherstellungsvorgang beendet. Falls kein Medienname in der RESTORE-Anweisung angegeben wird, wird keine Überprüfung auf einen übereinstimmenden Mediennamen auf den Sicherungsvolumes ausgeführt.  
  
> [!IMPORTANT]  
>  Das einheitliche Verwenden von Mediennamen in Sicherungs- und Wiederherstellungsvorgängen ermöglicht eine zusätzliche Sicherheitsüberprüfung der Medien, die für den Wiederherstellungsvorgang ausgewählt wurden.  
  
 MEDIAPASSWORD **=** { *mediapassword* | **@***mediapassword_variable* }  
 **Unterstützt durch:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Stellt das Kennwort für den Mediensatz bereit. Das Kennwort für einen Mediensatz ist eine Zeichenfolge.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Wenn beim Formatieren des Mediensatzes ein Kennwort bereitgestellt wurde, ist dieses Kennwort für den Zugriff auf einen beliebigen Sicherungssatz auf dem Mediensatz erforderlich. Die Angabe eines falschen Kennworts oder die Angabe eines Kennworts, wenn der Mediensatz nicht über ein Kennwort verfügt, stellt einen Fehler dar.  
  
> [!IMPORTANT]  
>  Dieses Kennwort bietet nur einen geringen Schutz für den Mediensatz. Weitere Informationen finden Sie im Abschnitt zu den Berechtigungen der jeweiligen Anweisung.  
  
 BLOCKSIZE **=** { *blocksize* | **@***blocksize_variable* }  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Legt die physische Blockgröße in Bytes fest. Die unterstützten Größen sind 512, 1024, 2048, 4096, 8192, 16.384, 32.768 und 65.536 (64 KB) Bytes. Der Standardwert ist 65.536 für Bandmedien und andernfalls 512. In der Regel ist diese Option nicht erforderlich, da von RESTORE automatisch eine Blockgröße ausgewählt wird, die für das Medium geeignet ist. Mit der expliziten Angabe einer Blockgröße wird die automatische Wahl der Blockgröße überschrieben.  
  
 Wenn Sie eine Sicherung von einer CD-ROM wiederherstellen, geben Sie BLOCKSIZE=2048 an.  
  
> [!NOTE]  
>  Diese Option hat i. d. R. nur dann Auswirkungen auf die Leistung, wenn von Bandmedien gelesen wird.  
  
##### <a name="data-transfer-options"></a>Datenübertragungsoptionen  
 Die Optionen ermöglichen es Ihnen, die Datenübertragung vom Sicherungsmedium zu optimieren.  
  
 BUFFERCOUNT **=** { *buffercount* | **@***buffercount_variable* }  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Gibt die Gesamtanzahl von E/A-Puffern an, die für den Wiederherstellungsvorgang verwendet werden sollen. Sie können eine beliebige positive ganze Zahl angeben. Eine große Pufferanzahl kann jedoch wegen eines ungeeigneten virtuellen Adressraumes im Prozess Sqlservr.exe zu Fehlern aufgrund von nicht genügend Arbeitsspeicher führen.  
  
 Der gesamte von den Puffern belegte Speicherplatz wird durch *buffercount***\****maxtransfersize* bestimmt.  
  
 MAXTRANSFERSIZE **=** { *maxtransfersize* | **@***maxtransfersize_variable* }  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Gibt die größte zu verwendende Übertragungseinheit zwischen dem Sicherungsmedium und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Bytes an. Die möglichen Werte sind Vielfache von 65.536 Bytes (64 KB) bis hin zu 4.194.304 Bytes (4 MB).  
> [!NOTE]  
>  Wenn für die Datenbank FILESTREAM konfiguriert ist oder In-Memory-OLTP-Dateigruppen enthält, muss `MAXTRANSFERSIZE` zum Zeitpunkt der Wiederherstellung größer als oder gleich dem Wert sein, der bei der Erstellung der Sicherung verwendet wurde.  
  
##### <a name="error-management-options"></a>Fehlerverwaltungsoptionen  
 Mit diesen Optionen können Sie bestimmen, ob Sicherungsprüfsummen für den Wiederherstellungsvorgang aktiviert werden und ob der Vorgang beim Auftreten eines Fehlers beendet wird.    
  
 { CHECKSUM | NO_CHECKSUM }  
 **Unterstützt durch:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Das Standardverhalten besteht darin, Prüfsummen zu überprüfen, falls sie vorhanden sind, oder den Vorgang ohne Überprüfung fortzusetzen, falls sie nicht vorhanden sind.  
  
 CHECKSUM  
 Gibt an, dass Sicherungsprüfsummen überprüft werden müssen, und bewirkt, falls die Sicherung keine Sicherungsprüfsummen aufweist, dass der Wiederherstellungsvorgang einen Fehler erzeugt und eine Meldung ausgegeben wird, die auf das Fehlen der Prüfsummen hinweist.  
  
> [!NOTE]  
>  Seitenprüfsummen sind für Sicherungsvorgänge nur bei Verwendung von Sicherungsprüfsummen relevant.  
  
 Wenn eine ungültige Prüfsumme festgestellt wird, meldet RESTORE standardmäßig einen Prüfsummenfehler und beendet den Vorgang. Wenn Sie jedoch CONTINUE_AFTER_ERROR angeben, fährt RESTORE mit der Wiederherstellung fort. Dies erfolgt, nachdem ein Prüfsummenfehler und die Nummer der Seite zurückgegeben wurde, vorausgesetzt, die Beschädigung lässt dies zu.  
  
 Weitere Informationen zur Arbeit mit Prüfsummen für Sicherungen finden Sie unter [Mögliche Medienfehler während der Sicherung und Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 NO_CHECKSUM  
 Deaktiviert explizit die Überprüfung von Prüfsummen durch den Wiederherstellungsvorgang.  
  
 { **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }  
 **Unterstützt durch:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 STOP_ON_ERROR  
 Gibt an, dass der Wiederherstellungsvorgang beendet wird, sobald der erste Fehler festgestellt wird. Das ist das Standardverhalten von RESTORE. Eine Ausnahme stellt VERIFYONLY dar; hier wird das Standardverhalten durch CONTINUE_AFTER_ERROR definiert.  
  
 CONTINUE_AFTER_ERROR  
 Gibt an, dass der Wiederherstellungsvorgang fortgesetzt werden soll, nachdem ein Fehler festgestellt wurde.  
  
 Wenn eine Sicherung beschädigte Seiten enthält, ist es das Beste, den Wiederherstellungsvorgang mithilfe einer alternativen Sicherung zu wiederholen, in der die Fehler nicht enthalten sind. Dies kann beispielsweise eine Sicherung sein, die ausgeführt wurde, bevor die Seiten beschädigt wurden. Als letzte Möglichkeit können Sie eine beschädigte Sicherung mithilfe der Option CONTINUE_AFTER_ERROR der Wiederherstellungsanweisung wiederherstellen und so versuchen, die Daten zu retten.  
  
##### <a name="filestream-options"></a>FILESTREAM-Optionen  
 FILESTREAM ( DIRECTORY_NAME =*directory_name* )  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
**Gilt für** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Ein Windows-kompatibler Verzeichnisname. Dieser Name sollte für alle FILESTREAM-Verzeichnisnamen auf Datenbankebene in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz eindeutig sein. Bei Eindeutigkeitsvergleichen wird unabhängig von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortiereinstellungen die Groß-/Kleinschreibung nicht beachtet.  
  
##### <a name="monitoring-options"></a>Überwachungsoptionen  
 Diese Optionen ermöglichen es Ihnen, die Datenübertragung vom Sicherungsmedium zu überwachen.  
  
 STATS [ **=** *percentage* ]  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 Zeigt nach jedem abgeschlossenen Prozentsatz eine Meldung an und wird als Statusanzeige verwendet. Wird der *Prozentsatz* nicht angegeben, zeigt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jedes Mal eine Meldung an, wenn weitere ca. 10 % des Vorgangs abgeschlossen sind.  
  
 Mit der Option STATS wird der Prozentsatz gemeldet, der beim Erreichen des Schwellenwertes für das nächste Meldungsintervall abgeschlossen ist. Dies entspricht ungefähr dem angegebenen Prozentsatz. Wenn beispielsweise STATS=10 angegeben wird, meldet [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Status ungefähr in diesem Intervall. Statt z. B. genau 40 % anzuzeigen, würde durch diese Option möglicherweise der Wert 43 % angezeigt. Bei größeren Sicherungssätzen stellt dies kein Problem dar, da sich der Wert für den abgeschlossenen Prozentsatz zwischen abgeschlossenen E/A-Aufrufen nur sehr langsam verändert.  
  
##### <a name="tape-options"></a>Bandoptionen  
 Diese Optionen werden nur für Bandmedien verwendet. Diese Optionen werden ignoriert, wenn ein anderes Medium als ein Bandmedium verwendet wird.  
  
 { **REWIND** | NOREWIND }  
 Diese Optionen werden nur für Bandmedien verwendet. Die Optionen werden ignoriert, wenn ein anderes Medium als ein Bandmedium verwendet wird.  
  
 REWIND  
 **Unterstützt durch:** [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Band freigeben und zurückspulen soll. REWIND ist die Standardeinstellung.  
  
 NOREWIND  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 Das Angeben von NOREWIND in anderen als den angegebenen Wiederherstellungsanweisungen generiert einen Fehler.  
  
 Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Band nach dem Sicherungsvorgang offen hält. Diese Option dient der Leistungsverbesserung, wenn mehrere Sicherungsvorgänge auf einem Band ausgeführt werden.  
  
 NOREWIND impliziert NOUNLOAD, und diese Optionen sind innerhalb einer RESTORE-Anweisung inkompatibel.  
  
> [!NOTE]  
>  Wenn Sie NOREWIND verwenden, bleibt die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Besitzer des Bandlaufwerks, bis in einer BACKUP- oder RESTORE-Anweisung, die in demselben Prozess ausgeführt wird, die Option REWIND oder UNLOAD verwendet wird oder bis die Serverinstanz heruntergefahren wird. Ein Offenhalten des Bandes verhindert, dass andere Prozesse auf das Band zugreifen können. Informationen zum Anzeigen einer Liste offener Bänder und zum Schließen eines offenen Bandes finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 { **UNLOAD** | NOUNLOAD }  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md), [RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md) und [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Diese Optionen werden nur für Bandmedien verwendet. Die Optionen werden ignoriert, wenn ein anderes Medium als ein Bandmedium verwendet wird.  
  
> [!NOTE]  
>  UNLOAD/NOUNLOAD ist eine Sitzungseinstellung, die für die Dauer der Sitzung oder bis zur Angabe der alternativen Einstellung persistent gespeichert wird.  
  
 UNLOAD  
 Gibt an, dass das Band automatisch zurückgespult und ausgeworfen wird, wenn die Sicherung vollständig ausgeführt ist. UNLOAD ist die Standardeinstellung beim Beginn einer Sitzung.  
  
 NOUNLOAD  
 Gibt an, dass das Band nach dem RESTORE-Vorgang im Bandlaufwerk geladen bleibt.  
  
#### <a name="replicationwithoption"></a><replication_WITH_option>  
 Diese Option ist nur relevant, wenn die Datenbank beim Erstellen der Sicherung repliziert wurde.  
  
 KEEP_REPLICATION  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
Verwenden Sie KEEP_REPLICATION, wenn eine Replikation für die Verwendung von Protokollversand eingerichtet ist. Diese Option verhindert, dass Replikationseinstellungen entfernt werden, wenn eine Datenbank- oder Protokollsicherung auf einem betriebsbereiten Standbyserver wiederhergestellt und anschließend die Datenbank wiederhergestellt wird. Diese Option darf nicht angegeben werden, wenn eine Sicherung mit der Option NORECOVERY wiederhergestellt wird. Damit die Funktionsfähigkeit der Replikation nach einer Wiederherstellung sichergestellt ist, muss Folgendes erfüllt sein:  
  
-   Die Datenbanken **msdb** und **master** auf dem betriebsbereiten Standbyserver müssen mit den Datenbanken **msdb** und **master** auf dem primären Server synchron sein.  
  
-   Der betriebsbereite Standbyserver muss so umbenannt werden, dass er denselben Namen wie der primäre Server verwendet.  
  
#### <a name="changedatacapturewithoption"></a><change_data_capture_WITH_option>  
 Diese Option ist nur relevant, wenn die Datenbank beim Erstellen der Sicherung für Change Data Capture aktiviert wurde.  
  
 KEEP_CDC  
 **Unterstützt durch:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 KEEP_CDC sollte verwendet werden, um zu verhindern, dass Change Data Capture-Einstellungen entfernt werden, wenn eine Datenbank- oder Protokollsicherung auf einem anderen Server wiederhergestellt und anschließend die Datenbank wiederhergestellt wird. Diese Option darf nicht angegeben werden, wenn eine Sicherung mit der Option NORECOVERY wiederhergestellt wird.  
  
 Beim Wiederherstellen der Datenbank mit KEEP_CDC werden keine Change Data Capture-Aufträge erstellt. Wenn Sie nach der Datenbankwiederherstellung Änderungen aus dem Protokoll wiederherstellen möchten, müssen Sie den Auftrag für den Aufzeichnungsprozess und den Cleanupauftrag für die wiederhergestellte Datenbank neu erstellen. Weitere Informationen finden Sie unter [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md).  
  
 Informationen zur Verwendung von Change Data Capture bei der Datenbankspiegelung finden Sie unter [Change Data Capture und andere SQL Server-Features](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md).  
  
#### <a name="servicebrokerwithoptions"></a>\<service_broker_WITH_options>  
 Aktiviert oder deaktiviert die [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Nachrichtenübermittlung oder legt einen neuen [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Bezeichner fest. Diese Option ist nur relevant, wenn für die Datenbank bei Erstellung der Sicherung [!INCLUDE[ssSB](../../includes/sssb-md.md)] aktiviert wurde.  
  
 { ENABLE_BROKER  | ERROR_BROKER_CONVERSATIONS  | NEW_BROKER }  
 **Unterstützt durch:**  [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 ENABLE_BROKER  
 Gibt an, dass die [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Nachrichtenübermittlung nach Abschluss der Wiederherstellung aktiviert wird, sodass Nachrichten unmittelbar gesendet werden können. Standardmäßig wird die [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Nachrichtenübermittlung während einer Wiederherstellung deaktiviert. Der vorhandene Service Broker-Bezeichner der Datenbank wird beibehalten.  
  
 ERROR_BROKER_CONVERSATIONS  
 Beendet alle Konversationen mit einem Fehler, der angibt, dass die Datenbank angefügt oder wiederhergestellt wird. Auf diese Weise können Anwendungen reguläre Cleanups für bestehende Konversationen ausführen. Die Service Broker-Nachrichtenübermittlung wird deaktiviert, bis dieser Vorgang abgeschlossen ist, und dann aktiviert. Der vorhandene Service Broker-Bezeichner der Datenbank wird beibehalten.  
  
 NEW_BROKER  
 Gibt an, dass der Datenbank ein neuer Service Broker-Bezeichner zugewiesen wird. Da die Datenbank als neuer Service Broker betrachtet wird, werden alle bestehenden Konversationen in der Datenbank sofort entfernt, ohne Nachrichten über das Beenden des Dialogs zu erstellen. Jede Route, die auf den alten Service Broker-Bezeichner verweist, muss mit dem neuen Bezeichner neu erstellt werden.  
  
#### <a name="pointintimewithoptions"></a>\<point_in_time_WITH_options>  
 **Unterstützt durch:** [RESTORE {DATABASE|LOG}](../../t-sql/statements/restore-statements-transact-sql.md) und nur für die vollständigen oder massenprotokollierten Wiederherstellungsmodelle.  
  
 Sie können eine Datenbank für einen bestimmten Zeitpunkt oder eine bestimmte Transaktion wiederherstellen, indem Sie den Zielwiederherstellungspunkt in einer STOPAT-, STOPATMARK- oder STOPBEFOREMARK-Klausel angeben. Die Wiederherstellung zu einem bestimmten Zeitpunkt oder einer bestimmten Transaktion erfolgt immer aus einer Protokollsicherung. In jeder RESTORE LOG-Anweisung der Wiederherstellungssequenz müssen Sie den Zielzeitpunkt oder die Transaktion in einer identischen STOPAT-, STOPATMARK- oder STOPBEFOREMARK-Klausel angeben.  
  
 Als Voraussetzung für eine Zeitpunktwiederherstellung müssen Sie zuerst eine vollständige Datenbanksicherung wiederherstellen, deren Endpunkt vor dem Zielwiederherstellungspunkt liegt. Damit Sie besser ermitteln können, welche Datenbanksicherung wiederhergestellt werden soll, können Sie optional die WITH STOPAT-, STOPATMARK- oder STOPBEFOREMARK-Klausel in einer RESTORE DATABASE-Anweisung angeben, um einen Fehler auszulösen, wenn eine Datensicherung zu aktuell für den angegebenen Zielzeitpunkt ist. Die vollständige Datensicherung wird jedoch immer wiederhergestellt, auch wenn sie den Zielzeitpunkt enthält.  
  
> [!NOTE]  
>  Die point-in-time WITH-Optionen für RESTORE_DATABASE und RESTORE_LOG sind ähnlich, aber nur RESTORE LOG unterstützt das *mark_name*-Argument.  
  
 { STOPAT | STOPATMARK | STOPBEFOREMARK }   
 
 STOPAT **=** { **'***datetime***'** | **@***datetime_var* }  
 Gibt an, dass die Datenbank in dem Status wiederhergestellt wird, der zu dem Zeitpunkt (Datum und Uhrzeit) bestand, der durch den *datetime*-Parameter oder den **@***datetime_var*-Parameter angegeben wird. Weitere Informationen zur Angabe von Datum und Uhrzeit finden Sie unter [Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 Wenn eine Variable für STOPAT verwendet wird, muss es sich um eine Variable vom Datentyp **varchar**, **char**, **smalldatetime** oder **datetime** handeln. Nur Transaktionsprotokolleinträge, die vor dem angegebenen Datum und der angegebenen Uhrzeit geschrieben wurden, werden auf die Datenbank angewendet.  
  
> [!NOTE]  
>  Liegt die angegebene STOPAT-Zeit nach der letzten LOG-Sicherung, bleibt die Datenbank in einem nicht wiederhergestellten Status, als wäre RESTORE LOG mit NORECOVERY ausgeführt worden.  
  
 Informationen finden Sie unter [Wiederherstellen einer SQL Server-Datenbank auf einen Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
 STOPATMARK **=** { **'***mark_name***'** | **'**lsn:*lsn_number***'** } [ AFTER **'***datetime***'** ]  
 Gibt die Wiederherstellung bis zu einem bestimmten Wiederherstellungspunkt an. Die angegebene Transaktion wird in die Wiederherstellung eingeschlossen. Es wird jedoch nur dann ein Commit für die Transaktion ausgeführt, wenn auch für die ursprünglich generierte Transaktion ein Commit ausgeführt wurde.  
  
 Sowohl für RESTORE DATABASE als auch für RESTORE LOG wird der *lsn_number*-Parameter unterstützt. Mit diesem Parameter wird eine Protokollfolgenummer angegeben.  
  
 Der *mark_name*-Parameter wird nur von der RESTORE LOG-Anweisung unterstützt. Mit diesem Parameter wird eine Transaktionsmarkierung in der Protokollsicherung angegeben.  
  
 Wenn AFTER *datetime* in einer RESTORE LOG-Anweisung nicht angegeben ist, wird die Wiederherstellung bei der ersten Markierung mit dem angegebenen Namen beendet. Wenn AFTER *datetime* angegeben ist, wird die Wiederherstellung bei der ersten Markierung beendet, die den angegebenen Namen genau um oder nach *datetime* hat.  
  
> [!NOTE]  
>  Liegt die angegebene Markierung, LSN oder Zeit nach der letzten LOG-Sicherung, bleibt die Datenbank in einem nicht wiederhergestellten Status, als wäre RESTORE LOG mit NORECOVERY ausgeführt worden.  
  
 Weitere Informationen finden Sie unter [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) und unter [Wiederherstellen einer Protokollfolgenummer &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md).  
  
 STOPBEFOREMARK **=** { **'***mark_name***'** | **'**lsn:*lsn_number***'** } [ AFTER **'***datetime***'** ]  
 Gibt die Wiederherstellung bis zu einem bestimmten Wiederherstellungspunkt an. Die angegebene Transaktion wird nicht in die Wiederherstellung aufgenommen, und es wird ein Rollback für sie ausgeführt, wenn WITH RECOVERY verwendet wird.  
  
 Sowohl für RESTORE DATABASE als auch für RESTORE LOG wird der *lsn_number*-Parameter unterstützt. Mit diesem Parameter wird eine Protokollfolgenummer angegeben.  
  
 Der *mark_name*-Parameter wird nur von der RESTORE LOG-Anweisung unterstützt. Mit diesem Parameter wird eine Transaktionsmarkierung in der Protokollsicherung angegeben.  
  
 Wenn AFTER *datetime* in einer RESTORE LOG-Anweisung nicht angegeben ist, wird die Wiederherstellung unmittelbar vor der ersten Markierung mit dem angegebenen Namen beendet. Wenn AFTER *datetime* angegeben ist, wird die Wiederherstellung bei der ersten Markierung beendet, die den angegebenen Namen genau um oder nach *datetime* hat.  
  
> [!IMPORTANT]  
>  Wenn in einer Teilwiederherstellungssequenz eine FILESTREAM-Dateigruppe ausgeschlossen wird, wird die Wiederherstellung bis zu einem bestimmten Zeitpunkt nicht unterstützt. Sie können das Fortsetzen der Wiederherstellungssequenz erzwingen. Die FILESTREAM-Dateigruppen, die in die RESTORE-Anweisung nicht angegeben sind, können jedoch zu keinem Zeitpunkt wiederhergestellt werden. Wenn Sie eine Wiederherstellung bis zu einem bestimmten Zeitpunkt erzwingen möchten, geben Sie die CONTINUE_AFTER_ERROR-Option zusammen mit der Option STOPAT, STOPATMARK oder STOPBEFOREMARK an. Wenn Sie CONTINUE_AFTER_ERROR angeben, ist die Teilwiederherstellungssequenz erfolgreich, und die FILESTREAM-Dateigruppe wird nicht mehr wiederherstellbar.  
  
## <a name="result-sets"></a>Resultsets  
 Informationen zu Resultsets finden Sie in den folgenden Themen:  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
## <a name="remarks"></a>Remarks  
 Zusätzliche Hinweise finden Sie in den folgenden Themen:  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="specifying-a-backup-set"></a>Angeben eines Sicherungssatzes  
 Ein *Sicherungssatz* enthält die Sicherung aus einem einzelnen, erfolgreichen Sicherungsvorgang. Die Anweisungen RESTORE, RESTORE FILELISTONLY, RESTORE HEADERONLY und RESTORE VERIFYONLY verarbeiten einen einzelnen Sicherungssatz innerhalb des Mediensatzes auf den angegebenen Sicherungsmedien. Sie sollten den benötigten Sicherungssatz innerhalb des Mediensatzes angeben. Sie können die *backup_set_file_number* eines Sicherungssatzes mit der [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) -Anweisung abrufen.  
  
 Der wiederherzustellende Sicherungssatz wird mit der folgenden Option angegeben:  
  
 FILE **=**{ *backup_set_file_number* | **@***backup_set_file_number* }  
  
 Dabei gibt *backup_set_file_number* die Position der Sicherung im Mediensatz an. Wenn *backup_set_file_number* den Wert 1 (FILE = 1) besitzt, weist dies auf den ersten Sicherungssatz auf dem Sicherungsmedium hin. Und wenn *backup_set_file_number* den Wert 2 (FILE = 2) besitzt, entspricht dies dem zweiten Sicherungssatz, usw.  
  
 Das Verhalten der Option hängt von der Anweisung ab, wie in der folgenden Tabelle beschrieben:  
  
|-Anweisung.|Verhalten der Sicherungssatzoption FILE|  
|---------------|-----------------------------------------|  
|RESTORE|Der Standardwert für die Sicherungssatz-Dateinummer ist 1. In einer RESTORE-Anweisung ist nur eine einzelne Sicherungssatzoption FILE zulässig. Es ist wichtig, dass Sicherungssätze in der richtigen Reihenfolge angegeben werden.|  
|RESTORE FILELISTONLY|Der Standardwert für die Sicherungssatz-Dateinummer ist 1.|  
|RESTORE HEADERONLY|Standardmäßig werden alle Sicherungssätze im Mediensatz verarbeitet. Die Resultsets von RESTORE HEADERONLY geben Informationen zu jedem Sicherungssatz zurück, einschließlich seiner **Position** im Mediensatz. Geben Sie die Positionsnummer eines Sicherungssatzes als *backup_set_file_number*-Wert in der FILE-Option an, um Informationen zu einem bestimmten Sicherungssatz zurückzugeben.<br /><br /> Hinweis: Bei Bandmedien verarbeitet RESTORE HEADER nur Sicherungssätze auf dem geladenen Band.|  
|RESTORE VERIFYONLY|Der Standardwert für *backup_set_file_number* beträgt 1.|  
  
> [!NOTE]  
>  Diese FILE-Option für die Angabe eines Sicherungssatzes steht in keinem Zusammenhang mit der FILE-Option für die Angabe einer Datenbankdatei, FILE **=** { *logical_file_name_in_backup* | **@***logical_file_name_in_backup_var* }.  
  
## <a name="summary-of-support-for-with-options"></a>Zusammenfassung der Unterstützung für WITH-Optionen  
 Die folgenden WITH-Optionen werden nur von der RESTORE-Anweisung unterstützt: BLOCKSIZE, BUFFERCOUNT, MAXTRANSFERSIZE, PARTIAL, KEEP_REPLICATION, { RECOVERY | NORECOVERY | STANDBY }, REPLACE, RESTART, RESTRICTED_USER und { STOPAT | STOPATMARK | STOPBEFOREMARK }  
  
> [!NOTE]  
>  Die Option PARTIAL wird nur von RESTORE DATABASE unterstützt.  
  
 In der folgenden Liste sind die WITH-Optionen aufgeführt, die von einer oder mehreren Anweisungen verwendet werden. Für jede Option ist angegeben, von welchen Anweisungen sie unterstützt wird. Ein Häkchen (√) zeigt die Unterstützung der jeweiligen Option an, ein Strich (—) zeigt an, dass die Option nicht unterstützt wird.  
  
|WITH-Option|RESTORE|RESTORE FILELISTONLY|RESTORE HEADERONLY|RESTORE LABELONLY|RESTORE REWINDONLY|RESTORE VERIFYONLY|  
|-----------------|-------------|--------------------------|------------------------|-----------------------|------------------------|------------------------|  
|{ CHECKSUM<br /><br /> &#124; NO_CHECKSUM }|√|√|√|√|—|√|  
|{ CONTINUE_AFTER_ERROR<br /><br /> &#124; STOP_ON_ERROR }|√|√|√|√|—|√|  
|FILE<sup>1</sup>|√|√|√|—|—|√|  
|LOADHISTORY|—|—|—|—|—|√|  
|MEDIANAME|√|√|√|√|—|√|  
|MEDIAPASSWORD|√|√|√|√|—|√|  
|MOVE|√|—|—|—|—|√|  
|PASSWORD|√|√|√|—|—|√|  
|{ REWIND &#124; NOREWIND }|√|Nur REWIND|Nur REWIND|Nur REWIND|—|√|  
|STATS|√|—|—|—|—|√|  
|{ UNLOAD &#124; NOUNLOAD }|√|√|√|√|√|√|  
  
 <sup>1</sup> FILE **=***backup_set_file_number*, unterscheidet sich von {FILE | FILEGROUP}.  
  
## <a name="permissions"></a>Berechtigungen  
 Informationen zu Berechtigungen finden Sie in den folgenden Themen:  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="examples"></a>Beispiele  
 Beispiele finden Sie in den folgenden Themen:  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
  
  

