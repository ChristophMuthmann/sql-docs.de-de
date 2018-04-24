---
title: Upgrade der Volltextsuche | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], installing
- migrating full-text indexes [SQL Server]
- upgrading Full-Text Search
- installing Full-Text Search
- full-text search [SQL Server], upgrading
ms.assetid: 2fee4691-f2b5-472f-8ccc-fa625b654520
caps.latest.revision: 106
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f0215117505c5873fdaeda174de3e50e8c22a610
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="upgrade-full-text-search"></a>Upgrade der Volltextsuche
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Das Aktualisieren der Volltextsuche auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] erfolgt während des Setups und beim Anfügen, Wiederherstellen und Kopieren von Datenbankdateien und Volltextkatalogen aus einer älteren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des Assistenten zum Kopieren von Datenbanken.  
  
  
##  <a name="Upgrade_Server"></a> Upgrade einer Serverinstanz  
 Bei einem direkten Upgrade wird eine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] parallel zur alten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert, und die Daten werden migriert. Wenn die Volltextsuche in der alten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert war, wird automatisch eine neue Version der Volltextsuche installiert. Eine parallele Installation bedeutet, dass jede der folgenden Komponenten auf der Instanzebene von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]vorhanden ist.  
  
 Wörtertrennung, Wortstammerkennung und Filter  
 Jede Instanz verwendet ihren eigenen Satz von Wörtertrennung, Wortstammerkennung und Filtern, anstatt auf die Betriebssystemversion dieser Komponenten zurückzugreifen. Diese Komponenten sind auf Instanzebene einfacher zu registrieren und zu konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) und [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
 Filterdaemonhost  
 Bei Volltext-Filterdaemonhosts handelt es sich um Prozesse, die erweiterbare externe Komponenten für Indizierung und Abfragen wie Wörtertrennung, Wortstammerkennung und Filter auf sichere Weise laden und ausführen, ohne die Integrität des Volltextmoduls zu gefährden. Eine Serverinstanz verwendet einen Multithreadprozess für alle Multithreadfilter und einen Singlethreadprozess für alle Filter mit einem einzigen Thread.  
  
> [!NOTE]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Mit wurde ein Dienstkonto für den FDHOST-Startdienst (MSSQLFDLauncher) eingeführt. Dieser Dienst gibt die Dienstkontoinformationen an die Filterdaemonhost-Prozesse einer bestimmten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]weiter. Informationen zum Festlegen des Dienstkontos finden Sie unter [Festlegen des Dienstkontos für das Startprogramm des Volltextfilterdaemons](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md).  
  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]befindet sich jeder Volltextindex in einem Volltextkatalog, der einer Dateigruppe angehört, über einen physischen Pfad verfügt und als Datenbankdatei behandelt wird. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und späteren Versionen ist ein Volltextkatalog ein logisches oder virtuelles Objekt, das eine Gruppe von Volltextindizes enthält. Deshalb wird ein neuer Volltextkatalog nicht als Datenbankdatei mit einem physischen Pfad behandelt. Wenn jedoch ein Volltextkatalog aktualisiert wird, der Datendateien enthält, wird auf demselben Datenträger jeweils eine neue Dateigruppe erstellt. Auf diese Weise wird nach dem Upgrade das alte Datenträger-E/A-Verhalten beibehalten. Jeder Volltextindex aus diesem Katalog wird in die neue Dateigruppe eingefügt, wenn der Stammpfad vorhanden ist. Falls der alte Volltextkatalogpfad ungültig ist, wird beim Upgrade der Volltextindex in derselben Dateigruppe wie die Basistabelle bzw. bei einer partitionierten Tabelle in der primären Dateigruppe beibehalten.  
  
  
##  <a name="FT_Upgrade_Options"></a> Volltextupgrade-Optionen  
 Beim Aktualisieren einer Serverinstanz auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie auf der Benutzeroberfläche eine der folgenden Volltextupgrade-Optionen wählen.  
  
