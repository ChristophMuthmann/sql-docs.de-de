---
title: RecordStatusEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2315d18add9b25aab826d47346d8725aaa2af6e7
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="recordstatusenum"></a>RecordStatusEnum
Gibt an, die [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) eines Datensatzes in Bezug auf BatchUpdates und andere Massenvorgänge.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|Gibt an, dass der Datensatz wurde nicht gespeichert werden, da der Vorgang abgebrochen wurde.|  
|**adRecCantRelease**|0x400|Gibt an, dass der neue Datensatz wurde nicht gespeichert werden, da die vorhandene Datensatz gesperrt wurde.|  
|**adRecConcurrencyViolation**|0x800|Gibt an, dass der Datensatz nicht gespeichert werden, wurde da durch vollständige Parallelität verwendet wurde.|  
|**adRecDBDeleted**|0x40000|Gibt an, dass der Datensatz bereits aus der Datenquelle gelöscht wurde.|  
|**adRecDeleted**|0x4|Gibt an, dass der Datensatz gelöscht wurde.|  
|**adRecIntegrityViolation**|0x1000|Gibt an, dass der Datensatz nicht gespeichert werden, wurde da der Benutzer die Einschränkungen für die Integrität verletzt.|  
|**adRecInvalid**|0x10|Gibt an, dass der Datensatz nicht gespeichert werden, wurde da seine Textmarke ungültig ist.|  
|**adRecMaxChangesExceeded**|0x2000|Gibt an, dass der Datensatz nicht gespeichert werden, wurde da zu viele ausstehende Änderungen vorhanden waren.|  
|**adRecModified**|0x2|Gibt an, dass der Datensatz geändert wurde.|  
|**adRecMultipleChanges**|0x40|Gibt an, dass der Datensatz wurde nicht gespeichert werden, da er mehrere Datensätze auswirken würde.|  
|**adRecNew**|0x1|Gibt an, dass der Datensatz neu ist.|  
|**adRecObjectOpen**|0x4000|Gibt an, dass der Datensatz wurde aufgrund eines Konflikts mit einem geöffneten Speicherobjekt nicht gespeichert.|  
|**adRecOK**|0|Gibt an, dass der Datensatz wurde erfolgreich aktualisiert wurde.|  
|**adRecOutOfMemory**|0x8000|Gibt an, dass der Datensatz wurde nicht gespeichert werden, da der Computer nicht genügend Arbeitsspeicher zur Verfügung steht.|  
|**adRecPendingChanges**|0x80|Gibt an, dass der Datensatz nicht gespeichert werden, wurde weil er auf eine ausstehende Einfügung verweist.|  
|**adRecPermissionDenied**|0x10000|Gibt an, dass der Datensatz nicht gespeichert werden, wurde da der Benutzer keine ausreichenden Berechtigungen aufweist.|  
|**adRecSchemaViolation**|0x20000|Gibt an, dass der Datensatz nicht gespeichert werden, wurde da er die Struktur der zugrunde liegenden Datenbank verletzt.|  
|**adRecUnmodified**|0x8|Gibt an, dass der Datensatz nicht geändert wurde.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 AdoEnums.RecordStatus.  
  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.RecordStatus.CANCELED|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums.RecordStatus.CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums.RecordStatus.OUTOFMEMORY|  
|AdoEnums.RecordStatus.PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>Gilt für  
 [Status-Eigenschaft (ADO Recordset)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
