---
title: "Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten | Microsoft Docs"
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
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d731e2d1655872e3b8a196d36225b401586f2b34
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten
  Die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Bereitstellungs-Assistent verwendet die JSON-Ausgabedateien generiert eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt als Eingabedateien. Diese Eingabedateien können problemlos geändert werden, um die Bereitstellung eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts anzupassen. Anschließend kann das generierte Bereitstellungsskript entweder sofort ausgeführt oder für eine spätere Bereitstellung gespeichert werden.  
  
 Sie können die Bereitstellung mithilfe des Assistenten wie hier beschrieben durchführen. Sie können die Bereitstellung auch automatisieren oder die Synchronisierungsfunktion verwenden. Wenn die bereitgestellte Datenbank groß ist, sollten Sie die Verwendung von Partitionen auf den Zielsystemen in Erwägung ziehen. Mithilfe von Analysis Management Objects (AMO) können Sie auch die Partitionserstellung und Auffüllung automatisieren.  
  
> [!IMPORTANT]  
>  Weder die Ausgabedateien noch das Bereitstellungsskript wird der Benutzer-Id oder das Kennwort enthalten, wenn diese in der Verbindungszeichenfolge für eine Datenquelle oder für Identitätswechsel angegeben sind. Da diese Informationen zum Verarbeiten in diesem Szenario erforderlich sind, müssen Sie sie manuell hinzufügen. Wenn die Bereitstellung keine Verarbeitung umfasst, können Sie die Verbindungs- und Identitätswechselinformationen bei Bedarf nach der Bereitstellung hinzufügen. Wenn die Bereitstellung die Verarbeitung umfasst, können Sie diese Informationen nach dem Speichern entweder innerhalb des Assistenten oder im Bereitstellungsskript hinzufügen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In den folgenden Themen wird beschrieben, wie Sie mit dem Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , den Eingabedateien und dem Bereitstellungsskript arbeiten:  
  
|Thema|Description|  
|-----------|-----------------|  
|[Ausführen des Bereitstellungs-Assistenten für Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)|Beschreibt die verschiedenen Möglichkeiten zum Ausführen des Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)|Beschreibt, welche Dateien der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] als Eingabewerte verwendet und was jede dieser Dateien enthält. Stellt außerdem Links zu Themen bereit, in denen beschrieben wird, wie Sie die Werte in den einzelnen Eingabedateien ändern können.|  
|[Grundlegendes zum Analysis Services-Bereitstellungsskript](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)|Beschreibt den Inhalt des Bereitstellungsskripts und wie das Skript ausgeführt wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellen von Modelllösungen mit XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Synchronisieren von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)   
 [Bereitstellen von Modelllösungen mit dem Bereitstellungshilfsprogramm](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  
