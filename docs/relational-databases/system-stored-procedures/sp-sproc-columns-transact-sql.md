---
title: Sp_sproc_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
- sp_sproc_columns
- sp_sproc_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_sproc_columns
ms.assetid: 62c18c21-35c5-4772-be0d-ffdcc19c97ab
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f176d3f6be7f48920bee35ceae38977e6b947623
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spsproccolumns-transact-sql"></a>sp_sproc_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Spalteninformationen für eine einzelne gespeicherte Prozedur oder benutzerdefinierte Funktion in der aktuellen Umgebung zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_sproc_columns [[@procedure_name = ] 'name']   
    [ , [@procedure_owner = ] 'owner']   
    [ , [@procedure_qualifier = ] 'qualifier']   
    [ , [@column_name = ] 'column_name']  
    [ , [@ODBCVer = ] 'ODBCVer']  
    [ , [@fUsePattern = ] 'fUsePattern']  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@procedure_name =** ] **'***name***'**  
 Der Name der Prozedur zur Rückgabe von Kataloginformationen. *Namen* ist **Nvarchar (**390**)**, hat den Standardwert %, womit alle Tabellen in der aktuellen Datenbank. Mustervergleiche mit Platzhalterzeichen werden unterstützt.  
  
 [  **@procedure_owner =**] **"***Besitzer***"**  
 Der Name des Besitzers der Prozedur. *Besitzer*ist **Nvarchar (**384**)**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden unterstützt. Wenn *owner* nicht angegeben wird, gelten die Standardregeln für die Sichtbarkeit von Prozeduren des zugrunde liegenden DBMS.  
  
 Wenn der aktuelle Benutzer eine Prozedur mit dem angegebenen Namen besitzt, werden Informationen zu dieser Prozedur zurückgegeben. Wenn *Besitzer*nicht angegeben wird und der aktuelle Benutzer besitzt eine Prozedur mit dem angegebenen Namen nicht **Sp_sproc_columns** sucht nach einer Prozedur mit dem angegebenen Namen, die dem Datenbankbesitzer gehört. Sofern die Prozedur vorhanden ist, werden Information zu deren Spalten zurückgegeben.  
  
 [  **@procedure_qualifier =**] **"***Qualifizierer***"**  
 Der Name des Prozedurqualifizierers. *qualifier* ist vom Datentyp **sysname**und hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*qualifier.owner.name*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entspricht dieser Parameter dem Datenbanknamen. Bei anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
 [  **@column_name =**] **"***Column_name***"**  
 Eine einzelne Spalte, und wird verwendet, wenn nur eine Spalte mit Kataloginformationen gewünscht wird. *Column_name* ist **Nvarchar (**384**)**, hat den Standardwert NULL. Wenn *Column_name* wird weggelassen wird, werden alle Spalten zurückgegeben. Mustervergleiche mit Platzhalterzeichen werden unterstützt. Für eine optimale Interoperabilität sollte der Gatewayclient nur einen ISO-Standardmustervergleich voraussetzen (die Platzhalterzeichen % und _).  
  
 [  **@ODBCVer =**] **"***ODBCVer***"**  
 Ist die Version von ODBC verwendet wird. *ODBCVer* ist **Int**, Standardwert 2 gibt ODBC, Version 2.0. Weitere Informationen zu den Unterschieden zwischen ODBC, Version 2.0 und ODBC, Version 3.0, finden Sie in der ODBC **SQLProcedureColumns** Spezifikation für ODBC, Version 3.0  
  
 [  **@fUsePattern =**] **"***fUsePattern***"**  
 Bestimmt, ob der Unterstrich (_), das Prozentzeichen (%) und eckige Klammern ([ ]) als Platzhalterzeichen interpretiert werden. Gültige Werte sind 0 (Mustervergleich ist deaktiviert) und 1 (Mustervergleich ist aktiviert). *fUsePattern* ist vom Datentyp **bit**. Der Standardwert ist 1.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|Der Name des Prozedurqualifizierers. Diese Spalte kann NULL enthalten.|  
