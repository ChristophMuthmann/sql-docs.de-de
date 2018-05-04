---
title: Verschieben von Datamining-Objekten | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], models
- data mining editor [Analysis Services]
- mining models [Analysis Services], managing
- Data Mining Designer
- mining models [Analysis Services], modifying
ms.assetid: bc108407-2603-4387-b930-b5bb9df78069
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9d542908c4690e1f5fdf756ce5d3e030f914b3f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="moving-data-mining-objects"></a>Verschieben von Data Mining-Objekten
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Die häufigsten Szenarien beim Verschieben von Data Mining-Objekten sind das Bereitstellen eines Modells aus einer Test- oder Analyseumgebung in einer Produktionsumgebung oder die Freigabe von Modellen an andere Benutzer.  
  
 In diesem Thema wird beschrieben, wie Sie die Tools und Skripterstellungssprachen aus [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]zum Verschieben von Data Mining-Objekten verwenden können.  
  
## <a name="moving-data-mining-objects-between-databases-or-servers"></a>Verschieben von Data Mining-Objekten zwischen Datenbanken oder Servern  
 Sie können Data Mining-Objekte zwischen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken oder Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf folgende Weise verschieben:  
  
-   Erneutes Bereitstellen der Lösung an eine andere Datenbank.  
  
-   Skripterstellung einzelne Objekte.  
  
-   Sichern und anschließendes Wiederherstellen einer Kopie der Datenbank.  
  
-   Exportieren und Importieren von Strukturen und Modellen.  
  
 Im folgenden Abschnitt werden diese Optionen ausführlich erläutert.  
  
### <a name="deploying"></a>Bereitstellen  
 Für die Bereitstellung der Projektmappe auf einem anderen Server bzw. einer anderen Datenbank benötigen Sie die Projektmappendatei, die mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]erstellt wurde.  
  
 Weitere Informationen zur Bereitstellung von Analysis Services-Projektmappen finden Sie unter [Bereitstellen von Analysis Services-Projekten &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md).  
  
### <a name="scripting"></a>Skripterstellung  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]stellt mehrere Sprachen, mit denen Sie Skripte für Objekte bereit.  
  
-   **XMLA:** Sie können Objekte mit XMLA schreiben, indem Sie mit der rechten Maustaste auf Objekte in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]klicken. Um das Skript auszuführen, öffnen Sie es in einem **XMLA-Abfrage** -Fenster auf dem Zielserver.  
  
-   **DMX**: Sie können Skripte anhand von Vorlagen oder einem der Abfrage-Generatoren erstellen, die in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]bereitgestellt werden.  
  
 Beachten Sie jedoch, dass es Unterschiede in den Aufgaben gibt, die Sie mit den einzelnen Skripterstellungssprachen ausführen können:  
  
-   Eigenschaften wie Objektbeschreibung und Datenbindungen können nur mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL-Sprachen erstellt oder geändert werden, nicht mit DMX.  
  
-   Nur DMX unterstützt den Import und den Export von Miningobjekten.  
  
-   Nur DMX unterstützt das Generieren von PMML oder Importieren von Modelldefinitionen aus PMML.  
  
-   Nur DMX unterstützt das Trainieren eines Modells mit Anwendungsdaten. Darüber hinaus unterstützt die DMX-Anweisung INSERT INTO das Trainieren eines Modells ohne Bereitstellung von Werten für eine Schlüsselspalte.  
  
 Weitere Informationen finden Sie unter [Entwickeln mit Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
### <a name="backup-and-restore"></a>Sichern und Wiederherstellen  
 Sichern und Wiederherstellen einer gesamten Analysis Services-Datenbank bietet sich an, wenn Ihre Data Mining-Projektmappe auf OLAP-Objekten aufbaut. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Stellt die sicherungs- und Wiederherstellungsfunktionalität bereit, mit der datenbanksicherungen schneller und einfacher.  
  
 Weitere Informationen zur Sicherung finden Sie unter [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
### <a name="exporting-and-importing"></a>Exportieren und Importieren  
 Das Exportieren und anschließende erneute Importieren von Miningmodellen und -Strukturen mit DMX-Anweisungen ist die einfachste Möglichkeit, einzelne relationale Data Mining-Objekte zu verschieben oder zu sichern. Weitere Informationen zur DMX-Syntax für diese Vorgänge finden Sie unter den folgenden Themen:  
  
-   [EXPORT & #40; DMX & #41;](../../dmx/export-dmx.md)  
  
-   [-IMPORT & #40; DMX & #41;](../../dmx/import-dmx.md)  
  
 Wenn Sie die INCLUDE DEPENDENCIES-Option festlegen, exportiert [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auch die Definition erforderlicher Datenquellensichten. Beim Importieren des Modells oder der Struktur wird die Datenquellensicht auf dem Zielserver erneut erstellt. Stellen Sie nach dem Importieren des Modells sicher, dass die notwendigen Miningberechtigungen für das Objekt festgelegt werden.  
  
> [!NOTE]  
>  Sie können OLAP-Modelle nicht mit DMX exportieren und importieren. Wenn das Miningmodell auf einem OLAP-Cube basiert, müssen Sie die Funktionalität verwenden, die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zum Sichern und Wiederherstellen einer ganzen Datenbank bereitgestellt wird, oder den Cube und seine Modelle erneut bereitstellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwaltung von Datamining-Lösungen und-Objekten](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)  
  
  
