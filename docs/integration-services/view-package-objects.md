---
title: "Anzeigen von Paketobjekten | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services-Pakete, Eigenschaften"
  - "Eigenschaften [Integration Services]"
  - "Paket-Explorer (Fenster) [Integration Services]"
  - "Pakete [Integration Services], Eigenschaften"
  - "Explorersicht [Integration Services]"
  - "SSIS-Pakete, Eigenschaften"
  - "Anzeigen von Paketobjekten"
  - "SQL Server Integration Services-Pakete, Eigenschaften"
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# Anzeigen von Paketobjekten
  Im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer stellt die Registerkarte **Paket-Explorer** eine Explorer-Sicht des Pakets bereit. Diese Sicht gibt die Containerhierarchie der [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Architektur wieder. Der Paketcontainer befindet sich ganz oben in der Hierarchie, und Sie erweitern das Paket, um die Verbindungen, ausführbaren Dateien, Ereignishandler, Protokollanbieter, Rangfolgeneinschränkungen und Variablen im Paket anzuzeigen.  
  
 Die ausführbaren Dateien, also die Container und Tasks im Paket, können Ereignishandler, Rangfolgeneinschränkungen und Variablen einschließen. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] unterstützt eine geschachtelte Hierarchie von Containern, und der For-Schleifencontainer, der Foreach-Schleifencontainer und der Sequenzcontainer können andere ausführbare Dateien einschließen.  
  
 Falls ein Paket einen Datenfluss enthält, wird im **Paket-Explorer** der Datenflusstask aufgelistet, und er enthält den Ordner **Komponenten** , in dem die Datenflusskomponenten aufgelistet werden.  
  
 Auf der Registerkarte **Paket-Explorer** können Sie Objekte in einem Paket löschen und auf das Fenster **Eigenschaften** zugreifen, um Objekteigenschaften anzuzeigen.  
  
 Das folgende Diagramm zeigt eine Strukturansicht eines einfachen Pakets.  
  
 ![Screenshot der Registerkarte "Paket-Explorer"](../integration-services/media/packageexplorer.gif "Screenshot der Registerkarte "Paket-Explorer"")  
  
### So zeigen Sie den Paketinhalt an  
  
-   [Anzeigen von Paketobjekten im Paket-Explorer](../Topic/View%20Package%20Objects%20in%20Package%20Explorer.md)  
  
## Siehe auch  
 [Integration Services-Tasks](../integration-services/control-flow/integration-services-tasks.md)   
 [SQL Server Integration Services-Container](../integration-services/control-flow/integration-services-containers.md)   
 [Rangfolgeneinschränkungen](../integration-services/control-flow/precedence-constraints.md)   
 [Integration Services-Variablen &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md)   
 [Integration Services-Ereignishandler &#40;SSIS&#41;](../integration-services/integration-services-ssis-event-handlers.md)   
 [Integration Services-Protokollierung &#40;SSIS&#41;](../integration-services/performance/integration-services-ssis-logging.md)  
  
  