|**PROCEDURE_OWNER**|**sysname**|Der Name des Prozedurbesitzers. Diese Spalte gibt immer einen Wert zurück.|  
|**PROCEDURE_NAME**|**Nvarchar (**134**)**|Der Name der Prozedur. Diese Spalte gibt immer einen Wert zurück.|  
|**COLUMN_NAME**|**sysname**|Spaltenname für jede Spalte von der **TABLE_NAME** zurückgegeben. Diese Spalte gibt immer einen Wert zurück.|  
|**COLUMN_TYPE**|**smallint**|Dieses Feld gibt immer einen Wert zurück:<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE|  
|**DATA_TYPE**|**smallint**|Ein ganzzahliger Code für einen ODBC-Datentyp. Wenn dieser Datentyp keinem ISO-Datentyp zugeordnet werden kann, lautet der Wert NULL. Den Namen des systemeigenen Datentyps wird zurückgegeben, der **TYPE_NAME** Spalte.|  
|**TYPE_NAME**|**sysname**|Die Zeichenfolgendarstellung des Datentyps. Es handelt sich um die DBMS-spezifische Darstellung des Datentypnamens.|  
|**PRECISION**|**int**|Die Anzahl von signifikanten Stellen. Der Rückgabewert für die **Genauigkeit** Spalte hat die Basis 10.|  
|**LENGTH**|**int**|Die Übertragungsgröße der Daten.|  
|**SKALIERUNG**|**smallint**|Die Anzahl der Ziffern rechts vom Dezimalzeichen|  
|**BASIS**|**smallint**|Die Basis für die Darstellung numerischer Datentypen.|  
|**NULL-WERTE ZULÄSST**|**smallint**|Gibt die NULL-Zulässigkeit an:<br /><br /> 1 = Datentyp mit NULL-Werten ist zulässig.<br /><br /> 0 = NULL-Werte sind nicht zulässig.|  
|**"HINWEISE"**|**Varchar (**254**)**|Beschreibung der Prozedurspalte. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt für diese Spalte keinen Wert zurück.|  
|**COLUMN_DEF**|**Nvarchar (**4000**)**|Standardwert der Spalte|  
|**SQL_DATA_TYPE**|**smallint**|Wert des SQL-Datentyps, wie in der **Typ** Feld des Deskriptors. Diese Spalte ist identisch mit der **DATA_TYPE** Spalte, mit Ausnahme der **"DateTime"** und ISO **Intervall** Datentypen. Diese Spalte gibt immer einen Wert zurück.|  
|**SQL_DATETIME_SUB**|**smallint**|Die **"DateTime"** ISO **Intervall** subcode, wenn der Wert der **SQL_DATA_TYPE** ist **SQL_DATETIME** oder **SQL_INTERVAL**. Bei allen Datentypen außer **"DateTime"** und ISO **Intervall**, dieses Feld ist NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Maximale Länge in Bytes, der eine **Zeichen** oder **binäre** -Datentypspalte. Bei allen anderen Datentypen gibt diese Spalte einen NULL-Wert zurück.|  
|**ORDINAL_POSITION**|**int**|Die Position einer Spalte innerhalb der Tabelle. Die erste Spalte in der Tabelle ist "1". Diese Spalte gibt immer einen Wert zurück.|  
|**IS_NULLABLE**|**varchar(254)**|NULL-Zulässigkeit der Spalte in der Tabelle. Die NULL-Zulässigkeit wird gemäß den ISO-Regeln bestimmt. Ein DBMS nach ISO kann keine leere Zeichenfolge zurückgeben.<br /><br /> YES, wenn die Spalte NULL-Werte einschließen kann. NO, wenn die Spalte keine NULL-Werte einschließen kann.<br /><br /> Die Spalte gibt eine leere Zeichenfolge zurück, wenn die NULL-Zulässigkeit unbekannt ist.<br /><br /> Der für diese Spalte zurückgegebene Wert ist ein anderer als der für die NULLABLE-Spalte zurückgegebene Wert.|  
|**SS_DATA_TYPE**|**tinyint**|Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp, der von erweiterten gespeicherten Prozeduren verwendet wird. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_sproc_columns** entspricht **SQLProcedureColumns** in ODBC. Die zurückgegebenen Ergebnisse sind sortiert, indem **PROCEDURE_QUALIFIER**, **PROCEDURE_OWNER**, **PROCEDURE_NAME**, und die Reihenfolge, die die Parameter in der Prozedur angezeigt werden. Definition.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für Kataloginformationen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
