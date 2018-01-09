---
title: DISCOVER_ENUMERATORS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DISCOVER_ENUMERATORS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_ENUMERATORS rowset
ms.assetid: ddc7b13c-3135-4419-8166-eddd459167da
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0be0cb9885cf48911a31ba4181a235eae032094b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="discoverenumerators-rowset"></a>DISCOVER_ENUMERATORS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Gibt eine Liste von Namen, Datentypen und Enumerationswerten von Enumeratoren, die von unterstützt die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA)-Anbieter für eine bestimmte Datenquelle. Der XMLA-Anbieter veröffentlicht alle Enumerationskonstanten, die er erkennt.  
  
 Beim Aufrufen der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode mit der **DISCOVER_ENUMERATORS** Enumerationswert in der [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) Element, das **Discover** Methode gibt die **DISCOVER_ENUMERATORS** -Schemarowsets.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Für jeden Enumerator gibt es mehrere Elemente, eines für jeden Wert in der Enumeration. Das Rowset, das jeden Enumerator repräsentiert, ist "flat", und der Name des Enumerators kann für Elemente, die zur selben Enumeration gehören, wiederholt werden.  
  
 Das **DISCOVER_ENUMERATORS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**Enumerationsname**|**DBTYPE_WSTR**||Der Name des Enumerators, der eine Wertemenge enthält.|  
|**EnumDescription**|**DBTYPE_WSTR**||Eine lokalisierbare Beschreibung des Enumerators. Kann **NULL**sein.|  
|**EnumType**|**DBTYPE_WSTR**||Der Datentyp der Enumerationswerte.|  
|**ElementName**|**DBTYPE_WSTR**||Der Name eines der Wertelemente im Enumeratorsatz.<br /><br /> Beispiel: **TDP**|  
|**ElementDescription**|**DBTYPE_WSTR**||(Optional) Eine lokalisierbare Beschreibung des Elements. Kann **NULL**sein.|  
|**ElementValue**|**DBTYPE_WSTR**||Der Wert des Elements. Kann **NULL**sein.<br /><br /> Beispiel: **01**|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_ENUMERATORS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**Enumerationsname**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis – Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
