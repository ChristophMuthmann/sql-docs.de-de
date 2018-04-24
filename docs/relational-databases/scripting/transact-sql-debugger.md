---
title: Transact-SQL-Debugger | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Transact-SQL debugger, introduction
ms.assetid: 6e914699-0d85-46c2-aa2d-3e339ac2c4ce
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e42e548f35aadcdbe3661444b6523117e6ddc047
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="transact-sql-debugger"></a>Transact-SQL-Debugger
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger ist bei der Fehlersuche in [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code hilfreich, da sich mit ihm das Laufzeitverhalten des Codes untersuchen lässt. Nachdem Sie das [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Fenster in den Debugmodus geschaltet haben, können Sie die Ausführung bei bestimmten Codezeilen anhalten und die Informationen und Daten untersuchen, die von diesen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen verwendet oder zurückgegeben werden.  
  
## <a name="stepping-through-transact-sql-code"></a>Schrittweises Durchlaufen von Transact-SQL-Code  
 Der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger stellt die folgenden Optionen bereit, die Sie zum Navigieren durch [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code verwenden können, wenn sich das [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Fenster im Debugmodus befindet:  
  
-   Festlegen von Breakpoints für einzelne [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen.  
  
     Ein Breakpoint gibt einen Punkt an, an dem die Ausführung angehalten werden soll, um Daten zu untersuchen. Wenn Sie den Debugger starten, hält er an der ersten Codezeile im Abfrage-Editor-Fenster an. Um die Ausführung bis zum ersten Breakpoint fortzusetzen, den Sie festgelegt haben, können Sie die Funktion **Weiter** verwenden. Sie können die Funktion **Weiter** auch verwenden, um die Ausführung von einer beliebigen Position, an der das Fenster angehalten wurde, bis zum nächsten Breakpoint fortzusetzen. Sie können Breakpoints bearbeiten, um Aktionen anzugeben, wie z. B. die Bedingungen, unter denen der Breakpoint die Ausführung anhalten soll, oder im Fenster **Ausgabe** auszugebende Informationen. Außerdem können Sie den Ort des Breakpoints ändern.  
  
-   Einen Einzelschritt in die nächste Anweisung ausführen  
  
     Mit dieser Option können Sie Schritt für Schritt durch eine Gruppe von Anweisungen navigieren und dabei deren Verhalten beobachten.  
  
-   Ausführen gespeicherter Prozeduren oder Funktionen im Einzel- oder Prozedurschrittmodus.  
  
     Wenn Sie sicher sind, dass in der gespeicherten Prozedur keine Fehler vorliegen, können Sie sie überspringen. Die Prozedur wird vollständig ausgeführt, und die Ergebnisse werden an den Code zurückgegeben.  
  
     Wenn Sie eine gespeicherte Prozedur oder eine Funktion debuggen möchten, können Sie das Modul im Einzelschrittmodus ausführen. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] öffnet ein neues Fenster des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editors, das mit dem Quellcode für das Modul aufgefüllt wird, schaltet das Fenster in den Debugmodus und hält dann die Ausführung bei der ersten Anweisung im Modul an. Sie können dann durch den Modulcode navigieren, indem Sie z. B. Breakpoints festlegen oder den Code schrittweise durchlaufen.  
  
 Weitere Informationen zum Navigieren im Code mithilfe des Debuggers finden Sie unter [Schrittweises Durchlaufen von Transact-SQL-Code](../../relational-databases/scripting/step-through-transact-sql-code.md).  
  
## <a name="viewing-debugger-information"></a>Anzeigen von Debuggerinformationen  
 Jedes Mal, wenn der Debugger die Ausführung bei einer bestimmten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung anhält, können Sie den aktuellen Ausführungsstatus in den folgenden Debuggerfenstern anzeigen:  
  
-   **Lokal** und **Überwachen** Diese Fenster zeigen die aktuell zugeordneten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Ausdrücke an. Ausdrücke sind [!INCLUDE[tsql](../../includes/tsql-md.md)] -Klauseln, die zu einem einzelnen Skalarausdruck ausgewertet werden. Der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debugger unterstützt die Anzeige von Ausdrücken, die auf [!INCLUDE[tsql](../../includes/tsql-md.md)]-Variablen oder -Parameter oder auf die integrierten Funktionen verweisen, deren Namen mit @@ beginnen. Diese Fenster zeigen auch die Datenwerte an, die den Ausdrücken derzeit zugewiesen sind.  
  
-   **Schnellüberwachung.** In diesem Fenster wird der Wert eines [!INCLUDE[tsql](../../includes/tsql-md.md)] -Ausdrucks angezeigt. Außerdem können Sie diesen Ausdruck in einem **Überwachen** Überwachungsfenster speichern.  
  
-   **Breakpoints.** In diesem Fenster können die derzeit festgelegten Breakpoints angezeigt und verwaltet werden.  
  
-   **Aufrufliste.** In diesem Fenster wird der aktuelle Ausführungsort angezeigt. Außerdem zeigt es Informationen über die Art und Weise an, in der die Ausführung vom ursprünglichen Abfrage-Editor-Fenster über Funktionen, gespeicherte Prozeduren oder Trigger geleitet wurde, um den aktuellen Ausführungsort zu erreichen.  
  
-   **Ausgabe.** In diesem Fenster werden verschiedene Meldungen und Programmdaten angezeigt, wie z. B. Systemmeldungen des Debuggers.  
  
-   **Ergebnisse** und **Meldungen** Diese Registerkarten im Abfrage-Editor-Fenster zeigen die Ergebnisse der zuvor ausgeführten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen an.  
  
## <a name="transact-sql-debugger-tasks"></a>Transact-SQL-Debuggertasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt das Konfigurieren des [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debuggers.|[Konfigurieren von Firewallregeln vor dem Ausführen des TSQL-Debuggers](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)|  
|Beschreibt, wie der Betrieb des Debuggers gestartet, angehalten und gesteuert wird.|[Ausführen des Transact-SQL-Debuggers](../../relational-databases/scripting/run-the-transact-sql-debugger.md)|  
|Beschreibt die Verwendung des [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debuggers, um Code in Einzelschritten auszuführen.|[Schrittweises Durchlaufen von Transact-SQL-Code](../../relational-databases/scripting/step-through-transact-sql-code.md)|  
|Beschreibt die Verwendung des Debuggers, um [!INCLUDE[tsql](../../includes/tsql-md.md)] -Daten, z. B. Parameter und Variablen, und Systeminformationen anzuzeigen.|[Transact-SQL-Debuggerinformationen](../../relational-databases/scripting/transact-sql-debugger-information.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Abfrage- und Text-Editoren &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
