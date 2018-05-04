---
title: Sp_statistics (Transact-SQL) | Microsoft Docs
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
- sp_statistics_TSQL
- sp_statistics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_statistics
ms.assetid: 0bb6495f-258a-47ec-9f74-fd16671d23b8
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 74dbd18e87e0e39bfd65daca4c3d1107de97c464
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spstatistics-transact-sql"></a>sp_statistics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Liste mit allen Indizes und Statistiken einer angegebenen Tabelle oder indizierten Sicht zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_statistics [ @table_name = ] 'table_name'    
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
     [ , [ @accuracy = ] 'accuracy' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@table_name=** ] **"***Table_name***"**  
 Gibt die Tabelle zum Zurückgeben von Kataloginformationen an. *TABLE_NAME* ist **Sysname**, hat keinen Standardwert. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt.  
  
 [  **@table_owner=** ] **"***Besitzer***"**  
 Der Name des Tabellenbesitzers für die Tabelle zum Zurückgeben von Kataloginformationen. *Table_owner* ist **Sysname**, hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden nicht unterstützt. Wenn *Besitzer* nicht angegeben ist, werden die Standardregeln für die Sichtbarkeit von Tabellen des zugrunde liegenden DBMS angewendet.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden die Indizes einer Tabelle zurückgegeben, wenn der aktuelle Benutzer diese Tabelle mit dem angegebenen Namen besitzt. Wenn *Besitzer* nicht angegeben wird und der aktuelle Benutzer keine Tabelle mit dem angegebenen *Namen*, sucht Sie dieses Verfahren für eine Tabelle mit dem angegebenen *Namen* im Besitz der der Datenbankbesitzer. Sofern eine solche Tabelle vorhanden ist, werden die Indizes dieser Tabelle zurückgegeben.  
  
 [  **@table_qualifier=** ] **"***Qualifizierer***"**  
 Der Name des Tabellenqualifizierers. *qualifier* ist vom Datentyp **sysname**und hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen (*Qualifizierer ***.*** Besitzer ***.*** Namen*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entspricht dieser Parameter dem Datenbanknamen. Bei anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
 [  **@index_name=** ] **"***Index_name***"**  
 Ist der Indexname. *Index_name* ist **Sysname**, hat den Standardwert %. Mustervergleiche mit Platzhalterzeichen werden unterstützt.  
  
 [  **@is_unique=** ] **"***Is_unique***"**  
 Ist, ob nur eindeutige Indizes (Wenn **Y**) zurückgegeben werden sollen. *Is_unique* ist **char(1)**, hat den Standardwert **N**.  
  
 [  **@accuracy=** ] **"***Genauigkeit***"**  
 Die Ebene der Kardinalität und Seitengenauigkeit für Statistiken. *Genauigkeit* ist **char(1)**, hat den Standardwert **Q**. Geben Sie **E** um sicherzustellen, dass die Statistiken aktualisiert werden, sodass Kardinalität und Seiten richtig sind.  
  
 Der Wert **E** (SQL_ENSURE) weist den Treiber zum unbedingten Abrufen der Statistiken.  
  
 Der Wert **Q** (SQL_QUICK) weist den Treiber zum Abrufen der Kardinalität und Seiten nur dann, wenn sie ohne weiteres auf dem Server verfügbar sind. In diesem Fall wird vom Treiber nicht sichergestellt, dass die Werte aktuell sind. Anwendungen, die nach dem "Open Group"-Standard geschrieben wurden, rufen immer das SQL_QUICK-Verhalten von Treibern ab, die mit ODBC 3.x kompatibel sind.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|Tabelle der Name des Prozedurqualifizierers. Diese Spalte kann NULL enthalten.|  
|**TABLE_OWNER**|**sysname**|Name des Tabellenbesitzers. Diese Spalte gibt immer einen Wert zurück.|  
|**TABLE_NAME**|**sysname**|Tabellenname. Diese Spalte gibt immer einen Wert zurück.|  
|**NON_UNIQUE**|**smallint**|NICHT NULL IST.<br /><br /> 0 = Eindeutig<br /><br /> 1 = Nicht eindeutig|  
|**INDEX_QUALIFIER**|**sysname**|Der Name des Indexbesitzers. Verschiedene DBMS-Produkte ermöglichen neben dem Tabellenbesitzer auch anderen Benutzern das Erstellen von Indizes. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], diese Spalte ist immer identisch **TABLE_NAME**.|  
|**INDEX_NAME**|**sysname**|Der Name des Indexes. Diese Spalte gibt immer einen Wert zurück.|  
|**TYPE**|**smallint**|Diese Spalte gibt immer einen Wert zurück:<br /><br /> 0 = Statistiken für eine Tabelle<br /><br /> 1 = In einem Cluster gruppiert<br /><br /> 2 = Hash<br /><br /> 3 = nicht gruppiert|  
|**SEQ_IN_INDEX**|**smallint**|Position der Spalte im Index|  
|**COLUMN_NAME**|**sysname**|Spaltenname für jede Spalte von der **TABLE_NAME** zurückgegeben. Diese Spalte gibt immer einen Wert zurück.|  
|**COLLATION**|**char(1)**|Die in der Sortierung verwendete Reihenfolge. Mögliche Werte sind:<br /><br /> A = Aufsteigend<br /><br /> D = Absteigend<br /><br /> NULL = Nicht zutreffend|  
|**KARDINALITÄT**|**int**|Anzahl der Zeilen in der Tabelle oder der eindeutigen Werte im Index|  
|**SEITEN**|**int**|Anzahl der Seiten, die zum Speichern des Indexes oder der Tabelle benötigt werden|  
|**FILTER_CONDITION**|**varchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt keinen Wert zurück.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Die Indizes im Resultset angezeigt werden, in aufsteigender Reihenfolge nach den Spalten **NON_UNIQUE**, **Typ**, **INDEX_NAME**, und **SEQ_IN_INDEX**.  
  
 Die Indexart Gruppiert bezeichnet einen Index, der sich dadurch auszeichnet, dass die in der Tabelle gespeicherten Daten in der durch den Index vorgegebenen Reihenfolge abgelegt sind. Dies entspricht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gruppierte Indizes.  
  
 Beim Indextyp Hash ist die Suche nach genauen Übereinstimmungen oder Wertebereichen zwar zulässig, bei Mustervergleichen wird der Index jedoch nicht verwendet.  
  
 **Sp_statistics** entspricht **SQLStatistics** in ODBC. Die zurückgegebenen Ergebnisse sind sortiert, indem **NON_UNIQUE**, **Typ**, **INDEX_QUALIFIER**, **INDEX_NAME**, und **SEQ_IN_ INDEX**. Weitere Informationen finden Sie unter der [ODBC API Reference](http://go.microsoft.com/fwlink/?LinkId=68323).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="example-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiel: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Das folgende Beispiel gibt Informationen zu den `DimEmployee` Tabelle.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_statistics DimEmployee;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für Kataloginformationen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

