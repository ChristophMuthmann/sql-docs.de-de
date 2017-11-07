---
title: DimensionAttribute-Datentyp (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DimensionAttribute Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DimensionAttribute
helpviewer_keywords:
- DimensionAttribute data type
ms.assetid: 94349a87-b284-49d1-ac72-888f0375ceb8
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ea4cdde9cf38c673b5894849097c2cc3c6c43309
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dimensionattribute-data-type-assl"></a>DimensionAttribute-Datentyp (ASSL)
  Definiert einen primitiven Datentyp, der ein Attribut in einer Dimension darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DimensionAttribute>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <Type>...</Type>  
   <Usage>...</Usage>  
   <Source>...</Source>  
   <EstimatedCount>...</EstimatedCount>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <ValueColumn>...</ValueColumn>  
   <Translations>...</Translations>  
   <AttributeRelationships>...</AttributeRelationships>  
   <DiscretizationMethod>...</DiscretizationMethod>  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   <RootMemberIf>...</RootMemberIf>  
   <OrderBy>...</OrderBy>  
   <DefaultMember>...</DefaultMember>  
   <OrderByAttributeID>...</OrderByAttributeID>  
   <SkippedLevelsColumn>...</SkippedLevelsColumn>  
   <NamingTemplate>...</NamingTemplate>  
   <MembersWithData>...</MembersWithData>  
   <MembersWithDataCaption>...</MembersWithDataCaption>  
   <NamingTemplateTranslations>...</NamingTemplateTranslations>  
   <CustomRollupColumn>...</CustomRollupColumn>  
   <CustomRollupPropertiesColumn>...</CustomRollupPropertiesColumn>  
   <UnaryOperatorColumn>...</UnaryOperatorColumn>  
   <AttributeHierarchyOrdered>...</AttributeHierarchyOrdered>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <IsAggregatable>...</IsAggregatable>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <AttributeHierarchyDisplayFolder>...</AttributeHierarchyDisplayFolder>  
   <KeyUniquenessGuarantee>...<KeyUniquenessGuarantee>  
   <InstanceSelection>...</InstanceSelection>  
   <Annotations>...</Annotations>  
</DimensionAttribute>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|Keine|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [AttributeHierarchyDisplayFolder](../../../analysis-services/scripting/properties/attributehierarchydisplayfolder-element-assl.md), [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md), [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md), [AttributeHierarchyOrdered](../../../analysis-services/scripting/properties/attributehierarchyordered-element-assl.md), [AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md), [AttributeRelationships](../../../analysis-services/scripting/collections/attributerelationships-element-assl.md), [CustomRollupColumn](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md), [CustomRollupPropertiesColumn](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md), [DefaultMember](../../../analysis-services/scripting/properties/defaultmember-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [DiscretizationBucketCount](../../../analysis-services/scripting/properties/discretizationbucketcount-element-assl.md), [DiscretizationMethod](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md), [EstimatedCount](../../../analysis-services/scripting/properties/estimatedcount-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [InstanceSelection](../../../analysis-services/scripting/properties/instanceselection-element-assl.md), [IsAggregatable](../../../analysis-services/scripting/properties/isaggregatable-element-assl.md), [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md), [KeyUniquenessGuarantee](../../../analysis-services/scripting/properties/keyuniquenessguarantee-element-assl.md), [MemberNamesUnique](../../../analysis-services/scripting/properties/membernamesunique-element-assl.md), [MembersWithData](../../../analysis-services/scripting/properties/memberswithdata-element-assl.md), [MembersWithDataCaption](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md), [NamingTemplate](../../../analysis-services/scripting/properties/namingtemplate-element-assl.md), [NamingTemplateTranslations](../../../analysis-services/scripting/collections/namingtemplatetranslations-element-assl.md), [OrderBy](../../../analysis-services/scripting/properties/orderby-element-assl.md), [OrderByAttributeID](../../../analysis-services/scripting/properties/orderbyattributeid-element-assl.md), [RootMemberIf](../../../analysis-services/scripting/properties/rootmemberif-element-assl.md), [SkippedLevelsColumn](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md), [Type](../../../analysis-services/scripting/properties/type-element-dimensionattribute-assl.md), [UnaryOperatorColumn](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md), [Usage](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md), [ValueColumn](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|  
|Abgeleitete Elemente|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) ([Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md) -Auflistung von [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md))|  
  
## <a name="remarks"></a>Hinweise  
 Die folgenden Einschränkungen gelten beim Ausführen des Diensts DeploymentMode-konfigurationseigenschaftswerten 1 und 2 (SharePoint- und tabellarischer Modus zum Ausführen [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] und tabellarischen modelldatenbanken):  
  
-   Usage-Element akzeptiert nur den KEY-Wert oder REGULAR-Wert.  
  
-   IsAggregatable-Element kann nicht den Wert false haben.  
  
-   OrderBy-Element akzeptiert nur den KEY-Wert oder PROPERTYKEY-Wert.  
  
-   Eine berechnete Spalte kann kein Primärschlüssel in der Tabelle sein.  
  
-   Eine berechnete Spalte kann nicht DataSize in der Bindung enthalten.  
  
-   Für jede berechnete Spalte wird eine Syntaxüberprüfung vor dem Speichern der Attributdefinition ausgeführt.  
  
-   Für AttributeRelationships muss RelationshipType auf den Wert Flexible festgelegt werden.  
  
-   Das von 'RowNumber' angegebene Attribut 'RowNumber' muss den Typ integer aufweisen.  
  
-   Nur das Attribut 'RowNumber' kann KeyBinding vom Typ RowNumberBinding aufweisen.  
  
-   Alle anderen Attribute als 'RowNumber' müssen über eine Kardinalität von eins im Verhältnis zum Schlüssel verfügen, außer wenn das Attribut selbst der Schlüssel ist.  
  
-   Wenn die von OrderBy angegebene Spalte auch der PropertyKey ist, kann OrderByAttributeId nicht auf die Zeilennummernspalte verweisen.  
  
-   Als Schlüssel verwendete Attribute sollten sich auf alle anderen Attribute beziehen; andere Typen von Beziehungen werden nicht unterstützt.  
  
-   Das NullProcessing-Element kann nicht auf 'UnknownMember' festgelegt werden.  
  
-   Bindungen können nicht auf 'Value' festgelegt werden.  
  
 Die folgenden Elemente werden nicht unterstützt, wenn der Dienst in der Konfiguration der DeploymentMode-konfigurationseigenschaftswerten 1 und 2 ausgeführt (SharePoint- und tabellarischer Modus zum Ausführen [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] und tabellarischen modelldatenbanken):  
  
-   AttributeHierarchyOptimizedState  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   DefaultMember  
  
-   DiscretizationBucketCount  
  
-   DiscretizationMethod  
  
-   SkippedLevelsColumn  
  
-   Source  
  
-   UnaryOperatorColumn  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

