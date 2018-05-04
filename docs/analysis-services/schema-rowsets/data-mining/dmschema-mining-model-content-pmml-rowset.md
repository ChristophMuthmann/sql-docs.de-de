---
title: DMSCHEMA_MINING_MODEL_CONTENT_PMML-Rowset | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DMSCHEMA_MINING_MODEL_CONTENT_PMML
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT_PMML rowset
ms.assetid: fa05bb08-a955-4c8d-b57f-ffcd82470220
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 153624dce91c2b94707170e94c9da3c497da02e6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dmschemaminingmodelcontentpmml-rowset"></a>DMSCHEMA_MINING_MODEL_CONTENT_PMML-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Gibt die XML-Struktur des Miningmodells wieder. Das Format der XML-Zeichenfolge entspricht dem Standard der Predictive Model Markup Language (PMML 2.1).  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DMSCHEMA_MINING_MODEL_CONTENT_PMML** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||Der Katalogname der mit dem Namen der Datenbank aufgefüllt wird, von der das Modell ein Element ist.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||Der nicht gekennzeichnete Schemaname. Diese Spalte wird nicht von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**MODEL_NAME**|**DBTYPE_WSTR**||Der Name des Modells. Diese Spalte darf keinen **NULL**-Wert enthalten.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**||Der Modelltyp. Dies ist eine anbieterspezifische Zeichenfolge. Diese kann **NULL**sein.|  
|**MODEL_GUID**|**DBTYPE_GUID**||Der GUID, der das Modell identifiziert. Anbieter, die keine GUIDs verwenden, um Tabellen zu identifizieren, geben **NULL**zurück.|  
|**MODEL_PMML**|**DBTYPE_WSTR**||Eine XML-Wiedergabe des Modellinhalts im PMML-Format.|  
|**SIZE**|**DBTYPE_UI4**||Die Anzahl der Bytes in der XML-Zeichenfolge.|  
|**SPEICHERORT**|**DBTYPE_WSTR**||Der Speicherort der XML-Datei. Der Wert ist **NULL** , wenn kein Speicherort verfügbar ist.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DMSCHEMA_MINING_MODEL_CONTENT_PMML** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Optional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Optional.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|Optional.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Schemarowsets](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
