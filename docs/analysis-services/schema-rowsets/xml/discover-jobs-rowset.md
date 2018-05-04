---
title: DISCOVER_JOBS-Rowset | Microsoft Docs
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
- DISCOVER_JOBS rowset
ms.assetid: b4d83bb6-aed3-4513-b516-cefadf95dad2
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f7a74c1d420a4982864b76dc9cd35848992ce5ff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="discoverjobs-rowset"></a>DISCOVER_JOBS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Stellt Informationen über die aktiven Aufträge bereit, die auf dem Server ausgeführt werden. Ein Auftrag ist ein Teil eines Befehls, der für den Befehl einen bestimmten Task ausführt.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_JOBS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**JOB_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||UTC-Datum und -Zeit des Servers, zu denen der Auftrag erstellt wurde.|  
|**JOB_DESCRIPTION**|**DBTYPE_WSTR**||Die vom Serverdienst zugeordnete Auftragsbeschreibung.|  
|**JOB_EXECUTION_TIME_MS**|**DBTYPE_I8**||Die Zeit in Millisekunden, die der Auftrag aktiv ist.|  
|**JOB_ID**|**DBTYPE_I4**||Der eindeutige Bezeichner des Auftrags.|  
|**JOB_START_TIME**|**DBTYPE_DBTIMESTAMP**||UTC-Datum und -Zeit des Servers, zu denen der Auftrag gestartet wurde.|  
|**JOB_THREADPOOL_ID**|**DBTYPE_I4**||Der Threadpool, aus dem der aktuelle Auftrag gestartet wurde.|  
|**JOB_TOTAL_TIME_MS**|**DBTYPE_I8**||Die Zeit in Millisekunden, seit der der Auftrag gestartet wurde.|  
|**SPID**|**DBTYPE_I4**||Die Sitzungs-ID.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_JOBS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|Optional.|  
|JOB_ID|DBTYPE_I4|Optional.|  
|JOB_DESCRIPTION|DBTYPE_WSTR|Optional.|  
|JOB_THREADPOOL_ID|DBTYPE_I4|Optional.|  
|JOB_MIN TOTAL_TIME_MS|DBTYPE_I8|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
