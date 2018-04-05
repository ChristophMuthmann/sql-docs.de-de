---
title: DISCOVER_OBJECT_MEMORY_USAGE-Rowset | Microsoft Docs
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
- DISCOVER_OBJECT_MEMORY_USAGE rowset
ms.assetid: 211cfa04-7bd6-43fe-8bd5-bfbff78bdafb
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9be5091d26d264d71dad5e6892f7f8d7448d83c4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="discoverobjectmemoryusage-rowset"></a>DISCOVER_OBJECT_MEMORY_USAGE-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Stellt Informationen über von Objekten verwendete Speicherressourcen bereit.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_OBJECT_MEMORY_USAGE** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||Der Pfad zu dem übergeordneten Element des aktuellen Objekts.|  
|**OBJECT_ID**|**DBTYPE_WSTR**||Die ID des Objekts, die zur Erstellungszeit definiert wurde.|  
|**OBJECT_MEMORY_SHRINKABLE**|**DBTYPE_I8**||Die Gesamtmenge des von allen verkleinerbaren Objekten verwendeten Speichers (Bytes), die sich unmittelbar im Besitz des aktuellen Objekts befinden. Der aktuelle Wert beinhaltet keinen Speicher von Objekten, die sich im Besitz von benannten Objekten befinden, die sich wiederum im Besitz des aktuellen Objekts befinden.|  
|**OBJECT_MEMORY_NONSHRINKABLE**|**DBTYPE_I8**||Die Menge des von allen nicht verkleinerbaren Objekten verwendeten Speichers (Bytes), die sich unmittelbar im Besitz des aktuellen Objekts befinden. Der aktuelle Wert beinhaltet keinen Speicher von Objekten, die sich im Besitz von benannten Objekten befinden, die sich im Besitz des aktuellen Objekts befinden.|  
|**OBJECT_VERSION**|**DBTYPE_I4**||Die Metadatenversionsnummer des Objekts. Diese Nummer ändert sich jedes Mal, wenn das Objekt geändert wird.|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||Die Herkunftszahl der Daten in dem Objekt. Diese Zahl erhöht sich jedes Mal, wenn das Objekt verarbeitet wird.|  
|**OBJECT_TYPE_ID**|**DBTYPE_I4**||Für die interne Verwendung vorgesehen.|  
|**OBJECT_TIME_CREATED**|**DBTYPE_DBTIMESTAMP**||Die UTC-Serverzeit zum Zeitpunkt der Erstellung des Objekts.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_OBJECT_MEMORY_USAGE** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**|Optional.|  
|**OBJECT_ID**|**DBTYPE_WSTR**|Optional|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis – Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
