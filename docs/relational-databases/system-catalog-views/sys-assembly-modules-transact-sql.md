---
title: Sys. assembly_modules (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.assembly_modules
- sys.assembly_modules_TSQL
- assembly_modules
- assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_modules catalog view
ms.assetid: 5f9e644e-8065-49a2-b53d-db7df98f70d8
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62b918d77e4cdf7b90d4519e39adf3ddd6811e7b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysassemblymodules-transact-sql"></a>sys.assembly_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Gibt eine Zeile für jede Funktion, jede Prozedur oder jeden Trigger zurück, die bzw. der mit einer CLR-Assembly (Common Language Runtime) definiert ist. Diese Katalogsicht ordnet CLR-gespeicherte Prozeduren, CLR-Trigger oder CLR-Funktionen der zugrunde liegenden Implementierung zu. Objekten vom Typ TA, AF, PC, FS und FT ist ein Assemblymodul zugeordnet. Um die Zuordnung zwischen dem Objekt und der Assembly zu finden, können Sie diese Katalogsicht mit anderen Katalogsichten verknüpfen. Wenn Sie z. B. eine CLR-gespeicherte Prozedur erstellen, wird diese durch eine Zeile in **sys.objects**, eine Zeile in **sys.procedures** (geerbt von **sys.objects**) und eine Zeile in **sys.assembly_modules**dargestellt. Die gespeicherte Prozedur selbst wird durch die Metadaten in **sys.objects** und **sys.procedures**dargestellt. Verweise auf die zugrunde liegende CLR-Implementierung der Prozedur finden Sie in **sys.assembly_modules**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Objekt-ID des SQL-Objekts. Ist innerhalb einer Datenbank eindeutig.|  
|**assembly_id**|**int**|ID der Assembly, aus der dieses Modul erstellt wurde.|  
|**assembly_class**|**sysname**|Der Name der Klasse innerhalb der Assembly, die dieses Modul definiert.|  
|**assembly_method**|**sysname**|Der Name der Methode innerhalb von **assembly_class** , die dieses Modul definiert.<br /><br /> NULL für Aggregatfunktionen (AF).|  
|**null_on_null_input**|**bit**|Für das Modul wurde deklariert, dass für jede NULL-Eingabe eine NULL-Ausgabe erstellt wird.|  
|**execute_as_principal_id**|**int**|Die ID des Datenbankprinzipals, unter dem der Kontext ausgeführt wird, gemäß der EXECUTE AS-Klausel der CLR-Funktion, der gespeicherten Prozedur oder des Triggers.<br /><br /> NULL = EXECUTE AS CALLER. Dies ist die Standardeinstellung.<br /><br /> Die ID des angegebenen Datenbankprinzipals = EXECUTE AS SELF, EXECUTE AS *user_name*oder EXECUTE AS *login_name*.<br /><br /> -2 = EXECUTE AS OWNER.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