**Importieren**  
 Volltextkataloge werden importiert. Normalerweise ist der Import bedeutend schneller als eine Neuerstellung. Wenn Sie zum Beispiel nur eine CPU verwenden, läuft ein Import etwa zehnmal schneller ab als eine Neuerstellung. Ein importierter Volltextkatalog verwendet jedoch nicht die neuen mit der letzten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installierten Wörtertrennungen. Volltextkataloge müssen neu erstellt werden, um die Konsistenz in Abfrageergebnissen sicherzustellen.  
  
> [!NOTE]  
>  Sie können die Neuerstellung im Multithreadmodus ausführen. Wenn mehr als 10 CPUs verfügbar sind, ist die Neuerstellung ggf. schneller als der Import, falls dabei alle CPUs genutzt werden können.  
  
 Wenn ein Volltextkatalog nicht verfügbar ist, werden die zugehörigen Volltextindizes neu erstellt. Diese Option ist nur für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbanken verfügbar.  
  
 Informationen zu den Auswirkungen eines Imports von Volltextindizes finden Sie unter "Überlegungen beim Auswählen einer Volltextupgrade-Option" weiter unten in diesem Thema.  
  
 **Neu erstellen**  
 Volltextkataloge werden mithilfe der neuen und verbesserten Worttrennmodule neu erstellt. Das Neuerstellen von Indizes kann einige Zeit dauern, und nach dem Upgrade ist ggf. eine beträchtliche Menge an CPU-Leistung und Arbeitsspeicherkapazität erforderlich.  
  
 **Zurücksetzen**  
 Volltextkataloge werden zurückgesetzt. Beim Aktualisieren von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]werden Volltextkatalogdateien entfernt. Die Metadaten für die Volltextkataloge und die Volltextindizes bleiben jedoch erhalten. Nach der Upgrade wird die Änderungsnachverfolgung für alle Volltextindizes deaktiviert, und Durchforstungen werden nicht automatisch gestartet. Der Katalog bleibt leer, bis Sie ihn nach Beendigung des Upgrades manuell vollständig auffüllen.  
  
##  <a name="Choosing_Upgade_Option"></a> Überlegungen beim Auswählen einer Volltextupgrade-Option  
 Beachten Sie beim Auswählen der Aktualisierungsoption Folgendes:  
  
-   Ist die Konsistenz in Abfrageergebnissen erforderlich?  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] installiert neue Wörtertrennungen, die von der Volltextsuche und semantischen Suche verwendet werden. Die Wörtertrennungen werden sowohl bei der Indizierung als auch bei Abfragen verwendet. Wenn Sie die Volltextkataloge nicht neu erstellen, sind die Suchergebnisse möglicherweise inkonsistent. Wenn Sie eine Volltextabfrage senden, die nach einem Ausdruck sucht, der von der Wörtertrennung in einer früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version und der aktuellen Wörtertrennung unterschiedlich getrennt wird, können Dokumente oder Zeilen, in denen der Ausdruck enthalten ist, möglicherweise nicht abgerufen werden. Das liegt daran, dass die indizierten Ausdrücke anhand einer anderen Logik getrennt wurden als der von der Abfrage verwendeten Logik. Die Lösung besteht darin, die Volltextkataloge mit den neuen Wörtertrennungen aufzufüllen (neu zu erstellen), damit das Verhalten bei der Indizierung und bei Abfragen gleich ist. Sie können dafür die Option zur Neuerstellung auswählen oder nach dem Auswählen der Option "Importieren" die Kataloge manuell neu erstellen.  
  
-   Wurden Volltextindizes basierend auf ganzzahligen Volltextschlüsselspalten erstellt?  
  
     Bei der Neuerstellung werden interne Optimierungen durchgeführt, die die Abfrageleistung des aktualisierten Volltextindex in einigen Fällen verbessern. Mit der Neuerstellung erzielen Sie nach dem Upgrade besonders dann eine optimale Leistung der Volltextabfragen, wenn Sie Volltextkataloge mit Volltextindizes verwenden, bei denen die Volltextschlüsselspalte der Basistabelle ein integer-Datentyp ist. In diesem Fall ist es sehr zu empfehlen, die Option **Neu erstellen** zu verwenden.  
  
    > [!NOTE]  
    >  Für die Volltextindizes in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ist es ratsam, dass es sich bei der Spalte, die als Volltextschlüssel dient, um einen ganzzahligen Datentyp handelt. Weitere Informationen finden Sie unter [Verbessern der Leistung von Volltextindizes](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md).  
  
