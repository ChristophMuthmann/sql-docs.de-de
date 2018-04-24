---
title: Fenster „Aufrufliste“ | Microsoft-Dokumentation
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
f1_keywords:
- vs.debug.callstack
helpviewer_keywords:
- Call Stack Window [Transact-SQL]
ms.assetid: ddb0b19c-87cd-4883-bcb8-ec09ffb30369
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f131bfaa5e32339f26932fbc4806233aa9c571ab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="transact-sql-debugger---call-stack-window"></a>Transact-SQL-Debugger – Fenster „Aufrufliste“
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Im Fenster **Aufrufliste** werden die Module in der Aufrufliste angezeigt sowie die Datentypen und die Werte aller Parameter, die an die Module übergeben werden. [!INCLUDE[tsql](../../includes/tsql-md.md)] -Module umfassen gespeicherte Prozeduren, benutzerdefinierte Funktionen und Trigger. Um die Aufrufliste anzuzeigen, müssen Sie sich im Debugmodus befinden.  
  
## <a name="task-list"></a>Aufgabenliste  
 **So greifen Sie auf das Fenster Aufrufliste zu**  
  
-   Klicken Sie im Menü **Debuggen** auf **Fenster**und dann auf **Aufrufliste**.  
  
 **So ändern Sie den aktuellen Aufruflistenrahmen**  
  
 Sie können eine der folgenden Prozeduren verwenden, um einen Stapelrahmen zum aktuellen Rahmen zu machen:  
  
-   Klicken Sie mit der rechten Maustaste auf den Stapelrahmen, und klicken Sie dann auf **Zu Rahmen wechseln**.  
  
-   Doppelklicken Sie auf den Stapelrahmen.  
  
 **So zeigen Sie die Quelle eines anderen Rahmens an, der nicht der aktuelle Rahmen ist**  
  
-   Klicken Sie mit der rechten Maustaste auf den Stapelrahmen, und klicken Sie dann auf **Gehe zu Quellcode**.  
  
## <a name="stack-frames"></a>Stapelrahmen  
 Jede Zeile im Fenster **Aufrufliste** wird als Stapelrahmen bezeichnet und stellt entweder einen Aufruf aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skriptdatei zu einem Modul oder einen Aufruf von einem Modul zu einem anderen dar. Der untere Stapelrahmen im Anzeigebereich gibt die Zeile im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Fenster an, die den ersten Aufruf an den Stapel ausgelöst hat. Die oberste Zeile gibt die Zeile an, an der der Debugger die Ausführung angehalten hat und die am linken Rand des Fensters durch einen gelben Pfeil gekennzeichnet ist. Jede dazwischen liegende Zeile gibt das Modul und die Zeilennummer des Quellcodes an, der den nächsthöheren Stapelrahmen aufgerufen hat.  
  
 Alle Ausdrücke in den Fenstern **Lokal**, **Überwachung**und **Schnellüberwachung** werden auf Grundlage des aktuellen Stapelrahmens ausgewertet. Im Abfrage-Editor-Fenster wird der Code für den aktuellen Rahmen angezeigt. Standardmäßig ist der aktuelle Stapelrahmen der Rahmen, in dem der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger die Ausführung angehalten hat. Wenn Sie den aktuellen Stapelrahmen zu einem anderen Rahmen ändern, werden die Ausdrücke in den Fenstern **Lokal**, **Überwachung**und **Schnellüberwachung** im Kontext des neuen Rahmens neu ausgewertet, und der Quellcode des neuen Rahmens wird im Abfrage-Editor-Fenster angezeigt.  
  
## <a name="columns"></a>Spalte  
 **Name**  
 Zeigt Informationen über ein Modul in der Aufrufliste an.  
  
 Für die letzte Zeile in der Aufrufliste werden unter **Name** das Abfrage-Editor-Quellcodefenster und die Zeilennummer des ersten Aufrufs an den Stapel aufgelistet. Für die anderen Zeilen hat **Name** das Format **Modul(Instanz.Datenbank)(Parameterliste) Zeilennummer**.  
  
 **Modul**  
 Der Name der gespeicherten Prozedur, Funktion oder gespeicherten Prozedur, die einen Aufruf zum nächsten Rahmen ausgelöst hat.  
  
 **Instanz.Datenbank**  
 Die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] sowie die Datenbank, die das Modul enthält.  
  
 **Parameterliste**  
 Gibt für jeden Parameter, der während des Aufrufs an das Modul übergeben wird, den Datentyp, Namen und Wert an.  
  
 **LineNumber**  
 Für alle Zeilen mit Ausnahme der obersten gibt **Zeilennummer** an, welche Zeile im Modul einen Aufruf zum Rahmen ausgelöst hat. Für die oberste Zeile gibt **Zeilennummer** die Zeile an, auf die der Debugger gerade fokussiert ist.  
  
 **Sprache**  
 Zeigt **Transact-SQL** für [!INCLUDE[tsql](../../includes/tsql-md.md)]an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Transact-SQL-Debugger](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL-Debuggerinformationen](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Schrittweises Durchlaufen von Transact-SQL-Code](../../relational-databases/scripting/step-through-transact-sql-code.md)  
  
  
