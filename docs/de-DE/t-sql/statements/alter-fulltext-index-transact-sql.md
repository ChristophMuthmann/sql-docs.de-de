---
title: ALTER FULLTEXT INDEX (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT INDEX
- ALTER_FULLTEXT_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- modifying full-text indexes
- full-text indexes [SQL Server], modifying
- search property lists [SQL Server], associating with full-text indexes
- ALTER FULLTEXT INDEX statement
ms.assetid: b6fbe9e6-3033-4d1b-b6bf-1437baeefec3
caps.latest.revision: 95
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 327f527ad470d36dac37bb044fe77149794c1650
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-fulltext-index-transact-sql"></a>ALTER FULLTEXT INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ändert die Eigenschaften eines Volltextindex in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER FULLTEXT INDEX ON table_name  
   { ENABLE   
   | DISABLE  
   | SET CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF }  
   | ADD ( column_name   
           [ TYPE COLUMN type_column_name ]   
           [ LANGUAGE language_term ]  
           [ STATISTICAL_SEMANTICS ]  
           [,...n]   
         )  
     [ WITH NO POPULATION ]  
   | ALTER COLUMN column_name  
     { ADD | DROP } STATISTICAL_SEMANTICS  
     [ WITH NO POPULATION ]  
   | DROP ( column_name [,...n] )  
     [ WITH NO POPULATION ]   
   | START { FULL | INCREMENTAL | UPDATE } POPULATION  
   | {STOP | PAUSE | RESUME } POPULATION   
   | SET STOPLIST [ = ] { OFF| SYSTEM | stoplist_name }  
     [ WITH NO POPULATION ]   
   | SET SEARCH PROPERTY LIST [ = ] { OFF | property_list_name }  
     [ WITH NO POPULATION ]   
   }  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *table_name*  
 Der Name der Tabelle oder der indizierten Sicht mit den Spalten, die im Volltextindex enthalten sind. Die Angabe des Datenbank- und Tabellenbesitzernamens ist optional.  
  
 ENABLE | DISABLE  
 Teilt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit, ob Volltextindexdaten für *table_name* gesammelt werden sollen. Mit ENABLE wird der Volltextindex aktiviert, mit DISABLE wird er deaktiviert. In der Tabelle werden Volltextabfragen nicht unterstützt, während der Index deaktiviert wird.  
  
 Das Deaktivieren eines Volltextindexes ermöglicht Ihnen, die Änderungsnachverfolgung zu deaktivieren, den Volltextindex jedoch beizubehalten, den Sie jederzeit mittels ENABLE reaktivieren können. Wenn der Volltextindex deaktiviert ist, werden die Metadaten des Volltextindexes weiterhin in den Systemtabellen gespeichert. Falls sich CHANGE_TRACKING im aktivierten Status befindet (automatisches oder manuelles Update) und der Volltextindex deaktiviert ist, wird der Status der Indizes eingefroren. Ein zurzeit ausgeführter Durchforstungsvorgang wird angehalten, und neue Änderungen an den Tabellendaten werden nicht nachverfolgt und an den Index weitergeleitet.  
  
 SET CHANGE_TRACKING {MANUAL | AUTO | OFF}  
 Gibt an, ob vom Volltextindex abgedeckte Änderungen (Updates, Löschungen oder Einfügungen) an Tabellenspalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an den Volltextindex weitergegeben werden. Datenänderungen durch WRITETEXT und UPDATETEXT werden im Volltextindex nicht wiedergegeben und bei der Änderungsnachverfolgung nicht ausgewählt.  
  
