---
title: DISCOVER_INSTANCES-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_INSTANCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_INSTANCES rowset
ms.assetid: e0842e63-089d-468d-869f-634da343d9fb
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fbed6de71f83da959591003039fe5910a1a4c53d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES-Rowset
  Beschreibt die Instanzen auf dem Server.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_INSTANCES** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**INSTANZNAME**|**DBTYPE_WSTR**||Der Name der Instanz.|  
|**INSTANCE_PORT_NUMBER**|**DBTYPE_I4**||Die Portnummer, die die Instanz überwacht.|  
|**INSTANCE_STATE**|**DBTYPE_I4**||Der Status der Serverinstanz.<br /><br /> **Schritte**<br /><br /> **Beendet**<br /><br /> **Starten**<br /><br /> **Beenden**<br /><br /> **Angehalten**|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_INSTANCES** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**INSTANZNAME**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

