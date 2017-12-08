---
title: Arbeiten mit Analysis Services-Projekten und Datenbanken in der Produktion | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
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
helpviewer_keywords: Analysis Services, projects
ms.assetid: c589097f-ad29-4b97-8c7e-b8a910909c1a
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ec62b7e30c7060a92b4ccfb36a8e5bfa2a0e6520
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="work-with-analysis-services-projects-and-databases-in-production"></a>Arbeiten mit Analysis Services-Projekten und Datenbanken in der Produktion
  Nachdem Sie die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts auf einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz entwickelt und bereitgestellt haben, müssen Sie festlegen, auf welche Weise Objekte in der bereitgestellten Datenbank geändert werden sollen. Bestimmte Änderungen, wie z. B. Änderungen in Bezug auf Sicherheitsrollen, Partitionierungen und Speichereinstellungen, können mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]vorgenommen werden. Andere Änderungen (z. B. das Hinzufügen von Attributen oder benutzerdefinierten Hierarchien) können nur mithilfe von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]im Onlinemodus oder im Projektmodus vorgenommen werden.  
  
 Sobald Sie eine bereitgestellte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Onlinemodus ändern, ist das für die Bereitstellung verwendete [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt ist nicht mehr auf dem neuesten Stand. Wenn ein Entwickler Änderungen an einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt vornimmt und versucht, das geänderte Projekt bereitzustellen, wird er dazu aufgefordert, die gesamte Datenbank zu überschreiben. Überschreibt der Entwickler die gesamte Datenbank, so ist auch die Verarbeitung der Datenbank erforderlich. Dieses Problem wird verschärft, wenn die Produktionsmitarbeiter die Änderungen direkt an der bereitgestellten Datenbank durchgeführt haben, ohne dies an das Entwicklungsteam zu kommunizieren, was dazu führt, dass das Entwicklungsteam nicht versteht, weshalb die von ihnen vorgenommen Änderungen nicht mehr in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank angezeigt werden.  
  
 Es gibt mehrere Methoden, um mithilfe von SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Tools die in solchen Situationen auftretenden Probleme zu umgehen:  
  
-   Methode 1: Verwenden Sie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] beim Ändern einer Produktionsversion einer [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] -Datenbank, um ein neues [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt auf Basis der geänderten [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankversion zu erstellen. Dieses neue [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt kann im Quellcodeverwaltungssystem als Masterkopie des Projekts eingecheckt werden. Diese Methode funktioniert unabhängig davon, ob die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Onlinemodus geändert wurde.  
  
-   Methode 2: Ändern Sie nur die Produktionsversion einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Projektmodus. Mit dieser Methode können Sie die im Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verfügbaren Optionen verwenden, um die über [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]vorgenommenen Änderungen beizubehalten, wie z. B. Sicherheitsrollen und Speichereinstellungen. Mit dieser Methode wird sichergestellt, dass die entwurfsbezogenen Einstellungen in der Projektdatei beibehalten werden (Speichereinstellungen und Sicherheitsrollen können ignoriert werden) und der Onlineserver für Speichereinstellungen und Sicherheitsrollen verwendet wird.  
  
-   Methode 3: Ändern Sie nur die Produktionsversion einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Onlinemodus. Da beide Tools nur mit demselben Onlineserver arbeiten, ist es ausgeschlossen, dass Sie verschiedene, unsynchrone Versionen erhalten.  
  
  
