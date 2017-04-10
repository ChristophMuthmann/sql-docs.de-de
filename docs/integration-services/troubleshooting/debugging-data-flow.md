---
title: "Debuggen des Datenflusses | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Fortschrittsberichterstellung [Integration Services]"
  - "Daten-Viewer [Integration Services]"
  - "Datenfluss [Integration Services], Debuggen"
  - "Debuggen [Integration Services], Datenfluss"
  - "Zählen von Zeilen"
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Debuggen des Datenflusses
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer enthalten Funktionen und Tools, mit denen Sie die Datenflüsse in einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket behandeln können.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer stellt Daten-Viewer bereit.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer und [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Transformationen stellen die Zeilenanzahl bereit.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer stellt zur Laufzeit Fortschrittsberichte bereit.  
  
## Daten-Viewer  
 Daten-Viewer zeigen Daten zwischen zwei Komponenten in einem Datenfluss an. Mit Daten-Viewern können Daten angezeigt werden, wenn die Daten von einer Datenquelle extrahiert werden und an einen Datenfluss weitergegeben werden, vor und nach dem Update der Daten durch eine Transformation sowie vor dem Laden der Daten in das Ziel.  
  
 Um die Daten anzuzeigen, fügen Sie dem Pfad, der zwei Datenflusskomponenten verbindet, Daten-Viewer hinzu. Durch die Möglichkeit, Daten zwischen Datenflusskomponenten anzuzeigen, können Sie auf einfache Weise unerwartete Datenwerte identifizieren, die Änderung von Spaltenwerten durch eine Transformation anzeigen sowie die Ursache für einen Fehler bei einer Transformation ermitteln. Beispielsweise kann es sein, dass bei einer Suche in einer Verweistabelle ein Fehler auftritt. Um dieses Problem zu beseitigen, können Sie eine Transformation hinzufügen, die Standarddaten für leere Spalten bereitstellt.  
  
 Ein Daten-Viewer kann Daten in einem Raster anzeigen. Bei einem Raster wählen Sie die Spalten aus, die angezeigt werden sollen. Die Werte für die ausgewählten Spalten werden im Tabellenformat angezeigt.  
  
 Sie können auch mehrere Daten-Viewer in einen Pfad einschließen. Daten können in unterschiedlichen Formaten angezeigt werden (erstellen Sie z. B. eine Diagrammsicht und eine Rasteransicht der Daten), und es können unterschiedliche Daten-Viewer für verschiedene Datenspalten erstellt werden.  
  
 Wenn Sie einem Pfad einen Daten-Viewer hinzufügen, fügt der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer der Entwurfsoberfläche der Registerkarte **Datenfluss** neben dem Pfad ein Daten-Viewer-Symbol hinzu. Transformationen mit mehreren Ausgaben, wie z. B. die Transformation für bedingtes Teilen, können in jedem Pfad einen Daten-Viewer enthalten.  
  
 Zur Laufzeit wird ein **Daten-Viewer** -Fenster geöffnet, in dem die vom Daten-Viewer-Format definierten Informationen angezeigt werden. Beispielsweise zeigt ein Daten-Viewer, der das Rasterformat verwendet, Daten für die ausgewählten Spalten, die Anzahl von an die Datenflusskomponente übergebenen Ausgabezeilen sowie die Anzahl dargestellter Zeilen an. Die Informationen werden pufferweise angezeigt und, ein Puffer kann, abhängig von der Zeilenbreite im Datenfluss, mehr oder weniger Zeilen enthalten.  
  
 Im Dialogfeld **Daten-Viewer** können Sie die Daten in die Zwischenablage kopieren, alle Daten aus der Tabelle löschen, den Daten-Viewer neu konfigurieren, den Datenfluss fortsetzen und den Daten-Viewer anfügen oder trennen.  
  
#### So fügen Sie einen Daten-Viewer hinzu  
  
-   [Hinzufügen eines Daten-Viewers zu einem Datenfluss](../../integration-services/troubleshooting/add-a-data-viewer-to-a-data-flow.md)  
  
## Zeilenanzahl  
 Die Anzahl von Zeilen, die über einen Pfad verschoben wurden, werden in der Entwurfsoberfläche der Registerkarte **Datenfluss** in [!INCLUDE[ssIS](../../includes/ssis-md.md)] neben dem Pfad angezeigt. Dieser Wert wird regelmäßig aktualisiert, während die Daten über den Pfad verschoben werden.  
  
 Sie können dem Datenfluss auch eine Transformation für Zeilenanzahl hinzufügen, um die endgültige Zeilenanzahl in einer Variablen aufzuzeichnen. Weitere Informationen finden Sie unter [Row Count Transformation](../../integration-services/data-flow/transformations/row-count-transformation.md).  
  
## Fortschrittsberichte  
 Wenn Sie ein Paket ausführen, stellt der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer den Fortschritt in der Entwurfsoberfläche der Registerkarte **Datenfluss** dar, indem jede Datenflusskomponente in der entsprechenden Statusfarbe dargestellt wird. Wenn eine Komponente mit der Arbeit beginnt, wird die Farbe von keiner Farbe in gelb geändert. Wenn die Komponente erfolgreich abgeschlossen ist, wird sie in grün geändert. Rot bedeutet, dass bei der Komponente ein Fehler aufgetreten ist.  
  
 In der folgenden Tabelle wird die Farbcodierung beschrieben.  
  
|Farbe|Description|  
|-----------|-----------------|  
|Keine Farbe|Wartet auf den Aufruf durch das Datenflussmodul.|  
|Gelb|Führt eine Transformation aus, extrahiert Daten oder lädt Daten.|  
|Green|Wurde erfolgreich ausgeführt.|  
|Rot|Wurde mit Fehlern ausgeführt.|  
  
## Siehe auch  
 [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
  