---
title: CREATE FULLTEXT INDEX (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/05/2017
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
- FULLTEXT_INDEX_TSQL
- CREATE_FULLTEXT_INDEX_TSQL
- CREATE FULLTEXT INDEX
- FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], creating
- index creation [SQL Server], CREATE FULLTEXT INDEX statement
- CREATE FULLTEXT INDEX statement
ms.assetid: 8b80390f-5f8b-4e66-9bcc-cabd653c19fd
caps.latest.revision: 110
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5ac9e0f05e639e74dd83cdea7c8f7030e6249b8e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-fulltext-index-transact-sql"></a>CREATE FULLTEXT INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt einen Volltextindex für eine Tabelle oder eine indizierte Sicht in einer Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pro Tabelle oder indizierter Sicht ist nur ein Volltextindex zulässig, und jeder Volltextindex gilt für eine einzelne Tabelle oder indizierte Sicht. Ein Volltextindex kann bis zu 1024 Spalten enthalten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE FULLTEXT INDEX ON table_name  
   [ ( { column_name   
             [ TYPE COLUMN type_column_name ]  
             [ LANGUAGE language_term ]   
             [ STATISTICAL_SEMANTICS ]  
        } [ ,...n]   
      ) ]  
    KEY INDEX index_name   
    [ ON <catalog_filegroup_option> ]  
    [ WITH [ ( ] <with_option> [ ,...n] [ ) ] ]  
[;]  
  
<catalog_filegroup_option>::=  
 {  
    fulltext_catalog_name   
 | ( fulltext_catalog_name, FILEGROUP filegroup_name )  
 | ( FILEGROUP filegroup_name, fulltext_catalog_name )  
 | ( FILEGROUP filegroup_name )  
 }  
  
<with_option>::=  
 {  
   CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF [, NO POPULATION ] }   
 | STOPLIST [ = ] { OFF | SYSTEM | stoplist_name }  
 | SEARCH PROPERTY LIST [ = ] property_list_name   
 }  
