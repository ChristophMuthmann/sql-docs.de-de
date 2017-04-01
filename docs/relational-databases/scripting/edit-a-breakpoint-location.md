---
title: "Bearbeiten einer Breakpointposition | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.debug.breakpt.location.file"
helpviewer_keywords: 
  - "Transact-SQL-Debugger, Breakpointposition"
ms.assetid: 5c28e411-0377-4210-a7ce-2a5c13dcdf74
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# Bearbeiten einer Breakpointposition
  Die Breakpointposition gibt die Zeile und das Zeichen an, wo sich der Breakpoint in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skriptdatei befindet. Sie können die Position des Breakpoints bearbeiten, um diesen an eine andere Position im Skript oder in ein anderes Skript zu verschieben.  
  
## Bearbeiten einer Position  
 Wenn Sie die Position eines Breakpoints bearbeiten, wird dieser mitsamt aller vorhandenen Eigenschaften, z. B. der Trefferanzahl oder einer Bedingung, an die neue Position verschoben.  
  
#### So bearbeiten Sie eine Breakpointposition  
  
1.  Klicken Sie im Editor-Fenster mit der rechten Maustaste auf das Breakpointsymbol, und klicken Sie dann im Kontextmenü auf **Speicherort**.  
  
     -oder-  
  
     Klicken Sie im Breakpointfenster** **mit der rechten Maustaste auf das Breakpointsymbol, und klicken Sie dann im Kontextmenü auf **Speicherort**.  
  
2.  Bearbeiten Sie im Dialogfeld **Dateihaltepunkt** die Option **Datei** , um eine neue Datei anzugeben, **Zeile** , um eine neue Zeile anzugeben, oder **Zeichen** , um eine neue Position auf derselben Zeile anzugeben. Wenn die angegebene neue Datei bereits in einem Abfrage-Editor-Fenster geöffnet ist, wird der Breakpoint in dieses Editorfenster verschoben. Wenn die Datei nicht geöffnet wird, wird ein neues Editorfenster geöffnet, die Datei darin geladen und der Breakpoint an die neue Position verschoben.  
  
     Beim Debuggen von **hat die Option** Unterschiede zwischen Quellcode und Originalversion zulassen [!INCLUDE[tsql](../../includes/tsql-md.md)]keine Auswirkungen.  
  
## Siehe auch  
 [Angeben einer Trefferanzahl](../../relational-databases/scripting/specify-a-hit-count.md)   
 [Angeben einer Breakpointaktion](../../relational-databases/scripting/specify-a-breakpoint-action.md)   
 [Angeben einer Breakpointbedingung](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [Angeben eines Breakpointfilters](../../relational-databases/scripting/specify-a-breakpoint-filter.md)  
  
  