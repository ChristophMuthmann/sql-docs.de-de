---
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f47c45f892618120b06a17f45f5d3155e092987a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="collation-functions---collationproperty-transact-sql"></a>Sortierungsfunktionen - COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt die Eigenschaft einer angegebenen Sortierung in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>Argumente  
*Sortierungsname*  
Der Name der Sortierung. *Collation_name* ist **vom Datentyp nvarchar(128)**, und hat keinen Standardwert.
  
*Eigenschaft*  
Die Eigenschaft der Sortierung. *Eigenschaft* ist **varchar(128)**, und kann einen der folgenden Werte sein:
  
|Eigenschaftsname|Description|  
|---|---|
|**CodePage**|Nicht-Unicode-Codepage der Sortierung. Finden Sie unter [Anhang G DBCS/Unicode-Zuordnen von Systemtabellen](https://msdn.microsoft.com/en-us/library/cc194886.aspx) und [Anhang H-Codepages](https://msdn.microsoft.com/en-us/library/cc195051.aspx) übersetzen diese Werte und finden Sie unter zuordnungsangaben Zeichen.|  
|**LCID**|Windows-LCID der Sortierung. Finden Sie unter [LCID-Struktur](https://msdn.microsoft.com/en-us/library/cc233968.aspx) übersetzen Sie diese Werte (Sie müssen zum Konvertieren **Varbinary** erste).|  
|**ComparisonStyle**|Windows-Vergleichsart der Sortierung. Gibt 0 für alle binären Sortierungen sowohl (\_"bin") und (\_BIN2), sowie wenn alle Eigenschaften und Kleinschreibung beachtet werden. Bitmaskenwerte:<br /><br /> Groß-/Kleinschreibung ignorieren: 1<br /><br /> Akzente ignorieren: 2<br /><br /> Kana ignorieren: 65536<br /><br /> Breite ignorieren: 131072<br /><br /> Hinweis: Obwohl er wirkt sich auf das Vergleichsverhalten die Variation Selektor unterschieden (\_VSS) Option ist in diesem Wert nicht dargestellt.|  
|**Version**|Die Version der Sortierung, abgeleitet vom Versionsfeld der Sortierungs-ID. Gibt einen ganzzahligen Wert zwischen 0 und 3.<br /><br /> Sortierungen mit "140" im Namen geben 3 zurück.<br /><br /> Sortierungen mit "100" im Namen geben 2 zurück.<br /><br /> Sortierungen mit "90" im Namen geben 1 zurück.<br /><br /> Alle anderen Sortierungen geben 0 zurück.|  
  
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
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>Siehe auch
[sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  

