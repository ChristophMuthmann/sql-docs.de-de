---
title: DMSCHEMA_MINING_FUNCTIONS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DMSCHEMA_MINING_FUNCTIONS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_FUNCTIONS rowset
ms.assetid: 9ace7493-a7b1-45ca-93de-3cb2f3597017
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c33bf605db92bae91a0d05c5b4ea8feb6d4542e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dmschemaminingfunctions-rowset"></a>DMSCHEMA_MINING_FUNCTIONS-Rowset
  Beschreibt die Datamining-Funktionen, die von Datamining-Algorithmen auf einem Server verfügbar, die ausgeführt wird, unterstützt werden [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DMSCHEMA_MINING_FUNCTIONS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**DIENSTNAME**|**DBTYPE_WSTR**||Name des Algorithmus|  
|**FUNKTIONSNAME**|**DBTYPE_WSTR**||Der Name der Funktion.|  
|**FUNCTION_SIGNATURE**|**DBTYPE_WSTR**||Die Signatur der Funktion.|  
|**RETURNS_TABLE**|**DBTYPE_BOOL**||**FALSE** , wenn die Funktion skalare Inhalte zurückgibt (wie die Länge des Zeichenarguments), **TRUE** , wenn die Funktion eine Tabelle zurückgibt (wie eine Histogrammtabelle).|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Eine benutzerfreundliche Beschreibung der Funktion.|  
|**HELP_FILE**|**DBTYPE_WSTR**||Der Name der Datei, die die Dokumentation dieser Funktion enthält.|  
|**HELP_CONTEXT**|**DBTYPE_I4**||Die Hilfekontext-ID für diese Funktion.|  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DMSCHEMA_MINING_FUNCTIONS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**DIENSTNAME**|**DBTYPE_WSTR**|Optional.|  
|**FUNKTIONSNAME**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining Schema Rowsets](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