> [!NOTE]  
>  Informationen zur Interaktion zwischen der Änderungsnachverfolgung und WITH NO POPULATION finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 MANUAL  
 Gibt an, dass die nachverfolgten Änderungen manuell durch einen Aufruf der Anweisung ALTER FULLTEXT INDEX … START UPDATE POPULATION [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung (*manuelles Auffüllung*). Sie können den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent verwenden, um die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung in regelmäßigen Abständen aufzurufen.  
  
 AUTO  
 Gibt an, dass die nachverfolgten Änderungen automatisch weitergegeben werden, wenn Daten in der Basistabelle geändert werden (*automatische Auffüllung*). Obwohl Änderungen automatisch weitergegeben werden, werden diese Änderungen u. U. nicht sofort im Volltextindex wiedergegeben. AUTO ist die Standardeinstellung.  
  
 OFF  
 Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Liste der Änderungen an den indizierten Daten speichert.  
  
 ADD | DROP *column_name*  
 Gibt die Spalten an, die einem Volltextindex hinzugefügt bzw. daraus gelöscht werden sollen. Die Spalte oder die Spalten müssen vom Typ **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** oder **varbinary(max)** sein.  
  
 Die DROP-Klausel sollte nur für Spalten verwendet werden, die zuvor für die Volltextindizierung aktiviert wurden.  
  
 Verwenden Sie TYPE COLUMN und LANGUAGE mit der ADD-Klausel, um diese Eigenschaften in *column_name* festzulegen. Wenn eine Spalte hinzugefügt wird, muss der Volltextindex in der Tabelle erneut aufgefüllt werden, damit die Volltextabfragen in dieser Spalte funktionieren können.  
  
> [!NOTE]  
>  Ob der Volltextindex aufgefüllt wird, nachdem eine Spalte hinzugefügt oder entfernt wurde, hängt davon ab, ob die Änderungsnachverfolgung aktiviert wurde und WITH NO POPULATION angegeben ist. Weitere Informationen finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 TYPE COLUMN *type_column_name*  
 Gibt den Namen der Tabellenspalte *table_column_name* an, die den Dokumenttyp für ein Dokument vom Typ **varbinary**, **varbinary(max)** oder **image** enthält. Diese Spalte, als Typspalte bezeichnet, enthält eine vom Benutzer angegebene Dateierweiterung (.doc, .pdf, .xls usw.) Die Typspalte muss vom Typ **char**, **nchar**, **varchar**oder **nvarchar**sein.  
  
 Geben Sie TYPE COLUMN *type_column_name* nur an, wenn *column_name* eine Spalte vom Typ **varbinary**, **varbinary(max)** oder **image** angibt, in der Daten als Binärdaten gespeichert werden. Andernfalls gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück.  
  
> [!NOTE]  
>  Bei der Indizierung verwendet die Volltext-Egine die Abkürzung in der Typspalte der einzelnen Tabellenzeilen, um den für das Dokument in *column_name* zu verwendenden Filter für die Volltextsuche zu ermitteln. Der Filter lädt das Dokument als binären Datenstrom, entfernt die Formatierungsinformationen und sendet den Text des Dokuments an die Wörtertrennungskomponente. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
 LANGUAGE *language_term*  
 Die Sprache der in **column_name** gespeicherten Daten.  
  
 *language_term* ist optional und kann als Zeichenfolge, ganze Zahl oder Hexadezimalwert entsprechend dem Gebietsschemabezeichner (Locale Identifier, LCID) einer Sprache angegeben werden. Wird *language_term* angegeben, wird die entsprechende Sprache auf alle Elemente der Suchbedingung angewendet. Wird kein Wert angegeben, wird die Standardvolltextsprache der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verwendet.  
  
 Mithilfe der gespeicherten Prozedur **sp_configure** können Sie auf Informationen zur Standardvolltextsprache der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zugreifen.  
  
 In Form einer Zeichenfolge entspricht *language_term* dem Wert der **alias**-Spalte in der **syslanguages**-Systemtabelle. Die Zeichenfolge muss in einfache Anführungszeichen eingeschlossen werden, z.B. '*language_term*'. In Form einer ganzen Zahl ist *language_term* der eigentliche Gebietsschemabezeichner, der die Sprache identifiziert. In Form eines Hexadezimalwerts ist *language_term* gleich 0x, gefolgt vom Hexadezimalwert des Gebietsschemabezeichners. Der Hexadezimalwert darf acht Ziffern nicht überschreiten, einschließlich führender Nullen.  
  
 Wird der Wert im Format Doppelbyte-Zeichensatz (Double-Byte Character Set, DBCS) angegeben, wird er von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Unicode konvertiert.  
  
 Ressourcen, wie die Wörtertrennung und die Wortstammerkennung, müssen für die mit *language_term* angegebene Sprache aktiviert sein. Falls die angegebene Sprache von den Ressourcen nicht unterstützt wird, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück.  
  
 Verwenden Sie die neutrale (0x0) Sprachenressource für Nicht-BLOB- und Nicht-XML-Spalten mit Textdaten in mehreren Sprachen oder für Fälle, in denen die Sprache des in der Spalte gespeicherten Texts unbekannt ist. Für Dokumente, die in Spalten vom Typ XML oder BLOB gespeichert werden, wird die Sprachcodierung innerhalb des Dokuments bei der Indizierung verwendet. In XML-Spalten wird die Sprache z. B. mit dem xml:lang-Attribut in XML-Dokumenten identifiziert. Zur Abfragezeit wird der Wert, der vorher in *language_term* angegeben wurde, die Standardsprache, die für Volltextabfragen verwendet wird, es sei denn *language_term* wird als Teil einer Volltextabfrage angegeben.  
  
 STATISTICAL_SEMANTICS  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Erstellt den zusätzlichen Schlüsselausdruck und die Dokumentähnlichkeitsindizes, die Teil der statistischen semantischen Indizierung sind. Weitere Informationen finden Sie unter [Semantische Suche &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 [ **,***...n*]  
 Gibt an, dass mehrere Spalten für die ADD-, ALTER- oder DROP-Klauseln angegeben werden können. Bei Angabe mehrerer Spalten müssen die Spalten mit Kommas getrennt werden.  
  
 WITH NO POPULATION  
 Gibt an, dass der Volltextindex nach einem ADD- oder DROP-Spaltenvorgang oder einem SET STOPLIST-Vorgang nicht aufgefüllt wird. Der Index wird nur aufgefüllt, wenn der Benutzer einen START...POPULATION-Befehl ausführt.  
  
 Wenn NO POPULATION angegeben ist, füllt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keinen Index auf. Der Index wird erst aufgefüllt, wenn der Benutzer einen ALTER FULLTEXT INDEX...START POPULATION-Befehl ausgibt. Wenn NO POPULATION nicht angegeben ist, füllt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Index auf.  
  
 Falls CHANGE_TRACKING aktiviert und WITH NO POPULATION angegeben ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück. Wenn CHANGE_TRACKING aktiviert und WITH NO POPULATION nicht angegeben ist, füllt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Index vollständig auf.  
  
> [!NOTE]  
>  Weitere Informationen zur Interaktion zwischen der Änderungsnachverfolgung und WITH NO POPULATION finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 {ADD | DROP } STATISTICAL_SEMANTICS  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aktiviert oder deaktiviert die statistische semantische Indizierung für die angegebenen Spalten. Weitere Informationen finden Sie unter [Semantische Suche &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 START {FULL|INCREMENTAL|UPDATE} POPULATION  
 Teilt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit, dass die Auffüllung des Volltextindex für *table_name* beginnen kann. Falls bereits eine Auffüllung des Volltextindexes ausgeführt wird, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Warnung zurück und startet keine neue Auffüllung.  
  
 FULL  
 Gibt an, dass jede Zeile der Tabelle für die Volltextindizierung abgerufen werden soll, auch wenn die Zeilen bereits indiziert wurden.  
  
 INCREMENTAL  
 Gibt an, dass nur die Zeilen für die Volltextindizierung abgerufen werden sollen, die seit dem letzten Auffüllen geändert wurden. INCREMENTAL kann nur angewendet werden, wenn die Tabelle eine Spalte vom Typ **timestamp**besitzt. Falls eine Tabelle im Volltextkatalog keine Spalte vom Typ **timestamp** besitzt, wird die Tabelle vollständig aufgefüllt.  
  
 UPDATE  
 Gibt die Verarbeitung aller Einfügungen, Updates oder Löschungen seit dem letzten Update des Index für die Änderungsnachverfolgung an. Das Auffüllen der Änderungsnachverfolgung muss in einer Tabelle aktiviert sein, nicht aktiviert sein sollten jedoch die Aktualisierung des Index im Hintergrund und die automatische Änderungsnachverfolgung.  
  
 {STOP | PAUSE | RESUME } POPULATION  
 Beendet eine zurzeit ausgeführte Auffüllung oder hält diese an; oder beendet eine angehaltene Auffüllung bzw. setzt diese fort.  
  
 Mit STOP POPULATION wird weder die automatische Änderungsnachverfolgung noch das Update des Index im Hintergrund beendet. Verwenden Sie SET CHANGE_TRACKING OFF, um die Änderungsnachverfolgung zu beenden.  
  
 PAUSE POPULATION und RESUME POPULATION können nur für vollständige Auffüllungen verwendet werden. Für andere Auffüllungstypen sind sie nicht relevant, da die anderen Auffüllungen Durchforstungsvorgänge dort fortsetzen, wo sie beendet wurden.  
  
 SET STOPLIST { OFF| SYSTEM | *stoplist_name* }  
 Ändert die Volltextstoppliste, die dem Index zugeordnet ist, wenn überhaupt.  
  
 OFF  
 Gibt an, dass dem Volltextindex keine Stoppliste zugeordnet wird.  
  
 SYSTEM  
 Gibt an, dass die Standardvolltext-Systemstoppliste STOPLIST für diesen Volltextindex verwendet werden soll.  
  
 *stoplist_name*  
 Gibt den Namen der Stoppliste an, die dem Volltextindex zugeordnet werden soll.  
  
 Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 SET SEARCH PROPERTY LIST { OFF | *property_list_name* } [ WITH NO POPULATION ]  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Ändert die ggf. Sucheigenschaftenliste, die dem Index zugeordnet ist.  
  
 OFF  
 Gibt an, dass dem Volltextindex keine Eigenschaftenliste zugeordnet werden soll. Wenn Sie die Sucheigenschaftenliste eines Volltextindexes (ALTER FULLTEXT INDEX … SET SEARCH PROPERTY LIST OFF) deaktivieren, ist keine Suche nach Eigenschaften in der Basistabelle mehr möglich.  
  
 Wenn Sie eine vorhandene Sucheigenschaftenliste deaktivieren, wird der Volltextindex standardmäßig automatisch wieder aufgefüllt. Wenn Sie beim Deaktivieren einer Sucheigenschaftenliste WITH NO POPULATION angeben, erfolgt keine automatische Wiederauffüllung. Es empfiehlt sich jedoch, zu einem späteren Zeitpunkt, eine vollständige Auffüllung für diesen Volltextindex durchzuführen. Wenn der Volltextindex wieder aufgefüllt wird, werden die eigenschaftenspezifischen Metadaten der gelöschten Sucheigenschaften entfernt, und der Volltextindex wird kleiner und leistungsfähiger.  
  
 *property_list_name*  
 Gibt den Namen der Sucheigenschaftenliste an, die dem Volltextindex zugeordnet werden soll.  
  
 Wenn Sie einem Volltextindex eine Sucheigenschaftenliste hinzufügen, muss der Index erneut aufgefüllt werden, damit die Sucheigenschaften indiziert werden können, die für die entsprechende Sucheigenschaftenliste registriert sind. Wenn Sie beim Hinzufügen der Sucheigenschaftenliste WITH NO POPULATION angeben, müssen Sie zu einem späteren Zeitpunkt eine Auffüllung des Index ausführen.  
  
> [!IMPORTANT]  
>  Wenn der Volltextindex zuvor einer anderen Sucheigenschaftenliste zugeordnet war, muss er neu erstellt werden, damit er wieder in einem konsistenten Zustand vorliegt. Bis eine vollständige Auffüllung ausgeführt wird, wird der Index sofort abgeschnitten, und er ist leer. Weitere Informationen zu den Fällen, in denen Änderungen der Sucheigenschaftenliste eine Neuerstellung bewirken, finden Sie unter "Hinweise" in diesem Thema.  
  
> [!NOTE]  
>  Sie können eine Sucheigenschaftenliste mehr als einem Volltextindex in der gleichen Datenbank zuordnen.  
  
 **So finden Sie die Sucheigenschaftenlisten für die aktuelle Datenbank:**  
  
-   [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 Weitere Informationen zu Sucheigenschaftenlisten finden Sie unter [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>Interaktionen zwischen der Änderungsnachverfolgung und dem Parameter NO POPULATION  
 Ob der Volltextindex aufgefüllt wird, hängt davon ab, ob die Änderungsnachverfolgung aktiviert wurde und WITH NO POPULATION in der ALTER FULLTEXT INDEX-Anweisung angegeben ist. In der folgenden Tabelle wird das Ergebnis ihrer Interaktion zusammengefasst.  
  
|Änderungsnachverfolgung|WITH NO POPULATION|Ergebnis|  
|---------------------|------------------------|------------|  
|Nicht aktiviert|Nicht angegeben|Der Index wird vollständig aufgefüllt.|  
|Nicht aktiviert|Specified|Der Index wird nicht aufgefüllt, bevor eine Anweisung ALTER FULLTEXT INDEX...START POPULATION ausgegeben wird.|  
|Aktiviert|Specified|Ein Fehler wird ausgelöst, und der Index wird nicht geändert.|  
|Aktiviert|Nicht angegeben|Der Index wird vollständig aufgefüllt.|  
  
 Weitere Informationen zum Auffüllen von Volltextindizes finden Sie unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="changing-the-search-property-list-causes-rebuilding-the-index"></a>Neuerstellung des Index durch Änderungen an der Sucheigenschaftenliste  
 Nachdem ein Volltextindex einer Sucheigenschaftenliste zum ersten Mal zugeordnet wurde, muss der Index neu aufgefüllt werden, damit eigenschaftenspezifische Suchbegriffe indiziert werden können. Die vorhandenen Indexdaten werden nicht abgeschnitten.  
  
 Wenn Sie den Volltextindex jedoch einer anderen Eigenschaftenliste zuordnen, wird der Index neu erstellt. Bei der Neuerstellung wird der Volltextindex unmittelbar abgeschnitten, alle vorhandenen Daten werden entfernt, und der Index muss erneut aufgefüllt werden. Während der erneuten Auffüllung werden von Volltextabfragen in der zugrunde liegenden Tabelle nur die Zeilen abgefragt, die bereits von der Auffüllung indiziert wurden. Die wieder aufgefüllten Indexdaten enthalten Metadaten aus den registrierten Eigenschaften der neu hinzugefügten Sucheigenschaftenliste.  
  
 Eine erneute Erstellung wird u. a. durch folgende Szenarien verursacht:  
  
-   Direkter Wechsel zu einer anderen Sucheigenschaftenliste (siehe "Szenario A" weiter unten in diesem Abschnitt).  
  
-   Deaktivieren der Sucheigenschaftenliste und späteres Zuordnen des Indexes zu einer beliebigen Sucheigenschaftenliste (siehe "Szenario B" weiter unten in diesem Abschnitt)  
  
> [!NOTE]  
>  Weitere Informationen zur Funktionsweise der Volltextsuche mit Sucheigenschaftenlisten finden Sie unter [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md). Weitere Informationen zum vollständigen Auffüllen finden Sie unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).  
  
### <a name="scenario-a-switching-directly-to-a-different-search-property-list"></a>Szenario A: Direkter Wechsel zu einer anderen Sucheigenschaftenliste  
  
1.  Es wird ein Volltextindex in `table_1` mit der Sucheigenschaftenliste `spl_1` erstellt:  
  
    ```  
    CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index   
       WITH SEARCH PROPERTY LIST=spl_1,   
       CHANGE_TRACKING OFF, NO POPULATION;   
    ```  
  
2.  Eine vollständige Auffüllung des Volltextindex wird ausgeführt:  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1 START FULL POPULATION;  
    ```  
  
3.  Der Volltextindex wird später mit der folgenden Anweisung einer anderen Sucheigenschaftenliste (`spl_2`) zugeordnet:  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_2;  
    ```  
  
     Diese Anweisung verursacht standardmäßig eine vollständige Auffüllung.  Vor Beginn der Auffüllung wird der Index jedoch automatisch vom Volltextmodul abgeschnitten.  
  
### <a name="scenario-b-turning-off-the-search-property-list-and-later-associating-the-index-with-any-search-property-list"></a>Szenario B: Deaktivieren der Sucheigenschaftenliste und späteres Zuordnen des Indexes zu einer Sucheigenschaftenliste  
  
1.  In `table_1` wird ein Volltextindex mit der Sucheigenschaftenliste `spl_1` erstellt, und der Index wird standardmäßig automatisch aufgefüllt:  
  
    ```  
    CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index   
       WITH SEARCH PROPERTY LIST=spl_1;   
    ```  
  
2.  Die Sucheigenschaftenliste wird wie folgt deaktiviert:  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1   
       SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;   
    ```  
  
3.  Der Volltextindex wird erneut der gleichen oder einer anderen Sucheigenschaftenliste zugeordnet.  
  
     Mit der folgenden Anweisung wird der Volltextindex beispielsweise wieder der ursprünglichen Sucheigenschaftenliste `spl_1` zugeordnet:  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_1;  
    ```  
  
     Diese Anweisung verursacht standardmäßig eine vollständige Auffüllung.  
  
    > [!NOTE]  
    >  Die Neuerstellung ist auch bei einer anderen Sucheigenschaftenliste wie `spl_2` erforderlich.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Benutzer muss über die ALTER-Berechtigung für die Tabelle oder die indizierte Sicht verfügen oder ein Mitglied der festen Serverrolle **sysadmin** oder der festen Datenbankrollen **db_owner** oder **db_ddladmin** sein.  
  
 Wenn SET STOPLIST angegeben wird, muss der Benutzer über die REFERENCES-Berechtigung für die Stoppliste verfügen. Wenn SET SEARCH PROPERTY LIST angegeben wird, muss der Benutzer über die REFERENCES-Berechtigung für die Sucheigenschaftenliste verfügen. Der Besitzer der angegebenen Stoppliste oder der angegebenen Sucheigenschaftenliste kann die REFERENCES-Berechtigung erteilen, wenn der Besitzer über ALTER FULLTEXT CATALOG-Berechtigungen verfügt.  
  
> [!NOTE]  
>  Der Datenbankrolle public wird für die Standardstoppliste, die mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeliefert wird, die REFERENCES-Berechtigung gewährt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-setting-manual-change-tracking"></a>A. Festlegen der manuellen Änderungsnachverfolgung  
 Im folgenden Beispiel wird die manuelle Änderungsnachverfolgung für den Volltextindex in der `JobCandidate`-Tabelle festgelegt.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate  
   SET CHANGE_TRACKING MANUAL;  
GO  
```  
  
### <a name="b-associating-a-property-list-with-a-full-text-index"></a>B. Zuordnen einer Eigenschaftenliste zu einem Volltextindex  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel wird die Eigenschaftenliste `DocumentPropertyList` dem Volltextindex in der Tabelle `Production.Document` zugeordnet. Mit dieser ALTER FULLTEXT INDEX-Anweisung wird eine vollständige Auffüllung gestartet, die das Standardverhalten der SET SEARCH PROPERTY LIST-Klausel darstellt.  
  
> [!NOTE]  
>  Ein Beispiel, in dem die Eigenschaftenliste `DocumentPropertyList` erstellt wird, finden Sie unter [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList;   
GO  
```  
  
### <a name="c-removing-a-search-property-list"></a>C. Entfernen einer Sucheigenschaftenliste  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel wird die Eigenschaftenliste `DocumentPropertyList` aus dem Volltextindex in der Tabelle `Production.Document` entfernt. In diesem Beispiel besteht keine dringende Notwendigkeit, die Eigenschaften aus dem Index zu entfernen; daher wird die WITH NO POPULATION-Option angegeben. Suchen auf Eigenschaftenebene in diesem Volltextindex sind jedoch nicht mehr zulässig.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;   
GO  
```  
  
### <a name="d-starting-a-full-population"></a>D. Starten einer vollständigen Auffüllung  
 Im folgenden Beispiel wird die vollständige Ausfüllung für den Volltextindex in der `JobCandidate`-Tabelle gestartet.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   START FULL POPULATION;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [Volltextsuche](../../relational-databases/search/full-text-search.md)   
 [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
