---
title: Create-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Create Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Create
- urn:schemas-microsoft-com:xml-analysis#Create
- microsoft.xml.analysis.create
helpviewer_keywords:
- Create command (XMLA)
ms.assetid: a623d362-a1ac-40e4-8816-65fac89cb391
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a5420a85c65a29a09da519207206d3406c4cd384
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-element-xmla"></a>Create-Element (XMLA)
  Enthält Analysis Services Scripting Language (ASSL)-Elementen, die verwendet werden, indem die **Execute** Methode zum Erstellen von Objekten auf einer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <Create Scope="enum" AllowOverwrite="boolean">  
      <ParentObject>...</ParentObject>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Create>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Untergeordnete Elemente|[ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md), [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)|  
  
## <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|AllowOverwrite|Optionales **Boolean** -Attribut. Wenn die Objekte auf "true" festgelegt, in definiert werden. die **ObjectDefinition** Element werden, vorhandene Objekte auf die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz. Wenn dieses Attribut weggelassen oder auf "False" gesetzt wird, generiert das Vorhandensein eines existierenden Objekts einen Fehler.|  
|Scope|Optionales **Enum** -Attribut. Definiert die Dauer der Objekte, die im **ObjectDefinition** -Element definiert sind. Wenn dieses Attribut weggelassen wird, definiert die Objekte der **ObjectDefinition** Element persistent auf der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz. Der folgende Wert ist verfügbar:<br /><br /> *Sitzung*: die in definierten Objekte die **"objectdefinition"** Element nur für die Dauer des XML für Analysis (XMLA) Sitzung vorhanden sein.<br />                  Beachten Sie, dass bei Verwendung der *Sitzung* festlegen, die **ObjectDefinition** Element darf nur [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md), [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md), oder [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL-Elemente.|  
  
## <a name="remarks"></a>Hinweise  
 Jeder **Create** -Vorgang erstellt unter einem vom **ParentObject** -Element gegebenen übergeordneten Element ein Hauptobjekt. Wenn das übergeordnete Objekt weggelassen wird, wird davon ausgegangen, dass es die Ziel-[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz ist. Dies generiert einen Fehler, wenn das übergeordnete Element eines Hauptobjekts nicht die Zielinstanz ist.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel erstellt eine leere Datenbank mit dem Namen **Testdatenbank** auf eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.  
  
```  
  
      <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
   <ObjectDefinition>  
      <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
         <Name>Test Database</Name>  
         <Description>A test database.</Description>  
      </Database>  
   </ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

