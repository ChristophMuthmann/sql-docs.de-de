---
title: Angeben eines Breakpointfilters | Microsoft Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.breakpt.contraints
helpviewer_keywords:
- Transact-SQL debugger, breakpoint filter
ms.assetid: 7bf1dddd-7b0b-4c47-8a7b-28a5569b4fa5
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 52893c5409981b492e10ff1706def0257367c494
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="specify-a-breakpoint-filter"></a>Angeben eines Breakpointfilters
  Bei Verwendung eines Breakpointfilters wird ein Breakpoint nur auf angegebene Computer, Betriebssystemprozesse und Threads angewendet. Breakpointfilter werden meist beim Debuggen paralleler Anwendungen verwendet.  
  
##  <a name="BKMK_ActionConsiderations"></a> Filteraspekte  
 Breakpointfilter werden selten mit dem [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger verwendet, da es sich bei [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts und gespeicherte Prozeduren nicht um parallele Anwendungen handelt.  
  
#### <a name="to-specify-a-breakpoint-filter"></a>So geben Sie einen Breakpointfilter an  
  
1.  Klicken Sie im Editor-Fenster mit der rechten Maustaste auf das Breakpointsymbol, und klicken Sie dann im Kontextmenü auf **Filter** .  
  
     -oder-  
  
     Klicken Sie im Fenster **Breakpoint** mit der rechten Maustaste auf das Breakpointsymbol, und klicken Sie dann im Kontextmenü auf **Filter** .  
  
2.  Geben Sie im Dialogfeld **Haltepunktfilter** im Feld **Filter** Computer mit Namen oder Betriebssystemprozesse und Threads mit Namen oder ID-Nummer an:  
  
    -   **MachineName** gibt den Computer an, auf dem die Instanz des Datenbankmoduls ausgeführt wird.  
  
    -   **ProcessID**und **ProcessName** geben den Betriebssystemprozess an, von dem die Instanz des Datenbankmoduls ausgeführt wird.  
  
    -   **ThreadID** und **ThreadName** geben den Betriebssystemthread an, unter dem der Batch, die Prozedur oder die Funktion von [!INCLUDE[tsql](../../includes/tsql-md.md)] in der Instanz des Datenbankmoduls ausgeführt wird.  
  
3.  Klicken Sie auf **OK** , um die Änderungen zu implementieren, oder auf **Abbrechen** , um den Vorgang zu beenden, ohne die Änderungen zu übernehmen.  
  
## <a name="see-also"></a>Siehe auch  
 [Angeben einer Breakpointbedingung](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [Angeben einer Trefferanzahl](../../relational-databases/scripting/specify-a-hit-count.md)   
 [Angeben einer Breakpointaktion](../../relational-databases/scripting/specify-a-breakpoint-action.md)  
  
  
