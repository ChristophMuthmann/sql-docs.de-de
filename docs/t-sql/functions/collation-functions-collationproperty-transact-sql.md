---
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/24/2017
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
- COLLATIONPROPERTY_TSQL
- COLLATIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], properties
- COLLATIONPROPERTY function
ms.assetid: f5029e74-a1db-4f69-b0f5-5ee920c3311d
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 76baefbaf0fc156d782c705e8a81683770bedc68
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="collation-functions---collationproperty-transact-sql"></a>Sortierungsfunktionen: COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt die Eigenschaft einer angegebenen Sortierung in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>Argumente  
*collation_name*  
Der Name der Sortierung. *collation_name* ist vom Datentyp **nvarchar(128)** und verfügt nicht über einen Standardwert.
  
*property*  
Die Eigenschaft der Sortierung. *property* ist vom Datentyp **varchar(128)**. Die folgenden Werte sind möglich:
  
|Eigenschaftenname|Description|  
|---|---|
|**CodePage**|Nicht-Unicode-Codepage der Sortierung. Informationen zum Übersetzen dieser Werte und zu ihren Zeichenzuordnungen finden Sie unter [Appendix G DBCS/Unicode Mapping Tables (Anhang G: DBCS/Tabellen zur Unicode-Zuordnung)](https://msdn.microsoft.com/en-us/library/cc194886.aspx) und [Appendix H Code Pages (Anhang H: Codeseiten)](https://msdn.microsoft.com/en-us/library/cc195051.aspx).|  
|**LCID**|Windows-LCID der Sortierung. Informationen zum Übersetzen dieser Werte erhalten Sie unter [LCID Structure (LCID-Struktur)](https://msdn.microsoft.com/en-us/library/cc233968.aspx). Sie müssen jedoch zunächst eine Konvertierung in **varbinary** vornehmen.|  
|**ComparisonStyle**|Die Windows-Vergleichsart der Sortierung. Gibt 0 (null) für binäre Sortierungen zurück. Sowohl (\_BIN) als auch (\_BIN2) werden ebenfalls zurückgegeben, wenn alle Eigenschaften als sensibel eingestuft sind. Bitmaskenwerte:<br /><br /> Groß-/Kleinschreibung ignorieren: 1<br /><br /> Akzente ignorieren: 2<br /><br /> Kana ignorieren: 65536<br /><br /> Breite ignorieren: 131072<br /><br /> Hinweis: Die Option „Variierungswahlzeichen“ (\_VSS) ist in diesem Wert nicht widergespiegelt, obwohl sie Auswirkungen auf das Vergleichsverhalten hat.|  
|**Version**|Die Version der Sortierung, abgeleitet vom Versionsfeld der Sortierungs-ID. Gibt einen ganzzahligen Wert zwischen 0 und 3 zurück.<br /><br /> Sortierungen, in deren Namen die Zahl 140 enthalten ist, geben 3 zurück.<br /><br /> Sortierungen, in deren Namen die Zahl 100 enthalten ist, geben 2 zurück.<br /><br /> Sortierungen, in deren Namen die Zahl 90 enthalten ist, geben 1 zurück.<br /><br /> Alle anderen Sortierungen geben 0 zurück.|  
  
## <a name="return-types"></a>Rückgabetypen
**sql_variant**
  
## <a name="examples"></a>Beispiele  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>Siehe auch
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  

