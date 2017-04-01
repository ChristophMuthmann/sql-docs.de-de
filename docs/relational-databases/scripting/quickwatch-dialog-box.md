---
title: "Dialogfeld &#39;Schnell&#252;berwachung&#39; | Microsoft Docs"
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
  - "vs.debug.quickwatch"
helpviewer_keywords: 
  - "Dialogfeld 'Schnellüberwachung' [Transact-SQL]"
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Dialogfeld &#39;Schnell&#252;berwachung&#39;
  Mithilfe des Dialogfelds **Schnellüberwachung** können Sie beim Debuggen von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code schnell den Datentyp und den Wert eines [!INCLUDE[tsql](../../includes/tsql-md.md)] -Ausdrucks anzeigen, wie z. B. einer Variable oder eines Parameters. Um mehrere Ausdrücke zu beobachten, können Sie den Ausdruck auch einem Überwachungsfenster **** hinzufügen.  
  
## Aufgabenliste  
 **So greifen Sie auf das Dialogfeld Schnellüberwachung zu**  
  
-   Klicken Sie im Menü **Debuggen** auf **Schnellüberwachung**.  
  
 **So zeigen Sie die Informationen zu einem Ausdruck an**  
  
1.  Geben Sie den gewünschten Ausdruck im Listenfeld **Ausdruck** ein, oder wählen Sie ihn aus. Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Ausdrücke werden unterstützt:  
  
    -   Variablen  
  
    -   Parameter.  
  
    -   Systemfunktionen, deren Name mit "@@" beginnt  
  
    -   Ausdrücke, die durch Anwenden von Operatoren auf eine oder mehrere Variablen, Parameter oder Systemfunktionen erstellt werden, z. B. "@IntegerCounter + 1" oder "FirstName + LastName"  
  
    -   Transact-SQL-Anweisungen, die einen einzelnen Wert zurückgeben, z. B.: "SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1"  
  
2.  Klicken Sie auf **Neu auswerten**.  
  
 **So fügen Sie den Ausdruck der Schnellüberwachung einem Überwachungsfenster hinzu**  
  
-   Klicken Sie auf **Überwachung hinzufügen**.  
  
 **So ändern Sie den Wert des Ausdrucks der Schnellüberwachung**  
  
-   Klicken mit der rechten Maustaste auf den Ausdruck, und wählen Sie anschließend **Wert bearbeiten** aus.  
  
## Optionen  
 **Ausdruckliste**  
 Zeigt den aktuell ausgewählten Ausdruck an. Die Dropdownliste enthält einen Satz von Ausdrücken, deren Anzeige Sie auswählen können. In der Liste sind jene Ausdrücke aufgeführt, die im Bereich des Stapelrahmens verfügbar sind, der im Fenster **Aufrufliste** aktuell ausgewählt ist. Um einen anderen Ausdruck anzuzeigen, geben Sie entweder den Ausdruck ein, oder wählen Sie ihn aus der Liste aus. Der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debugger unterstützt die folgenden Ausdrücke: Variablen, Parameter und die Systemfunktionen, deren Namen mit @@ beginnen.  
  
 **Werteraster**  
 Zeigt die Eigenschaften des Ausdrucks an, der gerade beobachtet wird.  
  
 **Name**  
 Entspricht dem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ausdruck, der beobachtet wird.  
  
 **Wert**  
 Zeigt den Wert an, der dem Ausdruck derzeit zugewiesen ist. Ein Leerzeichen wird angezeigt, wenn der Ausdruck gerade über keinen Wert verfügt.  
  
 Wenn die Länge eines Ausdrucks größer als die Breite der Spalte **Wert** ist, wird der vollständige Wert in einer QuickInfo angezeigt, wenn Sie den Mauszeiger über die **** Wertzelle für diesen Ausdruck bewegen.  
  
 Ein Lupensymbol in einer **** Wertzelle zeigt an, dass die [!INCLUDE[tsql](../../includes/tsql-md.md)] Debuggerschnellansicht verfügbar ist. In der Liste können Sie **Text-Schnellansicht**, **XML-Schnellansicht**oder **HTML-Schnellansicht**angeben. Um eine Debuggerschnellansicht zu starten, klicken Sie auf das Lupensymbol. Der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debugger öffnet ein Dialogfeld, in dem die Daten in einem für den Datentyp geeigneten Format angezeigt werden.  
  
 **Typ**  
 Zeigt den Datentyp des Ausdrucks an.  
  
## Siehe auch  
 [Transact-SQL-Debugger](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL-Debuggerinformationen](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Überwachung (Fenster)](../../relational-databases/scripting/watch-window.md)   
 [Lokal (Fenster)](../../relational-databases/scripting/locals-window.md)   
 [Fenster 'Aufrufliste'](../../relational-databases/scripting/call-stack-window.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  