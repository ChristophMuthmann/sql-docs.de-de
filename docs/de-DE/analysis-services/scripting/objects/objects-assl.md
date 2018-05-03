---
title: Objekte (ASSL) | Microsoft Docs
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ASSL, objects
- objects [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
ms.assetid: 0f672b93-c317-47e5-b44d-ecea9b587c98
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d45d482ecb50e0215b9d0ad5d57f537e8899d5c5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="objects-assl"></a>Objekte (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  In diesem Referenzabschnitt finden Sie Syntax- und Nutzungsinformationen für jedes Element, das im ASSL-Schema (Analysis Services Scripting Language) als Objekt agiert.  
  
 Obwohl das ASSL-Schema nur XML-Elemente, aus der Sicht eines Entwicklers, enthält die Elemente, die in diesem Abschnitt beschriebenen entsprechen für Objekte, z. B. **Datenbank**, **Cube**, und  **Dimension** Objekte, in der Hierarchie der enthaltenen Objekte von einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Objekte sind niemals Blattebenenelemente im ASSL-Schema, sondern besitzen untergeordnete Elemente und Elemente, die Objekteigenschaften entsprechen.  
  
 In einigen Fällen wird ein Blattebenenelement im Schema, das eine Eigenschaft zu sein scheint, als Objekt klassifiziert, da der Typ des Elements ein Objekttyp ist. Z. B. die **Quelle** von einem **Dimension** Objekt ist vom Typ **DimensionBinding**.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Element|Description|  
|-------------|-----------------|  
|[Konto Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/account-element-assl.md)|Enthält Details über einen Kontotyp innerhalb einer [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) Element.|  
|[Action-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/action-element-assl.md)|Enthält Informationen über eine Aktion in einem [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) -Element oder einem [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) -Element.|  
|[Aggregation-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)|Definiert eine einzelne Aggregation für ein [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md) Element.|  
|[AggregationDesign-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|Definiert einen Satz von Aggregationsdefinitionen, die für mehrere Partitionen in einer Datenbank freigegeben sein können.|  
|[AggregationInstance-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|Definiert für eine Partition eine Aggregationsinstanz.|  
|[AlgorithmParameter-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|Definiert einen Parameter für den Algorithmus, der verwendet wird, indem Sie eine [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) Element.|  
|[AllMemberTranslation-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/allmembertranslation-element-assl.md)|Enthält eine Übersetzung für die Beschriftung des alle-Elements ein [Hierarchie](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) Element.|  
|[Annotation-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/annotation-element-assl.md)|Enthält Elemente, die verwendet werden, um das ASSL-Schema zu erweitern.|  
|[Assembly-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)|Stellt eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Assembly oder einer COM-dynamic Link Library (DLL) zugeordnet eine [Server](../../../analysis-services/scripting/objects/server-element-assl.md) Element oder ein [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) Element.|  
|[-Attribut Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attribute-element-assl.md)|Enthält die Beschreibung eines Attributs.|  
|[AttributeAllMemberTranslation-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributeallmembertranslation-element-assl.md)|Enthält eine Übersetzung für die Beschriftung des alle-Elements ein [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) Element.|  
|[AttributePermission-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|Definiert den Berechtigungen, die Elemente einer [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element verfügen, auf die Attribute einer individuellen Dimension in einem [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) Element.|  
|[AttributeRelationship-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|Bietet Details über die Beziehung zwischen zwei Attributen.|  
|[Element sperren &#40;ASSL&#41;](../../../analysis-services/scripting/objects/block-element-assl.md)|Enthält alles oder einen Teil des binären Inhalts eine [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) Element.|  
|[Calculation-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/calculation-element-assl.md)|Weist eine Berechnung mit einem [Perspektive](../../../analysis-services/scripting/objects/perspective-element-assl.md) Element.|  
|[CalculationProperty-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)|Enthält eine Auflistung von Benutzeroberflächeneigenschaften für eine Berechnung, die in verwendet ein [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) Element.|  
|[CaptionColumn-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|Definiert die Spalte, die die Beschriftung für das Attribut bereitstellt.|  
|[CellPermission-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)|Beschreibt den Berechtigungen der Elemente einer [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element besitzen, für einzelne Zellen innerhalb einer [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) Element.|  
|[Column-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/column-element-assl.md)|Beschreibt eine Spalte in der Auflistung der Spalten, die mit dem übergeordneten Element verknüpft ist.|  
|[Befehl Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/command-element-assl.md)|Definiert einen Befehl, der im Kontext des übergeordneten Elements der Befehlsauflistung verfügbar ist.|  
|[Cube-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)|Definiert einen regulären, virtuellen oder verknüpften Cube in einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) Element.|  
|[CubePermission-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|Definiert die Berechtigungen der Elemente eines bestimmten [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element in einer bestimmten [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) Element.|  
|[CustomRollupColumn-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|Definiert die Details der Spalte, die eine benutzerdefinierte Rollupformel enthält.|  
|[CustomRollupPropertiesColumn-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|Definiert die Details einer Spalte, die die Eigenschaften einer benutzerdefinierten Rollupformel bereitstellen.|  
|[Datenelement &#40;ASSL&#41;](../../../analysis-services/scripting/objects/data-element-assl.md)|Enthält (in der Auflistung der untergeordneten **Block** Elemente) des binären Inhalts eine [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) Element.|  
|[Database-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)|Definiert eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Datenbank.|  
|[DatabasePermission-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|Definiert die Standardberechtigungen in einem [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) -Element für ein bestimmtes [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element.|  
|[DataSource-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasource-element-assl.md)|Definiert eine Datenquelle in einem [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) Element.|  
|[DataSourcePermission-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)|Definiert die Standardberechtigungen in einem [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) für einen bestimmten Datentyp [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element.|  
|[DataSourceView-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|Definiert eine Datenquellensicht, die verwendet werden, indem eine [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) Element.|  
|[Dimension-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)|Definiert eine Dimension.|  
|[DimensionPermission-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|Definiert die Berechtigungen, die zu einem bestimmten [Role](../../../analysis-services/scripting/objects/role-element-assl.md) -Element für eine spezifische Datenbank- oder Cubedimension gehören.|  
|[ErrorConfiguration-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|Gibt Einstellungen für den Umgang mit Fehlern an, die auftreten können, wenn das übergeordnete Element verarbeitet wird.|  
|[Event-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/event-element-assl.md)|Definiert ein Ereignis, das im Rahmen des erfasst werden eine [Ablaufverfolgung](../../../analysis-services/scripting/objects/trace-element-assl.md) Element.|  
|[Datei Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/file-element-assl.md)|Definiert eine der Dateien, aus denen sich, ein [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) Element.|  
|[ForeignKeyColumn-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|Identifiziert den Join zu einer übergeordneten Tabelle für eine relationale Datenquelle.|  
|[Group-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/group-element-assl.md)|Definiert eine Gruppe von Elementen, die an ein Attribut gebunden sind.|  
|[Hierarchy-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|Definiert eine Hierarchie in einer Dimension.|  
|[IncrementalProcessingNotification-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)|Enthält Informationen für die [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) Element über eine Abfrage zum Ermitteln des Fortschritts der inkrementellen Verarbeitung ausgeführt.|  
|[KeyColumn-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|Enthält die Definition einer Spalte, die der Schlüssel oder Teil eines Schlüssels für ein Attribut ist.|  
|[KPI-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/kpi-element-assl.md)|Definiert einen Key Performance Indicator (KPI) innerhalb eines [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) -Elements oder eines [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) -Elements.|  
|[Level-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/level-element-assl.md)|Definiert eine Ebene in einer [Hierarchie](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) Element.|  
|[MdxScript-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|Enthält Informationen über ein Multidimensional Expressions (MDX)-Skript, das zugeordnet ist ein [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) Element.|  
|[Measure-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measure-element-assl.md)|Definiert ein Measure.|  
|[MeasureGroup-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Definiert auf der gleichen Ebene wie die Granularität eine Menge von Measures.|  
|[Member-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/member-element-assl.md)|Enthält den Namen eines Mitglieds eines [Group](../../../analysis-services/scripting/objects/group-element-assl.md) - oder [Role](../../../analysis-services/scripting/objects/role-element-assl.md) -Elements.|  
|[MiningModel-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|Definiert ein einzelnes Data Mining-Modell.|  
|[Miningmodelpermission-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)|Definiert die Berechtigungen der Elemente einer [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element besitzen, für ein einzelnes [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) Element.|  
|[MiningStructure-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|Definiert die Struktur für einen Satz von Miningmodellen.|  
|[Miningstructurepermissions-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|Definiert den Berechtigungen, die Elemente einer [Rolle](../../../analysis-services/scripting/objects/role-element-assl.md) Element besitzen, für ein einzelnes [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) Element.|  
|[ModelingFlag-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/modelingflag-element-assl.md)|Enthält ein Modellierungsflag für eine Spalte in einer Miningstruktur oder einem Miningmodell.|  
|[NameColumn-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|Identifiziert die Spalte, die den Namen des übergeordneten Elements bereitstellt.|  
|[NamingTemplateTranslation-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/namingtemplatetranslation-element-assl.md)|Stellt eine lokalisierte Übersetzung der **NamingTemplate** -Element eines übergeordneten [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) -Datentyp.|  
|[Partitions-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|Definiert eine Partition eine [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) Element oder eine partitionsbindung in einem Out-of-Line [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)Element.|  
|[Perspective-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)|Definiert Details für eine Perspektive eines eine [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) Element.|  
|[ProactiveCaching-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|Definiert die Einstellungen für die proaktive Zwischenspeicherung für das übergeordnete Element.|  
|[QueryNotification-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/querynotification-element-assl.md)|Enthält Informationen für die [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) Element über eine Abfrage ausführen, um zu bestimmen, ob eine Datenquelle geändert wurde.|  
|[ReportFormatParameter-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|Enthält den Namen und Wert eines Parameters, der angibt, wie eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -Bericht bei der Ausführung formatiert ist.|  
|[ReportParameter-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|Enthält den Namen und den Wert eines Parameters, der bei der Ausführung an einen [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Bericht weitergeleitet wird.|  
|[Role-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/role-element-assl.md)|Enthält Informationen über eine Sicherheitsrolle.|  
|[Server-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/server-element-assl.md)|Beschreibt Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[ServerProperty-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|Definiert eine zugeordnete Servereigenschaft eine [Server](../../../analysis-services/scripting/objects/server-element-assl.md) Element.|  
|[SkippedLevelsColumn-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|Stellt die Details einer Spalte bereit, die die Anzahl der übersprungenen (leeren) Ebenen zwischen den einzelnen Elementen und den jeweils übergeordneten Elementen speichert.|  
|[SourceMeasureGroup-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|Identifiziert die Measuregruppe, die als Datenquelle für eine Miningstruktur-Spalte dient.|  
|[TableNotification-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|Enthält Informationen für die [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) Element zu einer Tabelle oder Sicht in einer Datenquelle, die geändert wurde.|  
|[Trace-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/trace-element-assl.md)|Definiert eine Ablaufverfolgung, die abgefragt werden kann.|  
|[Translation-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)|Stellt eine lokalisierte Übersetzung für das übergeordnete Element der [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md) -Auflistung bereit.|  
|[UnaryOperatorColumn-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|Definiert die Details einer Spalte, die einen unären Operator bereitstellt.|  
|[UnknownMemberTranslation-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)|Enthält eine Übersetzung für die Beschriftung des der [UnknownMember](../../../analysis-services/scripting/properties/unknownmember-element-assl.md) -Element für eine [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md) Element.|  
|[ValueColumn-Element &#40;ASSL&#41;](../../../analysis-services/scripting/objects/valuecolumn-element-assl.md)|Identifiziert die Spalte, die den Wert des übergeordneten Elements bereitstellt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Element-Hierarchie & #40; ASSL & #41;](../../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)  
  
  
