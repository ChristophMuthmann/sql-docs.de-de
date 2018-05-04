---
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7594e31bc4ffbf20b9c7a9cbd9dc65bfe279a76
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
Gibt an, wann die [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) Anbieter neu berechnet, aggregierte und berechnete Spalten in einem hierarchischen Recordset.  
  
 Diese Konstanten werden nur verwendet, mit der **MSDataShape** Anbieter und die **Recordset** "**automatische Neuberechnung**" dynamische Eigenschaft, die in verwiesen wird die [ADO Dynamische Property-Index](../../../ado/reference/ado-api/ado-dynamic-property-index.md) und die in der [Microsoft Cursor Service für OLE DB-](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) oder [Microsoft-Datenstrukturierungsdiensts für OLE DB-](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) Dokumentation.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Standard. Bei jedem berechnet die **MSDataShape** Anbieter bestimmt, Werte, die die berechneten Spalten von abhängen geändert haben.|  
|**adRecalcUpFront**|0|Berechnet nur, wenn zunächst die hierarchische Aufbau **Recordset**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.
