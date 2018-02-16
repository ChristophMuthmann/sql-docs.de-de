---
title: "Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: afcaef54af0b0bd100aba138c8372f04494a1880
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Bereitstellungs-Assistent verwendet die JSON-Ausgabedateien generiert eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt als Eingabedateien. Diese Eingabedateien können problemlos geändert werden, um die Bereitstellung eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts anzupassen. Anschließend kann das generierte Bereitstellungsskript entweder sofort ausgeführt oder für eine spätere Bereitstellung gespeichert werden.  
  
 Sie können die Bereitstellung mithilfe des Assistenten wie hier beschrieben durchführen. Sie können die Bereitstellung auch automatisieren oder die Synchronisierungsfunktion verwenden. Wenn die bereitgestellte Datenbank groß ist, sollten Sie die Verwendung von Partitionen auf den Zielsystemen in Erwägung ziehen. Mithilfe von Analysis Management Objects (AMO) können Sie auch die Partitionserstellung und Auffüllung automatisieren.  
  
> [!IMPORTANT]  
>  Weder die Ausgabedateien noch das Bereitstellungsskript wird der Benutzer-Id oder das Kennwort enthalten, wenn diese in der Verbindungszeichenfolge für eine Datenquelle oder für Identitätswechsel angegeben sind. Da diese Informationen zum Verarbeiten in diesem Szenario erforderlich sind, müssen Sie sie manuell hinzufügen. Wenn die Bereitstellung keine Verarbeitung umfasst, können Sie die Verbindungs- und Identitätswechselinformationen bei Bedarf nach der Bereitstellung hinzufügen. Wenn die Bereitstellung die Verarbeitung umfasst, können Sie diese Informationen nach dem Speichern entweder innerhalb des Assistenten oder im Bereitstellungsskript hinzufügen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In den folgenden Themen wird beschrieben, wie Sie mit dem Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , den Eingabedateien und dem Bereitstellungsskript arbeiten:  
  
|Thema|Description|  
|-----------|-----------------|  
|[Der Assistent für Analysis Services-Bereitstellung ausgeführt](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)|Beschreibt die verschiedenen Möglichkeiten zum Ausführen des Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)|Beschreibt, welche Dateien der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] als Eingabewerte verwendet und was jede dieser Dateien enthält. Stellt außerdem Links zu Themen bereit, in denen beschrieben wird, wie Sie die Werte in den einzelnen Eingabedateien ändern können.|  
|[Grundlegendes zum Analysis Services-Bereitstellungsskript](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)|Beschreibt den Inhalt des Bereitstellungsskripts und wie das Skript ausgeführt wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellen von Modelllösungen mit XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Synchronisieren von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)   
 [Bereitstellen von Modelllösungen mit dem Bereitstellungshilfsprogramm](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  
