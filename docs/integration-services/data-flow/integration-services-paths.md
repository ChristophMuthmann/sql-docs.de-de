---
title: "SQL Server Integration Services-Pfade | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.patheditor.general.f1"
  - "sql13.dts.designer.patheditor.metadata.f1"
  - "sql13.dts.designer.patheditor.visualizers.f1"
helpviewer_keywords: 
  - "Pfade [Integration Services], Informationen zu Pfaden"
  - "Datenfluss [Integration Services], Pfade"
  - "Pfade [Integration Services]"
  - "Ziele [Integration Services], Pfade"
  - "Quellen [Integration Services], Pfade"
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# SQL Server Integration Services-Pfade
  Ein Pfad verbindet zwei Komponenten in einem Datenfluss, indem die Ausgabe einer Datenflusskomponente mit der Eingabe einer anderen Komponente verbunden wird. Ein Pfad weist eine Quelle und ein Ziel auf. Wenn z. B. ein Pfad eine Verbindung mit einer OLE DB-Quelle und einer Transformation zum Sortieren herstellt, ist die OLE DB-Quelle die Quelle des Pfads, und die Transformation zum Sortieren ist das Ziel des Pfads. Die Quelle ist die Komponente, wo der Pfad beginnt, und das Ziel ist die Komponente, wo der Pfad endet.  
  
 Wenn Sie ein Paket im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer ausführen, können Sie die Daten in einem Datenfluss anzeigen, indem Sie Daten-Viewer an einen Pfad anfügen. Ein Daten-Viewer kann zur Anzeige von Daten in einem Raster konfiguriert werden. Ein Daten-Viewer ist ein hilfreiches Tool zum Debuggen. Weitere Informationen finden Sie unter [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## Konfiguration des Pfads  
 Der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer stellt das Dialogfeld **Datenflusspfad-Editor** bereit, in dem Sie Pfadeigenschaften festlegen, die Metadaten der Datenspalten, die über den Pfad übergeben werden, anzeigen sowie Daten-Viewer konfigurieren können.  
  
 Zu den konfigurierbaren Pfadeigenschaften gehört der Name, die Beschreibung und die Anmerkung des Pfads. Pfade können auch programmgesteuert konfiguriert werden. Weitere Informationen finden Sie unter [Programmgesteuertes Verbinden von Datenflusskomponenten](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
 Eine Pfadanmerkung zeigt den Namen der Pfadquelle oder den Pfadnamen in der Entwurfsoberfläche der Registerkarte **Datenfluss** im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer an. Pfadanmerkungen sind mit den Anmerkungen vergleichbar, die Sie Datenflüssen, Ablaufsteuerungen und Ereignishandlern hinzufügen können. Der einzige Unterschied besteht darin, dass eine Pfadanmerkung einem Pfad hinzugefügt wird, während andere Anmerkungen auf den Registerkarten **Datenfluss**, **Ablaufsteuerung**und **Ereignishandler**des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers angezeigt werden.  
  
 Die Metadaten zeigen den Namen, den Datentyp, die Genauigkeit, die Dezimalstellen, die Länge, die Codepage und die Quellkomponente jeder Spalte in der Ausgabe der vorherigen Komponente an. Die Quellkomponente ist jene Datenflusskomponente, die die Spalte erstellt hat. Dies kann, muss aber nicht die erste Komponente im Datenfluss sein. Beispielsweise werden mit einer Transformation für UNION ALL und einer Transformation zum Sortieren eigene Spalten erstellt, die die Quelle der Ausgabespalten sind. Dagegen können Spalten mit einer Transformation für das Kopieren von Spalten durchlaufen werden, ohne sie zu ändern. Es können auch neue Spalten erstellt werden, indem Eingabespalten kopiert werden. Die Transformation für das Kopieren von Spalten ist nur für neue Spalten die Quellkomponente.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Datenflusspfad-Editor** festlegen können:  
  
-   [Datenflusspfad-Editor &#40;Seite Allgemein&#41;](../Topic/Data%20Flow%20Path%20Editor%20\(General%20Page\).md)  
  
-   [Datenflusspfad-Editor &#40;Seite Metadaten&#41;](../Topic/Data%20Flow%20Path%20Editor%20\(Metadata%20Page\).md)  
  
-   [Datenflusspfad-Editor &#40;Seite Daten-Viewer&#41;](../Topic/Data%20Flow%20Path%20Editor%20\(Data%20Viewers%20Page\).md)  
  
 Weitere Informationen zu den Eigenschaften, die Sie programmgesteuert festlegen können, finden Sie unter [Path Properties](../Topic/Path%20Properties.md).  
  
## Verwandte Aufgaben  
  
-   [Anzeigen von Pfadmetadaten im Datenflusspfad-Editor](../Topic/View%20Path%20Metadata%20in%20the%20Data%20Flow%20Path%20Editor.md)  
  
-   [Verbinden von Komponenten in einem Datenfluss](../../integration-services/data-flow/connect-components-in-a-data-flow.md)  
  
## Siehe auch  
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  