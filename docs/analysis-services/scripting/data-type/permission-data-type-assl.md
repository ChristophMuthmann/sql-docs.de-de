---
title: Permission-Datentyp (ASSL) | Microsoft Docs
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
- Permission Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Permission
helpviewer_keywords:
- Permission data type
ms.assetid: 5f309544-59f8-4432-b1eb-b7c1a049f8df
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2db431e9da9930a9b275f0d385b2f9c045c0ae5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="permission-data-type-assl"></a>Permission-Datentyp (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Definiert einen abstrakten, Grunddatentyp, der Informationen über eine individuelle Berechtigung darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Permission>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <RoleID>...</RoleID>  
   <Description>...</Description>  
   <Process>...</Process>  
   <ReadDefinition>...</ReadDefinition>  
   <Read>...</Read>  
   <Write>...</Write>  
   <Annotations>...</Annotations>  
</Permission>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|Keine|  
|Abgeleitete Datentypen|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md), [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md), [DimensionPermission](../../../analysis-services/scripting/data-type/dimensionpermission-data-type-assl.md), [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [Process](../../../analysis-services/scripting/properties/process-element-assl.md), [Read](../../../analysis-services/scripting/properties/read-element-assl.md), [ReadDefinition](../../../analysis-services/scripting/properties/readdefinition-element-assl.md), [RoleID](../../../analysis-services/scripting/properties/roleid-element-assl.md), [Write](../../../analysis-services/scripting/properties/write-element-assl.md)|  
|Abgeleitete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 **Berechtigung** fungiert als abstrakter Basistyp für eine Anzahl abgeleiteter Berechtigungstypen, die in einer Instanz von verwendet [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Diesem Datentyp sind unter dem DeploymentMode-Wert 2 (tabellarischer Servermodus) die folgenden Überprüfungen zugeordnet:  
  
-   *Process* -Attribut, dessen Standardwert auf **False**festgelegt wird, außer wenn der Benutzer über die Berechtigung **Aktualisieren** verfügt. Für Benutzer mit der Berechtigung **Aktualisieren** wird der *Process* -Attributwert auf **True**festgelegt.  
  
-   *ReadDefinition* -Attribut, dessen Wert auf **None**festgelegt wird. Bei jedem anderen Wert wird ein Fehler generiert.  
  
-   Der*Read* -Attributwert wird auf **Allowed** für Benutzer mit der Berechtigung **Benutzer** und auf **None** festgelegt, wenn die Benutzer der Berechtigung **Aktualisieren** zugewiesen wurden. Wenn ein Benutzer sowohl über die Berechtigung **Benutzer** als auch über die Berechtigung **Aktualisieren** verfügt, wird das Attribut auf **Allowed**festgelegt. Für Benutzer mit Administratorrechten wird der Attributwert auf **Allowed**festgelegt.  
  
-   *Write* -Attribut, dessen Wert auf **None**festgelegt wird. Bei jedem anderen Wert wird ein Fehler generiert.  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Siehe auch  
 [Role-Element & #40; ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Analysis Services Scripting Language-XML-Datentypen & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
