---
title: Tabellarische Modelle | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 54cd62aa50aff198d2397843c528f09a1a2fc83b
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2018
---
# <a name="tabular-models"></a>Tabellarische Modelle
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Tabellarische Modelle sind Analysis Services-Datenbanken, die im In-Memory- oder im DirectQuery-Modus ausgeführt werden. Sie greifen in relationalen Back-End-Datenquellen direkt auf Daten zu. Mithilfe der Technik Komprimierungsalgorithmen und einen Multithreaded-Abfrageprozessor, das Analysemodul bietet schnellen Zugriff auf tabellenmodellobjekte und-Daten berichterstellungsclientanwendungen wie Power BI und Excel.  
  
 Während bei speicherinternen Modellen die Standardeinstellung sind, ist DirectQuery ein alternativer Abfragemodus für Modelle, die entweder zu groß für im Arbeitsspeicher, oder wenn datenflüchtigkeit eine angemessene verarbeitungsstrategie möglich. DirectQuery erzielt wie bei speicherinternen Modellen unterstützt eine Vielzahl von Datenquellen, zur Behandlung von berechneten Tabellen und Spalten in einem DirectQuery-Modell, Sicherheit auf Zeilenebene über DAX-Ausdrücke, die die Back-End-Datenbank zu erreichen, und Fragen Optimierungen, die zu einem höheren Durchsatz führen.
  
 In tabellarische Modellen erstellt [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mithilfe der Projektvorlage für tabellarische Modelle, die bietet eine Entwurfsoberfläche zum Erstellen eines Modells, Tabellen, Beziehungen und DAX-Ausdrücke. Sie können Daten aus mehreren Quellen importieren und das Modell erweitern, indem Sie Beziehungen, berechnete Tabellen und Spalten, Measures, KPIs, Hierarchien und Übersetzungen hinzufügen.  
  
 Modelle können dann mit Azure Analysis Services bereitgestellt werden, oder eine Instanz von SQL Server Analysis Services für den tabellarischen Servermodus konfiguriert. Bereitgestellte tabellarische Modelle können in SQL Server Management Studio verwaltet werden. Wie die Modelle zunehmen, können sie für die optimierte Verarbeitung partitioniert und auf die Zeilenebene mithilfe rollenbasierter Sicherheit gesichert werden.  

  
  
