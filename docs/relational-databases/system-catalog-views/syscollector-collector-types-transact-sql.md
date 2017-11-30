---
title: Syscollector_collector_types (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_collector_types
- syscollector_collector_types_TSQL
dev_langs: TSQL
helpviewer_keywords:
- data collector view
- syscollector_collector_types view
ms.assetid: d5cd30bb-89fd-4814-a7e8-9074f043f90f
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e041fba1cfe133ea7c34bb2e8c27945cc89629a7
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="syscollectorcollectortypes-transact-sql"></a>syscollector_collector_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stellt Informationen zu einem Sammlertyp für ein Sammelelement bereit.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**collector_type_uid**|**uniqueidentifier**|Die GUID für einen Sammlungstyp. Lässt keine NULL-Werte zu.|  
|**name**|**sysname**|Der Name des Sammlungstyps. Lässt keine NULL-Werte zu.|  
|**parameter_schema**|**xml**|Das XML-Schema, das die Konfiguration für den angegebenen Sammlertyp beschreibt. Dieses XML-Schema wird verwendet, um die tatsächliche XML-Konfiguration, die einer bestimmten Instanz eines Sammelelements zugeordnet ist, zu überprüfen. Lässt NULL-Werte zu.|  
|**parameter_formatter**|**xml**|Legt die Vorlage fest, die zum Transformieren des XML-Codes für die Seite "Eigenschaften für Datensammlungssätze" verwendet werden soll. Lässt NULL-Werte zu.|  
|**collection_package_id**|**uniqueidentifier**|GUID für ein Sammlungspaket. Lässt keine NULL-Werte zu.|  
|**collection_package_path**|**nvarchar(4000)**|Stellt den Pfad zum Sammlungspaket bereit. Lässt NULL-Werte zu.|  
|**collection_package_name**|**sysname**|Der Name des Sammlungspakets. Lässt keine NULL-Werte zu.|  
|**upload_package_id**|**uniqueidentifier**|GUID für das Uploadpaket. Lässt keine NULL-Werte zu.|  
|**upload_package_path**|**nvarchar(4000)**|Stellt den Pfad für das Uploadpaket bereit. Lässt NULL-Werte zu.|  
|**upload_package_name**|**sysname**|Der Name des Uploadpakets. Lässt keine NULL-Werte zu.|  
|**is_system**|**bit**|Aktiviert (1) oder deaktiviert (0), um anzugeben, ob der Sammlertyp im Lieferumfang des Datensammlers enthalten war oder ob er später von **dc_admin**hinzugefügt wurde. Dies könnte ein benutzerdefinierter Typ sein, der intern oder durch einen Drittanbieter entwickelt wurde. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT für **dc_operator**, **dc_proxy**.  
  
## <a name="change-history"></a>Änderungsverlauf  
  
|Aktualisierter Inhalt|  
|---------------------|  
|Der Spaltenname **collection_type_uid** wurde auf **collector_type_uid**aktualisiert.|  
|Die Beschreibung für die Spalte **parameter_schema** wurde korrigiert, um anzugeben, dass der Wert NULL sein kann.|  
|Die Spalte **parameter_formatter** wurde hinzugefügt.|  
|Der Datentyp für die Spalte **collection_package_path** wurde korrigiert, außerdem wurde die Beschreibung aktualisiert, um anzugeben, dass der Wert NULL sein kann.|  
|Der Datentyp für die Spalte **upload_package_path** wurde korrigiert, außerdem wurde die Beschreibung aktualisiert, um anzugeben, dass der Wert NULL sein kann.|  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Sichten des Datensammlers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)  
  
  
