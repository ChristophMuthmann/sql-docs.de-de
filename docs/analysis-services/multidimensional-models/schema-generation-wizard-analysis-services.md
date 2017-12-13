---
title: Schemagenerierungs-Assistent (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: relational schema [Analysis Services]
ms.assetid: 68bf7ba3-d0cb-437f-9a3e-9edc0999af19
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5bd04de3519739a08ba65b5ecf2e27e0b5915254
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="schema-generation-wizard-analysis-services"></a>Schemagenerierungs-Assistent (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] unterstützt zwei Methoden zum Arbeiten mit relationalen Schemas, beim Definieren von OLAP-innerhalb Objekte einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt oder einer Datenbank. Normalerweise erfolgt die Definition von OLAP-Objekten basierend auf einem logischen Datenmodell, das in einer Datenquellensicht innerhalb eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts oder einer Datenbank gebildet wird. Diese Datenquellensicht wird basierend auf Schemaelementen aus einer oder mehreren relationalen Datenquellen (wie in der Datenquellensicht angepasst) definiert.  
  
 Alternativ können Sie zuerst OLAP-Objekte definieren und dann eine Datenquellensicht, eine Datenquelle und das zugrunde liegende relationale Datenbankschema generieren, von dem diese OLAP-Objekte unterstützt werden. Diese relationale Datenbank wird als Themenbereichsdatenbank bezeichnet.  
  
 Dieser Ansatz wird mitunter Top-Down-Entwurf genannt und wird häufig für die Erstellung von Prototypen und die Modellierung zu Analysezwecken verwendet. Wenn Sie diesen Ansatz verwenden, können Sie mit dem Schemagenerierungs-Assistenten die zugrunde liegende Datenquellensicht und die Datenquellenobjekte auf Grundlage der in einem Projekt oder einer Datenbank von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] definierten OLAP-Objekte erstellen.  
  
 Dies ist eine iterative Vorgehensweise. Wahrscheinlich müssen Sie den Assistenten mehrere Male erneut ausführen, während Sie das Design der Dimensionen und Cubes ändern. Bei jeder Ausführung des Assistenten werden die Änderungen in die zugrunde liegenden Objekte integriert und so viele Daten der zugrunde liegenden Datenbanken wie möglich beibehalten.  
  
 Das generierte Schema entspricht einem relationalen SQL Server-Datenbankmodulschema. Der Assistent generiert keine Schemas für andere relationale Datenbankprodukte.  
  
 Die Daten, mit denen die Themenbereichsdatenbank aufgefüllt wird, werden getrennt hinzugefügt, und zwar mit dem Tools und Techniken, die Sie zum Auffüllen einer relationalen SQL Server-Datenbank verwenden. In den meisten Fällen werden die Daten beibehalten, wenn Sie den Assistenten erneut ausführen; es gibt jedoch auch Ausnahmen. Einige Daten müssen beispielsweise gelöscht werden, wenn Sie Dimensionen oder Attribute löschen, in denen diese Daten enthalten sind. Wenn der Schemagenerierungs-Assistent einige Daten aufgrund einer Schemaänderung löschen muss, wird vor dem Löschen der Daten eine Warnung angezeigt, sodass Sie die erneute Generierung abbrechen können.  
  
 In der Regel werden Änderungen an Objekten, die ursprünglich vom Schemagenerierungs-Assistenten generiert wurden, überschrieben, wenn der Schemagenerierungs-Assistent dieses Objekt später erneut generiert. Die wichtigste Ausnahme von dieser Regel stellen Spalten dar, die Sie zu einer vom Schemagenerierungs-Assistenten generierten Tabelle hinzufügen. In diesem Fall behält der Schemagenerierungs-Assistent die zur Tabelle hinzugefügten Spalten sowie die Daten in diesen Spalten bei.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In der folgenden Tabelle sind die zusätzlichen Themen in diesem Abschnitt aufgeführt, in denen die Verwendung des Schemagenerierungs-Assistenten erklärt wird.  
  
|Thema|Description|  
|-----------|-----------------|  
|[Verwenden des Schemagenerierungs-Assistenten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/use-the-schema-generation-wizard-analysis-services.md)|Beschreibt, wie das Schema für die Themenbereichs- und Stagingbereichsdatenbanken generiert wird.|  
|[Grundlegendes zu Datenbankschemas](../../analysis-services/multidimensional-models/understanding-the-database-schemas.md)|Beschreibt das Schema, das für die Themenbereichs- und Stagingbereichsdatenbanken generiert wird.|  
|[Grundlegendes zur inkrementellen Generierung](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)|Beschreibt die Funktionen der inkrementellen Generierung des Schemagenerierungs-Assistenten.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Datenquellen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Unterstützte Datenquellen &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
