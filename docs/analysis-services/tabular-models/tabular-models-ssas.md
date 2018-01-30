---
title: Tabellarische Modelle | Microsoft Docs
ms.custom: 
ms.date: 01/29/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: edeea89c1d767364f4f087d0f4b2e6d566895c52
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="tabular-models"></a>Tabellarische Modelle
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Tabellarische Modelle sind Analysis Services-Datenbanken, die im Arbeitsspeicher oder im DirectQuery-Modus Zugriff auf Daten direkt aus relationalen Back-End-Datenquellen auszuführen.  
  
 In-Memory ist die Standardeinstellung. Mithilfe der Technik Komprimierungsalgorithmen und einen Multithreaded-Abfrageprozessor, das Analysemodul bietet schnellen Zugriff auf tabellenmodellobjekte und-Daten berichterstellungsclientanwendungen wie Power BI und Excel.  
  
 DirectQuery ist ein alternativer Abfragemodus für Modelle, die für den Arbeitsspeicher zu groß sind. Er eignet sich auch, wenn aufgrund von Datenflüchtigkeit keine angemessene Verarbeitungsstrategie möglich ist. In dieser Version erzielt DirectQuery eine größere Parität mit In-Memory-Modellen, indem Folgendes unterstützt wird: zusätzliche Datenquellen, die Verarbeitung von berechneten Tabellen und Spalten in einem DirectQuery-Modell, die Sicherheit auf Zeilenebene über DAX-Ausdrücke, die die Back-End-Datenbank erreichen, sowie die Optimierung von Abfragen, die zu einem höheren Durchsatz als in früheren Versionen führen.
  
 Tabellarische Modelle werden in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] unter Verwendung der Projektvorlage für tabellarische Modelle erstellt. Diese bietet eine Entwurfsoberfläche zum Erstellen von Modellen, Tabellen, Beziehungen und DAX-Ausdrücken. Sie können Daten aus mehreren Quellen importieren und das Modell erweitern, indem Sie Beziehungen, berechnete Tabellen und Spalten, Measures, KPIs, Hierarchien und Übersetzungen hinzufügen.  
  
 Modelle können dann mit Azure Analysis Services bereitgestellt werden, oder eine Instanz von SQL Server Analysis Services für den tabellarischen Servermodus konfiguriert. Bereitgestellte tabellarische Modelle können genauso wie mehrdimensionale Modelle in SQL Server Management Studio verwaltet werden. Sie können partitioniert werden, um die Verarbeitung zu optimieren, und durch die Verwendung der rollenbasierten Sicherheit bis auf Zeilenebene gesichert werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Projektmappen für tabellarische Modelle](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md) -Themen in diesem Abschnitt wird beschrieben, erstellen und Bereitstellen von Projektmappen für tabellarische Modelle.
  
 [Tabellarische modelldatenbanken](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md) -Themen in diesem Abschnitt wird beschrieben, Verwalten von Projektmappen für bereitgestellte tabellarische Modelle.
  
 [Zugriff auf tabellarische Modelldaten](../../analysis-services/tabular-models/tabular-model-data-access.md) -Themen in diesem Abschnitt wird beschrieben, Herstellen einer Verbindung mit Projektmappen für tabellarische Modelle bereitgestellt.
  
## <a name="see-also"></a>Siehe auch  
 [Neuigkeiten in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Vergleichen von tabellarischen und mehrdimensionalen Lösungen](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [In Analysis Services verwendete Tools und Anwendungen](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [DirectQuery Mode](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
