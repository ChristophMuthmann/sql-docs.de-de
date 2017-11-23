---
title: Sp_fkeys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_fkeys
- sp_fkeys_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_fkeys
ms.assetid: 18110444-d38d-4cff-90d2-d1fc6236668b
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 511266de529055263470af2de8c463369d7f3c6e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spfkeys-transact-sql"></a>sp_fkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt logische Fremdschlüsselinformationen für die aktuelle Umgebung zurück. Diese Prozedur zeigt Fremdschlüsselbeziehungen an, wobei auch deaktivierte Fremdschlüssel berücksichtigt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_fkeys [ @pktable_name = ] 'pktable_name'   
     [ , [ @pktable_owner = ] 'pktable_owner' ]   
     [ , [ @pktable_qualifier = ] 'pktable_qualifier' ]   
     { , [ @fktable_name = ] 'fktable_name' }   
     [ , [ @fktable_owner = ] 'fktable_owner' ]   
     [ , [ @fktable_qualifier = ] 'fktable_qualifier' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @pktable_name=] '*Pktable_name*"  
 Der Name der Tabelle mit dem Primärschlüssel, mit der Kataloginformationen zurückgegeben werden. *Pktable_name* ist **Sysname**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt. Dieser Parameter oder die *Fktable_name* Parameter oder beides müssen angegeben werden.  
  
 [ @pktable_owner=] '*Pktable_owner*"  
 Ist der Name des Besitzers der Tabelle (mit dem Primärschlüssel) verwendet, um Kataloginformationen zurückzugeben. *Pktable_owner* ist **Sysname**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt. Wenn *Pktable_owner* nicht angegeben ist, werden die Standardregeln für die Sichtbarkeit von Tabellen des zugrunde liegenden DBMS angewendet.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bedeutet dies: Wenn der aktuelle Benutzer eine Tabelle mit dem angegebenen Namen besitzt, werden die Spalten dieser Tabelle zurückgegeben. Wenn *Pktable_owner* nicht angegeben wird und der aktuelle Benutzer keine Tabelle mit dem angegebenen *Pktable_name*, die für eine Tabelle mit dem angegebenen sucht *Pktable_name* gehören dem Datenbankbesitzer. Sofern eine solche Tabelle vorhanden ist, werden die Spalten dieser Tabelle zurückgegeben.  
  
 [ @pktable_qualifier =] '*Pktable_qualifier*"  
 Ist der Name des Qualifizierers der Tabelle (mit dem Primärschlüssel). *Pktable_qualifier* ist vom Datentyp Sysname und hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*qualifier.owner.name*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt der Qualifizierer den Datenbanknamen dar. Bei anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
 [ @fktable_name=] '*Fktable_name*"  
 Der Name der Tabelle (mit einem Fremdschlüssel), mit der Kataloginformationen zurückgegeben werden. *Fktable_name* ist vom Datentyp Sysname und hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt. Dieser Parameter oder die *Pktable_name* Parameter oder beides müssen angegeben werden.  
  
 [ @fktable_owner =] '*Fktable_owner*"  
 Der Name des Besitzers der Tabelle (mit einem Fremdschlüssel), mit der Kataloginformationen zurückgegeben werden. *Fktable_owner* ist **Sysname**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt. Wenn *Fktable_owner* nicht angegeben ist, werden die Standardregeln für die Sichtbarkeit von Tabellen des zugrunde liegenden DBMS angewendet.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bedeutet dies: Wenn der aktuelle Benutzer eine Tabelle mit dem angegebenen Namen besitzt, werden die Spalten dieser Tabelle zurückgegeben. Wenn *Fktable_owner* nicht angegeben wird und der aktuelle Benutzer keine Tabelle mit dem angegebenen *Fktable_name*, die für eine Tabelle mit dem angegebenen sucht *Fktable_name* gehören dem Datenbankbesitzer. Sofern eine solche Tabelle vorhanden ist, werden die Spalten dieser Tabelle zurückgegeben.  
  
 [ @fktable_qualifier=] '*Fktable_qualifier*"  
 Ist der Name des Qualifizierers der Tabelle (mit einem Fremdschlüssel). *FKTABLE_QUALIFIER* ist **Sysname**, hat den Standardwert NULL. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt der Qualifizierer den Datenbanknamen dar. Bei anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|PKTABLE_QUALIFIER|**sysname**|Der Name des Qualifizierers der Tabelle (mit dem Primärschlüssel). Dieses Feld kann den Wert NULL annehmen.|  
