---
title: "Fenster „Lokal“ | Microsoft-Dokumentation"
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
- vs.debug.locals
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 84668538d8c13c4317eec610afabcdf39d457899
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="transact-sql-debugger---locals-window"></a>Transact-SQL-Debugger – Fenster „Lokal“
  Im Fenster **Lokal** werden Informationen über die lokalen Ausdrücke im aktuellen Bereich des [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debuggers angezeigt. Der Bereich wird auf den aktuellen Aufruflistenrahmen festgelegt, der im Fenster **Aufrufliste** ausgewählt ist. Sie müssen sich im Debugmodus befinden, um die lokalen Ausdrücke anzuzeigen.  
  
## <a name="task-list"></a>Aufgabenliste  
 **So greifen Sie auf das Fenster Lokal zu**  
  
-   Klicken Sie im Menü **Debuggen** auf **Fenster**, und klicken Sie dann auf **Lokal**.  
  
 **So ändern Sie den Wert eines Ausdrucks**  
  
-   Klicken mit der rechten Maustaste auf den Ausdruck, und wählen Sie anschließend **Wert bearbeiten**aus.  
  
## <a name="columns"></a>Spalten  
 **Name**  
 Der Name des lokalen Ausdrucks. Der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debugger führt Variablen, Parameter und die Systemfunktionen, deren Namen mit @@ beginnen, auf.  
  
 **Value**  
 Zeigt den Wert an, der dem lokalen Ausdruck derzeit zugewiesen ist. Diese Spalte ist leer, wenn dem Ausdruck kein Wert zugewiesen wurde.  
  
 Wenn die Länge eines Ausdrucks größer als die Breite der Spalte **Wert** ist, wird der vollständige Wert in einer QuickInfo angezeigt, wenn Sie den Mauszeiger über die **Wertzelle** für diesen Ausdruck bewegen.  
  
 Ein Lupensymbol in einer **Wertzelle** zeigt an, dass die [!INCLUDE[tsql](../../includes/tsql-md.md)] Debuggerschnellansicht verfügbar ist. In der Liste können Sie **Text-Schnellansicht**, **XML-Schnellansicht**oder **HTML-Schnellansicht**angeben. Um eine Debuggerschnellansicht zu starten, klicken Sie auf das Lupensymbol. Der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger öffnet ein Dialogfeld, in dem die Daten in einem für den Datentyp geeigneten Format angezeigt werden.  
  
 **Typ**  
 Zeigt den Datentyp des Ausdrucks an.  
  
## <a name="see-also"></a>Siehe auch  
 [Transact-SQL-Debugger](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL-Debuggerinformationen](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Überwachung (Fenster)](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [Fenster 'Aufrufliste'](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [Dialogfeld 'Schnellüberwachung'](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
