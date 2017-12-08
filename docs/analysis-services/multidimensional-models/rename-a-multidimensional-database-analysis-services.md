---
title: Umbenennen einer mehrdimensionalen Datenbank (Analysis Services) | Microsoft Docs
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
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: renaming databases
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 98a777845371724e215ac0cf58fa5d1ec916f7c9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="rename-a-multidimensional-database-analysis-services"></a>Umbenennen einer mehrdimensionalen Datenbank (Analysis Services)
  Wie der Name einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank geändert wird, hängt davon ab, wie Sie die Verbindung mit der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank herstellen. Zum Ändern des Namens einer vorhandenen Datenbank müssen Sie die Verbindung im Onlinemodus herstellen. Zum Ändern des Namens der Datenbank, in die Objekte in einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt instanziiert werden, müssen Sie die Verbindung im Projektmodus herstellen.  
  
### <a name="to-change-the-database-name-in-online-mode"></a>So ändern Sie den Datenbanknamen im Onlinemodus  
  
1.  Stellen Sie mithilfe von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]eine direkte Verbindung mit der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank her.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf die Datenbank, und klicken Sie anschließend auf **Datenbank bearbeiten**.  
  
3.  Ändern Sie im Textfeld **Datenbankname** den Namen der Datenbank.  
  
4.  Klicken Sie auf der Symbolleiste auf **Speichern** oder **Alle speichern** , klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** oder **Alle speichern** , oder schließen Sie den **Datenbank-Designer** , und klicken Sie bei entsprechender Aufforderung auf **Speichern** .  
  
     Der Datenbankname wird in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz aktualisiert, und das Datenbankobjekt im Projektmappen-Explorer wird aktualisiert.  
  
### <a name="to-change-the-database-name-in-project-mode"></a>So ändern Sie den Datenbanknamen im Projektmodus  
  
1.  Öffnen Sie das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaftenseiten** im Abschnitt **Konfigurationseigenschaften** auf **Bereitstellung** .  
  
4.  Ändern Sie die **Database** -Eigenschaft in den neuen Datenbanknamen.  
  
     Bei der nächsten Bereitstellung des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts wird es mit diesem neuen Datenbanknamen bereitgestellt. Wenn eine Datenbank mit diesem Namen bereits vorhanden ist, wird sie überschrieben.  
  
### <a name="to-change-the-database-name-using-sql-server-management-studio"></a>So ändern Sie den Datenbanknamen mithilfe von SQL Server Management Studio  
  
-   Klicken Sie mit der rechten Maustaste auf die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank, und bearbeiten Sie die Eigenschaft „Name“.  
  
## <a name="see-also"></a>Siehe auch  
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Festlegen der Eigenschaften für mehrdimensionale Datenbanken &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)   
 [Konfigurieren von Analysis Services-Projekteigenschaften &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [Bereitstellen von Analysis Services-Projekten &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
