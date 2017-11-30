---
title: Sp_columns_ex (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_columns_ex
- sp_columns_ex_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_columns_ex
ms.assetid: c12ef6df-58c6-4391-bbbf-683ea874bd81
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 90ba287e14dc19afef8e19be65c81337c653fe48
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spcolumnsex-transact-sql"></a>sp_columns_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Spalteninformationen (eine Zeile pro Spalte) für die angegebenen Verbindungsservertabellen zurück. **Sp_columns_ex** gibt Spalteninformationen für die nur die spezifische Spalte zurück, wenn *Spalte* angegeben ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_columns_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@table_server =** ] **"***Table_server***"**  
 Der Name des Verbindungsservers, für den Spalteninformationen zurückgegeben werden sollen. *Table_server* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@table_name =** ] **"***Table_name***"**  
 Der Name der Tabelle, für die Spalteninformationen zurückgegeben werden sollen. *TABLE_NAME* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@table_schema =** ] **"***Table_schema***"**  
 Der Schemaname der Tabelle, für die Spalteninformationen zurückgegeben werden sollen. *TABLE_SCHEMA* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@table_catalog =** ] **"***" TABLE_CATALOG "***"**  
 Der Katalogname der Tabelle, für die Spalteninformationen zurückgegeben werden sollen. *"TABLE_CATALOG"* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@column_name =** ] **"***Spalte***"**  
 Der Name der Datenbankspalte, für die Informationen bereitgestellt werden sollen. *Spalte* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@ODBCVer =** ] **"***ODBCVer***"**  
 Ist die Version von ODBC, der verwendet wird. *ODBCVer* ist **Int**, Standardwert ist 2. Dieser gibt ODBC, Version 2, an. Gültige Werte sind 2 oder 3. Informationen zu den Verhaltensunterschieden zwischen den Versionen 2 und 3 finden Sie in der SQLColumns-Spezifikation von ODBC.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Der Name des Qualifizierers für die Tabelle oder Sicht. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*Qualifizierer***.** *Besitzer***.** *Namen*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte dem Datenbanknamen dar. Bei anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar. Dieses Feld kann den Wert NULL annehmen.|  
|**NACH "TABLE_SCHEM"**|**sysname**|Der Name des Besitzers der Tabelle oder Sicht. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Namen des Datenbankbenutzers dar, der die Tabelle erstellt hat. Dieses Feld gibt immer einen Wert zurück.|  
|**TABELLENNAME**|**sysname**|Der Name der Tabelle oder Sicht. Dieses Feld gibt immer einen Wert zurück.|  
|**SPALTENNAME**|**sysname**|Name der Spalte für jede Spalte von der **TABLE_NAME** zurückgegeben. Dieses Feld gibt immer einen Wert zurück.|  
|**DATA_TYPE**|**smallint**|Ein Wert für eine ganze Zahl, der den ODBC-Datentypbezeichnern entspricht. Bei einem Datentyp, der keinem ODBC-Datentyp zugeordnet werden kann, wird der Wert NULL zurückgegeben. Den Namen des systemeigenen Datentyps wird zurückgegeben, der **TYPE_NAME** Spalte.|  
|**TYPE_NAME**|**Varchar (**13**)**|Die Zeichenfolge, die den Datentyp darstellt. Den Datentypnamen stellt das zugrunde liegende DBMS bereit.|  
|**COLUMN_SIZE**|**int**|Die Anzahl von signifikanten Stellen. Der Rückgabewert für die **Genauigkeit** Spalte hat die Basis 10.|  
|**BUFFER_LENGTH**|**int**|Die Übertragungsgröße der Daten.1|  
|**DECIMAL_DIGITS**|**smallint**|Die Anzahl der Ziffern rechts vom Dezimalzeichen|  
|**NUM_PREC_RADIX**|**smallint**|Stellt die Basis für numerische Datentypen.|  
|**NULL-WERTE ZULÄSST**|**smallint**|Gibt die NULL-Zulässigkeit an.<br /><br /> 1 = NULL ist möglich<br /><br /> 0 = NOT NULL|  
|**"HINWEISE"**|**Varchar (**254**)**|Dieses Feld gibt immer NULL zurück.|  
|**COLUMN_DEF**|**Varchar (**254**)**|Standardwert der Spalte|  
|**SQL_DATA_TYPE**|**smallint**|Der Wert des SQL-Datentyps, wie er im TYPE-Feld des Deskriptors angezeigt wird. Diese Spalte ist identisch mit der **DATA_TYPE** Spalte, mit Ausnahme der **"DateTime"** und SQL-92 **Intervall** Datentypen. Diese Spalte gibt immer einen Wert zurück.|  
|**NOCH SQL_DATETIME_SUB**|**smallint**|Untertypcode für **"DateTime"** und SQL-92 **Intervall** Datentypen. Bei allen anderen Datentypen gibt diese Spalte NULL zurück.|  
|**CHAR_OCTET_LENGTH**|**int**|Die maximale Länge (in Byte) einer Spalte eines Zeichendatentyps oder eines ganzzahligen Datentyps. Für alle anderen Datentypen gibt diese Spalte NULL zurück.|  
|**ORDINAL_POSITION**|**int**|Die Position einer Spalte innerhalb der Tabelle. Die erste Spalte in der Tabelle ist "1". Diese Spalte gibt immer einen Wert zurück.|  
|**IS_NULLABLE**|**Varchar (**254**)**|NULL-Zulässigkeit der Spalte in der Tabelle. Die NULL-Zulässigkeit wird gemäß den ISO-Regeln bestimmt. Ein DBMS nach ISO SQL kann keine leere Zeichenfolge zurückgeben.<br /><br /> YES = Spalte kann NULL-Werte enthalten.<br /><br /> NO = Spalte kann keine NULL-Werte enthalten.<br /><br /> Die Spalte gibt eine leere Zeichenfolge zurück, wenn die NULL-Zulässigkeit unbekannt ist.<br /><br /> Der zurückgegebene Wert für diese Spalte unterscheidet sich von den Rückgabewert für die **NULLABLE** Spalte.|  
|**SS_DATA_TYPE**|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp, der von erweiterten gespeicherten Prozeduren verwendet wird.|  
  
 Weitere Informationen finden Sie in der Microsoft ODBC-Dokumentation.  
  
## <a name="remarks"></a>Hinweise  
 **Sp_columns_ex** wird ausgeführt, indem das COLUMNS-Schemarowset, von der **IDBSchemaRowset** -Schnittstelle des OLE DB-Anbieters entspricht *Table_server*. Die *Table_name*, *Table_schema*, *"TABLE_CATALOG"*, und *Spalte* Parameter übergeben werden, auf diese Schnittstelle, um die Zeilen einzuschränken zurückgegeben.  
  
 **Sp_columns_ex** gibt ein leeres Resultset, wenn der OLE DB-Anbieter des angegebenen Verbindungsservers das COLUMNS-Rowset der nicht unterstützt die **IDBSchemaRowset** Schnittstelle.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="remarks"></a>Hinweise  
 **Sp_columns_ex** erfüllt die Anforderungen für Begrenzungsbezeichner. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Datentyp der `JobTitle`-Spalte der `HumanResources.Employee`-Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank auf dem `Seattle1`-Verbindungsserver zurückgegeben.  
  
```  
EXEC sp_columns_ex 'Seattle1',   
   'Employee',   
   'HumanResources',   
   'AdventureWorks2012',   
   'JobTitle';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [Sp_foreignkeys &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [Sp_indexes &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [Sp_primarykeys &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [Sp_tables_ex &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [Sp_table_privileges &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
