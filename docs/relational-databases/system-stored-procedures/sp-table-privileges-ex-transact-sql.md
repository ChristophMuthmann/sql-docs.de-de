---
title: Sp_table_privileges_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_table_privileges_ex
- sp_table_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges_ex
ms.assetid: b58d4a07-5c40-4f17-b66e-6d6b17188dda
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2ad7d7746c1bd436a6473d7d25921c7a3437e75a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sptableprivilegesex-transact-sql"></a>sp_table_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Privileginformationen zu der angegebenen Tabelle vom angegebenen Verbindungsserver zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_table_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
     [ , [@fUsePattern =] 'fUsePattern']  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@table_server =** ] **"***Table_server***"**  
 Der Name des Verbindungsservers, für den Informationen zurückgegeben werden sollen. *Table_server* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@table_name =** ] **"***Table_name***"**]  
 Der Name der Tabelle, für die Tabellenprivileginformationen bereitgestellt werden sollen. *TABLE_NAME* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@table_schema =** ] **"***Table_schema***"**  
 Das Tabellenschema. Dies ist in einigen DBMS-Umgebungen der Tabellenbesitzer. *TABLE_SCHEMA* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@table_catalog =** ] **"***" TABLE_CATALOG "***"**  
 Der Name der Datenbank, in der angegebenen *Table_name* befindet. *"TABLE_CATALOG"* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@fUsePattern =**] **"***fUsePattern***"**  
 Bestimmt, ob die Zeichen '_', '%', '[', und ']' als Platzhalterzeichen interpretiert werden. Gültige Werte sind 0 (Mustervergleich ist deaktiviert) und 1 (Mustervergleich ist aktiviert). *fUsePattern* ist vom Datentyp **bit**. Der Standardwert ist 1.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Tabelle der Name des Prozedurqualifizierers. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*Qualifizierer ***.*** Besitzer ***.*** Namen*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt diese Spalte den Datenbanknamen dar. Bei anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar. Dieses Feld kann den Wert NULL annehmen.|  
|**NACH "TABLE_SCHEM"**|**sysname**|Name des Tabellenbesitzers. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], diese Spalte dar, der Name des Datenbankbenutzers, der die Tabelle erstellt. Dieses Feld gibt immer einen Wert zurück.|  
|**TABLE_NAME**|**sysname**|Tabellenname. Dieses Feld gibt immer einen Wert zurück.|  
|**GRANTOR**|**sysname**|Datenbank-Benutzername, der für diese Berechtigungen erteilt hat **TABLE_NAME** aufgeführten **Empfänger**. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], diese Spalte entspricht immer der **TABLE_OWNER**. Dieses Feld gibt immer einen Wert zurück. Darüber hinaus kann die GRANTOR-Spalte entweder der Datenbankbesitzer sein (**TABLE_OWNER**) oder einen Benutzer, denen der Datenbankbesitzer die Berechtigung mithilfe der WITH GRANT OPTION-Klausel in der GRANT-Anweisung erteilt.|  
|**EMPFÄNGER**|**sysname**|Datenbank-Benutzername, die gewährten Berechtigungen für dieses **TABLE_NAME** aufgeführte **GRANTOR**. Dieses Feld gibt immer einen Wert zurück.|  
|**BERECHTIGUNG**|**Varchar (** 32 **)**|Eine der verfügbaren Tabellenberechtigungen. Tabellenberechtigungen können folgende Werte annehmen bzw. auch andere Werte, die von der Datenquelle bei der Definition der Implementierung unterstützt werden.<br /><br /> Wählen Sie = **Empfänger** können Daten für eine oder mehrere Spalten abrufen.<br /><br /> INSERT = **Empfänger** kann Daten für mindestens eine der Spalten für neue Zeilen bereitstellen.<br /><br /> UPDATE = **Empfänger** kann vorhandene Daten für mindestens eine der Spalten ändern.<br /><br /> Löschen Sie = **Empfänger** kann Zeilen aus der Tabelle entfernen.<br /><br /> REFERENCES = **Empfänger** können auf eine Spalte in einer Fremdschlüsseltabelle in einem Primärschlüssel/Fremdschlüssel-Beziehung verweisen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Primär-/Fremdschlüsselbeziehungen mithilfe von Tabelleneinschränkungen definiert.<br /><br /> Der Gültigkeitsbereich der Aktion übergeben, um die **Empfänger** durch ein bestimmtes Tabellenprivileg erteilte Aktionsbereich ist datenquellenabhängig. Z. B. die UPDATE-Berechtigung aktivieren konnte die **Empfänger** so aktualisieren Sie alle Spalten in einer Tabelle für eine Datenquelle und nur die Spalten für die die **GRANTOR** UPDATE-Berechtigung für eine andere Datenquelle hat.|  
|**IS_GRANTABLE**|**Varchar (** 3 **)**|Gibt an, ob die **Empfänger** ist zulässig, anderen Benutzern Berechtigungen erteilen. Dies wird häufig als "Berechtigung mit Recht zum Erteilen" bezeichnet. Dieses Feld kann die Werte YES, NO oder NULL annehmen. Ein unbekannter Wert oder NULL-Wert verweist auf eine Datenquelle, für die die "Berechtigung mit Recht zum Erteilen" nicht anwendbar ist.|  
  
## <a name="remarks"></a>Hinweise  
 Die zurückgegebenen Ergebnisse sind sortiert, indem **TABLE_QUALIFIER**, **TABLE_OWNER**, **TABLE_NAME**, und **Berechtigung**.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel werden die Privileginformationen zu Tabellen zurückgegeben, deren Namen in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank des angegebenen Verbindungsservers `Product` mit `Seattle1` beginnen. ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird als Verbindungsserver angenommen).  
  
```  
EXEC sp_table_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Product%',   
   @table_schema = 'Production',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_column_privileges_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-ex-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Verteilte Abfragen, gespeicherten Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
