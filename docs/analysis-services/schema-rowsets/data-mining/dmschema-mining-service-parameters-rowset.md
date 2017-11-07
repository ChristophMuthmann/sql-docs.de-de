---
title: DMSCHEMA_MINING_SERVICE_PARAMETERS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_SERVICE_PARAMETERS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e867952dac5e49b5f563ba7a9aed29eef3564d1a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingserviceparameters-rowset"></a>DMSCHEMA_MINING_SERVICE_PARAMETERS-Rowset
  Beschreibt die Parameter für die Algorithmen auf dem Server.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DMSCHEMA_MINING_SERVICE_PARAMETERS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**DIENSTNAME**|**DBTYPE_WSTR**|Name des Algorithmus|  
|**PARAMETERNAME**|**DBTYPE_WSTR**|Der Name des Parameters.|  
|**PARAMETERTYP**|**DBTYPE_WSTR**|Der Typ des Parameters.|  
|**IS_REQUIRED**|**DBTYPE_BOOL**|Ein boolescher Wert, der **TRUE** zurückgibt, wenn der Parameter erforderlich ist.|  
|**PARAMETER_FLAGS**|**DBTYPE_UI4**|Eine Bitmaske, die die Eigenschaften des Parameters beschreibt:<br /><br /> **DM_PARAMETER_TRAINING** (**0x0000001**) gibt an, dass der Parameter für das Training verwendet wird.<br /><br /> **DM_PARAMETER_PREDICTION** (**0x00000002**) gibt an, dass der Parameter für die Vorhersage verwendet wird.<br /><br /> **DM_PARAMETER_CONTENT** (**0x00000003**) gibt an, dass der Parameter für die Inhaltseinschränkung verwendet wird.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Eine benutzerfreundliche Beschreibung des Parameters.|  
|**STANDARDWERT**|**DBTYPE_WSTR**|Der Standardwert des Parameters. Gibt **NULL** zurück, wenn der Standardwert kein einfacher Datentyp ist.|  
|**VALUE_ENUMERATION**|**DBTYPE_WSTR**|Ein Enumerator von möglichen Werten für den Parameter.|  
|**HELP_FILE**|**DBTYPE_WSTR**|Der Name der Datei, die die Dokumentation dieses Parameters enthält.|  
|**HELP_CONTEXT**|**DBTYPE_I4**|Die Hilfekontext-ID für diese Funktion.|  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DMSCHEMA_MINING_SERVICE_PARAMETERS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**DIENSTNAME**|**DBTYPE_WSTR**|Optional.|  
|**PARAMETERNAME**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Schemarowsets](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

