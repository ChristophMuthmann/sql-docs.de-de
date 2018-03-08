---
title: REFERENTIAL_CONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REFERENTIAL_CONSTRAINTS
- REFERENTIAL_CONSTRAINTS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS view
- REFERENTIAL_CONSTRAINTS view
ms.assetid: 5d358f18-0a85-4b55-af4b-98d5f4cd1020
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 998ae8fcbae2ca33ffe13f6c9699829982c62c73
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="referentialconstraints-transact-sql"></a>REFERENTIAL_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede FOREIGN KEY-Einschränkung in der aktuellen Datenbank zurück. Diese Informationsschemasicht gibt Informationen zu den Objekten zurück, für die der aktuelle Benutzer Berechtigungen besitzt.  
  
 Geben Sie zum Abrufen von Informationen aus diesen Sichten den vollqualifizierten Namen des **INFORMATION_SCHEMA.** *View_name*.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**Nvarchar (**128**)**|Einschränkungsqualifizierer|  
|**CONSTRAINT_SCHEMA**|**Nvarchar (**128**)**|Name des Schemas, das die Einschränkung enthält.<br /><br /> **\*\*Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**CONSTRAINT_NAME**|**sysname**|Einschränkungsname|  
|**UNIQUE_CONSTRAINT_CATALOG**|**Nvarchar (**128**)**|Der UNIQUE-Einschränkungsqualifizierer.|  
|**UNIQUE_CONSTRAINT_SCHEMA**|**Nvarchar (**128**)**|Der Name des Schemas, das die UNIQUE-Einschränkung enthält.<br /><br /> **\*\*Wichtige \* \***  verwenden Sie keine INFORMATION_SCHEMA-Sichten, die um das Schema eines Objekts zu bestimmen. Die einzig zuverlässige Möglichkeit zum Finden des Schemas eines Objekts besteht darin, die sys.objects-Katalogsicht abzufragen.|  
|**UNIQUE_CONSTRAINT_NAME**|**sysname**|UNIQUE-Einschränkung.|  
|**MATCH_OPTION**|**Varchar (**7**)**|Referenzielle Bedingungen für die Übereinstimmung von Einschränkungen. Es wird immer SIMPLE zurückgegeben. Dies bedeutet, dass keine Übereinstimmung definiert ist. Die Bedingung wird als Übereinstimmung betrachtet, wenn eine der folgenden Bedingungen zutrifft:<br /><br /> Mindestens ein Wert in der Fremdschlüsselspalte ist NULL.<br /><br /> Keiner der Werte in der Fremdschlüsselspalte ist NULL, und in der Primärschlüsseltabelle ist eine Zeile mit demselben Schlüssel vorhanden.|  
|**UPDATE_RULE**|**Varchar (**11**)**|Aktion, die ausgeführt wird, wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung verstößt gegen die referenzielle Integrität, die durch diese Einschränkung definiert ist. Gibt einen der folgenden Werte zurück: <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> Wenn für diese Einschränkung NO ACTION für ON UPDATE angegeben ist, wird das Update des Primärschlüssels, auf den in der Einschränkung verwiesen wird, nicht an den Fremdschlüssel weitergegeben. Wenn das Update eines Primärschlüssels einen Verstoß gegen die referenzielle Integrität verursacht, weil mindestens ein Fremdschlüssel den gleichen Wert enthält, werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Änderungen an der übergeordneten Tabelle und der verweisenden Tabelle vorgenommen. Außerdem löst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler aus.<br /><br /> Wenn für diese Einschränkung CASCADE für ON UPDATE angegeben ist, werden alle Änderungen des Primärschlüsselwerts automatisch an den Fremdschlüsselwert weitergegeben.|  
|**DELETE_RULE**|**Varchar (**11**)**|Die Aktion, die ausgeführt wird, wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung die referenzielle Integrität verletzt, die durch diese Einschränkung definiert ist. Gibt einen der folgenden Werte zurück: <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> Wenn für diese Einschränkung NO ACTION für ON DELETE angegeben ist, wird das Löschen des Primärschlüssels, auf den in der Einschränkung verwiesen wird, nicht an den Fremdschlüssel weitergegeben. Wenn das Löschen eines Primärschlüssels einen Verstoß gegen die referenzielle Integrität verursacht, weil mindestens ein Fremdschlüssel den gleichen Wert enthält, werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Änderungen an der übergeordneten Tabelle und der verweisenden Tabelle vorgenommen. Außerdem löst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler aus.<br /><br /> Wenn für diese Einschränkung CASCADE für ON DELETE angegeben ist, werden alle Änderungen des Primärschlüsselwerts automatisch an den Fremdschlüsselwert weitergegeben.|  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Informationsschemasichten &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys. Foreign_Keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
