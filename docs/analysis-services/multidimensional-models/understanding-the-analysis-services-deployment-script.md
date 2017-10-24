---
title: Grundlegendes zu den Analysis Services-Bereitstellungsskript | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], scripts
- Analysis Services deployments, scripts
- scripts [Analysis Services], deployment
ms.assetid: a63ebee9-9848-48f1-82ad-64ecf2e47019
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ccc1b2b2861a20de2f02bf118a5abcf14e8ea6b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="understanding-the-analysis-services-deployment-script"></a>Grundlegendes zum Analysis Services-Bereitstellungsskript
  Das vom [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Bereitstellungs-Assistenten erstellte XMLA-Bereitstellungsskript besteht aus zwei Abschnitten:  
  
-   Der erste Teil des Bereitstellungsskripts enthält die Befehle, die zum Erstellen, Ändern oder Löschen der entsprechenden [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte in der Zieldatenbank erforderlich sind. Standardmäßig basieren die vom [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt generierten Eingabedateien auf einer inkrementellen Bereitstellung. Folglich wirkt sich das XMLA-Bereitstellungsskript nur auf Objekte aus, die geändert oder gelöscht wurden.  
  
-   Der zweite Teil des Bereitstellungsskripts enthält die Befehle, die zum Verarbeiten der Objekte erforderlich sind, die auf dem Zielserver erstellt oder geändert wurden (Option Standard verarbeiten), oder zum vollständigen Verarbeiten der Zieldatenbank. Sie können auch festlegen, dass das Bereitstellungsskript keine Verarbeitungsbefehle enthalten soll.  
  
 Das gesamte Bereitstellungsskript kann in einer einzelnen Transaktion oder in mehreren Transaktionen ausgeführt werden. Wenn das Skript in mehreren Transaktionen ausgeführt wird, wird der erste Teil des Skripts als einzelne Transaktion ausgeführt, und jedes Objekt wird in einer eigenen Transaktion verarbeitet.  
  
> [!IMPORTANT]  
>  Der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Bereitstellungs-Assistent stellt nur Objekte in einer einzelnen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank bereit. Er stellt keinerlei Objekte oder Daten auf Serverebene bereit.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen des Bereitstellungs-Assistenten für Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)  
  
  

