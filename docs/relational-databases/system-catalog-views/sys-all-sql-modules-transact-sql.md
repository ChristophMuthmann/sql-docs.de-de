---
title: Sys. all_sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- all_sql_modules_TSQL
- sys.all_sql_modules
- all_sql_modules
- sys.all_sql_modules_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.all_sql_modules catalog view
ms.assetid: 7477a3fe-afb3-44c8-bb2c-c6e1d9bdee6f
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dd4ffb3ff3362ca918d97432f56ff97471d26c7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysallsqlmodules-transact-sql"></a>sys.all_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Vereinigung der **sql_modules** und **Sys. system_sql_modules**.  
  
 Die Sicht gibt eine Zeile für jede systemintern kompilierte, skalare benutzerdefinierte Funktion zurück. Weitere Informationen finden Sie unter [Skalarfunktionen für In-Memory OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die Objekt-ID des enthaltenen Objekts. Ist innerhalb einer Datenbank eindeutig.|  
|**Definition**|**nvarchar(max)**|Der SQL-Text, der dieses Modul definiert.<br /><br /> NULL = Verschlüsselt|  
|**uses_ansi_nulls**|**bit**|Das Modul wurde mit SET ANSI_NULLS ON erstellt.|  
|**uses_quoted_identifier**|**bit**|Das Modul wurde mit SET QUOTED_IDENTIFIER ON erstellt.|  
|**is_schema_bound**|**bit**|Das Modul wurde mit der SCHEMABINDING-Option erstellt.|  
|**uses_database_collation**|**bit**|1 = Die richtige Auswertung der schemagebundenen Moduldefinition ist abhängig von der Standardsortierung der Datenbank; andernfalls ist der Wert 0. Diese Abhängigkeit verhindert die Änderung der Standardsortierung der Datenbank.|  
|**is_recompiled**|**bit**|Die Prozedur wurde mit der WITH RECOMPILE-Option erstellt.|  
|**null_on_null_input**|**bit**|Das Modul wurde so deklariert, dass auf eine NULL-Eingabe eine NULL-Ausgabe folgt.|  
|**execute_as_principal_id**|**int**|Die ID des Datenbankprinzipals EXECUTE AS.<br /><br /> NULL als Standardwert oder bei Verwendung von EXECUTE AS CALLER.<br /><br /> ID des angegebenen Prinzipals bei EXECUTE AS SELF oder EXECUTE AS \<principal >.<br /><br /> -2 = EXECUTE AS OWNER.|  
|**uses_native_compilation**|bit|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = nicht systemintern kompiliert<br /><br /> 1 = systemintern kompiliert<br /><br /> Der Standardwert ist 0.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Sys. system_sql_modules &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-sql-modules-transact-sql.md)   
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
