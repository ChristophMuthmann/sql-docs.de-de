---
title: EntityContainer-Element (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: e328558e-16b0-4d4a-a79a-fdd3c9493595
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e5328a9c360fa4465e0bcf53bd0f017447c7c113
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="entitycontainer-element-csdlbi"></a>EntityContainer-Element (CSDLBI)
  Das EntityContainer-Element ist ein komplexer Typ, der auf dem CSDL-Typ EntityContainer basiert, und eine Auflistung von Entitäten innerhalb eines einzelnen Datenmodells definiert. In einer Business Intelligence-Anwendung kann das vom einem EntityContainer dargestellte Datenmodell mehrere Tabellen mit durch Beziehungen verknüpften Spalten sowie Berechnungen, Measures und KPIs enthalten. Das Konzept des Modells ähnelt einer Datenbank oder einer Datenquelle.  
  
 Der EntityContainer muss jeden der Entitätstypen angeben, die im Datenmodell enthalten sind, einschließlich Tabellen und Beziehungen. Informationen zu diesen Modellentitäten werden anhand der Auflistung von untergeordneten Entitäten des Typs (Entitätselement) angegeben. Weitere Informationen finden Sie unter [EntityType-Element &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md).  
  
 Eigenschaften wie Sortierung und Sprache werden auf der EntityContainer-Ebene und nicht auf Ebene einzelner Objekte definiert. Spalten und Textattribute innerhalb des Modells können jedoch über Beschriftungen oder Übersetzungen in anderen Sprachen verfügen.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der nachfolgenden Tabelle werden die Elemente und Attribute beschrieben, die im EntityContainer-Element definiert werden.  
  
|Name|Ist erforderlich|Beschreibung|  
|----------|-----------------|-----------------|  
|Name|Ja|Der Name des Datenmodells.|  
|Beschriftung|Nein|Eine Beschreibung der Datenbank oder des Datenmodells.|  
|Culture|Ja|Eine Zeichenfolge, die die LCID der Anforderung enthält.|  
|CompareOptions|Ja|Optionen für die sprachenspezifische Sortierung und den Zeichenfolgenvergleich für das Modell.|  
|DirectQueryMode|Nein|Eine Enumeration, die den Abfragemodus angibt, wenn das Modell den DirectQuery-Modus verwendet.|  
|EntitySet-Element|ja|[EntitySet-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)|  
|AssociationSet-Element|Nein|[AssociationSet-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)|  
  
## <a name="compareoptions-element"></a>CompareOptions-Element  
 Das CompareOptions-Attribut definiert Sortierungseigenschaften, die auf das Datenmodell angewendet werden. Die von CompareOptions definierten Eigenschaften werden von Einstellungen für die Sortierreihenfolge sowie von der Unterscheidung nach Kana und Berücksichtigung der Groß-/Kleinschreibung abgeleitet, die in der Analysis Services-Datenbank zum Zeitpunkt des Modellentwurfs festgelegt werden. In der folgenden Tabelle werden die Werte beschrieben, die als Teil des CompareOptions-Attributs enthalten sind.  
  
|Wert|Description|  
|-----------|-----------------|  
|IgnoreCase|Ein boolescher Wert, der angibt, ob Zeichenfolgenvergleiche die Groß- und Kleinschreibung ignorieren sollen.|  
|IgnoreNonSpace|Ein boolescher Wert, der angibt, ob Zeichenfolgenvergleiche Kombinationszeichen ohne Zwischenraum wie diakritische Zeichen ignorieren sollen.|  
|IgnoreKanaType|Ein boolescher Wert, der angibt, ob Zeichenfolgenvergleiche den Kanatyp ignorieren sollen.|  
|IgnoreWidth|Ein boolescher Wert, der angibt, ob Zeichenfolgenvergleiche die Zeichenbreite ignorieren sollen.|  
  
## <a name="directquerymode"></a>DirectQueryMode  
 **DirectQueryMode**  
  
 Der einfache Typ DirectQueryMode definiert den Typ der Abfrage, die standardmäßig verwendet wird, wenn mit dem Modell Daten direkt aus einer relationalen Datenquelle abgerufen werden können. Diese Eigenschaft kann nur für tabellarische Modelle verwendet werden, die im DirectQuery-Modus ausgeführt werden. In der folgenden Tabelle sind die möglichen Werte für die Enumeration des DirectQuery-Modus aufgelistet.  
  
|Wert|Description|  
|-----------|-----------------|  
|InMemory|Gibt an, dass für Abfragen des Modells Daten im Cache verwendet werden.|  
|InMemoryWithDirectQuery|Gibt an, dass Abfragen des Modells standardmäßig Daten aus der relationalen Datenquelle verwenden.|  
|DirectQueryWithInMemory|Gibt an, dass für Abfragen des Modells standardmäßig Daten im Cache verwendet werden.|  
|DirectQuery|Gibt an, dass für Abfragen des Modells nur Daten in der relationalen Datenquelle verwendet werden.|  
  
## <a name="example"></a>Beispiel  
 **Tabellarisch**  
  
 Im folgenden Beispiel wird ein Teil des tabellarischen AdventureWorks-Datenmodells in CSDLBI, Version 1.1, dargestellt.  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
       Name="DimEmployee"   
       EntityType="Sandbox.DimEmployee">  
   <bi:EntitySet />  
   </EntitySet>  
  
   <EntitySet   
     Name="DimProduct"   
       EntityType="Sandbox.DimProduct">  
    <bi:EntitySet />  
    </EntitySet>  
  
<bi:EntityContainer Caption="AWSimple" Culture="en-US">  
  
```  
  
## <a name="example"></a>Beispiel  
 **Multidimensional**  
  
 Im folgenden Beispiel wird ein Auszug aus dem Contoso-Vorgangscube in CSDLBI, Version 1.1, dargestellt.  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
      Name="Bike"   
      EntityType="Sandbox.Bike">  
    <bi:EntitySet Hidden="true" />  
   </EntitySet>  
…  
<bi:EntityContainer   
   Caption="CSDLTest"   
   Culture="en-US">  
<bi:CompareOptions   
   IgnoreCase="true" />  
</bi:EntityContainer>  
</EntityContainer>  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [EntitySet-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)  
  
  
