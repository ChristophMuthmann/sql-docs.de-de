---
title: Angeben einer Trefferanzahl | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.breakpt.hitcount
helpviewer_keywords:
- Transact-SQL debugger, breakpoint hit count
ms.assetid: 24836939-94ed-4e57-aa85-5d6938d859e4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1430ec114f5aa14457fcff1d58a7f41e2e5bbe48
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="specify-a-hit-count"></a>Angeben einer Trefferanzahl
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Die Breakpoint-Trefferanzahl bildet einen Leistungsindikator, der bei jedem Erreichen des Breakpoints vom [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debugger inkrementiert wird. Wenn die angegebene Trefferanzahl erreicht ist und alle angegebenen Breakpointbedingungen erfüllt sind, führt der Debugger die für den Breakpoint angegebene Aktion aus.  
  
## <a name="hit-count-considerations"></a>Überlegungen zur Trefferanzahl  
 Standardmäßig wird die Ausführung stets unterbrochen, wenn ein Breakpoint erreicht wird. Folgende Optionen sind verfügbar:  
  
-   Immer anhalten (Standard).  
  
-   Anhalten, wenn die Trefferanzahl gleich einem angegebenen Wert ist.  
  
-   Anhalten, wenn die Trefferanzahl ein Vielfaches ist von einem angegebenen Wert.  
  
-   Anhalten, wenn die Trefferanzahl größer oder gleich einem angegebenen Wert ist.  
  
 Die Breakpoint-Trefferanzahlen werden innerhalb einer Debugsitzung inkrementiert. Zu Beginn jeder Debugsitzung werden alle Trefferanzahlen auf 0 festgelegt.  
  
 Wenn Sie die Häufigkeit nachverfolgen möchten, mit der ein Breakpoint erreicht wurde, ohne die Ausführung zu unterbrechen, geben Sie eine Trefferanzahl mit sehr hohen Wert an, damit beim Breakpoint nie eine Unterbrechung eintritt.  
  
 Die Standardaktion für einen Breakpoint besteht darin, die Ausführung zu unterbrechen, wenn die Trefferanzahl- und die Breakpointbedingung erfüllt sind. Informationen zum Angeben anderer Aktionen finden Sie unter [Angeben einer Breakpointaktion](../../relational-databases/scripting/specify-a-breakpoint-action.md).  
  
#### <a name="to-specify-a-hit-count"></a>So geben Sie eine Trefferanzahl an  
  
1.  Klicken Sie im Editor-Fenster mit der rechten Maustaste auf das Breakpointsymbol, und klicken Sie dann im Kontextmenü auf **Trefferanzahl** .  
  
     -oder-  
  
     Klicken Sie im Fenster **Breakpoints** mit der rechten Maustaste auf das Breakpointsymbol, und klicken Sie dann im Kontextmenü auf **Trefferanzahl** .  
  
2.  Wählen Sie im Dialogfeld **Trefferanzahl für Haltepunkt** im Feld **Wenn der Haltepunkt erreicht wird** das gewünschte Verhalten aus.  
  
     Wenn Sie eine andere Einstellung als **Immer anhalten**auswählen, wird rechts neben der Liste ein Textfeld angezeigt. Geben Sie in diesem Textfeld die gewünschte Trefferanzahl als ganze Zahl ein.  
  
3.  Klicken Sie auf **OK** , um die Änderungen zu implementieren, oder auf **Abbrechen** , um den Vorgang zu beenden, ohne die Änderungen zu übernehmen.  
  
#### <a name="to-view-or-reset-the-current-hit-count"></a>So zeigen Sie die aktuelle Trefferanzahl an oder setzen diese zurück  
  
1.  Klicken Sie im Editor-Fenster mit der rechten Maustaste auf das Breakpointsymbol, und klicken Sie dann im Kontextmenü auf **Trefferanzahl** .  
  
     -oder-  
  
     Klicken Sie im Fenster **Breakpoints** mit der rechten Maustaste auf das Breakpointsymbol, und klicken Sie dann im Kontextmenü auf **Trefferanzahl** .  
  
2.  Im Dialogfeld **Trefferanzahl für Haltepunkt** wird direkt über der Schaltfläche **Zurücksetzen** der Wert **Aktuelle Trefferanzahl** angezeigt.  
  
3.  Klicken Sie auf **Zurücksetzen** , wenn Sie die aktuelle Trefferanzahl auf 0 festlegen möchten.  
  
4.  Klicken Sie auf **OK** oder **Abbrechen** , um das Dialogfeld zu schließen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Angeben einer Breakpointbedingung](../../relational-databases/scripting/specify-a-breakpoint-condition.md)  
  
  
