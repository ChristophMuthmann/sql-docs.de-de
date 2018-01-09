---
title: Dimensionsbeziehungen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- relationships [Analysis Services]
- member groups [Analysis Services]
- regular dimensions [Analysis Services]
- many-to-many relationships [Analysis Services]
- cubes [Analysis Services], relationships
- reference dimensions
- dimensions [Analysis Services], relationships
- fact dimensions [Analysis Services]
- relationships [Analysis Services], dimensions
ms.assetid: de54c059-cb0f-4f66-bd70-8605af05ec4f
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 0ba0ea6e2797d15134dc6bfbf9a595a1ef83c583
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="dimension-relationships"></a>Dimensionsbeziehungen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Die Dimensionsverwendung werden die Beziehungen zwischen Cubedimensionen und Measuregruppen in einem Cube definiert. Bei einer Cubedimension handelt es sich um eine Instanz einer Datenbankdimension, die in einem bestimmten Cube verwendet wird. Ein Cube kann über Cubedimensionen verfügen (und verfügt oft über solche), die nicht direkt mit einer Measuregruppe verknüpft sind, die jedoch möglicherweise über eine andere Dimension oder Measuregruppe indirekt mit der Measuregruppe verknüpft sind. Wenn Sie einen Cube, eine Datenbankgruppe Dimension oder Measuregruppe hinzufügen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] versucht, die Dimensionsverwendung zu bestimmen, indem die Beziehungen zwischen den Dimensionstabellen und Faktentabellen in der Datenquellensicht des Cubes sowie durch Untersuchen die Beziehungen zwischen Attributen. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] legt die Einstellungen für die Dimensionsverwendung für die erkannten Beziehungen automatisch fest.  
  
 Eine Beziehung zwischen einer Dimension und einer Measuregruppe besteht aus den an der Beziehung teilnehmenden Dimensions- und Faktentabellen und einem Granularitätsattribut, das die Granularität der Dimension in der jeweiligen Measuregruppe angibt.  
  
## <a name="regular-dimension-relationships"></a>Reguläre Dimensionsbeziehungen  
 Eine reguläre Dimensionsbeziehung zwischen einer Cubedimension und einer Measuregruppe ist vorhanden, wenn die Schlüsselspalte der Dimension direkt mit der Faktentabelle verknüpft ist. Diese direkte Beziehung basiert auf einer Primärschlüssel-Fremdschlüssel-Beziehung in der zugrunde liegenden relationalen Datenbank, kann jedoch auch auf einer in der Datenquellensicht definierten logischen Beziehung basieren. Eine reguläre Dimensionsbeziehung stellt die Beziehung zwischen Dimensionstabellen und einer Faktentabelle in einem traditionellen Sternschemaentwurf dar. Weitere Informationen zu regulären Beziehungen finden Sie unter [Definieren einer regulären Beziehung und die Eigenschaften der regulären Beziehung](../../analysis-services/multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md).  
  
## <a name="reference-dimension-relationships"></a>Bezugsdimensionsbeziehungen  
 Eine Bezugsdimensionsbeziehung zwischen einer Cubedimension und einer Measuregruppe ist vorhanden, wenn die Schlüsselspalte für die Dimension über einen Schlüssel in einer anderen Dimensionstabelle indirekt mit der Faktentabelle verknüpft ist, wie in der folgenden Abbildung gezeigt.  
  
 ![Logisches Diagramm, referenzierte dimensionsbeziehung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-refdimension1.gif "logisches Diagramm, referenzierte dimensionsbeziehung")  
  
 Eine Bezugsdimensionsbeziehung stellt die Beziehung zwischen Dimensionstabellen und einer Faktentabelle in einem Schneeflocken-Schemaentwurf dar. Wenn Dimensionstabellen in einem Schneeflockenschema verbunden sind, können Sie eine einzelne Dimension mithilfe von Spalten aus mehreren Tabellen definieren, oder Sie können separate Dimensionen basierend auf den separaten Dimensionstabellen definieren und anschließend mithilfe der Einstellung für die Bezugsdimensionsbeziehung einen Link zwischen ihnen definieren. Die folgende Abbildung zeigt eine Faktentabelle namens **InternetSales**und zwei Dimensionstabellen namens **Customer** und **Geography**in einem Schneeflockenschema.  
  
 ![Logisches Schema, referenzierte dimensionsbeziehung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-refdim-schema1.gif "logisches Schema, referenzierte dimensionsbeziehung")  
  
 Sie können eine Dimension mit der **Customer** -Tabelle als Haupttabelle der Dimension erstellen und die **Geography** -Tabelle als verknüpfte Tabelle einschließen. Anschließend wird eine reguläre Beziehung zwischen der Dimension und der InternetSales-Measuregruppe definiert.  
  
 Alternativ können Sie zwei mit der InternetSales-Measuregruppe verknüpfte Dimensionen erstellen: eine auf der **Customer** -Tabelle basierende Dimension und eine auf der **Geography** -Tabelle basierende Dimension. Anschließend können Sie die Geography-Dimension mit einer Bezugsdimensionsbeziehung mithilfe der Customer-Dimension mit der InternetSales-Measuregruppe verknüpfen. In diesem Fall werden die Fakten in der InternetSales-Measuregruppe, wenn sie durch die Geography-Dimension dimensioniert werden, nach Kunde und nach Geografie dimensioniert. Wenn der Cube eine zweite Measuregruppe namens Reseller Sales enthalten würde, können Sie die Fakten in der Reseller Sales-Measuregruppe nicht durch Geography dimensionieren, da keine Beziehung zwischen Reseller Sales und Geography vorhanden wäre.  
  
 Es gibt keine Begrenzung der Anzahl der Bezugsdimensionen, die miteinander verkettet werden können, wie in der folgenden Abbildung gezeigt.  
  
 ![Logisches Diagramm, referenzierte dimensionsbeziehung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-refdimension2.gif "logisches Diagramm, referenzierte dimensionsbeziehung")  
  
 Weitere Informationen zu referenzierten Beziehungen finden Sie unter [Definieren einer referenzierten Beziehung und referenzierten Beziehungseigenschaften](../../analysis-services/multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md).  
  
