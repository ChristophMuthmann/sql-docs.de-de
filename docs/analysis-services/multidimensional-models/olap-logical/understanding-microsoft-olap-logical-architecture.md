---
title: "Logische Architektur (Analysis Services – mehrdimensionale Daten) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Services, architecture
- logical architecture [Analysis Services Multidimensional Data]
ms.assetid: 1b9cae0a-8990-4194-af5f-a1ea5f2aff06
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 454dddc6914853bf202376c47a1c929a0df4a6ac
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="understanding-microsoft-olap-logical-architecture"></a>Grundlegendes zur Microsoft OLAP-logische Architektur
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verwendet sowohl Server-als auch Clientkomponenten zum Bereitstellen von online analytical Processing (OLAP) und Datamining-Funktionalität für Business Intelligence-Anwendungen:  
  
-   Die Serverkomponente von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] wird als Microsoft Windows-Dienst implementiert. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] unterstützt mehrere Instanzen auf demselben Computer, wobei jede Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] als eine separate Instanz des Windows-Diensts implementiert.  
  
-   Clients kommunizieren mit [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mithilfe des öffentlichen Standards für XMLA (XML for Analysis). Hierbei handelt es sich um ein SOAP-basiertes Protokoll für die Ausgabe von Befehlen und den Empfang von Antworten in Form eines Webdiensts. Clientobjektmodelle werden ebenfalls über XMLA bereitgestellt. Auf diese Modelle kann sowohl ein verwalteter Anbieter (ADOMD.NET) als auch ein eigener OLE DB-Anbieter zugreifen.  
  
-   Abfragebefehle können mithilfe der folgenden Abfragesprachen ausgegeben werden: SQL; MDX (Multidimensional Expressions), eine Abfragesprache nach Industriestandard für Analysen; oder DMX (Data Mining Extensions), eine am Data Mining orientierte Abfragesprache nach Industriestandard. ASSL (Analysis Services Scripting Language) kann außerdem zum Verwalten von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Datenbankobjekten verwendet werden.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] unterstützt darüber hinaus ein lokales Cubemodul, mit dessen Hilfe Anwendungen auf nicht verbundenen Clients lokal gespeicherte mehrdimensionale Daten suchen können. Weitere Informationen finden Sie unter [Anforderungen an die Clientarchitektur für Analysis Services-Entwicklung](../../../analysis-services/multidimensional-models/olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 **Übersicht über logische Architektur**  
 [Übersicht über logische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **Serverobjekte**  
 [Serverobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/server-objects-analysis-services-multidimensional-data.md)  
  
 **Datenbankobjekte**  
 [Datenbankobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
 **Dimensionsobjekte**  
 [Dimensionsobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Cubeobjekte**  
 [Cubeobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **Sicherheit für den Benutzerzugriff**  
 [Sicherheitsarchitektur für den Benutzerzugriff](http://msdn.microsoft.com/library/71b44e10-2bd0-44f7-8de9-7c8f5b7ac082)  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zur Microsoft OLAP-Architektur](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [Physische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
