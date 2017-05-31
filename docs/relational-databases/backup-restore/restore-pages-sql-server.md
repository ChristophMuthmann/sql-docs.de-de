---
title: Wiederherstellung von Seiten (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.restorepage.general.f1
helpviewer_keywords:
- restoring pages [SQL Server]
- pages [SQL Server], restoring
- databases [SQL Server], damaged
- page restores [SQL Server]
- pages [SQL Server], damaged
- restoring [SQL Server], pages
ms.assetid: 07e40950-384e-4d84-9ac5-84da6dd27a91
caps.latest.revision: 67
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1cdf13c937ecdaa54c31831625dc6fc41b35be70
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="restore-pages-sql-server"></a>Wiederherstellung von Seiten (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Seiten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]wiederhergestellt werden. Das Ziel einer Seitenwiederherstellung besteht darin, eine oder mehrere beschädigte Seiten wiederherzustellen, ohne dazu die gesamte Datenbank wiederherstellen zu müssen. In der Regel wurden Seiten, die wiederhergestellt werden sollen, aufgrund eines Fehlers beim Zugriff auf die Seite als fehlerverdächtig gekennzeichnet. Fehlerverdächtige Seiten werden in der [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) -Tabelle in der **msdb** -Datenbank identifiziert.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Wann ist eine Seitenwiederherstellung sinnvoll?](#WhenUseful)  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **Wiederherstellen von Seiten mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="WhenUseful"></a> Wann ist eine Seitenwiederherstellung sinnvoll?  
 Eine Seitenwiederherstellung ist zum Reparieren einzelner beschädigter Seiten vorgesehen. Die Wiederherstellung weniger Einzelseiten erfolgt möglicherweise schneller als eine Dateiwiederherstellung, sodass sich die Menge der Daten reduziert, die während der Wiederherstellung offline sind. Wenn Sie jedoch mehrere Seiten in einer Datei wiederherstellen müssen, erweist sich die Wiederherstellung der vollständigen Datei in der Regel als effizienter. Wenn auf einem Gerät sehr viele Seiten beschädigt sind, kann das ein Hinweis auf einen Gerätefehler sein. In diesem Fall sollten Sie die Datei nach Möglichkeit an einem anderen Speicherort wiederherstellen und das Gerät reparieren.  
  
 Nicht für alle Fehler für einzelne Seiten ist eine Wiederherstellung erforderlich. In zwischengespeicherten Daten, z. B. einem sekundären Index, kann ein Problem auftreten, das durch das Neuberechnen der Daten behoben werden kann. Wenn der Datenbankadministrator beispielsweise einen sekundären Index löscht und erneut erstellt, werden die beschädigten Daten, obwohl sie repariert sind, nicht als solche in der [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) -Tabelle angezeigt.  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die Seitenwiederherstellung gilt für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken, für die das vollständige oder massenprotokollierte Wiederherstellungsmodell verwendet wird. Die Seitenwiederherstellung wird nur für Dateigruppen mit Lese-/Schreibzugriff unterstützt.  
  
-   Es können nur Datenbankseiten wiederhergestellt werden. Die Seitenwiederherstellung kann nicht zum Wiederherstellen der folgenden Elemente verwendet werden:  
  
    -   Transaktionsprotokoll  
  
    -   Zuordnungsseiten: GAM-Seiten (Global Allocation Map), SGAM-Seiten (Shared Global Allocation Map) und PFS-Seiten (Page Free Space).  
  
    -   Seite 0 von allen Datendateien (die Startseite der Datei)  
  
    -   Seite 1:9 (die Startseite der Datenbank)  
  
    -   Volltextkatalog  
  
-   Wenn für eine Datenbank das massenprotokollierte Wiederherstellungsmodell verwendet wird, gelten für die Seitenwiederherstellung die folgenden zusätzlichen Bedingungen:  
  
    -   Wenn die Dateigruppen- oder Seitendaten offline sind, gestaltet sich die Sicherung bei massenprotokollierten Daten problematisch, da die offline verfügbaren Daten nicht im Protokoll erfasst sind. Die Protokollsicherung kann durch jede beliebige Offlineseite verhindert werden. In diesen Fällen empfiehlt es sich, DBCC REPAIR zu verwenden, da dadurch weniger Daten verloren gehen als bei der Wiederherstellung der letzten Sicherung.  
  
    -   Wenn eine Protokollsicherung einer massenprotokollierten Datenbank eine beschädigte Seite erkennt, schlägt der Vorgang fehl, es sei denn, WITH CONTINUE_AFTER_ERROR wurde angegeben.  
  
    -   Die Seitenwiederherstellung ist bei der massenprotokollierten Wiederherstellung grundsätzlich nicht möglich.  
  
         Die bewährte Methode zum Ausführen einer Seitenwiederherstellung besteht darin, für die Datenbank das vollständige Wiederherstellungsmodell festzulegen und eine Protokollsicherung zu versuchen. Wenn die Protokollsicherung ausgeführt werden kann, können Sie die Seitenwiederherstellung fortsetzen. Wenn die Protokollsicherung fehlschlägt, geht entweder die Arbeit seit der letzten Protokollsicherung verloren, oder Sie müssen versuchen, DBCC mit der Option REPAIR_ALLOW_DATA_LOSS auszuführen.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Szenarien für die Seitenwiederherstellung  
  
     Offlineseitenwiederherstellung  
     In allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird das Wiederherstellen von Seiten unterstützt, wenn die Datenbank offline ist. Bei einer Offlinewiederherstellung von Seiten ist die Datenbank offline, während beschädigte Seiten wiederhergestellt werden. Am Ende der Wiederherstellungssequenz wird die Datenbank wieder online geschaltet.  
  
     Onlineseitenwiederherstellung  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition unterstützt Onlineseitenwiederherstellungen, es wird aber die Offlinewiederherstellung verwendet, wenn die Datenbank gerade offline ist. In den meisten Fällen kann eine beschädigte Seite wiederhergestellt werden, wenn die Datenbank einschließlich der Dateigruppen, für die eine Seite wiederhergestellt wird, online bleibt. Wenn die primäre Dateigruppe online ist, selbst wenn eine oder mehrere der sekundären Dateigruppen offline sind, werden Seitenwiederherstellungen in der Regel online durchgeführt. In Einzelfällen ist für beschädigte Seiten jedoch eine Offlinewiederherstellung erforderlich. Beispielsweise können Schäden an bestimmten, wichtigen Seiten dazu führen, dass die Datenbank nicht gestartet wird.  
  
    > [!WARNING]  
    >  Wenn auf beschädigten Seiten wichtige Datenbankmetadaten gespeichert sind, schlagen erforderliche Updates der Metadaten während einer Onlineseitenwiederherstellung möglicherweise fehl. In diesem Fall können Sie eine Offlineseitenwiederherstellung durchführen, Sie müssen jedoch zuerst eine [Protokollfragmentsicherung](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) erstellen (indem Sie das Transaktionsprotokoll mithilfe von RESTORE WITH NORECOVERY sichern).  
  
-   Bei der Seitenwiederherstellung werden die verbesserten Fehlerberichts- und Nachverfolgungsfunktionen auf Seitenebene (einschließlich Seitenprüfsummen) verwendet. Seiten, die aufgrund der Prüfsumme beschädigt sein müssen oder für die ein unterbrochener Schreibvorgang festgestellt wurde, *beschädigte Seiten*, können durch einen Seitenwiederherstellungsvorgang wiederhergestellt werden. Es werden nur explizit angegebene Seiten wiederhergestellt. Jede angegebene Seite wird durch die Kopie dieser Seite aus der angegebenen Datensicherung ersetzt.  
  
     Wenn Sie die nachfolgenden Protokollsicherungen wiederherstellen, werden diese nur auf Datenbankdateien angewendet, die mindestens eine Seite enthalten, die wiederhergestellt wird. Es muss eine ununterbrochene Kette von Protokollsicherungen auf die letzte vollständige oder differenzielle Wiederherstellung angewendet werden, um die Dateigruppe, in der die Seite enthalten ist, auf den Stand der aktuellen Protokolldatei zu bringen. Wie bei der Dateiwiederherstellung wird die Rollforwardgruppe auch bei der Seitenwiederherstellung durch einen einzelnen Protokollwiederholungsschritt weitergegeben. Damit die Seitenwiederherstellung erfolgreich ist, müssen die wiederhergestellten Seiten zu einem Status wiederhergestellt werden, der mit der Datenbank konsistent ist.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Ist die wiederherzustellende Datenbank nicht vorhanden, muss der Benutzer über CREATE DATABASE-Berechtigungen verfügen, um RESTORE ausführen zu können. Ist die Datenbank vorhanden, werden RESTORE-Berechtigungen standardmäßig den Mitgliedern der festen Serverrollen **sysadmin** und **dbcreator** sowie dem Besitzer (**dbo**) der Datenbank erteilt (für die Option FROM DATABASE_SNAPSHOT ist die Datenbank immer vorhanden).  
  
 RESTORE-Berechtigungen werden Rollen erteilt, in denen Mitgliedsinformationen immer für den Server verfügbar sind. Da die Mitgliedschaft in einer festen Datenbankrolle nur geprüft werden kann, wenn die Datenbank unbeschädigt ist und auf sie zugegriffen werden kann, was beim Ausführen von RESTORE nicht immer der Fall ist, verfügen Mitglieder der festen Datenbankrolle **db_owner** nicht über RESTORE-Berechtigungen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Ab [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]unterstützt [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Seitenwiederherstellungen.  
  
#### <a name="to-restore-pages"></a>So stellen Sie Seiten wieder her  
  
1.  Stellen Sie eine Verbindung mit der entsprechenden Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und klicken Sie im Objekt-Explorer auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**. Wählen Sie je nach Datenbank entweder eine Benutzerdatenbank aus, oder erweitern Sie **Systemdatenbanken**, und wählen Sie eine Systemdatenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, zeigen Sie auf **Aufgaben**, zeigen Sie auf **Wiederherstellen**, und klicken Sie anschließend auf **Seite**. Daraufhin wird das Dialogfeld **Seite wiederherstellen** geöffnet.  
  
     **Wiederherstellen**  
     Über diesen Abschnitt führen Sie die gleiche Funktion wie mit **Wiederherstellen in** unter [Datenbank wiederherstellen (Seite „Allgemein“)](../../relational-databases/backup-restore/restore-database-general-page.md)aus.  
  
     **Datenbank**  
     Gibt die Datenbank an, die wiederhergestellt werden soll. Sie können eine neue Datenbank eingeben oder eine vorhandene Datenbank aus der Dropdownliste auswählen. Die Liste umfasst alle Datenbanken auf dem Server, mit Ausnahme der **master** -Datenbank und der **tempdb**-Datenbank.  
  
    > [!WARNING]  
    >  Verwenden Sie die [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) -Anweisung, um eine kennwortgeschützte Sicherung wiederherzustellen.  
  
     **Sicherung des Protokollfragments**  
     Geben Sie unter **Sicherungsmedium** den Namen der Datei ein, in der die Sicherung des Protokollfragments für die Datenbank gespeichert werden soll, oder wählen Sie diesen aus.  
  
     **Sicherungssätze**  
     Dieser Abschnitt zeigt die an der Wiederherstellung beteiligten Sicherungssätze an.  
  
    |Header|Werte|  
    |------------|------------|  
    |**Name**|Name des Sicherungssatzes.|  
    |**Komponente**|Die gesicherte Komponente: **Datenbank**, **Datei** oder **\<leer>** (bei Transaktionsprotokollen).|  
    |**Typ**|Der Typ der ausgeführten Sicherung: **Vollständig**, **Differenziell**oder **Transaktionsprotokoll**.|  
    |**Server**|Der Name der Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)] s, von der der Sicherungsvorgang ausgeführt wurde.|  
    |**Datenbank**|Name der an der Sicherungsoperation beteiligten Datenbank.|  
    |**Position**|Position des Sicherungssatzes auf dem Volume.|  
    |**Erste LSN**|Die Protokollfolgenummer (Log Sequence Number, LSN) der ersten Transaktion im Sicherungssatz. Bei Dateisicherungen leer.|  
    |**Erste LSN**|Die Protokollfolgenummer (Log Sequence Number, LSN) der letzten Transaktion im Sicherungssatz. Bei Dateisicherungen leer.|  
    |**Prüfpunkt-LSN**|Protokollsequenznummer (LSN) des letzten Prüfpunkts zum Zeitpunkt der Erstellung der Sicherung.|  
    |**Vollständige LSN**|Die Protokollfolgenummer (Log Sequence Number, LSN) der neuesten vollständigen Datenbanksicherung.|  
    |**Startdatum**|Datum und Uhrzeit des Sicherungsbeginns, entsprechend den Ländereinstellungen des Clients.|  
    |**Beendigungsdatum**|Datum und Uhrzeit des Endes des Sicherungsvorgangs, entsprechend den Ländereinstellungen des Clients.|  
    |**Größe**|Größe des Sicherungssatzes in Byte.|  
    |**Benutzername**|Name des Benutzers, der den Sicherungsvorgang ausgeführt hat.|  
    |**Ablauf**|Datum und Uhrzeit des Zeitpunkts, an dem der Sicherungssatz verfällt.|  
  
     Klicken Sie auf **Überprüfen** , um die Integrität der Sicherungsdateien zu überprüfen, die zum Ausführen der Seitenwiederherstellung benötigt werden.  
  
