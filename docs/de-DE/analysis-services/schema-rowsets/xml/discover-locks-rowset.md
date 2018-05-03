---
title: DISCOVER_LOCKS-Rowset | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_LOCKS rowset
ms.assetid: dea48167-212c-40b7-a416-434042a1b697
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d93f7d578defe5aa10aaa8e1a5f7ac94c3cc05ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="discoverlocks-rowset"></a>DISCOVER_LOCKS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Stellt Informationen über die aktuellen Sperren auf dem Server bereit.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_LOCKS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LOCK_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||Die UTC-Serverzeit zum Zeitpunkt der Anforderung der Sperre.|  
|**LOCK_GRANT_TIME**|**DBTYPE_DBTIMESTAMP**||Die UTC-Serverzeit zum Zeitpunkt der Zuweisung der Sperre auf der Ressource.|  
|**LOCK_ID**|**DBTYPE_GUID**||Der eindeutige Bezeichner der Sperre als GUID.|  
|**LOCK_OBJECT_ID**|**DBTYPE_WSTR**||Der eindeutige Bezeichner des gesperrten Objekts.|  
|**LOCK_STATUS**|**DBTYPE_I4**||Der Status der Sperre:<br /><br /> 0 bedeutet "Warte auf Sperrung des Objekts".<br /><br /> 1 bedeutet "Sperre zugewiesen".|  
|**LOCK_TRANSACTION_ID**|**DBTYPE_GUID**||Der eindeutige Bezeichner der Transaktion als GUID.|  
|**LOCK_TYPE**|**DBTYPE_I4**||Eine Bitmaske von Sperrentypen. Weitere Informationen finden Sie im Abschnitt "Hinweise" in diesem Thema.|  
|**SPID**|**DBTYPE_I4**||Die Sitzungs-ID.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_LOCKS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|Optional.|  
|LOCK_TRANSACTION_ID|DBTYPE_GUID|Optional.|  
|LOCK_OBJECT_ID|DBTYPE_WSTR|Optional.|  
|LOCK_STATUS|DBTYPE_I4|Optional.|  
|LOCK_TYPE|DBTYPE_I4|Optional.|  
|LOCK_MIN_TOTAL_MS|DBTYPE_I8|Optional.|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="lock-types"></a>Typen von Sperren  
  
|Name der Sperre|Wert|Description|  
|---------------|-----------|-----------------|  
|LOCK_NONE|0x0000000|Keine Sperre.|  
|LOCK_SESSION_LOCK|0x0000001|Inaktive Sitzung, führt nicht zu Einschränkungen von anderen Sperren.|  
|LOCK_READ|0x0000002|Lesesperre während der Verarbeitung.|  
|LOCK_WRITE|0x0000004|Schreibsperre während der Verarbeitung.|  
|LOCK_COMMIT_READ|0x0000008|Commitsperre, freigegeben.|  
|LOCK_COMMIT_WRITE|0x0000010|Commitsperre, exklusiv.|  
|LOCK_COMMIT_ABORTABLE|0x0000020|Bricht einen Commitvorgang ab.|  
|LOCK_COMMIT_INPROGRESS|0x0000040|Commit wird ausgeführt.|  
|LOCK_INVALID|0x0000080|Ungültige Sperre.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
