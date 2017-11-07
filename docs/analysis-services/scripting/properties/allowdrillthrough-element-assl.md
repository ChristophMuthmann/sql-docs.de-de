---
title: AllowDrillThrough-Element (ASSL) | Microsoft Docs
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
- AllowDrillThrough Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AllowDrillThrough
helpviewer_keywords:
- AllowDrillThrough element
ms.assetid: 53c9e4a3-a376-447d-a13f-80d845cc9789
caps.latest.revision: 51
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5b0b2212ec86f1bb0c5a95fbf9f23768b36bb133
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="allowdrillthrough-element-assl"></a>AllowDrillThrough-Element (ASSL)
  Bestimmt, ob Drillthrough auf dem übergeordneten Element erlaubt wird.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MiningModel> <!-- or MiningModelPermission -->  
<!-- or MiningStructurePermission -->   ...  
   <AllowDrillThrough>...</AllowDrillThrough>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Boolean|  
|Standardwert|**False**|  
|Cardinality|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[MiningModel-Element](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md), [miningstructurepermission-Objekte](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Die Elemente, die den übergeordneten Elementen von entsprechen **AllowDrillThrough** im Objektmodell von Analysis Management Objects (AMO) sind <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, und <xref:Microsoft.AnalysisServices.MiningStructurePermission>.  
  
## <a name="drillthrough-on-mining-structures"></a>Drillthrough in Miningstrukturen  
 In [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], können Sie definieren **AllowDrillthrough** Berechtigungen für Miningstrukturen sowie Miningmodelle. Wenn Sie diese Berechtigung einer Rolle zuordnen, kann jedes Mitglied dieser Rolle das Data Mining-Modell abfragen und Strukturspalten zurückgeben, die nicht im Modell enthalten waren. Zum Beispiel erstellen Sie nur mit folgenden Spalten ein Modell: Kundenschlüssel, Kundeneinkommen und Kundenkäufe. Wenn Sie Drillthrough im Modell aktivieren, können Benutzer Informationen in anderen Spalten der Miningstruktur, z.&nbsp;B. E-Mail-Adressen oder Namen von Kunden, zurückgeben.  
  
 Um sensible Daten zu schützen, gehen Sie daher beim Hinzufügen von Spalten zur Miningstruktur sorgfältig vor. Erteilen Sie außerdem die **AllowDrillthrough** -Berechtigung für eine Struktur nur, wenn es erforderlich ist.  
  
 Um einen Drillthrough zu Strukturspalten auszuführen, verwenden Sie eine Abfrage in einem der folgenden Formate:  
  
 `SELECT * FROM <structure>.CASES`  
  
 oder  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>Siehe auch  
 [Role-Element &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

