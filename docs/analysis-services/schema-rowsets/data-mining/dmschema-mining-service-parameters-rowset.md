---
title: DMSCHEMA_MINING_SERVICE_PARAMETERS-Rowset | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
ms.openlocfilehash: 497396bf0679afbabbebe9936ba6c5f443942bec
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="dmschemaminingserviceparameters-rowset"></a>DMSCHEMA_MINING_SERVICE_PARAMETERS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Beschreibt die Parameter für die Algorithmen auf dem Server.  
  
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
 [Data Mining Schema Rowsets](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