|PKTABLE_OWNER|**sysname**|Der Name des Besitzers der Tabelle (mit dem Primärschlüssel). Dieses Feld gibt immer einen Wert zurück.|  
|PKTABLE_NAME|**sysname**|Name der Tabelle (mit dem Primärschlüssel). Dieses Feld gibt immer einen Wert zurück.|  
|PKCOLUMN_NAME|**sysname**|Der Name der Primärschlüsselspalten für jede Spalte des zurückgegebenen TABLE_NAME-Werts. Dieses Feld gibt immer einen Wert zurück.|  
|FKTABLE_QUALIFIER|**sysname**|Der Name des Qualifizierers der Tabelle (mit einem Fremdschlüssel). Dieses Feld kann den Wert NULL annehmen.|  
|FKTABLE_OWNER|**sysname**|Der Name des Besitzers der Tabelle (mit einem Fremdschlüssel). Dieses Feld gibt immer einen Wert zurück.|  
|FKTABLE_NAME|**sysname**|Der Name der Tabelle (mit einem Fremdschlüssel). Dieses Feld gibt immer einen Wert zurück.|  
|FKCOLUMN_NAME|**sysname**|Der Name der Fremdschlüsselspalten für jede Spalte des zurückgegebenen TABLE_NAME-Werts. Dieses Feld gibt immer einen Wert zurück.|  
|KEY_SEQ|**smallint**|Die Sequenznummer der Spalte in einem mehrspaltigen Primärschlüssel. Dieses Feld gibt immer einen Wert zurück.|  
|UPDATE_RULE|**smallint**|Die Aktion, die für den Fremdschlüssel ausgeführt wird, wenn es sich bei dem SQL-Vorgang um ein Update handelt.  Mögliche Werte:<br /> 0=CASCADE; kaskadierende Änderungen am Fremdschlüssel.<br /> 1=NO ACTION; keine Änderungen, wenn der Fremdschlüssel vorhanden ist.<br />   2 = Null festlegen <br /> 3 = Standard festlegen |  
|DELETE_RULE|**smallint**|Die Aktion, die für den Fremdschlüssel ausgeführt wird, wenn es sich bei dem SQL-Vorgang um eine Löschung handelt. Mögliche Werte:<br /> 0=CASCADE; kaskadierende Änderungen am Fremdschlüssel.<br /> 1=NO ACTION; keine Änderungen, wenn der Fremdschlüssel vorhanden ist.<br />   2 = Null festlegen <br /> 3 = Standard festlegen |  
|FK_NAME|**sysname**|Der Fremdschlüsselbezeichner. Ist NULL, wenn er auf die Datenquelle nicht anwendbar ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt den Namen der FOREIGN KEY-Einschränkung zurück.|  
|PK_NAME|**sysname**|Der Primärschlüsselbezeichner. Ist NULL, wenn er auf die Datenquelle nicht anwendbar ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt den Namen der PRIMARY KEY-Einschränkung zurück.|  
  
 Die zurückgegebenen Ergebnisse sind nach FKTABLE_QUALIFIER, FKTABLE_OWNER, FKTABLE_NAME und KEY_SEQ sortiert.  
  
## <a name="remarks"></a>Hinweise  
 Eine Anwendungscodierung, die Tabellen mit deaktivierten Fremdschlüsseln enthält, kann folgendermaßen implementiert werden:  
  
-   Deaktivieren Sie bei Verwendung der Tabellen vorübergehend die Überprüfung von Einschränkungen (ALTER TABLE NOCHECK oder CREATE TABLE NOT FOR REPLICATION), und aktivieren Sie sie später wieder.  
  
-   Erzwingen Sie Beziehungen mithilfe von Triggern oder Anwendungscode.  
  
Wenn für die Primärschlüsseltabelle ein Name, für die Fremdschlüsseltabelle jedoch NULL angegeben wurde, gibt sp_fkeys alle Tabellen mit einem Fremdschlüssel für die angegebene Tabelle zurück. Im umgekehrten Fall, d. h., wenn für die Fremdschlüsseltabelle ein Name, für die Primärschlüsseltabelle jedoch NULL angegeben wird, gibt sp_fkeys alle Tabellen zurück, die einen mit der Fremdschlüsseltabelle in Beziehung stehenden Primärschlüssel besitzen.  
  
Die gespeicherte Prozedur Sp_fkeys entspricht SQLForeignKeys in ODBC.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert `SELECT` Berechtigung für das Schema.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Liste der Fremdschlüssel für die `HumanResources.Department`-Tabelle in der `AdventureWorks2012`-Datenbank abgerufen.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_fkeys @pktable_name = N'Department'  
    ,@pktable_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel wird eine Liste der Fremdschlüssel für die `DimDate`-Tabelle in der `AdventureWorksPDW2012`-Datenbank abgerufen. Es werden keine Zeilen zurückgegeben, da [!INCLUDE[ssDW](../../includes/ssdw-md.md)] Fremdschlüssel nicht unterstützt.  
  
```sql  
EXEC sp_fkeys @pktable_name = N'DimDate;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalog gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Sp_pkeys &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-pkeys-transact-sql.md)  
  
  