```  
  
## <a name="arguments"></a>Argumente  
 *table_name*  
 Der Name der Tabelle oder der indizierten Sicht mit den Spalten, die im Volltextindex enthalten sind.  
  
 *column_name*  
 Der Name der Spalte, die im Volltextindex berücksichtigt wird. Es können nur Spalten der Typen **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml** und **varbinary(max)** für die Volltextsuche indiziert werden. Um mehrere Spalten anzugeben, wiederholen Sie die *column_name*-Klausel wie folgt:  
  
 CREATE FULLTEXT INDEX ON *table_name* (*column_name1* […], *column_name2* […]) …  
  
 TYPE COLUMN *type_column_name*  
 Gibt den Namen der Tabellenspalte *type_column_name* an, die den Dokumenttyp für ein Dokument vom Typ **varbinary(max)** oder **image** enthält. Diese Spalte, als Typspalte bezeichnet, enthält eine vom Benutzer angegebene Dateierweiterung (.doc, .pdf, .xls usw.) Die Typspalte muss vom Typ **char**, **nchar**, **varchar**oder **nvarchar**sein.  
  
 Geben Sie TYPE COLUMN *type_column_name* nur an, wenn *column_name* eine Spalte vom Typ **varbinary(max)** oder **image** angibt, in der Daten als Binärdaten gespeichert sind. Andernfalls gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück.  
  
> [!NOTE]  
>  Bei der Indizierung verwendet die Volltext-Egine die Abkürzung in der Typspalte der einzelnen Tabellenzeilen, um den für das Dokument in *column_name* zu verwendenden Filter für die Volltextsuche zu ermitteln. Der Filter lädt das Dokument als binären Datenstrom, entfernt die Formatierungsinformationen und sendet den Text des Dokuments an die Wörtertrennungskomponente. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
 LANGUAGE *language_term*  
 Die Sprache der in *column_name* gespeicherten Daten.  
  
 *language_term* ist optional und kann als Zeichenfolge, ganze Zahl oder Hexadezimalwert entsprechend dem Gebietsschemabezeichner (Locale Identifier, LCID) einer Sprache angegeben werden. Wenn kein Wert angegeben wird, wird die Standardsprache der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verwendet.  
  
 Wenn *language_term* angegeben ist, wird die davon dargestellte Sprache zum Indizieren von Daten verwendet, die in Spalten vom Typ **char**, **nchar**, **varchar**, **nvarchar**, **text** und **ntext** gespeichert sind. Diese Sprache ist die Standardsprache, die zur Abfragezeit verwendet wird, wenn *language_term* nicht als Teil eines Volltextprädikats für die Spalte angegeben wird.  
  
 In Form einer Zeichenfolge entspricht *language_term* dem Wert der alias-Spalte in der syslanguages-Systemtabelle. Die Zeichenfolge muss in einfache Anführungszeichen gesetzt werden, z.B. **'***language_term***'**. In Form einer ganzen Zahl ist *language_term* der eigentliche Gebietsschemabezeichner, der die Sprache identifiziert. In Form eines Hexadezimalwerts ist *language_term* gleich 0x, gefolgt vom Hexadezimalwert des Gebietsschemabezeichners. Der Hexadezimalwert darf acht Ziffern nicht überschreiten, einschließlich führender Nullen.  
  
 Wird der Wert im Format Doppelbyte-Zeichensatz (Double-Byte Character Set, DBCS) angegeben, wird er von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Unicode konvertiert.  
  
 Ressourcen, wie die Wörtertrennung und die Wortstammerkennung, müssen für die mit *language_term* angegebene Sprache aktiviert sein. Falls die angegebene Sprache von den Ressourcen nicht unterstützt wird, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück.  
  
 Verwenden Sie die gespeicherte Prozedur sp_configure, um auf Informationen zur Standardvolltextsprache der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zuzugreifen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)noch nicht kennen.  
  
 Verwenden Sie die neutrale (0x0) Sprachenressource für Nicht-BLOB- und Nicht-XML-Spalten mit Textdaten in mehreren Sprachen oder für Fälle, in denen die Sprache des in der Spalte gespeicherten Texts unbekannt ist. Zuerst sollten Sie jedoch die möglichen Folgen der Verwendung der neutralen (0x0) Sprachressource verstehen. Informationen zu den möglichen Lösungen und Folgen der Verwendung der neutralen (0x0) Sprachressource finden Sie unter [Auswählen einer Sprache beim Erstellen eines Volltextindex](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
 Für Dokumente, die in Spalten vom Typ XML oder BLOB gespeichert werden, wird die Sprachcodierung innerhalb des Dokuments bei der Indizierung verwendet. In XML-Spalten wird die Sprache z.B. mit dem **xml:lang**-Attribut in XML-Dokumenten identifiziert. Zur Abfragezeit wird der Wert, der vorher in *language_term* angegeben wurde, die Standardsprache, die für Volltextabfragen verwendet wird, es sei denn *language_term* wird als Teil einer Volltextabfrage angegeben.  
  
 STATISTICAL_SEMANTICS  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Erstellt den zusätzlichen Schlüsselausdruck und die Dokumentähnlichkeitsindizes, die Teil der statistischen semantischen Indizierung sind. Weitere Informationen finden Sie unter [Semantische Suche &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 KEY INDEX *index_name*  
 Der Name des eindeutigen Schlüsselindexes für *table_name*. KEY INDEX muss eine eindeutige Spalte mit einem Schlüssel sein, die nicht auf Null gesetzt werden kann. Wählen Sie als eindeutigen Volltextschlüssel stets den kleinsten eindeutigen Index aus.  Für die optimale Leistung empfehlen wir einen Integer-Datentyp als Volltextschlüssel.  
  
 *fulltext_catalog_name*  
 Der Volltextkatalog, der für den Volltextindex verwendet wird. Der Katalog muss bereits in der Datenbank vorhanden sein. Diese Klausel ist optional. Wenn sie nicht angegeben wird, wird ein Standardkatalog verwendet. Ist kein Standardkatalog vorhanden, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler zurück.  
  
 FILEGROUP *filegroup_name*  
 Erstellt den angegebenen Volltextindex für die angegebene Dateigruppe. Die Dateigruppe muss bereits vorhanden sein. Wenn die FILEGROUP-Klausel nicht angegeben ist, wird der Volltextindex für eine nicht partitionierte Tabelle als Basistabelle oder -ansicht in dieselbe Dateigruppe oder für eine partitionierte Tabelle in die primäre Dateigruppe platziert.  
  
 CHANGE_TRACKING [ = ] { MANUAL | **AUTO** | OFF [ , NO POPULATION ] }  
 Gibt an, ob vom Volltextindex abgedeckte Änderungen (Updates, Löschungen oder Einfügungen) an Tabellenspalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an den Volltextindex weitergegeben werden. Datenänderungen durch WRITETEXT und UPDATETEXT werden im Volltextindex nicht wiedergegeben und bei der Änderungsnachverfolgung nicht ausgewählt.  
  
 MANUAL  
 Gibt an, dass die nachverfolgten Änderungen manuell durch einen Aufruf der Anweisung ALTER FULLTEXT INDEX … START UPDATE POPULATION [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung (*manuelles Auffüllung*). Sie können den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent verwenden, um die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung in regelmäßigen Abständen aufzurufen.  
  
 **AUTO**  
 Gibt an, dass die nachverfolgten Änderungen automatisch weitergegeben werden, wenn Daten in der Basistabelle geändert werden (*automatische Auffüllung*). Obwohl Änderungen automatisch weitergegeben werden, werden diese Änderungen u. U. nicht sofort im Volltextindex wiedergegeben. AUTO ist die Standardeinstellung.  
  
 OFF [ `,` NO POPULATION]  
 Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Liste der Änderungen an den indizierten Daten verwaltet. Wird NO POPULATION nicht angegeben, füllt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Index nach seiner Erstellung auf.  
  
 Die Option NO POPULATION kann nur dann verwendet werden, wenn für CHANGE_TRACKING der Wert OFF festgelegt ist. Wenn NO POPULATION angegeben ist, füllt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Index nach dessen Erstellung nicht auf. Der Index wird erst aufgefüllt, wenn der Benutzer den Befehl ALTER FULLTEXT INDEX mit der Klausel START FULL POPULATION oder START INCREMENTAL POPULATION ausführt.  
  
 STOPLIST [ = ] { OFF | **SYSTEM** | *stoplist_name* }  
 Ordnet dem Index eine Volltext-Stoppliste zu. Der Index wird nicht mit Token aufgefüllt, die Bestandteil der angegebenen Stoppliste sind. Wenn STOPLIST nicht angegeben wird, ordnet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Index die Systemvolltextstoppliste zu.  
  
 OFF  
 Gibt an, dass dem Volltextindex keine Stoppliste zugeordnet wird.  
  
 **SYSTEM**  
 Gibt an, dass die Standardvolltext-Systemstoppliste STOPLIST für diesen Volltextindex verwendet werden soll.  
  
 *stoplist_name*  
 Gibt den Namen der Stoppliste an, die dem Volltextindex zugeordnet werden soll.  
  
 SEARCH PROPERTY LIST [ = ] *property_list_name*  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Ordnet dem Index eine Sucheigenschaftenliste zu.  
  
 OFF  
 Gibt an, dass dem Volltextindex keine Eigenschaftenliste zugeordnet werden soll.  
  
 *property_list_name*  
 Gibt den Namen der Sucheigenschaftenliste an, die dem Volltextindex zugeordnet werden soll.  
  
## <a name="remarks"></a>Remarks  
 Weitere Informationen zu Volltextindizes finden Sie unter [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md).  
  
 Für **xml**-Spalten können Sie einen Volltextindex erstellen, mit dem der Inhalt der XML-Elemente indiziert, das XML-Markup jedoch ignoriert wird. Attributwerte werden volltextindiziert, sofern es sich nicht um numerische Werte handelt. Elementtags werden als Tokenbegrenzungen verwendet. Wohlgeformte XML- oder HTML-Dokumente und -Fragmente in mehreren Sprachen werden unterstützt. Weitere Informationen finden Sie unter [Verwenden der Volltextsuche mit XML-Spalten](../../relational-databases/xml/use-full-text-search-with-xml-columns.md).  
  
 Es ist empfehlenswert, als Indexschlüsselspalte einen Integer-Datentyp zu verwenden. Auf diese Weise kann die Ausführungszeit der Abfragen optimiert werden.  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>Interaktionen zwischen der Änderungsnachverfolgung und dem Parameter NO POPULATION  
 Ob der Volltextindex aufgefüllt wird, hängt davon ab, ob die Änderungsnachverfolgung aktiviert wurde und WITH NO POPULATION in der ALTER FULLTEXT INDEX-Anweisung angegeben ist. In der folgenden Tabelle wird das Ergebnis ihrer Interaktion zusammengefasst.  
  
|Änderungsnachverfolgung|WITH NO POPULATION|Ergebnis|  
|---------------------|------------------------|------------|  
|Nicht aktiviert|Nicht angegeben|Der Index wird vollständig aufgefüllt.|  
|Nicht aktiviert|Specified|Der Index wird nicht aufgefüllt, bevor eine Anweisung ALTER FULLTEXT INDEX...START POPULATION ausgegeben wird.|  
|Aktiviert|Specified|Ein Fehler wird ausgelöst, und der Index wird nicht geändert.|  
|Aktiviert|Nicht angegeben|Der Index wird vollständig aufgefüllt.|  
  
 Weitere Informationen zum Auffüllen von Volltextindizes finden Sie unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer müssen über die REFERENCES-Berechtigung für den Volltextkatalog und die ALTER-Berechtigung für die Tabelle oder indizierte Sicht verfügen oder Mitglied der festen Serverrolle sysadmin oder der festen Datenbankrollen db_owner bzw. db_ddladmin sein.  
  
 Wenn SET STOPLIST angegeben wird, muss der Benutzer die REFERENCES-Berechtigung für die angegebene Stoppliste haben. Der Besitzer der STOPLIST kann diese Berechtigung gewähren.  
  
> [!NOTE]  
>  Der public-Datenbankrolle wird für die Standardstoppliste, die mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeliefert wird, die REFERENCE-Berechtigung gewährt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-unique-index-a-full-text-catalog-and-a-full-text-index"></a>A. Erstellen eines eindeutigen Indexes, eines Volltextkatalogs und eines Volltextindexes  
 Im folgenden Beispiel wird ein eindeutiger Index für die Spalte `JobCandidateID` der `HumanResources.JobCandidate`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Beispieldatenbank erstellt. Im Beispiel wird dann der Standardvolltextkatalog `ft` erstellt. Im Beispiel wird schließlich mit dem `Resume`-Katalog und der Systemstoppliste ein Volltextindex in der Spalte `ft` erstellt.  
  
```  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH STOPLIST = SYSTEM;  
GO  
```  
  
### <a name="b-creating-a-full-text-index-on-several-table-columns"></a>B. Erstellen eines Volltextindexes für mehrere Tabellenspalten  
 Im folgenden Beispiel wird ein Volltextkatalog, `production_catalog`, in der `AdventureWorks`-Beispieldatenbank erstellt. Im Beispiel wird dann ein Volltextindex erstellt, der diesen neuen Katalog verwendet. Der Volltextindex befindet sich in den `ReviewerName`-, `EmailAddress`- und `Comments`-Spalten der `Production.ProductReview`-Tabelle. Im Beispiel wird für jede Spalte die LCID für Englisch `1033` angegeben. Dies entspricht der Sprache der Daten in den Spalten. Dieser Volltextindex verwendet einen vorhandenen eindeutigen Schlüsselindex, `PK_ProductReview_ProductReviewID`. Wie empfohlen befindet sich dieser Indexschlüssel in einer ganzzahligen Spalte, `ProductReviewID`.  
  
```  
CREATE FULLTEXT CATALOG production_catalog;  
GO  
CREATE FULLTEXT INDEX ON Production.ProductReview  
 (   
  ReviewerName  
     Language 1033,  
  EmailAddress  
     Language 1033,  
  Comments   
     Language 1033       
 )   
  KEY INDEX PK_ProductReview_ProductReviewID   
      ON production_catalog;   
