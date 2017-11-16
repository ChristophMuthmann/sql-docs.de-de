---
title: Mehrdimensionale Modelldatenbanken (SSAS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [Analysis Services], databases
- SQL Server Analysis Services, databases
- SSAS, databases
- Analysis Services, databases
- databases [Analysis Services], designing
- Business Intelligence Development Studio, databases [Analysis Services]
- databases [Analysis Services]
ms.assetid: 78b2f22a-b7bd-4a2b-b6fc-0bff4d2b3168
caps.latest.revision: 55
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b9b4fa79c4ef7a37158c1fbeea32a80c56effa2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="multidimensional-model-databases-ssas"></a>Mehrdimensionale Modelldatenbanken (SSAS)
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
  
 [Umschalten einer Analysis Services-Datenbank zwischen schreibgeschütztem Modus und Lese-/Schreibmodus](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Herstellen in Onlinemodus einer Verbindung mit einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)   
 [Erstellen eines Analysis Services-Projekts &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [Abfragen von mehrdimensionalen Daten mit MDX](../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
  

