---
title: DataSource-Datentyp (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- DataSource Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataSource data type
ms.assetid: 05e8de8d-452d-4128-98a6-4437df227fec
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 852397bf390325ff979a14b5ed57ec4f71850288
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="datasource-data-type-assl"></a>DataSource-Datentyp (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Definiert einen abstrakten Grunddatentyp, der eine Datenquelle in einem [Database](../../../analysis-services/scripting/objects/database-element-assl.md) -Element darstellt.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<DataSource>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <ManagedProvider>...</ManagedProvider>  
   <ConnectionString>...</ConnectionString>  
   <ConnectionStringSecurity>...</ConnectionStringSecurity>  
   <ImpersonationInfo>...</ImpersonationInfo>  
   <Isolation>...</Isolation>  
   <MaxActiveConnections>...</MaxActiveConnections>  
   <Description>...</Description>  
   <Timeout>...</Timeout>  
   <Annotations>...</Annotations>  
   <DataSourcePermission>...</DataSourcePermission>  
</DataSource>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|Keine|  
|Abgeleitete Datentypen|[RelationalDataSource](../../../analysis-services/scripting/data-type/relationaldatasource-data-type-assl.md), [OlapDataSource](../../../analysis-services/scripting/data-type/olapdatasource-data-type-assl.md), [PushedDataSource](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [ConnectionString](../../../analysis-services/scripting/properties/connectionstring-element-assl.md), [ConnectionStringSecurity](../../../analysis-services/scripting/properties/connectionstringsecurity-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [DataSourcePermission](../../../analysis-services/scripting/collections/datasourcepermissions-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [ImpersonationInfo](../../../analysis-services/scripting/properties/impersonationinfo-element-assl.md), [Isolation](../../../analysis-services/scripting/properties/isolation-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [ManagedProvider](../../../analysis-services/scripting/properties/managedprovider-element-assl.md), [MaxActiveConnections](../../../analysis-services/scripting/properties/maxactiveconnections-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [Timeout](../../../analysis-services/scripting/properties/timeout-element-assl.md)|  
|Abgeleitete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Beim Definieren von Out-of-Line-Bindungen ist das **Name** -Element optional. Wenn kein **Name** -Element spezifiziert werden muss, können Datenquellen innerhalb der Bindung für Cubes, Partitionen usw. definiert werden. Für Datenquellen, die in einem **Database** -Element enthalten sind, ist **Name** ein erforderliches Element.  
  
 Weitere Informationen zu Datenquellen finden Sie unter [Datenquellen in mehrdimensionalen Modellen](../../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md).  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.DataSource>.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
