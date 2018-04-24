---
title: INDEXPROPERTY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- INDEXPROPERTY
- INDEXPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INDEXPROPERTY function
- indexes [SQL Server], viewing
- indexes [SQL Server], properties
ms.assetid: 998d5788-4871-44a8-8125-0d9390868b84
caps.latest.revision: 56
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b632f46999c70ec1d4653def8ec2a29112435ce9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="indexproperty-transact-sql"></a>INDEXPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den benannten Index- oder Statistikeigenschaftswert für eine angegebene Tabellenidentifikationsnummer (Tabellen-ID), den angegebenen Index- oder Statistiknamen und den angegebenen Eigenschaftsnamen zurück. Gibt für XML-Indizes NULL zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
INDEXPROPERTY ( object_ID , index_or_statistics_name , property )   
```  
  
## <a name="arguments"></a>Argumente  
 *object_ID*  
 Ein Ausdruck, der die Objekt-ID der Tabelle oder indizierten Sicht enthält, für die Indexeigenschafteninformationen bereitgestellt werden sollen. *object_id* ist vom Datentyp **int**.  
  
 *index_or_statistics_name*  
 Ein Ausdruck, der den Namen des Index oder der Statistik enthält, für den bzw. die Eigenschafteninformationen zurückgegeben werden sollen. *index_or_statistics_name* entspricht **nvarchar(128)**.  
  
 *property*  
 Ein Ausdruck, der den Namen der zurückzugebenden Datenbankeigenschaft enthält. *property* ist vom Datentyp **varchar(128)**. Die folgenden Werte sind möglich:  
  
> [!NOTE]  
>  Wenn nicht anders angegeben, wird NULL zurückgegeben, wenn *property* kein gültiger Eigenschaftsname ist, *object_ID* keine gültige Objekt-ID ist, *object_ID* ein nicht unterstützter Objekttyp für die angegebene Eigenschaft ist oder der Aufrufer nicht über die Berechtigung zum Anzeigen der Metadaten des Objekts verfügt.  
  
|Eigenschaft|Description|value|  
|--------------|-----------------|-----------|  
|**IndexDepth**|Schachtelungstiefe des Indexes.|Anzahl von Indexebenen.<br /><br /> NULL = Ungültiger XML-Index oder ungültige Eingabe.|  
|**IndexFillFactor**|Der beim Erstellen oder letzten Neuerstellen des Indexes verwendete Füllfaktor.|Füllfaktor|  
|**IndexID**|Index-ID des Indexes einer angegebenen Tabelle oder indizierten Sicht.|Index-ID|  
|**IsAutoStatistics**|Statistiken wurden durch die Option AUTO_CREATE_STATISTICS von ALTER DATABASE erzeugt.|1 = True<br /><br /> 0 = False oder XML-Index.|  
|**IsClustered**|Der Index ist gruppiert.|1 = True<br /><br /> 0 = False oder XML-Index.|  
|**IsDisabled**|Der Index ist deaktiviert.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsFulltextKey**|Index ist der Schlüssel für die Volltext- und semantische Indizierung für eine Tabelle.|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False oder XML-Index.<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsHypothetical**|Der Index ist hypothetisch und kann nicht direkt als Datenzugriffspfad verwendet werden. Hypothetische Indizes enthalten Statistiken auf Spaltenebene und werden vom Datenbankmodul-Optimierungsratgeber verwaltet und verwendet.|1 = True<br /><br /> 0 = False oder XML-Index<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsPadIndex**|Der Index gibt den Speicherplatz an, der auf jedem inneren Knoten freigelassen werden soll.|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False oder XML-Index.|  
|**IsPageLockDisallowed**|Der Wert für Seitensperren wird von der Option ALLOW_PAGE_LOCKS von ALTER INDEX festgelegt.|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Seitensperren sind nicht zulässig.<br /><br /> 0 = Seitensperren sind zulässig.<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsRowLockDisallowed**|Der Wert für Zeilensperren wird von der Option ALLOW_ROW_LOCKS von ALTER INDEX festgelegt.|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Zeilensperren sind nicht zulässig.<br /><br /> 0 = Zeilensperren sind zulässig.<br /><br /> NULL = Eingabe ist nicht gültig.|  
|**IsStatistics**|*index_or_statistics_name* stellt Statistiken dar, die durch die CREATE STATISTICS-Anweisung oder die AUTO_CREATE_STATISTICS-Option von ALTER DATABASE erstellt werden.|1 = True<br /><br /> 0 = False oder XML-Index.|  
|**IsUnique**|Der Index ist eindeutig.|1 = True<br /><br /> 0 = False oder XML-Index.|  
|**IsColumnstore**|Index ist ein speicheroptimierter xVelocity-columnstore-Index.|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False|  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt.  
  
 Ein Benutzer kann nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. INDEXPROPERTY, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Werte für die Eigenschaften **IsClustered**, **IndexDepth** und **IndexFillFactor** für den `PK_Employee_BusinessEntityID`-Index der `Employee`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
SELECT   
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IsClustered')AS [Is Clustered],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexDepth') AS [Index Depth],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexFillFactor') AS [Fill Factor];  
  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
Is Clustered Index Depth Fill Factor   
------------ ----------- -----------   
1            2           0  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 Im folgenden Beispiel werden die Eigenschaften von einem der Indizes der `FactResellerSales`-Tabelle überprüft.  
  
```  
-- Uses AdventureWorks  
  
SELECT   
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsClustered') AS [Is Clustered],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsColumnstore') AS [Is Columnstore Index],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IndexFillFactor') AS [Fill Factor];  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [Statistiken](../../relational-databases/statistics/statistics.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

