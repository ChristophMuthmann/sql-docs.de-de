---
title: Anzeigen von Paketobjekten | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- Package Explorer window [Integration Services]
- packages [Integration Services], properties
- explorer view [Integration Services]
- SSIS packages, properties
- viewing package objects
- SQL Server Integration Services packages, properties
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4314664538d2f3f328e0fbc48965e2541089a95c
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="view-package-objects"></a>Anzeigen von Paketobjekten
  Im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer stellt die Registerkarte **Paket-Explorer** eine Explorer-Sicht des Pakets bereit. Diese Sicht gibt die Containerhierarchie der [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Architektur wieder. Der Paketcontainer befindet sich ganz oben in der Hierarchie, und Sie erweitern das Paket, um die Verbindungen, ausführbaren Dateien, Ereignishandler, Protokollanbieter, Rangfolgeneinschränkungen und Variablen im Paket anzuzeigen.  
  
 Die ausführbaren Dateien, also die Container und Tasks im Paket, können Ereignishandler, Rangfolgeneinschränkungen und Variablen einschließen. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] unterstützt eine geschachtelte Hierarchie von Containern, und der For-Schleifencontainer, der Foreach-Schleifencontainer und der Sequenzcontainer können andere ausführbare Dateien einschließen.  
  
 Falls ein Paket einen Datenfluss enthält, wird im **Paket-Explorer** der Datenflusstask aufgelistet, und er enthält den Ordner **Komponenten** , in dem die Datenflusskomponenten aufgelistet werden.  
  
 Auf der Registerkarte **Paket-Explorer** können Sie Objekte in einem Paket löschen und auf das Fenster **Eigenschaften** zugreifen, um Objekteigenschaften anzuzeigen.  
  
 Das folgende Diagramm zeigt eine Strukturansicht eines einfachen Pakets.  
  
 ![Screenshot der Registerkarte Paket-Explorer](../integration-services/media/packageexplorer.gif "Screenshot der Registerkarte Paket-Explorer")  
  
## <a name="view-the-package-structure-and-content"></a>Zeigen Sie die Paketstruktur und den Inhalt an.  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, das Sie im Bereich **Paket-Explorer**anzeigen möchten.  
  
2.  Klicken Sie auf die Registerkarte **Paket-Explorer** .  
  
3.  Um den Inhalt der Ordner **Variablen**, **Rangfolgeneinschränkungen**, **Ereignishandler**, **Verbindungs-Manager**, **Protokollanbieter**oder **Ausführbare Dateien** anzuzeigen, erweitern Sie den entsprechenden Ordner.  
  
4.  Erweitern Sie in Abhängigkeit von der Paketstruktur Ordner der nächsten Ebene.  
  
## <a name="view-the-properties-of-a-package-object"></a>Anzeigen der Eigenschaften eines Pakets-Objekts
  
-   Klicken Sie mit der rechten Maustaste auf ein Objekt, und klicken Sie auf **Eigenschaften** , um das Fenster **Eigenschaften** zu öffnen.  
  
## <a name="delete-an-object-in-a-package"></a>Löschen eines Objekts in einem Paket  
  
-   Klicken Sie mit der rechten Maustaste auf ein Objekt, und klicken Sie anschließend auf **Löschen**. 
 
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Tasks](../integration-services/control-flow/integration-services-tasks.md)   
 [Integration Services-Container](../integration-services/control-flow/integration-services-containers.md)   
 [Rangfolgeneinschränkungen](../integration-services/control-flow/precedence-constraints.md)   
 [Integration Services-Variablen &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md)   
 [Integrationsservices &#40; SSIS &#41; Ereignishandler](../integration-services/integration-services-ssis-event-handlers.md)   
 [Integrationsservices &#40; SSIS &#41; Protokollierung](../integration-services/performance/integration-services-ssis-logging.md)  
  
  

