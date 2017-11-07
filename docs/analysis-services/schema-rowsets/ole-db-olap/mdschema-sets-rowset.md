---
title: MDSCHEMA_SETS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_SETS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_SETS rowset
ms.assetid: abb00dc0-2b83-48d6-b2ba-6615c1488d06
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4820c18992da2aab0ac8e0550a5cadd75ca193bc
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemasets-rowset"></a>MDSCHEMA_SETS-Rowset
  Beschreibt alle Sätze, die zurzeit in einer Datenbank definiert werden, einschließlich Sätzen im Bereich einer Sitzung.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **MDSCHEMA_SETS** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Der Name der Datenbank.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Wird nicht unterstützt.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Der Name des Cubes.|  
|**GRUPPENNAME**|**DBTYPE_WSTR**|Der Name der Menge, gemäß der **CREATE SET** Anweisung.|  
|**BEREICH**|**DBTYPE_I4**|Der Gültigkeitsbereich des Satzes:<br /><br /> **MDSET_SCOPE_GLOBAL** (**1**)<br /><br /> **MDSET_SCOPE_SESSION** (**2**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Wird nicht unterstützt.|  
|**AUSDRUCK**|**DBTYPE_WSTR**|Der Ausdruck für den Satz.|  
|**DIMENSIONEN**|**DBTYPE_WSTR**|Eine durch Trennzeichen getrennte Liste der in dem Satz enthaltenen Hierarchien.|  
|**SET_CAPTION**|**DBTYPE_WSTR**|Eine Bezeichnung oder Beschriftung, die dem Satz zugeordnet ist. Die Bezeichnung oder Beschriftung dient hauptsächlich zu Anzeigezwecken.|  
|**SET_DISPLAY_FOLDER**|**DBTYPE_WSTR**|Eine Zeichenfolge, die den Pfad des Anzeigeordners angibt, der von der Clientanwendung zum Anzeigen der Menge verwendet wird. Das Trennzeichen für Ordnerebenen wird von der Clientanwendung definiert. Zu den Tools und Clients, die vom [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], den umgekehrten Schrägstrich (\\) ebenentrennzeichen ist. Um mehrere Anzeigeordner bereitzustellen, verwenden Sie ein Semikolon (;), um die Ordner zu trennen.|  
|**SET_EVALUATION_CONTEXT**|**DBTYPE_I4**|Der Kontext für den Satz. Der Satz kann statisch oder dynamisch sein. Diese Spalte kann einen der folgenden Werte besitzen:<br /><br /> MDSET_RESOLUTION_STATIC=1<br /><br /> MDSET_RESOLUTION_DYNAMIC=2|  
  
 Das Rowset wird sortiert nach **CATALOG_NAME**, **SCHEMA_NAME**und **CUBE_NAME**.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **MDSCHEMA_SETS** Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Optional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**GRUPPENNAME**|**DBTYPE_WSTR**|Optional.|  
|**BEREICH**|**DBTYPE_I4**|Optional.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|Optional.<br /><br /> Hinweis: Nur eine Hierarchie enthalten sein, und nur die benannten Mengen, deren Hierarchien den Einschränkungen exakt zurückgegeben werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

