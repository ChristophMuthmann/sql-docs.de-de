---
title: Überwachung (Fenster) | Microsoft-Dokumentation
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
- vs.debug.watch
helpviewer_keywords:
- Watch Window [Transact-SQL]
ms.assetid: 23f3baa4-14c2-4262-92f7-3f43fcfa0436
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c5af124d567e001afc3d1790de38d87daebe0d84
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="transact-sql-debugger---watch-window"></a>Transact-SQL-Debugger – Überwachung (Fenster)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Im Fenster **Überwachung** werden Informationen über die Ausdrücke angezeigt, die Sie ausgewählt haben. Es können bis zu vier Überwachungsfenster verfügbar sein: **Überwachen 1**, **Überwachen 2**, Überwachen 3 und **Überwachen 4**. Die Ausdrücke werden innerhalb des Bereichs des aktuellen Aufruflistenrahmens ausgewertet, der im Fenster **Aufrufliste** ausgewählt ist. Sie müssen sich im Debugmodus befinden, um Variablen und Ausdrücke zu beobachten.  
  
## <a name="task-list"></a>Aufgabenliste  
 **So greifen Sie auf die Überwachungsfenster zu**  
  
-   Klicken Sie im Menü **Debuggen** auf **Fenster**, klicken Sie auf **Überwachung**, und klicken Sie dann auf **Überwachung 1**, **Überwachung 2**, **Überwachung 3**oder Überwachung 4.  
  
 **So ändern Sie den Wert eines Ausdrucks**  
  
-   Klicken mit der rechten Maustaste auf den Ausdruck, und wählen Sie anschließend **Wert bearbeiten**aus.  
  
## <a name="columns"></a>Spalte  
 **Name**  
 Die Ausdrücke, die vom [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger aufgelistet werden. Die folgenden Ausdrücke werden unterstützt:  
  
-   Variablen  
  
-   Parameter.  
  
-   Systemfunktionen, deren Name mit „@@“ beginnt.  
  
-   Ausdrücke, die durch Anwenden von Operatoren auf eine oder mehrere Variablen, Parameter oder Systemfunktionen erstellt werden, z.B. "@IntegerCounter + 1" oder "FirstName + LastName"  
  
-   Transact-SQL-Anweisungen, die einen einzelnen Wert zurückgeben, z. B.: "SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1"  
  
 **ReplTest1**  
 Zeigt den Wert an, der zurückgegeben wird, nachdem der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger den in **Name**angegebenen Ausdruck ausgewertet hat.  
  
 Wenn die Länge eines Ausdrucks größer als die Breite der Spalte **Wert** ist, wird der vollständige Wert in einer QuickInfo angezeigt, wenn Sie den Mauszeiger über die **Wertzelle** für diesen Ausdruck bewegen.  
  
 Ein Lupensymbol in einer **Wertzelle** zeigt an, dass die [!INCLUDE[tsql](../../includes/tsql-md.md)] Debuggerschnellansicht verfügbar ist. In der Liste können Sie **Text-Schnellansicht**, **XML-Schnellansicht**oder **HTML-Schnellansicht**angeben. Um eine Debuggerschnellansicht zu starten, klicken Sie auf das Lupensymbol. Der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger öffnet ein Dialogfeld, in dem die Daten in einem für den Datentyp geeigneten Format angezeigt werden.  
  
 **Typ**  
 Zeigt den Datentyp des Ausdrucks an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Transact-SQL-Debugger](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL-Debuggerinformationen](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Lokal (Fenster)](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [Fenster 'Aufrufliste'](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [Dialogfeld 'Schnellüberwachung'](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
