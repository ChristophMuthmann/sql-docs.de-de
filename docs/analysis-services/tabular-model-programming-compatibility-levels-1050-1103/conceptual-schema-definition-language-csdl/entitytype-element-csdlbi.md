---
title: EntityType-Element (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 372e2c13-ec38-4bb1-981c-50758d59a1da
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 303f09187528dd7fa2c897fea5fd86ec6d7f23d9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="entitytype-element-csdlbi"></a>EntityType-Element (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Die **EntityType** Element ist ein komplexer Typ, der die Struktur einer Entität auf hoher Ebene, z. B. ein Kunde oder eine Bestellung in einem Datenmodell darstellt. Die **Bi: EntityType** Element erweitert die Definition von [EntityType](http://msdn.microsoft.com/library/bb399206.aspx) verwendet der [Entity Data Framework](http://msdn.microsoft.com/library/bb399567.aspx).  
  
 Ein EntityType-Element muss für jede der Entitäten angegeben werden, die im Datenmodell enthalten sind. Die Unterelemente von EntityType beschreiben die Spalten und Measures in der Tabelle. Beziehungen von Tabellen sind in **EntityContainer**enthalten.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der folgenden Tabelle sind die Elemente und Attribute aufgeführt, durch die das **EntityType** -Element definiert wird. Weitere Informationen finden Sie in den Attributen für das [EntityType](http://msdn.microsoft.com/library/bb399206.aspx) -Element.  
  
|Name|Ist erforderlich|Beschreibung|  
|----------|-----------------|-----------------|  
|Inhalt|Nein|Eine Zeichenfolge, die die möglichen Datentypen einer Spalte enthält. Der Wert wird vom Wert für den DimensionAttributeTypeEnumType im Datenmodell abgeleitet.<br /><br /> Wenn DimensionAttributeTypeEnumType den Wert "ExtendedType" aufweist, wird der Wert von Contents aus dem ExtendedType-Element von DimensionAttribute abgeleitet. Der Client muss nicht auf diese Werte reagieren.|  
|DefaultDetails|Nein|Eine Liste mit Eigenschaftsverweisen, die den Spaltensatz in der Tabelle darstellen.<br /><br /> Finden Sie unter [DefaultDetails-Element &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/defaultdetails-element-csdlbi.md).|  
|DefaultImage|Nein|Ein Verweis auf eine Spalte, die das Bild für die Illustration der Entität enthält.<br /><br /> In mehrdimensionalen Modellen entspricht dieses Element einem binären Attribut im Dimensionsattribut. Wenn dieses Attribut vorhanden ist, muss das Element genau ein MemberRef-Element enthalten.<br /><br /> Finden Sie unter [MemberRef-Element &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DefaultMeasure|Nein|Ein Verweis auf ein Measure in der Entität, das als Standardwert für Berechnungen bezüglich der Entität verwendet werden soll. Fehlt die Angabe, ist SUM der Standardwert.<br /><br /> Finden Sie unter [MemberRef-Element &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DisplayKey|Nein|Eine Liste mit Verweisen auf Spalten oder Rollenenden, die einen starken Bezeichner bilden, der eine Entitätsinstanz eindeutig identifizieren kann.<br /><br /> Finden Sie unter [DisplayKey-Element &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/displaykey-element-csdlbi.md).|  
|Hierarchy|Nein|Eine Liste der Hierarchien im Modell.<br /><br /> Finden Sie unter [Hierarchy-Element &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md).|  
|ReferenceName|Ja|Ein Bezeichner, der verwendet werden kann, um in einer DAX (Data Analysis Expressions)-Abfrage auf diese Entität zu verweisen.<br /><br /> Wenn dieses Attribut nicht angegeben wird, wird der vollqualifizierte Feldname der Entität verwendet.|  
|SortMembers|Nein|Eine Liste von Eigenschaften, nach denen sortiert werden kann. Das SortDirections-Attribut gibt an, ob die Sortierreihenfolge aufsteigend oder absteigend ist.|  
  
## <a name="contents-element"></a>Contents-Element  
 Das **Contents** -Element ist ein einfacher Typ, der den Typ der Daten in der Entität beschreibt.  
  
 Der Inhalt der Entität (Spalte) kann einer der folgenden Werte sein:  
  
|Wert|Description|  
|-----------|-----------------|  
|Regulär|Nicht anderweitig definiert.|  
|Zeit|Attribute, die Zeiträume darstellen, z. B. Jahre, Semester, Quartale, Monate oder Tage.|  
|Geography|Attribute, die geografische Informationen darstellen, z. B. Städte oder Postleitzahlen.|  
|Organization|Attribute, die organisatorische Informationen darstellen, z. B. Angestellte oder Tochterunternehmen.|  
|BillOfMaterials|Attribute, die Informationen zu Inventar oder zur Produktion darstellen, z. B. Stücklisten für Produkte|  
|Konten|Attribute, die ein Kontendiagramm für die Rechnungslegung darstellen.|  
|Customers|Attribute, die Kunden- oder Kontaktinformationen darstellen.|  
|Products|Attribute, die Produktinformationen darstellen.|  
|Szenario|Attribute, die Informationen für die Planung oder strategische Analyse darstellen.|  
|Quantitative|Attribute, die quantitative Informationen darstellen.|  
|Hilfsprogramm|Attribute, die verschiedene Informationen darstellen.|  
|Währung|Enthält Währungsdaten und Metadaten.|  
|Rates|Attribute, die Währungskursinformationen darstellen.|  
|Channel|Attribute, die Kanalinformationen darstellen.|  
|Promotion|Attributen, die verschiedene Marketinghöherstufungsinformationen darstellen.|  
  
## <a name="example"></a>Beispiel  
 **Tabellarisch**  
  
 Das folgende Beispiel enthält eine teilweise Darstellung der Geography-Tabelle in CSDLBI, Version 1.1, die im tabellarischen AdventureWorks-Modell verwendet wird. Die RowNumber-Spalte ist eine ausgeblendete Spalte, die automatisch als Zeilenbezeichner in tabellarischen Modellen erstellt wird und daher Contents-Attribut **RowNumber**aufweist.  
  
```  
  
<EntityType   
     Name="DimGeography">  
     <Key>  
        <PropertyRef Name="RowNumber" />  
     </Key>  
     <Property   
        Name="RowNumber"   
        Type="Int64" Nullable="false">  
     <bi:Property   
        Hidden="true"   
        Contents="RowNumber"   
        Stability="RowNumber" />  
     </Property>  
....  
  
```  
  
## <a name="example"></a>Beispiel  
 **Multidimensional**  
  
 Im folgenden Beispiel werden die EntityType-Elemente in CSDLBI, Version 1.1, veranschaulicht, die einen Teil einer Zeitdimension des Contoso-Vorgangscubes darstellen.  
  
```  
<EntityType   
       Name="CalendarQuarter">  
    <Key>  
       <PropertyRef Name="RowNumber" />  
    </Key>  
  
    <Property Name="RowNumber"   
       Type="Int64"   
       Nullable="false">  
    <bi:Property   
       Hidden="true"   
       Contents="RowNumber"   
       Stability="RowNumber"   
    />  
    </Property>  
  
    <Property Name="CalendarQuarter2"   
       Type="String"   
       MaxLength="Max"   
       Unicode="true"   
       FixedLength="false"   
       Nullable="false">  
    <bi:Property   
       Caption="CalendarQuarter"   
       ReferenceName="CalendarQuarter"   
    />  
    </Property>  
   <bi:EntityType />  
</EntityType>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Technische Referenz für BI-Anmerkungen zu CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
