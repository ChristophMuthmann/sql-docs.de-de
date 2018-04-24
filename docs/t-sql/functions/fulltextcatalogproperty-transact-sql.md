---
title: FULLTEXTCATALOGPROPERTY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FULLTEXTCATALOGPROPERTY_TSQL
- FULLTEXTCATALOGPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- full-text catalogs [SQL Server], properties
- FULLTEXTCATALOGPROPERTY function
- status information [SQL Server], full-text catalogs
ms.assetid: f841dc79-2044-4863-aff0-56b8bb61f250
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7ae96c00e4eb4c558868ebec8f939eefd777065d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="fulltextcatalogproperty-transact-sql"></a>FULLTEXTCATALOGPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu Volltextkatalog-Eigenschaften in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FULLTEXTCATALOGPROPERTY ('catalog_name' ,'property')  
```  
  
## <a name="arguments"></a>Argumente  
  
> [!NOTE]  
>  Die folgenden Eigenschaften werden in einem künftigen Release von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr unterstützt: **LogSize** und **PopulateStatus**. Vermeiden Sie die Verwendung dieser Eigenschaften in Neuentwicklungen, und planen Sie die Änderung von Anwendungen, die diese Eigenschaften derzeit verwenden.  
  
 *catalog_name*  
 Ein Ausdruck, der den Namen des Volltextkatalogs enthält.  
  
 *property*  
 Ein Ausdruck, der den Namen der Volltext-Katalogeigenschaft enthält. In der folgenden Tabelle finden Sie eine Liste der Eigenschaften und eine Beschreibung der zurückgegebenen Informationen.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**AccentSensitivity**|Einstellung für die Unterscheidung nach Akzent.<br /><br /> 0 = Keine Unterscheidung nach Akzent<br /><br /> 1 = Unterscheidung nach Akzent|  
|**IndexSize**|Logische Größe des Volltextkatalogs in Megabyte (MB). Enthält die Größe des semantischen Schlüsselausdrucks und von Dokumentähnlichkeitsindizes.<br /><br /> Weitere Informationen finden Sie unter "Hinweise" weiter unten in diesem Thema.|  
|**ItemCount**|Anzahl der indizierten Elemente einschließlich aller Volltext-, Schlüsselausdruck- und Dokumentähnlichkeitsindizes in einem Katalog.|  
|**LogSize**|Wird nur aus Gründen der Abwärtskompatibilität unterstützt. Gibt immer 0 zurück.<br /><br /> Größe (in Bytes) der kombinierten Gruppe von Fehlerprotokollen, die mit einem Volltextkatalog des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search-Diensts verbunden sind.|  
|**MergeStatus**|Gibt an, ob eine Masterzusammenführung ausgeführt wird.<br /><br /> 0 = Masterzusammenführung befindet sich nicht in Verarbeitung<br /><br /> 1 = Masterzusammenführung befindet sich in Verarbeitung|  
|**PopulateCompletionAge**|Anzahl von Sekunden, die zwischen dem 01.01.1990, 00:00:00 Uhr, und der Beendigung des letzten Auffüllens des Volltextindex verstrichen sind.<br /><br /> Wird nur für vollständige und inkrementelle Durchforstungsvorgänge aktualisiert. Gibt 0 zurück, wenn keine Auffüllung aufgetreten ist.|  
|**PopulateStatus**|0 = Im Leerlauf.<br /><br /> 1 = Vollständiges Auffüllen wird ausgeführt<br /><br /> 2 = Angehalten<br /><br /> 3 = Gedrosselt<br /><br /> 4 = Wird wiederhergestellt<br /><br /> 5 = Herunterfahren<br /><br /> 6 = Inkrementelles Auffüllen wird ausgeführt<br /><br /> 7 = Index wird erstellt<br /><br /> 8 = Datenträger voll Angehalten.<br /><br /> 9 = Änderungsprotokollierung|  
|**UniqueKeyCount**|Anzahl der eindeutigen Schlüssel im Volltextkatalog.|  
|**ImportStatus**|Gibt an, ob der Volltextkatalog importiert wird.<br /><br /> 0 = Der Volltextkatalog wird nicht importiert.<br /><br /> 1 = Der Volltextkatalog wird importiert.|  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] kann ein Benutzer nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. FULLTEXTCATALOGPROPERTY, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [sp_help_fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 FULLTEXTCATALOGPROPERTY ('*catalog_name*','**IndexSize**') prüft wie in [sys.fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md) dargestellt nur Fragmente mit dem Status 4 oder 6. Diese Fragmente sind ein Teil des logischen Index. Daher gibt die **IndexSize**-Eigenschaft nur die logische Indexgröße zurück. Während eines Indexmerge könnte die tatsächliche Indexgröße jedoch doppelt so groß sein wie die logische Größe. Um die tatsächliche Größe zu ermitteln, die von einem Volltextindex während eines Merge beansprucht wird, verwenden Sie die gespeicherte Systemprozedur [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md). Diese Prozedur prüft alle Fragmente, die einem Volltextindex zugeordnet sind. Wenn Sie das Wachstum der Volltextkatalogdatei einschränken und nicht genügend Speicherplatz für den Mergeprozess zulassen, schlägt die Volltextauffüllung möglicherweise fehl. In diesem Fall gibt FULLTEXTCATALOGPROPERTY ('catalog_name', 'IndexSize') 0 zurück, und der folgende Fehler wird in das Volltextprotokoll geschrieben:  
  
 `Error: 30059, Severity: 16, State: 1. A fatal error occurred during a full-text population and caused the population to be cancelled. Population type is: FULL; database name is FTS_Test (id: 13); catalog name is t1_cat (id: 5); table name t1 (id: 2105058535). Fix the errors that are logged in the full-text crawl log. Then, resume the population. The basic Transact-SQL syntax for this is: ALTER FULLTEXT INDEX ON table_name RESUME POPULATION.`  
  
 Anwendungen sollten die **PopulateStatus**-Eigenschaft nicht in einer Schleife auf Leerlauf überprüfen (Leerlauf bedeutet hier, dass das Auffüllen beendet wurde). Dadurch werden CPU-Zyklen von der Datenbank und von Volltextsuchprozessen abgezogen und Timeoutfehler verursacht. Darüber hinaus ist es normalerweise besser, die entsprechende **PopulateStatus**-Eigenschaft auf Tabellenebene und **TableFullTextPopulateStatus** in der OBJECTPROPERTYEX-Systemfunktion zu überprüfen. Diese und andere neue Volltexteigenschaften in OBJECTPROPERTYEX stellen Informationen mit höherer Granularität zur Volltextindizierung von Tabellen bereit. Weitere Informationen finden Sie unter [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Anzahl der volltextindizierten Elemente in einem Volltextkatalog mit dem Namen `Cat_Desc` zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT fulltextcatalogproperty('Cat_Desc', 'ItemCount');  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Metadata Functions &#40;Transact-SQL&#41; (Metadatenfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
  
  
