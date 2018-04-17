---
title: sp_special_columns_100 (SQL Datawarehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
ms.assetid: 5774fadc-77cc-46f8-8f9f-a0f9efe95e21
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f63087431cfca9578d4af19c7a213a08806f97c8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spspecialcolumns100-sql-data-warehouse"></a>sp_special_columns_100 (SQL Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gibt die optimale Gruppe von Spalten zurück, die eine Zeile in der Tabelle eindeutig identifizieren. Außerdem werden Spalten zurückgegeben, die automatisch aktualisiert werden, wenn ein Wert in der Zeile durch eine Transaktion aktualisiert wird.  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_special_columns_100 [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @qualifier = ] 'qualifier' ]   
     [ , [ @col_type = ] 'col_type' ]   
     [ , [ @scope = ] 'scope' ]  
     [ , [ @nullable = ] 'nullable' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @table_name=] '*Table_name*"  
 Der Name der Tabelle zur Rückgabe von Kataloginformationen. *Namen* ist **Sysname**, hat keinen Standardwert. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt.  
  
 [ @table_owner=] '*Table_owner*"  
 Der Tabellenbesitzer für die Tabelle zum Zurückgeben von Kataloginformationen. *Besitzer* ist **Sysname**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt. Wenn *Besitzer* nicht angegeben ist, werden die Standardregeln für die Sichtbarkeit von Tabellen des zugrunde liegenden DBMS angewendet.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die Spalten einer Tabelle zurückgegeben, wenn der aktuelle Benutzer diese Tabelle mit dem angegebenen Namen besitzt. Wenn *Besitzer* nicht angegeben wird und der aktuelle Benutzer besitzt nicht die eine Tabelle mit dem angegebenen *Namen*, diese Prozedur sucht eine Tabelle mit dem angegebenen *Namen* im Besitz der Datenbank Besitzer. Wenn die Tabelle vorhanden ist, werden dessen Spalten zurückgegeben.  
  
 [ @qualifier=] '*Qualifizierer*"  
 Der Name des Tabellenqualifizierers. *qualifier* ist vom Datentyp **sysname**und hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*qualifier.owner.name*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Datenbanknamen dar. Bei einigen anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
 [ @col_type=] '*Col_type*"  
 Ist der Spaltentyp. *Col_type* ist **Char (**1**)**, hat den Standardwert von r Typ R Gibt die optimale(n) Spalte(n) oder eine Gruppe von Spalten zurück, der durch Aufrufen der entsprechenden Werte die Spalte(n), können Sie für jede Zeile in der angegebenen die Tabelle eindeutig identifiziert werden. Bei einer Spalte kann es sich entweder um eine Pseudospalte handeln, die speziell zu diesem Zweck erstellt wurde, oder um die Spalte(n) eines eindeutigen Index für die Tabelle. Der Typ "V" gibt ggf. die Spalte(n) in der angegebenen Tabelle zurück, die automatisch von der Datenquelle aktualisiert werden, sobald ein Wert in der Zeile durch eine Transaktion aktualisiert wird.  
  
 [ @scope=] '*Bereich*"  
 Der mindestens erforderliche Bereich der ROWID. *Bereich* ist **Char (**1**)**, hat den Standardwert von t Bereich C gibt an, dass die ROWID nur gültig, wenn in dieser Zeile positioniert ist. Der Bereich "T" gibt an, dass die ROWID für die Transaktion gültig ist.  
  
 [ @nullable=] '*NULL-Werte zu*"  
 Gibt an, ob die speziellen Spalten einen NULL-Wert akzeptieren können. *NULL-Werte zulassen* ist **Char (**1**)**, hat den Standardwert + u O gibt spezielle Spalten, die keine null-Werte zulassen. "U" definiert Spalten, die teilweise NULL zulassen.  
  
 [ @ODBCVer=] '*ODBCVer*'  
 Ist die ODBC-Version verwendet wird. *ODBCVer* ist **Int (**4**)**, Standardwert ist 2. Dieser gibt ODBC, Version 2.0, an. Weitere Informationen zu den Unterschieden zwischen ODBC, Version 2.0 und ODBC, Version 3.0 finden Sie unter der ODBC-SQLSpecialColumns-Spezifikation für ODBC, Version 3.0.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|SCOPE|**smallint**|Der Bereich der Zeilen-ID. Kann 0, 1 oder 2 sein. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gibt immer 0 zurück. Dieses Feld gibt immer einen Wert zurück.<br /><br /> 0 = SQL_SCOPE_CURROW. Die Zeilen-ID ist nur garantiert gültig, wenn sie sich in dieser Zeile befindet. Eine spätere erneute Auswahl mit dieser Zeilen-ID gibt möglicherweise keine Zeile zurück, wenn die Zeile durch eine andere Transaktion aktualisiert oder gelöscht wurde.<br /><br /> 1 = SQL_SCOPE_TRANSACTION. Die Zeilen-ID ist für die Dauer der aktuellen Transaktion garantiert gültig.<br /><br /> 2 = SQL_SCOPE_SESSION. Die Zeilen-ID ist für die Dauer der Sitzung garantiert gültig (über Transaktionsgrenzen hinweg).|  
|COLUMN_NAME|**sysname**|Spaltenname für jede Spalte von der *Tabelle*zurückgegeben. Dieses Feld gibt immer einen Wert zurück.|  
|DATA_TYPE|**smallint**|ODBC-SQL-Datentyp.|  
|TYPE_NAME|**sysname**|-Daten der Datenquelle abhängiger Datentypname; beispielsweise **Char**, **Varchar**, **Money**, oder **Text**.|  
|PRECISION|**Int**|Die Genauigkeit der Spalte bezüglich der Datenquelle. Dieses Feld gibt immer einen Wert zurück.|  
|LENGTH|**Int**|Länge in Bytes erforderlich für den Datentyp in seiner binären Form in der Datenquelle, z. B. 10 für **Char (**10**)**, 4 für **Ganzzahl**, und 2 für **"smallint"** .|  
|SCALE|**smallint**|Die Dezimalstellen der Spalte bezüglich der Datenquelle. NULL wird für Datentypen zurückgegeben, auf die Dezimalstellen nicht anwendbar sind.|  
|PSEUDO_COLUMN|**smallint**|Gibt an, ob es sich bei der Spalte um eine Pseudospalte handelt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt immer 1 zurück:<br /><br /> 0 = SQL_PC_UNKNOWN<br /><br /> 1 = SQL_PC_NOT_PSEUDO<br /><br /> 2 = SQL_PC_PSEUDO|  
  
## <a name="remarks"></a>Hinweise  
 Sp_special_columns entspricht SQLSpecialColumns in ODBC. Die zurückgegebenen Ergebnisse sind nach der SCOPE-Spalte geordnet.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 Im folgenden Beispiel werden Informationen zu der Spalte zurückgegeben, die Zeilen in der `FactFinance`-Tabelle eindeutig identifiziert.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_special_columns_100 @table_name = 'FactFinance';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für SQL Data Warehouse](../../relational-databases/system-stored-procedures/sql-data-warehouse-stored-procedures.md)  
  
  

