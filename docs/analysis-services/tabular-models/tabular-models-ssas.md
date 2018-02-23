---
title: Tabellarische Modelle | Microsoft Docs
ms.custom: 
ms.date: 02/21/2018
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
ms.openlocfilehash: 2df607b47e4bb2a5a770e27d1bceb5a6d7e6ebbc
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="tabular-models"></a>Tabellarische Modelle
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Tabellarische Modelle sind Analysis Services-Datenbanken, die im In-Memory- oder im DirectQuery-Modus ausgeführt werden. Sie greifen in relationalen Back-End-Datenquellen direkt auf Daten zu. Mithilfe der Technik Komprimierungsalgorithmen und einen Multithreaded-Abfrageprozessor das Analysemodul bietet schnellen Zugriff auf tabellenmodellobjekte und-Daten berichterstellungsclientanwendungen wie Power BI und Excel.  
  
 Bei speicherinternen Modellen den Standardeintrag sind, zwar DirectQuery ist ein alternativer Abfragemodus für Modelle, die entweder zu groß im Arbeitsspeicher, oder wenn datenflüchtigkeit eine angemessene verarbeitungsstrategie möglich. DirectQuery erzielt wie bei speicherinternen Modellen unterstützt eine Vielzahl von Datenquellen, zur Behandlung von berechneten Tabellen und Spalten in einem DirectQuery-Modell, Sicherheit auf Zeilenebene über DAX-Ausdrücke, die die Back-End-Datenbank zu erreichen, und Fragen Optimierungen, die zu einem höheren Durchsatz führen.
  
 Tabellarische Modelle werden in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] unter Verwendung der Projektvorlage für tabellarische Modelle erstellt. Diese bietet eine Entwurfsoberfläche zum Erstellen von Modellen, Tabellen, Beziehungen und DAX-Ausdrücken. Sie können Daten aus mehreren Quellen importieren und das Modell erweitern, indem Sie Beziehungen, berechnete Tabellen und Spalten, Measures, KPIs, Hierarchien und Übersetzungen hinzufügen.  
  
 Modelle können dann mit Azure Analysis Services bereitgestellt werden, oder eine Instanz von SQL Server Analysis Services für den tabellarischen Servermodus konfiguriert. Bereitgestellte tabellarische Modelle können in SQL Server Management Studio verwaltet werden. Wie die Modelle zunehmen, können sie für die optimierte Verarbeitung partitioniert und auf die Zeilenebene mithilfe rollenbasierter Sicherheit gesichert werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Projektmappen für tabellarische Modelle](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md) -Artikel in diesem Abschnitt wird beschrieben, erstellen und Bereitstellen von Projektmappen für tabellarische Modelle.
  
 [Tabellarische modelldatenbanken](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md) -Artikel in diesem Abschnitt wird beschrieben, Verwalten von Projektmappen für bereitgestellte tabellarische Modelle.
  
 [Zugriff auf tabellarische Modelldaten](../../analysis-services/tabular-models/tabular-model-data-access.md) -Artikel in diesem Abschnitt wird beschrieben, Herstellen einer Verbindung mit Projektmappen für tabellarische Modelle bereitgestellt.
  
## <a name="see-also"></a>Siehe auch  
 [Neuigkeiten in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Vergleichen von tabellarischen und mehrdimensionalen Lösungen](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [In Analysis Services verwendete Tools und Anwendungen](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [DirectQuery-Modus](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Kompatibilitätsgrad](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
