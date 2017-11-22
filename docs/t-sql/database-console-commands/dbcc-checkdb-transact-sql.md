---
title: DBCC CHECKDB (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKDB_TSQL
- DBCC_CHECKDB_TSQL
- DBCC CHECKDB
- CHECKDB
dev_langs: TSQL
helpviewer_keywords:
- CHECKDB [DBCC statement]
- database objects [SQL Server], checking
- counting pages
- per-index row counts
- per-table row counts
- DBCC CHECKDB statement
- per-table page counts
- allocation checks
- integrity [SQL Server], database objects
- per-index page counts
- counting rows
- table integrity checks [SQL Server]
- row count accuracy [SQL Server]
- negative counts
- checking database objects
- page count accuracy [SQL Server]
ms.assetid: 2c506167-0b69-49f7-9282-241e411910df
caps.latest.revision: "144"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 67d2d6b3b6ad42e444f8f7f2908f2327c4844933
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-checkdb-transact-sql"></a>DBCC CHECKDB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Überprüft die logische und physische Integrität aller Objekte in der angegebenen Datenbank durch Ausführen der folgenden Vorgänge:    
    
> **Hinweis:** DBCC CHECKDB wird für Datenbanken mit speicheroptimierten Tabellen unterstützt jedoch die Überprüfung erfolgt nur für datenträgerbasierte Tabellen. Im Rahmen der Sicherung und Wiederherstellung von Datenbanken wird die CHECKSUM-Überprüfung jedoch für Dateien in speicheroptimierten Dateigruppen ausgeführt.    
>     
>  Da DBCC-Reparaturoptionen sind nicht für speicheroptimierte Tabellen verfügbar. Sie müssen die Datenbanken regelmäßig sichern und die Sicherungen testen. Wenn bei einer speicheroptimierten Tabelle Datenintegritätsprobleme auftreten, müssen Sie die Tabelle von der letzten bekannten fehlerfreien Sicherung wiederherstellen.    
    
-   Führt [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md) für die Datenbank.    
    
-   Führt [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md) für jede Tabelle und Sicht in der Datenbank.    
    
-   Führt [DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md) für die Datenbank.    
    
-   Die Überprüfung des Inhalts jeder indizierten Sicht in der Datenbank.    
    
-   Überprüft auf Konsistenz zwischen Tabelle Metadaten und die Datei den Dateisystemverzeichnissen und-Dateien beim Speichern von **varbinary(max)** Daten im Dateisystem mithilfe von FILESTREAM.    
    
-   Die Überprüfung der [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Daten in der Datenbank.    
    
 Das bedeutet, dass die Befehle DBCC CHECKALLOC, DBCC CHECKTABLE oder DBCC CHECKCATALOG nicht separat von DBCC CHECKDB ausgeführt werden müssen. Ausführlichere Informationen zu den von diesen Befehlen ausgeführten Überprüfungen finden Sie in den Beschreibungen dieser Befehle.    
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Syntax    
    
```    
    
DBCC CHECKDB     
    [ ( database_name | database_id | 0    
        [ , NOINDEX     
        | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]    
    ) ]    
    [ WITH     
        {    
            [ ALL_ERRORMSGS ]    
            [ , EXTENDED_LOGICAL_CHECKS ]     
            [ , NO_INFOMSGS ]    
            [ , TABLOCK ]    
            [ , ESTIMATEONLY ]    
            [ , { PHYSICAL_ONLY | DATA_PURITY } ]    
            [ , MAXDOP  = number_of_processors ]    
        }    
    ]    
]    
```    
    
## <a name="arguments"></a>Argumente    
 *Database_name* | *Database_id* | 0  
 Der Name oder die ID der Datenbank, für die Integritätsprüfungen ausgeführt werden. Erfolgt keine Eingabe, oder wird 0 angegeben, wird die aktuelle Datenbank verwendet. Datenbanknamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
    
 NOINDEX  
 Legt fest, dass nicht gruppierte Indizes für Benutzertabellen nicht intensiv überprüft werden. Dadurch wird die Ausführungsdauer insgesamt verkürzt. NOINDEX wirkt sich nicht auf Systemtabellen aus, da Integritätsprüfungen für Systemtabellenindizes immer ausgeführt werden.  
    
 REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 Gibt an, dass DBCC CHECKDB gefundene Fehler behebt. Verwenden Sie die REPAIR-Optionen nur als letzte Möglichkeit. Die angegebene Datenbank muss sich im Einzelbenutzermodus befinden, damit eine der folgenden Reparaturoptionen verwendet werden kann.  
    
 REPAIR_ALLOW_DATA_LOSS  
 Versucht, alle gemeldeten Fehler zu reparieren. Diese Reparaturen können zu Datenverlusten führen.  
    
> [!WARNING]
> - Die REPAIR_ALLOW_DATA_LOSS-Option ist ein unterstütztes Feature, aber er möglicherweise nicht immer die beste Möglichkeit zur um eine Datenbank in einem physisch konsistenten Zustand. 
> – Wenn erfolgreich ist, kann die REPAIR_ALLOW_DATA_LOSS-Option zu Datenverlusten führen. Tatsächlich können dabei mehr Daten verloren gehen als bei einer Wiederherstellung der Datenbank aus der letzten als funktionierend bekannten Sicherung durch den Benutzer. 
>
> - [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt immer eine Wiederherstellung durch den Benutzer aus der letzten als funktionierend bekannten Sicherung als primäre Methode zur Wiederherstellung nach Fehlern, die von DBCC CHECKDB gemeldet wurden. Die REPAIR_ALLOW_DATA_LOSS-Option ist keine Alternative zur Wiederherstellung aus einer als funktionierend bekannten Sicherung. Diese Option ist nur für den Notfall als „letzte Option“ geeignet, wenn die Wiederherstellung aus einer Sicherung nicht möglich ist.    
>     
>  - Für bestimmte Fehler, die nur mithilfe der REPAIR_ALLOW_DATA_LOSS-Option behoben werden können, muss möglicherweise die Zuordnung einer Zeile, Seite oder Reihe von Seiten aufgehoben werden, um die Fehler zu löschen. Daten, deren Zuordnung aufgehoben wurde, sind für den Benutzer nicht mehr verfügbar oder wiederherstellbar, und der genaue Inhalt dieser Daten kann nicht bestimmt werden. Aus diesem Grund ist die referentielle Integrität möglicherweise nicht genau, nachdem die Zuordnung von Zeilen oder Seiten aufgehoben wurde, da Einschränkungen für Fremdschlüssel nicht als Teil dieses Reparaturvorgangs geprüft oder gewartet werden. Der Benutzer muss die referentielle Integrität der Datenbank (mit DBCC CHECKCONSTRAINTS) überprüfen, nachdem er die REPAIR_ALLOW_DATA_LOSS-Option verwendet hat.    
>     
>  - Erstellen Sie vor dem Ausführen der Reparatur physische Kopien der Dateien, die zu dieser Datenbank gehören. Dies schließt die primäre Datendatei (.mdf), beliebige sekundäre Datendateien (.ndf), alle Transaktionsprotokolldateien (.ldf) und andere Container ein, aus denen die Datenbank besteht, einschließlich Volltextkataloge, Datenstromordner, speicheroptimierte Daten usw.    
>     
>  - Erwägen Sie vor dem Ausführen der Reparatur, den Status der Datenbank in den Modus EMERGENCY zu ändern und zu versuchen, so viele Informationen wie möglich aus den kritischen Tabellen zu extrahieren und die Daten zu speichern.    
    
 REPAIR_FAST  
 Wird nur aus Gründen der Abwärtskompatibilität der Syntax beibehalten. Es werden keine Reparaturaktionen ausgeführt.  
    
 REPAIR_REBUILD  
 Führt Reparaturen aus, bei denen kein Datenverlust möglich ist. Dazu können schnelle Reparaturen gehören, wie z. B. das Reparieren fehlender Zeilen in nicht gruppierten Indizes, als auch zeitaufwändigere Reparaturen, wie das Neuerstellen von Indizes.  
 Dieses Argument ist Fehler im Zusammenhang mit FILESTREAM-Daten nicht repariert werden.  
    
> [!IMPORTANT] 
> Da DBCC CHECKDB mit einer der REPAIR-Optionen vollständig protokolliert und wiederherstellbar ist, empfiehlt [!INCLUDE[msCoName](../../includes/msconame-md.md)] immer, dass Benutzer CHECKDB mit REPAIR-Optionen innerhalb einer Transaktion verwenden (BEGIN TRANSACTION vor Ausführung des Befehls ausführen), damit der Benutzer bestätigen kann, dass er die Ergebnisse des Vorgangs akzeptieren möchte. Der Benutzer kann dann COMMIT TRANSACTION ausführen, um alle vom Reparaturvorgang vorgenommenen Arbeiten zu bestätigen. Wenn der Benutzer die Ergebnisse des Vorgangs nicht akzeptieren möchte, kann er eine ROLLBACK TRANSACTION durchführen, um die Auswirkungen der Reparaturvorgänge rückgängig zu machen.    
>     
>  Zum Reparieren von Fehlern empfiehlt sich das Wiederherstellen mithilfe einer Sicherung. Bei Reparaturvorgängen werden keine Einschränkungen berücksichtigt, die möglicherweise in oder zwischen Tabellen vorhanden sind. Wenn die angegebene Tabelle an einer oder mehreren Einschränkungen beteiligt ist, ist es empfehlenswert, nach einem Reparaturvorgang DBCC CHECKCONSTRAINTS auszuführen. Wenn Sie REPAIR verwenden müssen, sollten Sie DBCC CHECKDB ohne Reparaturoption ausführen, um die zu verwendende Reparaturstufe zu ermitteln. Wenn Sie die REPAIR_ALLOW_DATA_LOSS-Ebene verwenden, empfiehlt es sich, die Datenbank vor dem Ausführen von DBCC CHECKDB zu sichern.    
    
 ALL_ERRORMSGS  
 Zeigt alle gemeldeten Fehler für jedes Objekt an. Alle Fehlermeldungen werden standardmäßig angezeigt. Das Angeben oder Weglassen dieser Option hat keine Auswirkungen. Fehlermeldungen werden nach davon ausgenommen sind Meldungen generiert aus der Objekt-ID sortiert [Tempdb-Datenbank](../../relational-databases/databases/tempdb-database.md).  
    
> [!NOTE] 
> In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] werden maximal 1.000 Fehlermeldungen zurückgegeben. Wenn Sie ALL_ERRORMSGS angeben, es wird empfohlen, dass Sie mithilfe den DBCC-Befehl Ausführen der [Hilfsprogramms "Sqlcmd"](../../tools/sqlcmd-utility.md) oder durch die Planung einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentauftrag, um den Befehl auszuführen und die Ausgabe in eine Datei weiterleiten. Mit jeder dieser Methoden kann sichergestellt werden, dass beim einmaligen Ausführen des Befehls alle Fehlermeldugen gemeldet werden.    

 EXTENDED_LOGICAL_CHECKS  
 Wenn der Kompatiblitätsgrad 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) oder höher ist, werden logische Konsistenzprüfungen an einer indizierten Sicht, XML-Indizes und räumliche Indizes (sofern vorhanden) ausgeführt.  
 Weitere Informationen finden Sie unter "Ausführen logischer Konsistenzprüfungen an Indizes" im Abschnitt mit den Hinweisen weiter unten in diesem Thema.  
    
 NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
    
 TABLOCK  
 Bewirkt, dass DBCC CHECKDB Sperren erhält, statt eine interne Datenbankmomentaufnahme zu verwenden. Dies schließt eine kurzfristige exklusive Sperre (X) für die Datenbank ein. Durch TABLOCK wird DBCC CHECKDB schneller in einer stark ausgelasteten Datenbank ausgeführt, allerdings verringert sich während der Ausführung von DBCC CHECKDB die in der Datenbank verfügbare Parallelität.  
    
> [!IMPORTANT] 
> TABLOCK beschränkt die ausgeführten Überprüfungen. DBCC CHECKCATALOG wird nicht für die Datenbank ausgeführt, und [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Daten werden nicht überprüft.
    
 ESTIMATEONLY  
 Zeigt den geschätzten Speicherplatz in Tempdb, die erforderlich ist, um die Ausführung von DBCC CHECKDB mit allen anderen angegebenen Optionen. Die eigentliche Datenbankprüfung wird nicht ausgeführt.  
    
 PHYSICAL_ONLY  
 Begrenzt die Überprüfung der Integrität der physischen Struktur der Seiten- und Datensatzheader und der Zuordnungskonsistenz der Datenbank. Die Überprüfung soll dazu dienen, mit geringem Verwaltungsaufwand eine Überprüfung der physischen Konsistenz der Datenbank vorzunehmen. Dabei können auch zerrissene Seiten, Prüfsummenfehler und häufige Hardwarefehler erkannt werden, die Benutzerdaten gefährden können.  
 Eine vollständige Ausführung von DBCC CHECKDB kann erheblich mehr Zeit in Anspruch nehmen als in früheren Versionen. Dieses Verhalten tritt aus den folgenden Gründen auf:  
 -   Die logischen Überprüfungen sind umfassender.  
 -   Einige der zu überprüfenden zugrunde liegenden Strukturen sind komplexer.  
 -   Es wurden viele neue Überprüfungen eingeführt, um die neuen Funktionen einzuschließen.  
 Daher bewirkt das Verwenden der PHYSICAL_ONLY-Option möglicherweise eine viel kürzere Ausführungszeit von DBCC CHECKDB für große Datenbanken. Sie wird daher für die häufige Verwendung in Produktionssystemen empfohlen. Dennoch ist eine vollständige Ausführung von DBCC CHECKDB in regelmäßigen Abständen empfehlenswert. Die Häufigkeit dieser Ausführungsvorgänge hängt von Faktoren ab, die für einzelne Unternehmen und Produktionsumgebungen spezifisch sind.    
Diese Argment stets NO_INFOMSGS impliziert und ist nicht mit einer der Repair-Optionen zulässig.  
    
> [!WARNING] 
> Bei Angabe von PHYSICAL_ONLY überspringt DBCC CHECKDB alle Prüfungen der FILESTREAM-Daten.
    
 DATA_PURITY  
 Bewirkt, dass DBCC CHECKDB die Datenbank auf Spaltenwerte überprüft, die ungültig sind oder außerhalb des zulässigen Bereichs liegen. DBCC CHECKDB erkennt z. B. Spalten mit Datum und Uhrzeit-Werten, die größer als oder kleiner als der zulässige Bereich für die **"DateTime"** des Datentyps oder **decimal** oder ungefähren numerischen Datentyp Spalten mit Dezimalstellenangabe oder Genauigkeit Werte, die nicht gültig sind.  
 Die Überprüfung der Spaltenwertintegrität ist standardmäßig aktiviert. Die Option DATA_PURITY ist nicht erforderlich. Bei Datenbanken, die von früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert wurden, ist die Spaltenwertprüfung nicht standardmäßig aktiviert, die Aktivierung erfolgt erst, wenn DBCC CHECKDB WITH DATA_PURITY fehlerfrei für die Datenbank ausgeführt wurde. Danach wird die Spaltenwertintegrität standardmäßig von DBCC CHECKDB überprüft. Weitere Informationen zu den möglichen Auswirkungen des Upgrades einer Datenbank von einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie im Abschnitt mit Hinweisen weiter unten in diesem Thema.  
    
> [!WARNING]
> Wenn PHYSICAL_ONLY angegeben ist, wird die Spaltenintegrität nicht überprüft.
    
 Mit dieser Option gemeldete Überprüfungsfehler können nicht mithilfe der DBCC-Reparaturoptionen behoben werden. Informationen zur manuellen Behebung dieser Fehler finden Sie im Knowledge Base-Artikel 923247: [Problembehandlung bei DBCC-Fehler 2570 in SQL Server 2005 und höheren Versionen](http://support.microsoft.com/kb/923247).  
    
 MAXDOP  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
    
 Überschreibt die **Max. Grad an Parallelität** Konfigurationsoption von **Sp_configure** für die Anweisung. Der MAXDOP kann mit Sp_configure konfigurierten Wert überschreiten. Wenn MAXDOP den mit der Ressourcenkontrolle konfigurierten Wert überschreitet die [!INCLUDE[ssDEnoversion](../../includes/ssDEnoversion_md.md)] verwendet den Resource Governor MAXDOP-Wert, in der beschriebenen [ALTER WORKLOAD GROUP](../../t-sql/statements/alter-workload-group-transact-sql.md). Alle semantischen Regeln, die mit der Konfigurationsoption Max. Grad an Parallelität verwendet werden können, stehen beim Verwenden des MAXDOP-Abfragehinweises zur Verfügung. Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
 
> [!WARNING] 
> Wenn MAXDOP festgelegt ist, klicken Sie dann auf SQL Server NULL wählt die Max. Grad an Parallelität verwenden.    

## <a name="remarks"></a>Hinweise    
Deaktivierte Indizes werden von DBCC CHECKDB nicht untersucht. Weitere Informationen zu deaktivierten Indizes finden Sie unter [Deaktivieren von Indizes und Einschränkungen](../../relational-databases/indexes/disable-indexes-and-constraints.md).
Wenn ein benutzerdefinierter Typ als Typ markiert ist, dessen Sortierreihenfolge eine Bytereihenfolge ist, darf es nur eine Serialisierung des benutzerdefinierten Typs geben. Wenn keine konsistente Serialisierung benutzerdefinierter Typen vorhanden ist, deren Sortierreihenfolge eine Bytereihenfolge ist, wird bei der Ausführung von DBCC CHECKDB der Fehler 2537 ausgegeben. Weitere Informationen finden Sie unter [User-Defined Type Anforderungen](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-requirements.md).
Da die [Ressourcendatenbank](../../relational-databases/databases/resource-database.md) geändert werden nur im Einzelbenutzermodus, DBCC CHECKDB Befehl kann nicht direkt darauf ausgeführt werden. Wenn DBCC CHECKDB wird jedoch ausgeführt, für die [master-Datenbank](../../relational-databases/databases/master-database.md), ein zweiter CHECKDB-Befehl wird auch intern auf die Resource-Datenbank ausgeführt. Das bedeutet, dass DBCC CHECKDB möglicherweise zusätzliche Ergebnisse zurückgibt. Der Befehl gibt zusätzliche Resultsets zurück, wenn keine Optionen festgelegt wurden oder wenn entweder die Option PHYSICAL_ONLY oder die Option ESTIMATEONLY festgelegt wurde.
In Versionen von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] vor SP2 wurde beim Ausführen von DBCC CHECKDB der Plancache für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht. Durch das Löschen des Plancaches wird eine Neukompilierung aller späteren Ausführungspläne verursacht, und möglicherweise entsteht plötzlich eine temporäre Verringerung der Abfrageleistung. In SP2 und höher wird beim Ausführen von DBCC CHECKDB der Plancache nicht gelöscht.
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>Ausführen logischer Konsistenzprüfungen an Indizes    
Die logische Konsistenzprüfung an Indizes variiert wie folgt je nach dem Kompatibilitätsgrad der Datenbank:
-   Wenn der Kompatibilitätsgrad 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) oder höher ist:    
-   DBCC CHECKDB führt sowohl physische als auch logische Konsistenzprüfungen für eine einzelne Tabelle und alle nicht gruppierten Indizes aus, sofern nicht NOINDEX angegeben wird. Allerdings werden an XML-Indizes, räumlichen Indizes und indizierten Sichten standardmäßig nur physische Konsistenzprüfungen ausgeführt.
-   Bei Angabe von WITH EXTENDED_LOGICAL_CHECKS werden logische Konsistenzprüfungen an indizierten Sichten, XML-Indizes und räumlichen Indizes (sofern vorhanden) ausgeführt. Standardmäßig werden physische Konsistenzprüfungen vor den logischen Konsistenzprüfungen ausgeführt. Wenn NOINDEX ebenfalls angegeben wird, werden nur die logischen Prüfungen ausgeführt.
    
Diese logischen Konsistenzprüfungen überprüfen die interne Indextabelle des Indexobjekts anhand der Benutzertabelle, auf die verwiesen wird. Zum Auffinden externer Zeilen wird eine interne Abfrage konstruiert, um eine vollständige Schnittmenge der internen Tabellen und der Benutzertabellen zu bilden. Die Ausführung dieser Abfrage kann sich sehr stark auf die Leistung auswirken, und ihr Status kann nicht verfolgt werden. Daher empfiehlt es sich, WITH EXTENDED_LOGICAL_CHECKS nur dann anzugeben, wenn Sie Indexprobleme vermuten, die nicht mit einer physischen Beschädigung in Zusammenhang stehen, oder wenn die Prüfsummen auf Seitenebene deaktiviert wurden und Sie eine Beschädigung der Hardware auf Spaltenebene vermuten.
-   Bei einem gefilterten Index prüft DBCC CHECKDB anhand von Konsistenzprüfungen, ob die Indexeinträge dem Filterprädikat entsprechen.
-   Wenn der Kompatibilitätsgrad 90 oder weniger beträgt, führt DBCC CHECKDB sowohl physische als auch logische Konsistenzprüfungen für eine einzelne Tabelle oder indizierte Sicht und für alle nicht gruppierten Indizes und XML-Indizes aus, sofern nicht NOINDEX angegeben wird. Räumliche Indizes werden nicht unterstützt.  
- Beginnend mit SQL Server 2016, werden zusätzliche Überprüfungen auf persistente berechnete Spalten, UDT-Spalten und gefilterten Indizes nicht standardmäßig auf die aufwändige Ausdruck auswertungen vermeiden ausgeführt. Diese Änderung wird erheblich reduziert die Dauer der CHECKDB für Datenbanken, die diese Objekte enthält. Allerdings die physische konsistenzprüfungen für diese Objekte immer abgeschlossen ist. Nur wenn EXTENDED_LOGICAL_CHECKS-Option angegeben wird die auswertungen von Ausdrücken im Rahmen der Option "EXTENDED_LOGICAL_CHECKS" zusätzlich zu den bereits vorhandenen logischen Überprüfungen (indizierte Sicht, XML-Indizes und räumliche Indizes) ausgeführt werden.   
    
**Um den Kompatibilitätsgrad einer Datenbank zu erhalten.**
-   [Anzeigen oder Ändern des Kompatibilitätsgrads einer Datenbank](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>Interne Datenbankmomentaufnahme    
DBCC CHECKDB verwendet eine interne Datenbankmomentaufnahme für die Transaktionskonsistenz, die für diese Überprüfungen erforderlich ist. Auf diese Weise werden beim Ausführen dieser Befehle Blockierungs- und Parallelitätsprobleme verhindert. Weitere Informationen finden Sie unter [Anzeigen der Größe der Datei mit geringer Dichte einer Datenbank-Momentaufnahme &#40; Transact-SQL &#41; ](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) und den Abschnitt der internen DBCC-Datenbankmomentaufnahme in [DBCC &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-transact-sql.md). Wenn keine Momentaufnahme erstellt werden kann oder TABLOCK angegeben wird, ruft DBCC CHECKDB Sperren ab, um die erforderliche Konsistenz bereitzustellen. In diesem Fall ist für die Durchführung der Zuordnungsprüfungen eine exklusive Datenbanksperre erforderlich, und für die Durchführung der Tabellenprüfungen sind freigegebene Tabellensperren erforderlich.
DBCC CHECKDB schlägt fehl, wenn es mit Master ausgeführt werden soll, wenn eine interne Datenbankmomentaufnahme erstellt werden kann.
Ausführen von DBCC CHECKDB für die Tempdb führt keine Zuordnungs- oder katalogüberprüfungen Überprüfungen und tabellenprüfungen muss freigegebene Tabellensperren um tabellenüberprüfungen auszuführen. Dies liegt daran, dass aus Leistungsgründen keine Datenbankmomentaufnahmen auf tempdb verfügbar sind. Dies bedeutet, dass die erforderliche Transaktionskonsistenz nicht erhalten werden kann.
In Microsoft SQL Server 2012 oder einer früheren Version von SQL Server können Fehlermeldungen auftreten, beim Ausführen von DBCC CHECKDB-Befehls für eine Datenbank, die die befindet sich auf einem ReFS-formatierten Volume befinden. Weitere Informationen finden Sie im Knowledge Base-Artikel 2974455: [DBCC CHECKDB-Verhalten, wenn SQL Server-Datenbank auf einem ReFS-Volume befindet.](https://support.microsoft.com/kb/2974455)    
    
## <a name="checking-and-repairing-filestream-data"></a>Überprüfen und Reparieren von FILESTREAM-Daten    
Wenn FILESTREAM für eine Datenbank und die Tabelle aktiviert ist, können Sie optional speichern **varbinary(max)** binary large Object (BLOBs) im Dateisystem. Wenn Sie DBCC CHECKDB für eine Datenbank verwenden, die BLOBs im Dateisystem speichert, überprüft DBCC die Konsistenz auf Linkebene zwischen dem Dateisystem und der Datenbank.
Wenn eine Tabelle enthält beispielsweise eine **varbinary(max)** Spalte, die das FILESTREAM-Attribut, DBCC CHECKDB verwendet wird, eine 1: 1-Zuordnung zwischen den Dateisystemverzeichnissen und Dateien und Tabellenzeilen, Spalten und Spalte besteht überprüfen Werte. DBCC CHECKDB kann Beschädigungen reparieren, wenn Sie die REPAIR_ALLOW_DATA_LOSS-Option angeben. Um FILESTREAM-Beschädigung zu reparieren, löscht DBCC alle Tabellenzeilen, in denen Dateisystemdaten fehlen.
    
## <a name="best-practices"></a>Bewährte Methoden    
Es empfiehlt sich, die Option PHYSICAL_ONLY für die häufige Verwendung in Produktionssystemen zu verwenden. Das Verwenden von PHYSICAL_ONLY kann die Ausführungszeit von DBCC CHECKDB für große Datenbanken erheblich verkürzen. Darüber hinaus sollte in regelmäßigen Abständen DBCC CHECKDB ohne Optionen ausgeführt werden. Die Häufigkeit der Ausführung hängt von den jeweiligen Unternehmen und Produktionsumgebungen ab.
    
## <a name="checking-objects-in-parallel"></a>Paralleles Überprüfen von Objekten    
Standardmäßig führt DBCC CHECKDB eine parallele Überprüfung von Objekten aus. Der Grad der Parallelität wird automatisch durch den Abfrageprozessor bestimmt. Der Höchstgrad für die Parallelität wird genauso konfiguriert wie parallele Abfragen. Um die maximale Anzahl an Prozessoren zur Verfügung, für die DBCC-Überprüfungen einzuschränken, verwenden Sie [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md). Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Die parallele Überprüfung kann mithilfe des Ablaufverfolgungsflags 2528 deaktiviert werden. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
    
> [!NOTE]
> Diese Funktion ist nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Weitere Informationen finden Sie unter parallele konsistenzprüfung im Abschnitt RDBMS-Verwaltbarkeit [von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).    
    
## <a name="understanding-dbcc-error-messages"></a>Grundlegendes zu DBCC-Fehlermeldungen    
Nach der Fertigstellung des Befehls DBCC CHECKDB wird eine Meldung in das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll geschrieben. Falls der DBCC-Befehl erfolgreich ausgeführt wird, gibt die Meldung den Erfolg und die Dauer der Ausführung an. Falls der DBCC-Befehl vor Abschluss der Überprüfung aufgrund eines Fehlers beendet wird, gibt die Meldung die Beendigung des Befehls, einen Statuswert sowie die Dauer der Ausführung an. In der folgenden Tabelle sind die Statuswerte aufgeführt und beschrieben, die in der Meldung enthalten sein können.
    
|Status|Description|    
|-----------|-----------------|    
|0|Fehlernummer 8930 wurde ausgelöst. Dies weist auf eine Beschädigung der Metadaten hin, die zur Beendigung des DBCC-Befehls geführt hat.|    
|1|Fehlernummer 8967 wurde ausgelöst. Ein interner DBCC-Fehler ist aufgetreten.|    
|2|Beim Reparieren einer Datenbank im Notfallmodus ist ein Fehler aufgetreten.|    
|3|Dies weist auf eine Beschädigung der Metadaten hin, die zur Beendigung des DBCC-Befehls geführt hat.|    
|4|Eine Assertations- oder Zugriffsverletzung wurde entdeckt.|    
|5|Ein unbekannter Fehler ist aufgetreten, der den DBCC-Befehl beendet hat.|    
    
## <a name="error-reporting"></a>Fehlerberichterstellung    
Eine Dumpdatei (SQLDUMP*nnnn*".txt") wird erstellt, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Protokollverzeichnis, wenn DBCC CHECKDB Fehler durch eine Beschädigung erkennt. Falls die Funktionen zur Verwendung der Datensammlung und zur Fehlerberichterstellung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz aktiviert sind, wird die Datei automatisch an [!INCLUDE[msCoName](../../includes/msconame-md.md)] weitergeleitet. Die gesammelten Daten werden zur Verbesserung der Funktionalität von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet.
Die Sicherungsdatei enthält die Ergebnisse des DBCC CHECKDB-Befehls sowie eine zusätzliche Diagnoseausgabe. Zugriff ist auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto und Mitglieder der Sysadmin-Rolle. Die Rolle "Sysadmin" enthält standardmäßig alle Mitglieder der Windows-Gruppe VORDEFINIERT\Administratoren und der lokalen Administratorgruppe sein. Ein Fehler bei der Datensammlung verursacht keinen Fehler des DBCC-Befehls.
    
## <a name="resolving-errors"></a>Auflösen von Fehlern    
Wenn DBCC CHECKDB Fehler meldet, empfiehlt es sich, die Datenbank mithilfe einer Datenbanksicherung wiederherzustellen, statt REPAIR mit einer der REPAIR-Optionen auszuführen. Wenn keine Sicherung vorhanden ist, können Sie die gemeldeten Fehler durch Ausführen von REPAIR beheben. Die zu verwendende Reparaturoption wird am Ende der Liste gemeldeter Fehler angegeben. Wenn die Fehlerkorrektur mithilfe der Option REPAIR_ALLOW_DATA_LOSS erfolgen soll, müssen möglicherweise jedoch einige Seiten, und damit auch Daten, gelöscht werden.
Unter bestimmten Bedingungen werden möglicherweise Werte in die Datenbank eingegeben, die basierend auf dem Datentyp der Spalte ungültig sind oder außerhalb des gültigen Bereichs liegen. DBCC CHECKDB kann ungültige Spaltenwerte für alle Spaltendatentypen erkennen. Wird DBCC CHECKDB mit der Option DATA_PURITY für Datenbanken ausgeführt, die von früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert wurden, ist es daher möglich, dass bereits vorhandene Spaltenwertfehler aufgedeckt werden. Da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diese Fehler nicht automatisch reparieren kann, muss der Spaltenwert manuell aktualisiert werden. Wenn CHECKDB einen derartigen Fehler erkennt, werden eine Warnung, die Fehlernummer 2570 sowie Informationen zurückgegeben, anhand derer die betroffene Zeile identifiziert und der Fehler manuell behoben werden kann.
Die Reparatur kann im Rahmen einer Benutzertransaktion ausgeführt werden, damit der Benutzer für die vorgenommenen Änderungen ggf. ein Rollback ausführen kann. Falls für Reparaturen ein Rollback ausgeführt wird, enthält die Datenbank immer noch Fehler und muss von einer Sicherung wiederhergestellt werden. Nach Abschluss der Reparaturen sollten Sie eine Sicherung der Datenbank durchführen.
    
## <a name="resolving-errors-in-database-emergency-mode"></a>Beheben von Fehlern im Datenbank-Notfallmodus    
Wenn eine Datenbank vorsieht Notfallmodus mithilfe der [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) Anweisung DBCC CHECKDB können einige besonderen Reparaturen an der Datenbank ausführen, wenn die REPAIR_ALLOW_DATA_LOSS-Option angegeben wird. Durch diese Reparaturen können normalerweise nicht wiederherstellbare Datenbanken in einem physisch konsistenten Zustand wieder online geschaltet werden. Die Reparaturen sollten als letzte Möglichkeit und nur dann verwendet werden, wenn die Datenbank nicht von einer Sicherung wiederhergestellt werden kann. Wenn die Datenbank im Notfallmodus befindet festgelegt ist, die Datenbank ist als READ_ONLY markiert, ist die Protokollierung deaktiviert und Zugriff ist auf Mitglieder der festen Serverrolle Sysadmin beschränkt.
    
> [!NOTE]
> Sie können den DBCC CHECKDB-Befehl nicht im Notfallmodus in einer Benutzertransaktion ausführen und nach der Ausführung für die Transaktion ein Rollback ausführen.    
    
Wenn sich die Datenbank im Notfallmodus befindet und DBCC CHECKDB mit der REPAIR_ALLOW_DATA_LOSS-Klausel ausgeführt wird, werden die folgenden Aktionen ausgeführt:
-   DBCC CHECKDB verwendet Seiten, die aufgrund von E/A- oder Prüfsummenfehlern mit Kein Zugriff markiert wurden, als wären keine Fehler aufgetreten. Dadurch erhöhen sich die Chancen für eine Datenwiederherstellung aus der Datenbank.    
-   DBCC CHECKDB versucht, die Datenbank mithilfe regulärer, protokollbasierter Wiederherstellungstechniken wiederherzustellen.    
-   Falls die Datenbank aufgrund einer Beschädigung des Transaktionsprotokolls nicht wiederhergestellt werden kann, wird das Transaktionsprotokoll neu erstellt. Beim Neuerstellen des Transaktionsprotokolls kann die Transaktionskonsistenz möglicherweise verloren gehen.    
    
> [!WARNING]
> Die REPAIR_ALLOW_DATA_LOSS-Option ist ein unterstütztes Feature von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Jedoch ist sie möglicherweise nicht immer die beste Option, um eine Datenbank in einen physisch konsistenten Zustand zu versetzen. Im Erfolgsfall kann die REPAIR_ALLOW_DATA_LOSS-Option zu Datenverlusten führen. Tatsächlich können dabei mehr Daten verloren gehen als bei einer Wiederherstellung der Datenbank aus der letzten als funktionierend bekannten Sicherung durch den Benutzer. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt immer eine Wiederherstellung durch den Benutzer aus der letzten als funktionierend bekannten Sicherung als primäre Methode zur Wiederherstellung nach Fehlern, die von DBCC CHECKDB gemeldet wurden. Die REPAIR_ALLOW_DATA_LOSS-Option ist keine Alternative zur Wiederherstellung aus einer als funktionierend bekannten Sicherung. Diese Option ist nur für den Notfall als „letzte Option“ geeignet, wenn die Wiederherstellung aus einer Sicherung nicht möglich ist.    
>     
>  Nach dem Neuerstellen des Protokolls gibt es keine vollständige ACID-Garantie.    
>     
>  Nach der Neuerstellung des Protokolls wird DBCC CHECKDB automatisch ausgeführt, und physische Konsistenzprobleme werden gemeldet und korrigiert.    
>     
>  Durch logische Datenkonsistenz und Geschäftslogik erzwungene Dateneinschränkungen müssen manuell überprüft werden.    
>     
>  Die Größe des Transaktionsprotokolls wird auf der Standardgröße belassen und muss manuell wieder auf die letzte Größe angepasst werden.    
    
Ist der DBCC CHECKDB-Befehl erfolgreich, befindet sich die Datenbank in einem physisch konsistenten Zustand, und der Datenbankstatus wird auf ONLINE festgelegt. Die Datenbank kann jedoch Transaktionsinkonsistenzen enthalten. Es wird empfohlen, die Sie ausführen [DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md) identifizieren alle Logikfehler Business und sofort sichern Sie die Datenbank.
Falls der DBCC CHECKDB-Befehl einen Fehler generiert, kann die Datenbank nicht repariert werden.
    
## <a name="running-dbcc-checkdb-with-repairallowdataloss-in-replicated-databases"></a>Ausführen von DBCC CHECKDB mit REPAIR_ALLOW_DATA_LOSS in replizierten Datenbanken    
Das Ausführen des Befehls DBCC CHECKDB mit der Option REPAIR_ALLOW_DATA_LOSS kann Auswirkungen auf Benutzerdatenbanken (Veröffentlichungs- und Abonnementdatenbanken) und die von der Replikation verwendete Verteilungsdatenbank haben. Veröffentlichungs- und Abonnementdatenbanken schließen veröffentlichte Tabellen und Tabellen mit Replikationsmetadaten ein. Beachten Sie die folgenden potenziellen Probleme in diesen Datenbanken:
-   Veröffentlichte Tabellen. Aktionen, die vom CHECKDB-Prozess zur Reparatur beschädigter Benutzerdaten ausgeführt werden, werden möglicherweise nicht repliziert:    
-   Die Mergereplikation verwendet Trigger, um Änderungen an veröffentlichten Tabellen nachzuverfolgen. Wenn Zeilen vom CHECKDB-Prozess eingefügt, aktualisiert oder gelöscht werden, werden die Trigger nicht ausgelöst. Daher wird die Änderung nicht repliziert.
-   Die Transaktionsreplikation verwendet das Transaktionsprotokoll, um Änderungen an veröffentlichten Tabellen nachzuverfolgen. Anschließend verschiebt der Protokolllese-Agent diese Änderungen in die Verteilungsdatenbank. Einige DBCC-Reparaturen werden zwar protokolliert, können vom Protokolllese-Agent jedoch nicht repliziert werden. Wenn z. B. die Zuordnung einer Datenseite durch den CHECKDB-Prozess aufgehoben wird, übersetzt der Protokolllese-Agent dies nicht in eine DELETE-Anweisung. Daher wird die Änderung nicht repliziert.
-   Tabellen mit Replikationsmetadaten. Für Aktionen, die vom CHECKDB-Prozess zur Reparatur beschädigter Tabellen mit Replikationsmetadaten ausgeführt werden, ist das Entfernen und Neukonfigurieren der Replikation erforderlich.    
    
Führen Sie Folgendes aus, wenn Sie den Befehl DBCC CHECKDB mit der Option REPAIR_ALLOW_DATA_LOSS für eine Benutzerdatenbank oder Verteilungsdatenbank ausführen müssen:
1.  Versetzen Sie das System in einen inaktiven Status: Beenden Sie die Aktivität in der Datenbank und allen anderen Datenbanken in der Replikationstopologie, und versuchen Sie anschließend, alle Knoten zu synchronisieren. Weitere Informationen finden Sie unter [Versetzen einer Replikationstopologie in einen inaktiven Status &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).    
1.  Führen Sie DBCC CHECKDB aus.    
1.  Wenn der Bericht von DBCC CHECKDB Reparaturen für Tabellen in der Verteilungsdatenbank oder für Tabellen mit Replikationsmetadaten in einer Benutzerdatenbank einschließt, entfernen Sie die Replikation, und konfigurieren Sie sie neu. Weitere Informationen finden Sie unter [Deaktivieren der Veröffentlichung und Verteilung](../../relational-databases/replication/disable-publishing-and-distribution.md).    
1.  Wenn der Bericht von DBCC CHECKDB Reparaturen für replizierte Tabellen enthält, führen Sie eine Datenüberprüfung aus, um zu bestimmen, ob Unterschiede zwischen den Daten in den Veröffentlichungs- und Abonnementdatenbanken bestehen.    
    
## <a name="result-sets"></a>Resultsets    
DBCC CHECKDB gibt das folgende Resultset zurück. Die Werte können variieren, es sei denn, die Optionen ESTIMATEONLY, PHYSICAL_ONLY oder NO_INFOMSGS werden angegeben:
    
```sql
 DBCC results for 'model'.    
    
 Service Broker Msg 9675, Level 10, State 1: Message Types analyzed: 13.    
    
 Service Broker Msg 9676, Level 10, State 1: Service Contracts analyzed: 5.    
    
 Service Broker Msg 9667, Level 10, State 1: Services analyzed: 3.    
    
 Service Broker Msg 9668, Level 10, State 1: Service Queues analyzed: 3.    
    
 Service Broker Msg 9669, Level 10, State 1: Conversation Endpoints analyzed: 0.    
    
 Service Broker Msg 9674, Level 10, State 1: Conversation Groups analyzed: 0.    
    
 Service Broker Msg 9670, Level 10, State 1: Remote Service Bindings analyzed: 0.    
    
 DBCC results for 'sys.sysrowsetcolumns'.    
    
 There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.    
    
 DBCC results for 'sys.sysrowsets'.    
    
 There are 97 rows in 1 pages for object 'sys.sysrowsets'.    
    
 DBCC results for 'sysallocunits'.    
    
 There are 195 rows in 3 pages for object 'sysallocunits'.    
    
 There are 0 rows in 0 pages for object "sys.sysasymkeys".    
    
 DBCC results for 'sys.syssqlguides'.    
    
 There are 0 rows in 0 pages for object "sys.syssqlguides".    
    
 DBCC results for 'sys.queue_messages_1977058079'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_1977058079".    
    
 DBCC results for 'sys.queue_messages_2009058193'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2009058193".    
    
 DBCC results for 'sys.queue_messages_2041058307'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2041058307".    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'model'.    
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```

DBCC CHECKDB gibt das folgende Resultset (die folgende Meldung) zurück, wenn NO_INFOMSGS angegeben wird:
    
```sql
 The command(s) completed successfully.
 ```
 
DBCC CHECKDB gibt das folgende Resultset zurück, wenn PHYSICAL_ONLY angegeben wird:
    
```sql
 DBCC results for 'model'.    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'master'.  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
 ```
 
DBCC CHECKDB gibt das folgende Resultset zurück, wenn ESTIMATEONLY angegeben wird.
    
```sql
 Estimated TEMPDB space needed for CHECKALLOC (KB)    
    
 -------------------------------------------------  
    
 13   
    
 (1 row(s) affected)   
    
 Estimated TEMPDB space needed for CHECKTABLES (KB)    
    
 --------------------------------------------------    
    
 57 
    
 (1 row(s) affected)  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
    
## <a name="permissions"></a>Berechtigungen    
Erfordert die Mitgliedschaft in der festen Serverrolle Sysadmin oder der festen Datenbankrolle "Db_owner".
    
## <a name="examples"></a>Beispiele    
    
### <a name="a-checking-both-the-current-and-another-database"></a>A. Überprüfen der aktuellen und einer anderen Datenbank    
Im folgenden Beispiel wird `DBCC CHECKDB` für die aktuelle Datenbank und für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank ausgeführt.
    
```sql    
-- Check the current database.    
DBCC CHECKDB;    
GO    
-- Check the AdventureWorks2012 database without nonclustered indexes.    
DBCC CHECKDB (AdventureWorks2012, NOINDEX);    
GO    
```    
    
### <a name="b-checking-the-current-database-suppressing-informational-messages"></a>B. Überprüfen der aktuellen Datenbank, wobei Informationsmeldungen unterdrückt werden    
Im folgenden Beispiel wird die aktuelle Datenbank überprüft; alle Informationsmeldungen werden unterdrückt.
    
```sql    
DBCC CHECKDB WITH NO_INFOMSGS;    
GO    
```    
    
## <a name="see-also"></a>Siehe auch    
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Anzeigen der Größe der Datei mit geringer Dichte einer Datenbank-Momentaufnahme &#40;SQL Server&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)  
[Sp_helpdb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)  
[Systemtabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  