GO  
```  
  
### <a name="c-creating-a-full-text-index-with-a-search-property-list-without-populating-it"></a>C. Erstellen eines Volltextindexes mit einer Sucheigenschaftenliste ohne Auffüllen  
 Im folgenden Beispiel wird ein Volltextindex für die Spalten `Title`, `DocumentSummary` und `Document` der `Production.Document`-Tabelle erstellt. Im Beispiel wird die LCID für Englisch, `1033`, angegeben. Dies entspricht der Sprache der Daten in der Spalte. Dieser Volltextindex verwendet den Standardvolltextkatalog und den vorhandenen eindeutigen Schlüsselindex, `PK_Document_DocumentID`. Wie empfohlen befindet sich dieser Indexschlüssel in einer ganzzahligen Spalte, `DocumentID`.  
  
 Das Beispiel zeigt die SYSTEM-Stoppliste an. Außerdem wird eine Sucheigenschaftenliste angegeben: `DocumentPropertyList`. Ein Beispiel, in dem diese Eigenschaftenliste erstellt wird, finden Sie unter [PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
 Im Beispiel wird angegeben, dass die Änderungsnachverfolgung ohne Auffüllung deaktiviert ist. Im Beispiel wird eine ALTER FULLTEXT INDEX-Anweisung verwendet, um außerhalb der Spitzenbetriebszeiten eine vollständige Auffüllung mit dem neuen Index zu beginnen und die automatische Änderungsnachverfolgung zu aktivieren.  
  
```  
CREATE FULLTEXT INDEX ON Production.Document  
  (   
  Title  
      Language 1033,   
  DocumentSummary  
      Language 1033,   
  Document   
      TYPE COLUMN FileExtension  
      Language 1033   
  )  
  KEY INDEX PK_Document_DocumentID  
          WITH STOPLIST = SYSTEM, SEARCH PROPERTY LIST = DocumentPropertyList, CHANGE_TRACKING OFF, NO POPULATION;  
   GO  
```  
  
 Der Index wird später zu einem Zeitpunkt mit wenig Datenverkehr aufgefüllt:  
  
```  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [Volltextsuche](../../relational-databases/search/full-text-search.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
