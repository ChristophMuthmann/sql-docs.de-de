---
title: Mehrdimensionale Modelldatenbanken (SSAS) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 469665f46fea9651fdb054ab310500ef70710e8e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="multidimensional-model-databases-ssas"></a>Mehrdimensionale Modelldatenbanken (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank stellt eine Sammlung von Datenquellen, Datenquellensichten, Cubes, Dimensionen und Rollen dar. Optional kann eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank Data Mining-Strukturen und benutzerdefinierte Assemblys enthalten, mit deren Hilfe der Datenbank benutzerdefinierte Funktionen hinzugefügt werden können.  
  
 Cubes sind die grundlegenden Abfrageobjekte in Analysis Services. Wenn Sie über eine Clientanwendung eine Verbindung mit einer Analysis Services-Datenbank herstellen, werden Sie mit einem Cube innerhalb dieser Datenbank verbunden. Eine Datenbank kann mehrere Cubes enthalten, wenn Dimensionen, Assemblys, Rollen oder Miningstrukturen in mehreren Kontexten wiederverwendet werden.  
  
 Sie können eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank programmgesteuert erstellen und ändern oder eine der folgenden interaktiven Methoden verwenden:  
  
-   Stellen Sie ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt aus [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] auf einer festgelegten Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]bereit. Bei diesem Verfahren wird eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank erstellt, wenn in dieser Instanz noch keine Datenbank mit diesem Namen vorhanden ist, und die entworfenen Objekte innerhalb der neu erstellten Datenbank werden instanziiert. Wenn Sie eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]verwenden, werden Änderungen an Objekten im [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erst wirksam, wenn das Projekt in einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellt wird.  
  
-   Erstellen Sie eine leere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank innerhalb einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], entweder mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Anschließend können Sie mithilfe von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] eine direkte Verbindung mit dieser Datenbank herstellen und Objekte in dieser Datenbank (anstatt in einem Projekt) erstellen. Wenn Sie eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank auf diese Weise verwenden, werden Änderungen an den Objekten erst dann in der Datenbank, mit der Sie eine Verbindung herstellen, wirksam, wenn das geänderte Objekt gespeichert wird.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] dient die Einbindung der Quellcodeverwaltung dazu, die gleichzeitige Bearbeitung unterschiedlicher Objekte innerhalb eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts durch mehrere Entwickler zu unterstützen. Ein Entwickler kann eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank auch direkt bearbeiten und muss nicht den Umweg über ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt gehen. Hierbei besteht jedoch die Gefahr, dass die Objekte in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank nicht mehr mit dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt synchron sind, das für die Bereitstellung der Datenbank verwendet wurde. Nach der Bereitstellung können Sie eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verwalten. Bestimmte Änderungen an einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank können auch mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]vorgenommen werden, z. B. Änderungen an Partitionen und Rollen, was ebenfalls dazu führen kann, dass Objekte in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank nicht mehr mit dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt synchron sind, das für ihre Bereitstellung verwendet wurde.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Anfügen und Trennen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
 [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
 [Dokumentieren und Skripterstellung einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
 [Ändern oder Löschen einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)  
  
 [Verschieben einer Analysis Services Datenbank](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)  
  
 [Umbenennen einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md)  
  
 [Kompatibilitätsgrad einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)  
  
 [Festlegen von Eigenschaften für mehrdimensionale Datenbanken &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)  
  
 [Synchronisieren von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
 [Umschalten Sie in einer Analysis Services-Datenbank zwischen Schreib-und Lesemodus](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Herstellen in Onlinemodus einer Verbindung mit einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)   
 [Erstellen eines Analysis Services-Projekts &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [Abfragen von mehrdimensionalen Daten mit MDX](../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
  
