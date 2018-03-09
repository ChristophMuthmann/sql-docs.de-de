---
title: Sp_pkeys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_pkeys
- sp_pkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_pkeys
ms.assetid: e614c75d-847b-4726-8f6f-cd18de688eda
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bbf8a10a560bcf058f30281ceebe34a47689e3b1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sppkeys-transact-sql"></a>sp_pkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Primärschlüsselinformationen für eine einzelne Tabelle in der aktuellen Umgebung zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_pkeys [ @table_name = ] 'name'       
    [ , [ @table_owner = ] 'owner' ]   
    [ , [ @table_qualifier = ] 'qualifier' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @table_name=] '*Namen*"  
 Ist die Tabelle, für die Informationen zurückgegeben werden sollen. *Namen* ist **Sysname**, hat keinen Standardwert. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt.  
  
 [ @table_owner=] '*Besitzer*"  
 Gibt den Besitzer der angegebenen Tabelle an. *Besitzer* ist **Sysname**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt. Wenn *Besitzer* nicht angegeben ist, werden die Standardregeln für die Sichtbarkeit von Tabellen des zugrunde liegenden DBMS angewendet.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die Spalten einer Tabelle zurückgegeben, wenn der aktuelle Benutzer diese Tabelle mit dem angegebenen Namen besitzt. Wenn die *Besitzer* nicht angegeben wird und der aktuelle Benutzer keine Tabelle mit dem angegebenen *Namen*, diese Prozedur sucht für eine Tabelle mit dem angegebenen *Namen* im Besitz der der Datenbankbesitzer. Falls vorhanden, werden die Spalten dieser Tabelle zurückgegeben.  
  
 [ @table_qualifier=] '*Qualifizierer*"  
 Der Tabellenqualifizierer. *qualifier* ist vom Datentyp **sysname**und hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*Qualifizierer***.** *Besitzer***.** *Namen*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Datenbanknamen dar. Bei einigen anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|Der Name des Qualifizierers der Tabelle. Dieses Feld kann den Wert NULL annehmen.|  
|TABLE_OWNER|**sysname**|Der Name des Besitzers der Tabelle. Dieses Feld gibt immer einen Wert zurück.|  
|TABLE_NAME|**sysname**|Der Name der Tabelle. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Tabellennamen dar, der in der sysobjects-Tabelle angegeben ist. Dieses Feld gibt immer einen Wert zurück.|  
|COLUMN_NAME|**sysname**|Der Name der Spalte. Er wird für jede Spalte von TABLE_NAME zurückgegeben. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Spaltennamen dar, der in der sys.columns-Tabelle angegeben ist. Dieses Feld gibt immer einen Wert zurück.|  
|KEY_SEQ|**smallint**|Die Sequenznummer der Spalte in einem mehrspaltigen Primärschlüssel.|  
|PK_NAME|**sysname**|Der Primärschlüsselbezeichner. Gibt NULL zurück, wenn nicht auf die Datenquelle anwendbar|  
  
## <a name="remarks"></a>Hinweise  
 sp_pkeys gibt Informationen zu den Spalten zurück, die mit einer PRIMARY KEY-Einschränkung explizit definiert werden. Da nicht alle Systeme explizit benannte Primärschlüssel unterstützen, bestimmt die Gateway-Implementierung, was als Primärschlüssel gilt. Beachten Sie, dass sich der Begriff Primärschlüssel auf einen logischen Primärschlüssel für eine Tabelle bezieht. Es wird davon ausgegangen, dass für jeden als logischen Primärschlüssel aufgeführten Schlüssel ein eindeutiger Index definiert ist. Dieser eindeutige Index wird auch in sp_statistics zurückgegeben.  
  
 Die gespeicherte Prozedur Sp_pkeys entspricht in ODBC SQLPrimaryKeys. Die zurückgegebenen Ergebnisse werden folgendermaßen sortiert: TABLE_QUALIFIER, TABLE_OWNER, TABLE_NAME und KEY_SEQ.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Primärschlüssel für die `HumanResources.Department`-Tabelle in der `AdventureWorks2012`-Datenbank abgerufen.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_pkeys @table_name = N'Department'  
    ,@table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel wird der Primärschlüssel für die `DimAccount`-Tabelle in der `AdventureWorksPDW2012`-Datenbank abgerufen. Es gibt keine Zeilen gibt an, dass die Tabelle nicht über einen Primärschlüssel verfügt.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_pkeys @table_name = N'DimAccount;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalog gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

