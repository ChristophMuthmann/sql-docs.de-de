---
title: Sp_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_columns_TSQL
- sp_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns
ms.assetid: 2dec79cf-2baf-4c0f-8cbb-afb1a8654e1e
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7ea208a7c7c5c1cb969bfa556a5be27b32e5a856
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="spcolumns-transact-sql"></a>sp_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Spalteninformationen für die angegebenen, in der aktuellen Umgebung abfragbaren Objekte zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_columns [ @table_name = ] object  
     [ , [ @table_owner = ] owner ]   
     [ , [ @table_qualifier = ] qualifier ]   
     [ , [ @column_name = ] column ]   
     [ , [ @ODBCVer = ] ODBCVer ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@table_name=**] *object*  
 Der Name des Objekts zur Rückgabe von Kataloginformationen. *Objekt* kann eine Tabelle, Sicht oder ein anderes Objekt mit den Spalten z. B. Tabellenwertfunktionen. *Objekt* ist **nvarchar(384)**, hat keinen Standardwert. Mustervergleiche mit Platzhalterzeichen werden unterstützt.  
  
 [ **@table_owner****=**] *owner*  
 Ist der Objektbesitzer des Objekts zur Rückgabe von Kataloginformationen. *Besitzer* ist **nvarchar(384)**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden unterstützt. Wenn *Besitzer* nicht angegeben wird, gelten die Standardregeln für die Sichtbarkeit von Objekt des zugrunde liegenden DBMS.  
  
 Wenn der aktuelle Benutzer ein Objekt mit dem angegebenen Namen besitzt, werden die Spalten dieses Objekts zurückgegeben. Wenn *Besitzer* nicht angegeben wird und der aktuelle Benutzer besitzt nicht die ein Objekt mit dem angegebenen *Objekt*, **Sp_columns** sucht nach einem Objekt mit dem angegebenen  *Objekt* gehören dem Datenbankbesitzer. Sofern ein solches Objekt vorhanden ist, werden dessen Spalten zurückgegeben.  
  
 [ **@table_qualifier****=**] *qualifier*  
 Der Name des Objektqualifizierers. *qualifier* ist vom Datentyp **sysname**und hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Objekte (*Qualifizierer***.*** Besitzer***.*** Namen*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Datenbanknamen dar. Bei einigen anderen Produkten stellt sie den Servernamen der Datenbankumgebung für das Objekt dar.  
  
 [ **@column_name=**] *column*  
 Eine einzelne Spalte, die verwendet wird, wenn nur eine Spalte mit Kataloginformationen benötigt wird. *Spalte* ist **nvarchar(384)**, hat den Standardwert NULL. Wenn *Spalte* ist nicht angegeben ist, werden alle Spalten zurückgegeben. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *Spalte* dar, den Namen der Spalte in der **"syscolumns"** Tabelle. Mustervergleiche mit Platzhalterzeichen werden unterstützt. Für eine optimale Interoperabilität sollte der Gatewayclient nur einen SQL-92-Standardmustervergleich voraussetzen (die Platzhalterzeichen % und _).  
  
 [ **@ODBCVer=**] *ODBCVer*  
 Ist die Version von ODBC, der verwendet wird. *ODBCVer* ist **Int**, Standardwert ist 2. Dieser gibt ODBC, Version 2, an. Gültige Werte sind 2 oder 3. Informationen zu den verhaltensunterschieden zwischen den Versionen 2 und 3, finden Sie in der **SQLColumns** Spezifikation.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
 Die **Sp_columns** Katalogversion der gespeicherten Prozedur entspricht **SQLColumns** in ODBC. Die zurückgegebenen Ergebnisse sind sortiert, indem **TABLE_QUALIFIER**, **TABLE_OWNER**, und **TABLE_NAME**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Objektqualifizierername. Dieses Feld kann den Wert NULL annehmen.|  
|**TABLE_OWNER**|**sysname**|Objektbesitzername. Dieses Feld gibt immer einen Wert zurück.|  
|**TABLE_NAME**|**sysname**|Objektname. Dieses Feld gibt immer einen Wert zurück.|  
|**COLUMN_NAME**|**sysname**|Name der Spalte für jede Spalte von der **TABLE_NAME** zurückgegeben. Dieses Feld gibt immer einen Wert zurück.|  
|**DATA_TYPE**|**smallint**|Ganzzahligen Code für ODBC-Datentyp. Wenn dies einen-Datentyp, der ein ODBC-Datentyp zugeordnet werden kann ist, ist der Wert NULL. Den Namen des systemeigenen Datentyps wird zurückgegeben, der **TYPE_NAME** Spalte.|  
|**TYPE_NAME**|**sysname**|Die Zeichenfolge, die den Datentyp darstellt. Den Datentypnamen stellt das zugrunde liegende DBMS bereit.|  
|**PRECISION**|**int**|Die Anzahl von signifikanten Stellen. Der Rückgabewert für die **Genauigkeit** Spalte hat die Basis 10.|  
|**LENGTH**|**int**|Die Übertragungsgröße der Daten. <sup>1</sup>|  
|**SKALIERUNG**|**smallint**|Die Anzahl der Ziffern rechts vom Dezimalzeichen|  
|**RADIX**|**smallint**|Die Basis für numerische Datentypen.|  
|**NULLABLE**|**smallint**|Gibt die NULL-Zulässigkeit an.<br /><br /> 1 = NULL ist möglich<br /><br /> 0 = NOT NULL|  
|**"HINWEISE"**|**varchar(254)**|Dieses Feld gibt immer NULL zurück.|  
|**COLUMN_DEF**|**nvarchar(4000)**|Standardwert der Spalte|  
|**SQL_DATA_TYPE**|**smallint**|Der Wert des SQL-Datentyps, wie er im TYPE-Feld des Deskriptors angezeigt wird. Diese Spalte ist identisch mit der **DATA_TYPE** Spalte, mit Ausnahme der **"DateTime"** und SQL-92 **Intervall** Datentypen. Diese Spalte gibt immer einen Wert zurück.|  
|**SQL_DATETIME_SUB**|**smallint**|Untertypcode für **"DateTime"** und SQL-92 **Intervall** Datentypen. Bei allen anderen Datentypen gibt diese Spalte NULL zurück.|  
|**CHAR_OCTET_LENGTH**|**int**|Die maximale Länge (in Byte) einer Spalte eines Zeichendatentyps oder eines ganzzahligen Datentyps. Für alle anderen Datentypen gibt diese Spalte NULL zurück.|  
|**ORDINAL_POSITION**|**int**|Die Position einer Spalte innerhalb des Objekts. Die erste Spalte im Objekt hat den Wert 1. Diese Spalte gibt immer einen Wert zurück.|  
|**IS_NULLABLE**|**varchar(254)**|Die NULL-Zulässigkeit einer Spalte innerhalb des Objekts. Die NULL-Zulässigkeit wird gemäß den ISO-Regeln bestimmt. Ein DBMS nach ISO SQL kann keine leere Zeichenfolge zurückgeben.<br /><br /> YES = Spalte kann NULL-Werte enthalten.<br /><br /> NO = Spalte kann keine NULL-Werte enthalten.<br /><br /> Die Spalte gibt eine leere Zeichenfolge zurück, wenn die NULL-Zulässigkeit unbekannt ist.<br /><br /> Der zurückgegebene Wert für diese Spalte unterscheidet sich von den Rückgabewert für die **NULLABLE** Spalte.|  
|**SS_DATA_TYPE**|**tinyint**|Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp, der von erweiterten gespeicherten Prozeduren verwendet wird. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
  
 <sup>1</sup> Weitere Informationen finden Sie in der Microsoft ODBC-Dokumentation.  
  
## <a name="permissions"></a>Berechtigungen  
 Benötigt SELECT- und VIEW DEFINITION-Berechtigungen für das Schema an.  
  
## <a name="remarks"></a>Hinweise  
 **Sp_columns** erfüllt die Anforderungen für Begrenzungsbezeichner. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Spalteninformationen für die angegebene Tabelle zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 Im folgenden Beispiel werden die Spalteninformationen für die angegebene Tabelle zurückgegeben.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [Gespeicherte Prozeduren für Kataloginformationen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