## <a name="fact-dimension-relationships"></a>Faktendimensionsbeziehungen  
 Faktendimensionen, die häufig als degenerierte Dimensionen bezeichnet werden, sind Standarddimensionen, die aus Attributspalten in Faktentabellen statt aus Attributspalten in Dimensionstabellen erstellt werden. Nützliche Dimensionsdaten werden manchmal in einer Faktentabelle gespeichert, um die Duplizierung zu reduzieren. Z. B. das folgende Diagramm zeigt die **FactResellerSales** -Faktentabelle aus der [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] -Beispieldatenbank.  
  
 ![Spalten in der Tat können Dimensionen unterstützen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-factdim.gif "Spalten in der Tat können Dimensionen unterstützen")  
  
 Die Tabelle enthält Attributinformationen nicht nur für jede Zeile einer von einem Wiederverkäufer aufgegebenen Bestellung, sondern auch zu der Bestellung selbst. Die im vorherigen Diagramm eingekreisten Attribute identifizieren die Informationen in der **FactResellerSales** -Tabelle, die als Attribute in einer Dimension verwendet werden können. In diesem Fall werden zwei zusätzliche Informationen, die Transporteurkennung und die vom Wiederverkäufer ausgegebene Nummer der Bestellung, durch die Attributspalten CarrierTrackingNumber und CustomerPONumber dargestellt. Diese Informationen sind interessant – beispielsweise wären Benutzer auf jeden Fall daran interessiert, aggregierte Informationen, z. B. die Gesamtproduktkosten, für alle Bestellungen zu sehen, die unter einer einzelnen Kennung versendet werden. Aber ohne eine Dimension gibt es keine Möglichkeit, Daten für diese beiden Attribute zu organisieren oder zu aggregieren.  
  
 Theoretisch können Sie eine Dimensionstabelle erstellen, die die gleichen Schlüsselinformationen verwendet wie die FactResellerSales-Tabelle, und die anderen beiden Attributspalten, CarrierTrackingNumber und CustomerPONumber, in jene Dimensionstabelle verschieben. Sie würden jedoch einen wesentlichen Teil der Daten duplizieren und dem Data Warehouse unnötige Komplexität hinzufügen, um lediglich zwei Attribute als separate Dimension darzustellen.  
  
> [!NOTE]  
>  Faktendimensionen werden häufig zur Unterstützung von Drillthroughaktionen verwendet. Weitere Informationen zu Aktionstypen finden Sie unter [Aktionen &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Faktendimensionen müssen nach jedem Update der Measuregruppe, auf die durch die Faktenbeziehung verwiesen wird, inkrementell aktualisiert werden. Wenn die Fact-Dimension eine ROLAP-Dimension ist die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verarbeitungsmodul alle Caches und verarbeitet die Measuregruppe inkrementell.  
  
 Weitere Informationen zu faktenbeziehungen finden Sie unter [Definieren einer Faktenbeziehung und Faktenbeziehungseigenschaften](../../analysis-services/multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md).  
  
## <a name="many-to-many-dimension-relationships"></a>m:n-Dimensionsbeziehungen  
 In den meisten Dimensionen ist jedes Faktum mit einem und nur einem Dimensionselement verknüpft, und ein einzelnes Dimensionselement kann mehreren Fakten zugeordnet sein. In der Terminologie von relationalen Datenbanken wird dies als 1:n-Beziehung bezeichnet. Es ist jedoch oft nützlich, ein einzelnes Faktum mit mehreren Dimensionselementen zu verknüpfen. Ein Bankkunde verfügt z. B. möglicherweise über mehrere Konten (Giro-, Sparbuch-, Kreditkarten- und Investmentkonten), und ein Konto kann auch über gemeinsame oder mehrere Besitzer verfügen. Die aus diesen Beziehungen erstellte Customer-Dimension hätte dann mehrere Elemente, die mit einer einzelnen Kontotransaktion verknüpft sind.  
  
 ![Logische Schema/n: n-dimensionsbeziehung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-many-dimension1.gif "logische Schema/n: n-dimensionsbeziehung")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] können Sie eine m: n-Beziehung zwischen einer Dimension und einer Faktentabelle zu definieren.  
  
> [!NOTE]  
>  Zur Unterstützung einer m:n-Dimensionsbeziehung muss in der Datenquellensicht eine Fremdschlüsselbeziehung zwischen allen beteiligten Tabellen eingerichtet worden sein, wie in der vorherigen Abbildung dargestellt ist. Andernfalls können Sie beim Einrichten der Beziehung auf der Registerkarte **Dimensionsverwendung** des Dimensions-Designers nicht die richtige Zwischenmeasuregruppe auswählen.  
  
 Weitere Informationen zu viele-zu-viele-Beziehungen finden Sie unter [definieren eine m: N-Beziehung und viele-zu-viele-Beziehungseigenschaften](../../analysis-services/multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Dimensionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
