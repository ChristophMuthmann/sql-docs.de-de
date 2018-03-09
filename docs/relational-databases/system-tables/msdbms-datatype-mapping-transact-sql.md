---
title: MSdbms_datatype_mapping (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75f042866d01baa0a74143d2698644148a100b43
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msdbmsdatatypemapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSdbms_datatype_mapping** Tabelle enthält die zulässigen datentypzuordnungen vom Datentyp im Quell-Datenbank-Managementsystem (DBMS) für eine oder mehrere bestimmte Datentypen im Ziel-DBMS. Diese Tabelle wird gespeichert, der **Msdb** Datenbank und wird für heterogene Datenbankreplikation verwendet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|Identifiziert jede eindeutige Datentypzuordnung.|  
|**map_id**|**int**|Identifiziert den Quelldatentyp.|  
|**dest_datatype_id**|**int**|Identifiziert den Zieldatentyp.|  
|**dest_precision**|**bigint**|Definiert die Genauigkeit des Zieldatentyps, in dem ein Wert von NULL bedeutet, dass die Genauigkeit nicht verwendet wird, und der Wert **-1** bedeutet, dass die Genauigkeit des Quelldatentyps verwendet wird.|  
|**dest_scale**|**int**|Definiert die Dezimalstellen des Zieldatentyps, ein Wert von NULL bedeutet, dass Dezimalstellen nicht verwendet werden, und der Wert **-1** bedeutet, dass die Dezimalstellen des Quelldatentyps verwendet wird.|  
|**dest_length**|**bigint**|Definiert die Länge des Zieldatentyps, in dem ein Wert von NULL bedeutet, dass die Länge nicht verwendet wird, und der Wert **-1** bedeutet, dass die Länge des Quelldatentyps verwendet wird.|  
|**dest_nullable**|**bit**|Gibt an, ob die Zielspalte in der Zuordnung NULL-Werte zulässt. Ein Wert von NULL bedeutet, dass diese Definition nicht erforderlich ist.|  
|**dest_createparams**|**int**|Die Bitmap, die beschreibt, welche Kombination aus Länge, Genauigkeit und Dezimalstellen für den jeweiligen Datentyp anwendbar sind. Sie beinhaltet Folgendes:<br /><br /> **0 x 1** = mit einfacher Genauigkeit.<br /><br /> **0 x 2** = Skalierung.<br /><br /> **0 x 4** = Länge.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Angeben von Datentypzuordnungen für einen Oracle-Verleger](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