-   Worauf liegt beim Herstellen der Onlineverfügbarkeit der Serverinstanz die Priorität?  
  
     Das Importieren bzw. das Neuerstellen während eines Upgrades belegt viele CPU-Ressourcen. Dies führt zu Verzögerungen beim Aktualisieren und Herstellen der Onlineverfügbarkeit des Rests der Serverinstanz. Wenn die schnellstmögliche Onlineverfügbarkeit der Serverinstanz wichtig und das manuelle Auffüllen nach dem Upgrade akzeptabel ist, eignet sich die Option **Zurücksetzen** .  
  
## <a name="ensure-consistent-query-results-after-importing-a-full-text-index"></a>Sicherstellen von konsistenten Abfrageergebnissen nach dem Importieren eines Volltextindexes  
 Wenn beim Upgrade einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ein Volltextkatalog importiert wurde, kann es in einigen Fällen zu Konflikten zwischen der Abfrage und dem Inhalt des Volltextindexes kommen, weil zwischen den alten und neuen Wörtertrennungen Unterschiede bestehen können. Wählen Sie in diesem Fall eine der folgenden Optionen aus, um eine vollständige Übereinstimmung zwischen Abfragen und dem Inhalt des Volltextindexes sicherzustellen:  
  
-   Erstellen Sie den Volltextkatalog neu, der den Volltextindex enthält ([ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)*catalog_name* REBUILD)  
  
