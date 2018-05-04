---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
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
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a95040a932e35d96a7b2a384da1a910ada118349
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
Gibt an, welche Felder verwendet werden können, zum Erkennen von Konflikten während einer optimistischen Aktualisierung einer Zeile der Datenquelle mit einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
 Verwenden Sie diese Konstanten mit der **Recordset** "**Updatekriterium**" dynamische Eigenschaft, die in verwiesen wird die [ADO dynamische Property-Index](../../../ado/reference/ado-api/ado-dynamic-property-index.md) und in den dokumentiert[ Microsoft Cursor Service für OLE DB-](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) Dokumentation.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|Erkennt Konflikte, wenn jede Spalte der Quelle Datenzeile geändert wurde.|  
|**adCriteriaKey**|0|Erkennt Konflikte, wenn die Schlüsselspalte der Daten Datenquellenzeile geändert wurde, was bedeutet, dass die Zeile gelöscht wurde.|  
|**adCriteriaTimeStamp**|3|Erkennt Konflikte, wenn der Zeitstempel des ausgewählten Zeile Datenquelle geändert wurde, dies bedeutet, dass die Zeile nach zugegriffen wurde die **Recordset** abgerufen wurde.|  
|**adCriteriaUpdCols**|2|Erkennt Konflikte, wenn eine der Spalten der Datenquelle, die Zeile an aktualisierte Datenfelder entsprechen den **Recordset** geändert wurden.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