4.  Klicken Sie auf **Datenbankseiten prüfen** , um beschädigte Seiten zu identifizieren, dabei muss das Kontrollkästchen **Datenbank**aktiviert sein. Dieser Vorgang dauert lange.  
  
    > [!WARNING]  
    >  Klicken Sie auf **Hinzufügen** , und geben Sie die **Datei-ID** und **die Seiten-ID** der Seiten ein, die wiederhergestellt werden sollen, um bestimmte Seiten wiederherzustellen, die nicht beschädigt sind.  
  
5.  Das Seitenraster wird verwendet, um die wiederherzustellenden Seiten zu identifizieren. Zu Beginn wird dieses Raster von der Systemtabelle [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) aufgefüllt. Um Seiten aus dem Raster hinzuzufügen oder zu entfernen, klicken Sie auf **Hinzufügen** bzw. auf **Entfernen**. Weitere Informationen finden Sie unter [Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)wiederhergestellt werden.  
  
6.  Im Raster **Sicherungssätze** sind die Sicherungssätze im Standardwiederherstellungsplan aufgeführt. Klicken Sie optional auf **Überprüfen** , um zu überprüfen, dass die Sicherungen lesbar die Sicherungssätze vollständig sind, ohne sie wiederherzustellen. Weitere Informationen finden Sie unter [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
     **Seiten**  
  
7.  Um die im Seitenraster aufgeführten Seiten wiederherzustellen, klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Zum Angeben einer Seite in einer RESTORE DATABASE-Anweisung benötigen Sie die Datei-ID der Datei, die die Seite enthält, und die Seiten-ID der Seite. Die erforderliche Syntax lautet wie folgt:  
  
 `RESTORE DATABASE <database_name>`  
  
 `PAGE = '<file: page> [ ,... n ] ' [ ,... n ]`  
  
 `FROM <backup_device> [ ,... n ]`  
  
 `WITH NORECOVERY`  
  
 Weitere Informationen zu den in der Option PAGE verwendeten Parametern finden Sie unter [RESTORE-Argumente &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md). Weitere Informationen zur RESTORE DATABASE-Syntax finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
#### <a name="to-restore-pages"></a>So stellen Sie Seiten wieder her  
  
1.  Rufen Sie die Seiten-IDs der wiederherzustellenden beschädigten Seiten ab. Bei Prüfsummenfehlern oder einem unterbrochenen Schreibvorgang wird die Seiten-ID zurückgegeben, sodass die zum Angeben der Seiten benötigten Informationen zur Verfügung stehen. Sie können die Seiten-ID einer beschädigten Seite mithilfe der folgenden Quellen ermitteln:  
  
    |Quelle der Seiten-ID|Thema|  
    |-----------------------|-----------|  
    |**msdb..suspect_pages**|[Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)|  
    |Fehlerprotokoll|[Anzeigen des SQL Server-Fehlerprotokolls &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)|  
    |Ereignisverfolgungen|[Überwachen und Reagieren auf Ereignisse](http://msdn.microsoft.com/library/f7fbe155-5b68-4777-bc71-a47637471f32)|  
    |DBCC|[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)|  
    |WMI-Anbieter|[Konzepte des WMI-Anbieters für Serverereignisse](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)|  
  
2.  Beginnen Sie die Seitenwiederherstellung mit einer vollständigen Datenbanksicherung, einer Dateisicherung oder einer Dateigruppensicherung, die die Seite enthält. Listen Sie die Seiten-IDs der wiederherzustellenden Seiten mit der PAGE-Klausel der RESTORE DATABASE-Anweisung auf.  
  
3.  Wenden Sie die aktuellsten differenziellen Sicherungen an.  
  
4.  Wenden Sie die nachfolgenden Protokollsicherungen an.  
  
5.  Erstellen Sie eine neue Protokollsicherung der Datenbank, die die letzte LSN der wiederhergestellten Seiten enthält, d. h. den Zeitpunkt, an dem die zuletzt wiederhergestellte Seite offline geschaltet wurde. Die letzte LSN, die im Rahmen der ersten Wiederherstellung innerhalb der Sequenz festgelegt wird, ist die Wiederholungsziel-LSN. Das Onlinerollforward der Datei, die die Seite enthält, kann an der Wiederholungsziel-LSN anhalten. Die aktuelle Wiederholungsziel-LSN einer Datei entnehmen Sie der **redo_target_lsn**-Spalte von **sys.master_files**. Weitere Informationen finden Sie unter [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md).  
  
6.  Stellen Sie die neue Protokollsicherung wieder her. Sobald diese neue Protokollsicherung angewendet wird, ist die Seitenwiederherstellung abgeschlossen, und die Seiten können verwendet werden.  
  
    > [!NOTE]  
    >  Diese Sequenz erfolgt analog zur Dateiwiederherstellungssequenz. Seiten- und Dateiwiederherstellungen können beide als Bestandteil derselben Sequenz ausgeführt werden.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 Im folgenden Beispiel werden vier beschädigte Seiten der Datei `B` mit `NORECOVERY`wiederhergestellt. Anschließend werden zwei Protokollsicherungen mit `NORECOVERY`angewendet, gefolgt von der Sicherung des Protokollfragments, die mit `RECOVERY`wiederhergestellt wird. Im folgenden Beispiel wird eine Onlinewiederherstellung ausgeführt. In diesem Beispiel lautet die Datei-ID der Datei `B` : `1`. Die Seiten-IDs der beschädigten Seiten lauten `57`, `202`, `916`und `1016`.  
  
```tsql  
RESTORE DATABASE <database> PAGE='1:57, 1:202, 1:916, 1:1016'  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;   
BACKUP LOG <database> TO <new_log_backup>;   
RESTORE LOG <database> FROM <new_log_backup> WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)   
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