-   Geben Sie eine FULL POPULATION für den Volltextindex aus ([ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ON *table_name* START FULL POPULATION).  
  
 Weitere Informationen zur Wörtertrennung finden Sie unter [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
## <a name="upgrade-noise-word-files-to-stoplists"></a>Aktualisieren von Füllwortdateien auf Stoplisten  
Wenn eine Datenbank von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auf [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]aktualisiert wird, werden die Füllwortdateien nicht mehr verwendet. Die alten Füllwortdateien werden jedoch im Ordner "FTDATA\FTNoiseThesaurusBak" gespeichert, und Sie können sie später beim Aktualisieren oder Erstellen der entsprechenden [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Stopplisten verwenden.  
  
 Nach dem Upgrade von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]:  
  
-   Wenn Sie in Ihrer Installation von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]keine Füllwortdateien hinzugefügt, geändert oder gelöscht haben, dürften die Systemstopplisten Ihren Anforderungen entsprechen.  
  
-   Wenn die Füllwortdateien in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]geändert wurden, gehen diese Änderungen während des Upgrades verloren. Wenn Sie die Updates erneut erstellen möchten, müssen Sie diese Änderungen in der entsprechenden [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-Stoppliste manuell neu erstellen. Weitere Informationen finden Sie unter [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md).  
  
-   Wenn Sie auf die Volltextindizes keine Stoppwörter anwenden möchten (wenn Sie z. B. die Füllwortdateien in der [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Installation gelöscht haben), müssen Sie die Stopliste für jeden aktualisierten Volltextindex deaktivieren. Führen Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung aus ( *Datenbank* wird durch den Namen der aktualisierten Datenbank und *Tabelle* durch den Namen der *Tabelle*ersetzt):  
  
    ```  
    Use database;   
    ALTER FULLTEXT INDEX ON table  
       SET STOPLIST OFF;  
    GO  
    ```  
  
     Die STOPLIST OFF-Klausel entfernt die Stoppwortfilterung und löst eine Auffüllung der Tabelle aus, ohne Wörter zu filtern, die als Füllwörter betrachtet werden.  
  
## <a name="backup-and-imported-full-text-catalogs"></a>Sichern und Importieren von Volltextkatalogen  
 Für während des Upgrades neu erstellte oder zurückgesetzte Volltextkataloge (oder für neue Volltextkataloge) ist der Volltextkatalog ein logisches Konzept und nicht in einer Dateigruppe enthalten. Um in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]einen Volltextkatalog zu sichern, müssen Sie daher jede Dateigruppe identifizieren, die einen Volltextindex des Katalogs enthält, und diese einzeln sichern. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von Volltextkatalogen und Indizes](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md).  
  
 Bei Volltextkatalogen, die aus [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]importiert werden, ist der Volltextkatalog immer noch eine Datenbankdatei in einer eigenen Dateigruppe. Der Sicherungsprozess von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] für Volltextkataloge gilt weiterhin, jedoch mit der Ausnahme, dass der MSFTESQL-Dienst in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]nicht vorhanden ist. Weitere Informationen zum [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Prozess finden Sie unter [Sichern und Wiederherstellen von Volltextkatalogen](http://go.microsoft.com/fwlink/?LinkId=209154) in der SQL Server 2005-Onlinedokumentation.  
  
##  <a name="Upgrade_Db"></a> Migrieren von Volltextindizes beim Aktualisieren einer Datenbank auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Datenbankdateien und Volltextkataloge einer vorherigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können durch Anfügen, Wiederherstellen oder mithilfe des Assistenten zum Kopieren von Datenbanken auf eine vorhandene [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Serverinstanz aktualisiert werden. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Volltextindizes werden, falls vorhanden, importiert, zurückgesetzt oder neu erstellt. Die Servereigenschaft **upgrade_option** steuert, welche Volltextupgrade-Option die Serverinstanz während dieser Datenbankupgrades verwendet.  
  
 Nachdem Sie eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]angehängt, wiederhergestellt oder kopiert haben, ist die Datenbank sofort verfügbar und wird automatisch aktualisiert. Je nach Menge der indizierten Daten kann der Importvorgang mehrere Stunden dauern; die Neuerstellung sogar bis zu zehnmal länger. Wenn die Upgradeoption auf "Importieren" festgelegt und kein Volltextkatalog verfügbar ist, werden die zugehörigen Volltextindizes neu erstellt.  
  
 **So ändern Sie das Verhalten des Volltextupgrades für eine Serverinstanz**  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]: Verwenden Sie die **upgrade\_option**-Aktion von [sp\_fulltext\_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **:** Verwenden Sie im Dialogfeld **Servereigenschaften** die **Volltextupgrade-Option** . Weitere Informationen finden Sie unter [Verwalten und Überwachen der Volltextsuche auf einer Serverinstanz](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
##  <a name="Considerations_for_Restore"></a> Überlegungen zum Wiederherstellen eines [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Volltextkatalogs auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Eine Möglichkeit zum Aktualisieren der Volltextdaten einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] besteht darin, eine vollständige Datenbanksicherung für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]wiederherzustellen.  
  
 Beim Importieren eines [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Volltextkatalogs können Sie die Datenbank und die Katalogdatei sichern und wiederherstellen. Das Verhalten entspricht dem Verhalten in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]:  
  
-   Die vollständige Datenbanksicherung enthält den Volltextkatalog. Verwenden Sie zum Verweisen auf den Volltextkatalog seinen [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Dateinamen: sysft_+*catalog_name*.  
  
-   Wenn der Volltextkatalog offline ist, kann die Sicherung nicht ausgeführt werden.  
  
 Weitere Informationen zur Sicherung und Wiederherstellung von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Volltextkatalogen finden Sie unter [Sichern und Wiederherstellen von Volltextkatalogen](http://go.microsoft.com/fwlink/?LinkId=121052) und [Dateisicherung und -wiederherstellung und Volltextkataloge](http://go.microsoft.com/fwlink/?LinkId=121053)in der [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Onlinedokumentation.  
  
 Wenn die Datenbank für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]wiederhergestellt wird, wird für den Volltextkatalog eine neue Datenbankdatei erstellt. Der Standardname dieser Datei lautet ftrow_*catalog-name*.ndf. Wenn Sie für *catalog-name* (Katalogname) zum Beispiel `cat1`verwenden, lautet der Standardname der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Datenbankdatei `ftrow_cat1.ndf`. Wenn der Standardname im Zielverzeichnis jedoch bereits verwendet wird, erhält die neue Datenbankdatei den Namen `ftrow_`*catalog-name*`{`*GUID*`}.ndf`, wobei *GUID* für den eindeutigen Bezeichner (Globally Unique Identifier, GUID) der neuen Datei steht.  
  
 Nach dem Importieren der Kataloge werden die Dateien **sys.database_files** und **sys.master_file**aktualisiert, um die Katalogeinträge zu entfernen, und die Spalte **path** in der Datei **sys.fulltext_catalogs** wird auf NULL festgelegt.  
  
 **So sichern Sie eine Datenbank**  
  
-   [Vollständige Datenbanksicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
-   [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md) (nur vollständiges Wiederherstellungsmodell)  
  
 **So stellen Sie eine Datenbanksicherung wieder her**  
  
-   [Vollständige Datenbankwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [Vollständige Datenbankwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die MOVE-Klausel in der [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) -Anweisung verwendet, um eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank mit dem Namen `ftdb1`wiederherzustellen. Die [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbankdateien, -Protokolldateien und -Katalogdateien werden wie folgt an neue Speicherorte auf der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Serverinstanz verschoben:  
  
-   Die Datenbankdatei `ftdb1.mdf`wird an den Speicherort `C:\Program Files\Microsoft SQL Server\MSSQL.1MSSQL13.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf`verschoben.  
  
-   Die Protokolldatei `ftdb1_log.ldf`wird in ein Protokollverzeichnis auf Ihrem Protokolllaufwerk verschoben: *Protokolllaufwerk*`:\`*Protokollverzeichnis*`\ftdb1_log.ldf`.  
  
-   Die Katalogdateien, die dem Katalog `sysft_cat90` entsprechen, werden in `C:\temp`verschoben. Nachdem die Volltextindizes importiert wurden, werden diese automatisch in eine Datenbankdatei mit dem Namen C:\ftrow_sysft_cat90.ndf eingefügt, und das Verzeichnis C:\temp wird gelöscht.  
  
```  
RESTORE DATABASE [ftdb1] FROM  DISK = N'C:\temp\ftdb1.bak' WITH  FILE = 1,  
   MOVE N'ftdb1' TO N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf',  
    MOVE N'ftdb1_log' TO N'log_drive:\log_directory\ftdb1_log.ldf',  
    MOVE N'sysft_cat90' TO N'C:\temp';  
```  
  
##  <a name="Attaching_2005_ft_catalogs"></a> Anfügen einer SQL Server 2005-Datenbank an [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen ist ein Volltextkatalog ein logisches Konzept, bei dem eine Gruppe von Volltextindizes verwendet wird. Ein Volltextkatalog ist ein virtuelles Objekt und gehört keiner Dateigruppe an. Wenn Sie jedoch eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank mit Volltextkatalogdateien an eine [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Serverinstanz anfügen, werden die Katalogdateien von ihrem vorherigen Speicherort aus zusammen mit den anderen Datenbankdateien angefügt. Dies entspricht der Vorgehensweise für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Der Status der einzelnen angefügten Volltextkataloge von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] entspricht dem Status beim Trennen der Datenbank von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Wenn beim Trennvorgang eine Auffüllung des Volltextindex unterbrochen wurde, wird die Auffüllung in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]wieder aufgenommen, und der Volltextindex ist für die Volltextsuche verfügbar.  
  
 Wenn [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] keine Volltextkatalogdatei finden kann oder wenn die Volltextdatei während des Anfügens verschoben und ein neuer Speicherort angegeben wurde, ist das Verhalten von der gewählten Volltextupgrade-Option abhängig. Wenn die Volltextupgrade-Option **Importieren** oder **Neu erstellen**lautet, wird der angefügte Volltextkatalog neu erstellt. Wenn die Volltextupgrade-Option **Zurücksetzen** lautet, wird der angefügte Volltextkatalog zurückgesetzt.  
  
 Weitere Informationen zum Trennen oder Anfügen einer Datenbank finden Sie unter [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md), [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md), [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md), und [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit der Volltextsuche](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
  
