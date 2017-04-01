---
title: "Editor zum Aufl&#246;sen von Spaltenverweisen | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.resolvereferences.preview.F1"
  - "sql13.dts.designer.resolvereferences.mapper.F1"
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 5
---
# Editor zum Aufl&#246;sen von Spaltenverweisen
  Wenn ein Eingabepfad getrennt wurde, oder nicht zugeordnete Spalten im Pfad vorhanden sind, wird neben dem entsprechenden Datenpfad ein Fehlersymbol angezeigt. Der neue Editor zum Auflösen von Verweisen ermöglicht es, für alle Pfade in der Ausführungsstruktur nicht zugeordnete Eingabespalten mit zugeordneten Ausgabespalten zu verknüpfen, und vereinfacht dadurch die Lösung von Spaltenverweisfehlern. Der Editor zum Auflösen von Verweisen markiert auch die Pfade, um zu kennzeichnen, welche Pfade aufgelöst werden.  
  
> [!NOTE]  
>  Es ist nun möglich, eine Komponente zu bearbeiten, selbst wenn deren Eingabepfad getrennt ist.  
  
 Nachdem alle Spaltenverweise aufgelöst wurden und keine weiteren Datenpfadfehler auftreten, werden neben den Datenpfaden keine Fehlersymbole angezeigt.  
  
## enthalten  
 Nicht zugeordnete Ausgabespalten (Quelle):  
 Spalten vom Upstreampfad, die derzeit nicht zugeordnet sind.  
  
 Zugeordnete Spalten (Quelle):  
 Spalten vom Upstreampfad, die Spalten vom Downstreampfad zugeordnet sind.  
  
 Zugeordnete Spalten (Ziel):  
 Spalten vom Upstreampfad, die Spalten vom Downstreampfad zugeordnet sind.  
  
 Nicht zugeordnete Eingabespalten (Ziel):  
 Spalten vom Downstreampfad, die derzeit nicht zugeordnet sind.  
  
 Nicht zugeordnete Eingabespalten löschen  
 Aktivieren Sie "Nicht zugeordnete Eingabespalten löschen", um nicht zugeordnete Spalten am Ziel des Datenpfads zu ignorieren. Die Schaltfläche "Vorschau der Änderungen" zeigt eine Liste der Änderungen an, die auftreten, wenn Sie auf die Schaltfläche "OK" klicken.  
  
  