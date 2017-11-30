---
title: Sys.syscomments (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syscomments_TSQL
- syscomments
- syscomments_TSQL
- sys.syscomments
dev_langs: TSQL
helpviewer_keywords:
- sys.syscomments compatibility view
- syscomments system table
ms.assetid: 767dd410-6bc9-4c4a-ab0f-6d2cf6163426
caps.latest.revision: "53"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5c9b5a5269025f6ed9c3bed493b71a6be557dc25
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="syssyscomments-transact-sql"></a>sys.syscomments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die Tabelle enthält Einträge für alle Sichten, Regeln, Standards, Trigger, CHECK-Einschränkungen, DEFAULT-Einschränkungen und gespeicherten Prozeduren innerhalb der Datenbank. Die **Text** Spalte enthält die ursprüngliche SQL-definitionsanweisungen.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Stattdessen wird die Verwendung von sys.sql_modules empfohlen. Weitere Informationen finden Sie unter [Sys. sql_modules &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md).  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID des Objekts, auf das sich der Text bezieht.|  
|**Anzahl**|**smallint**|Nummer innerhalb der Prozedurgruppierung, wenn eine Gruppierung vorliegt.<br /><br /> 0 = Einträge sind keine Prozeduren.|  
|**Spalten-ID**|**smallint**|Zeilensequenznummer für Objektdefinitionen, die 4.000 Zeichen überschreiten.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**CTEXT**|**varbinary(8000)**|Die Rohbytes der SQL-Definitionsanweisung.|  
|**texttype**|**smallint**|0 = Vom Benutzer anzugebender Kommentar<br /><br /> 1 = Vom System anzugebender Kommentar<br /><br /> 4 = Verschlüsselter Kommentar|  
|**Sprache**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**verschlüsselt**|**bit**|Gibt an, ob die Prozedurdefinition verborgen ist.<br /><br /> 0 = Nicht verborgen<br /><br /> 1 = Verborgen<br /><br /> **\*\*Wichtige \* \***  zum Verbergen von Definitionen gespeicherter Prozeduren verwenden Sie CREATE PROCEDURE mit dem Schlüsselwort ENCRYPTION.|  
|**komprimiert**|**bit**|Es wird immer 0 zurückgegeben. Zeigt an, ob die Prozedur komprimiert ist.|  
|**text**|**nvarchar(4000)**|Tatsächlicher Text der SQL-Definitionsanweisung.<br /><br /> Die Semantik des decodierten Ausdrucks entspricht dem ursprünglichen Text. Es gibt jedoch keine syntaktische Garantie. Leerzeichen werden beispielsweise aus dem decodierten Ausdruck entfernt.<br /><br /> Dies [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]-kompatible Sicht enthält Informationen aus aktuellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Strukturen und kann mehr Zeichen zurückgeben als die **nvarchar(4000)** Definition. **Sp_help** gibt **nvarchar(4000)** mit dem Datentyp der Textspalte. Bei der Arbeit mit **Syscomments** erwägen **nvarchar(max)**. Verwenden Sie für neue Entwicklungen nicht **Syscomments**.|  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von Systemtabellen zu Systemsichten &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Kompatibilitätssichten &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
