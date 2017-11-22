---
title: Sys. identity_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
- identity_columns
- sys.identity_columns
- sys.identity_columns_TSQL
- identity_columns_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.identity_columns catalog view
ms.assetid: 97ee01e6-9c9e-4fd9-884b-68b4084669d5
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2669f1373bedec1256d3071b9fe1f85b7c8dab8f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysidentitycolumns-transact-sql"></a>sys.identity_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile für jede Spalte, bei der es sich um eine Identitätsspalte handelt.  
  
 Die **identity_columns** -Sicht erbt Zeilen aus der **sys.columns** anzeigen. Die **identity_columns** Sicht zurück, die Spalten in der **sys.columns** anzeigen, sowie die **Seed_value**, **Increment_value**, **Last_value**, und **Is_not_for_replication** Spalten. Weitere Informationen finden Sie unter [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**\<von sys.columns geerbte Spalten >**||Die **identity_columns** Ansicht gibt alle Spalten in der **sys.columns** anzeigen. Darüber hinaus werden die unten beschriebenen, zusätzlichen Spalten zurückgegeben. Eine Beschreibung der Spalten, die die **identity_columns** Ansicht erbt von **sys.columns**, finden Sie unter [sys.columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).|  
|**seed_value**|**sql_variant**|Der Ausgangswert für diese Identitätsspalte. Der Datentyp des Ausgangswerts ist der gleiche wie der Datentyp der Spalte selbst.|  
|**increment_value**|**sql_variant**|Der inkrementelle Wert für diese Identitätsspalte. Der Datentyp des Ausgangswerts ist der gleiche wie der Datentyp der Spalte selbst.|  
|**LAST_VALUE**|**sql_variant**|Der Wert, der zuletzt für diese Identitätsspalte generiert wurde. Der Datentyp des Ausgangswerts ist der gleiche wie der Datentyp der Spalte selbst.|  
|**is_not_for_replication**|**bit**|Die Identitätsspalte wird als NOT FOR REPLICATION deklariert.|  
  
> [!NOTE]  
>  Weitere Informationen zu einer automatisch inkrementierten Zahl, die in mehreren Tabellen verwendet oder aus Anwendungen aufgerufen werden kann, ohne dass auf eine Tabelle verwiesen wird, finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
