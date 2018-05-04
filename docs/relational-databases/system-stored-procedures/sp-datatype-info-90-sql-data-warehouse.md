---
title: sp_datatype_info_90 (SQL Datawarehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1d043964-dc6e-4c3e-ab61-bc444d5e25ae
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a633d790503357edef72b8c26b85515dd043c556
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdatatypeinfo90-sql-data-warehouse"></a>sp_datatype_info_90 (SQL Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gibt Informationen zu den von der aktuellen Umgebung unterstützten Datentypen zurück.  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_datatype_info_90 [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@data_type=** ] *data_type*  
 Die Codenummer für den angegebenen Datentyp. Um eine Liste aller Datentypen abzurufen, lassen Sie diesen Parameter weg. *Data_type* ist **Int**, hat den Standardwert 0.  
  
 [ **@ODBCVer=** ] *odbc_version*  
 Die verwendete ODBC-Version. *Odbc_version* ist **"tinyint"**, Standardwert ist 2.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|Der DBMS-abhängige Datentyp.|  
|DATA_TYPE|**smallint**|Der Code für den ODBC-Datentyp, dem alle Spalten dieses Datentyps zugeordnet sind.|  
|PRECISION|**int**|Die maximale Genauigkeit des Datentyps bezüglich der Datenquelle. NULL wird für Datentypen zurückgegeben, auf die die Genauigkeit nicht anwendbar ist. Der Rückgabewert für die PRECISION-Spalte hat die Basis 10.|  
|LITERAL_PREFIX|**Varchar (** 32 **)**|Das oder die Zeichen, die einer Konstante vorangestellt werden. Angenommen, ein einfaches Anführungszeichen (**"**) bei Zeichentypen und 0 X bei Binärtypen.|  
|LITERAL_SUFFIX|**Varchar (** 32 **)**|Das oder die Zeichen, die eine Konstante beenden. Angenommen, ein einfaches Anführungszeichen (**"**) bei Zeichentypen und keine Anführungszeichen bei Binärtypen.|  
|CREATE_PARAMS|**Varchar (** 32 **)**|Die Beschreibung der Erstellungsparameter für diesen Datentyp. Beispielsweise **decimal** ist "Precision, Scale", **"float"** NULL ist, und **Varchar** "max_length".|  
|NULLABLE|**smallint**|Gibt die NULL-Zulässigkeit an.<br /><br /> 1 = Lässt NULL-Werte zu.<br /><br /> 0 = NULL ist nicht zulässig.|  
|CASE_SENSITIVE|**smallint**|Gibt die Unterscheidung nach Groß-/Kleinschreibung an.<br /><br /> 1 = Bei allen Spalten dieses Typs wird nach Groß-/Kleinschreibung unterschieden (für Sortierungen).<br /><br /> 0 = Bei allen Spalten dieses Typs wird nicht nach Groß-/Kleinschreibung unterschieden.|  
|SEARCHABLE|**smallint**|Gibt die Suchfunktion des Spaltentyps an:<br /><br /> 1 = Kann nicht durchsucht werden.<br /><br /> 2 = Durchsuchbar mit LIKE<br /><br /> 3 = Durchsuchbar mit WHERE<br /><br /> 4 = Durchsuchbar mit WHERE oder LIKE|  
|UNSIGNED_ATTRIBUTE|**smallint**|Gibt das Vorzeichen des Datentyps an.<br /><br /> 1 = Datentyp ohne Vorzeichen<br /><br /> 0 = Datentyp mit Vorzeichen|  
|MONEY|**smallint**|Gibt an, die **Money** -Datentyp.<br /><br /> 1 = **Money** -Datentyp.<br /><br /> 0 = keine **Money** -Datentyp.|  
|AUTO_INCREMENT|**smallint**|Gibt die automatische Inkrementierung an.<br /><br /> 1 = Automatische Inkrementierung<br /><br /> 0 = Keine automatische Inkrementierung<br /><br /> NULL = Attribut nicht zutreffend.<br /><br /> Eine Anwendung kann zwar Werte in eine Spalte einfügen, die dieses Attribut aufweist, kann jedoch die Werte in der Spalte nicht aktualisieren. Mit Ausnahme von der **Bit** Datentyp AUTO_INCREMENT ist nur für Datentypen, die der genauen numerischen oder ungefähren numerischen Daten-Kategorien angehören.|  
|LOCAL_TYPE_NAME|**sysname**|Lokalisierte Version des von der Datenquelle abhängigen Datentypamens. Beispielsweise lautet DECIMAL auf Französisch DECIMALE. NULL wird zurückgegeben, wenn ein lokalisierter Name nicht von der Datenquelle unterstützt wird.|  
|MINIMUM_SCALE|**smallint**|Die minimalen Dezimalstellen des Datentyps bezüglich der Datenquelle. Weist ein Datentyp Feste Dezimalstellen, enthalten die Spalten MINIMUM_SCALE und MAXIMUM_SCALE dieser Wert auf. NULL wird zurückgegeben, wenn Dezimalstellen auf den Datentyp nicht anwendbar sind.|  
|MAXIMUM_SCALE|**smallint**|Die maximalen Dezimalstellen des Datentyps bezüglich der Datenquelle. Wenn die maximale Dezimalstellen für die Datenquelle nicht separat definiert, aber es und stattdessen definiert wurde, wurden dass Sie der maximalen Genauigkeit entsprechen, enthält diese Spalte den gleichen Wert wie die PRECISION-Spalte.|  
|SQL_DATA_TYPE|**smallint**|Der Wert des SQL-Datentyps, wie er im TYPE-Feld des Deskriptors angezeigt wird. Diese Spalte entspricht der DATA_TYPE-Spalte mit Ausnahme der **"DateTime"** und ANSI **Intervall** Datentypen. Dieses Feld gibt immer einen Wert zurück.|  
|SQL_DATETIME_SUB|**smallint**|**"DateTime"** oder ANSI **Intervall** subcode, wenn der Wert SQL_DATETIME SQL_DATETIME oder SQL_INTERVAL ist. Bei allen Datentypen außer **"DateTime"** und ANSI **Intervall**, dieses Feld ist NULL.|  
|NUM_PREC_RADIX|**int**|Die Anzahl der Bits oder Stellen für das Berechnen der höchsten Zahl, die eine Spalte enthalten kann. Wenn es sich um einen ungefähren numerischen Datentyp handelt, enthält diese Spalte den Wert 2 für mehrere Bits. Bei exakten numerischen Datentypen enthält diese Spalte den Wert 10 für mehrere Dezimalstellen. Andernfalls ist diese Spalte NULL. Aus der Kombination von Genauigkeit und Basis kann die Anwendung die höchste Zahl berechnen, die die Spalte enthalten kann.|  
|INTERVAL_PRECISION|**smallint**|Wert der Genauigkeit für anführenden Intervallwert Wenn *Data_type* ist **Intervall**; andernfalls NULL.|  
|USERTYPE|**smallint**|**Usertype** Wert aus der Systypes-Tabelle.|  
  
## <a name="remarks"></a>Hinweise  
 Sp_datatype_info ist gleichbedeutend mit SQLGetTypeInfo in ODBC. Die zurückgegebenen Ergebnisse sind sortiert nach DATA_TYPE und dann nach wie stark die Daten mit dem entsprechenden ODBC SQL-Datentyp.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 Das folgende Beispiel ruft Informationen für die **Sysname** und **Nvarchar** Datentypen durch Angabe der *Data_type* Wert `-9`.  
  
```  
USE master;  
GO  
EXEC sp_datatype_info_90 -9;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für SQL Data Warehouse](../../relational-databases/system-stored-procedures/sql-data-warehouse-stored-procedures.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  

