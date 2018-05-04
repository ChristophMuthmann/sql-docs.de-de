---
title: MDSCHEMA_FUNCTIONS-Rowset | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MDSCHEMA_FUNCTIONS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_FUNCTIONS rowset
ms.assetid: 5253fa8c-b1ce-4504-aff6-a246b5e675c7
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c26528fd259dbb950d29b36271cd60be6bb05b5a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdschemafunctions-rowset"></a>MDSCHEMA_FUNCTIONS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Beschreibt die Funktionen, die Clientanwendungen zur Verfügung stehen, die mit der Datenbank verbunden sind.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **MDSCHEMA_FUNCTIONS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**FUNKTIONSNAME**|**DBTYPE_WSTR**|Der Name der Funktion.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Eine Beschreibung der Funktion.|  
|**PARAMETER_LIST**|**DBTYPE_WSTR**|Eine durch Trennzeichen getrennte Liste von Parametern, die wie in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic formatiert sind. Zum Beispiel könnte ein Parameter "Name als Zeichenfolge" sein.|  
|**RETURN_TYPE**|**DBTYPE_I4**|Der **VARTYPE** des Rückgabedatentyps der Funktion.|  
|**URSPRUNG**|**DBTYPE_I4**|Der Ursprung der Funktion.<br /><br /> 1 für MDX-Funktionen.<br /><br /> 2 für benutzerdefinierte Funktionen.|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|Der Name der Schnittstelle für benutzerdefinierte Funktionen.<br /><br /> Der Gruppenname für MDX-Funktionen (Multidimensional Expressions).|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**|Der Name der Typschnittstelle für benutzerdefinierte Funktionen. **NULL** für MDX-Funktionen.|  
|**DLL-NAME**|**DBTYPE_WSTR**|(Optional) Der Name der Assembly, die die benutzerdefinierte Funktion implementiert.<br /><br /> Gibt **VT_NULL** für MDX-Funktionen zurück.|  
|**HELP_FILE**|**DBTYPE_WSTR**|(Optional) Der Name der Datei, die die Hilfedokumentation für die benutzerdefinierte Funktion enthält.<br /><br /> Gibt **VT_NULL** für MDX-Funktionen zurück.|  
|**HELP_CONTEXT**|**DBTYPE_I4**|(Optional) Gibt die Hilfekontext-ID für diese Funktion zurück.|  
|**OBJEKT**|**DBTYPE_WSTR**|(Optional) Der allgemeine Name der Objektklasse, für die eine Eigenschaft gilt. Z. B. das Rowset, der < Ebenenname >. Member-Funktion gibt "**Ebene**".<br /><br /> Gibt **VT_NULL** für benutzerdefinierte Funktionen oder MDX-Funktionen ohne Eigenschaft zurück.|  
|**BESCHRIFTUNG**|**DBTYPE_WSTR**|Die Anzeigebeschriftung für die Funktion.|  
  
 Das Rowset wird nach **ORIGIN**, **INTERFACE_NAME**und **FUNCTION_NAME**sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **MDSCHEMA_FUNCTIONS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**LIBRARY_NAME**|**DBTYPE_WSTR**|Optional.|  
|**INTERFACE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**FUNKTIONSNAME**|**DBTYPE_WSTR**|Optional.|  
|**URSPRUNG**|**DBTYPE_I4**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
