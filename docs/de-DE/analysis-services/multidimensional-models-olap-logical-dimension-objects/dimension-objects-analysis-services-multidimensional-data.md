---
title: Dimension-Objekten (Analysis Services – mehrdimensionale Daten) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e2c8ec6b4551605e7c2d659c021944966f630bda
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>Dimensionsobjekte (Analysis Services – Mehrdimensionale Daten)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ein einfaches <xref:Microsoft.AnalysisServices.Dimension>-Objekt besteht aus grundlegenden Informationen, Attributen und Hierarchien. Grundlegende Informationen beinhalten den Namen der Dimension, den Typ der Dimension, die Datenquelle, den Speichermodus usw. Attribute definieren die tatsächlichen Daten in der Dimension. Attribute gehören nicht notwendigerweise zu einer Hierarchie, aber Hierarchien werden aus Attributen erstellt. Eine Hierarchie erstellt geordnete Listen von Ebenen und definiert die Arten, wie ein Benutzer die Dimension durchsuchen kann.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In den folgenden Themen erhalten Sie weitere Informationen zum Entwerfen und Implementieren von Dimensionsobjekten.  
  
|Thema|Description|  
|-----------|-----------------|  
|[Dimensionen & #40; Analysis Services – mehrdimensionale Daten & #41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Dimensionen sind eine wesentliche Komponente von Cubes. Mit Dimensionen werden Daten nach Interessensbereichen geordnet, z. B. nach Kunden, Geschäften oder Angestellten.|  
|[Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)|Dimensionen sind Auflistungen von Attributen, die an eine oder mehrere Spalten in einer Tabelle oder Sicht in der Datenquellensicht gebunden sind.|  
|[Attributbeziehungen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)|In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Attributen innerhalb einer Dimension sind immer entweder direkt oder indirekt mit dem Schlüsselattribut verknüpft. Wenn Sie eine Dimension auf Basis eines Sternschemas definieren, in dem sämtliche Dimensionsattribute aus derselben relationalen Tabelle abgeleitet werden, wird automatisch eine Attributbeziehung zwischen dem Schlüsselattribut und den einzelnen Nichtschlüsselattributen definiert. Wenn Sie eine Dimension auf Basis eines Schneeflockenschemas definieren, in dem Dimensionsattribute aus mehreren verknüpften Tabellen abgeleitet werden, wird eine Attributbeziehung automatisch wie folgt definiert:<br /><br /> Zwischen dem Schlüsselattribut und den einzelnen Nichtschlüsselattributen, die an die Spalten in der Dimensionshaupttabelle gebunden sind<br /><br /> Zwischen dem Schlüsselattribut und dem Attribut, das an den Fremdschlüssel in der sekundären Tabelle gebunden ist, die die zugrunde liegenden Dimensionstabellen verknüpft<br /><br /> Zwischen dem Attribut, das an den Fremdschlüssel in der sekundären Tabelle gebunden ist, und den einzelnen Nichtschlüsselattributen, die an Spalten aus der sekundären Tabelle gebunden sind|  
  
  
