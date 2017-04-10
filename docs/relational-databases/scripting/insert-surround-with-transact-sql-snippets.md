---
title: "Einf&#252;gen von Transact-SQL-Umschlie&#223;ungsausschnitten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Ausschnitte [Transact-SQL], umschließen mit"
  - "IntelliSense [SQL Server], umschließen mit Ausschnitten"
  - "Transact-SQL-Ausschnitte, umschließen mit"
ms.assetid: 5b5a8c6c-968e-4361-a7f5-9e2ac186d927
caps.latest.revision: 6
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 6
---
# Einf&#252;gen von Transact-SQL-Umschlie&#223;ungsausschnitten
  Als Umschließungsausschnitt wird eine Vorlage bezeichnet, die Sie als Ausgangspunkt beim Einschließen von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in einem BEGIN-, IF- oder WHILE-Block verwenden können.  
  
## Einfügen von Umschließungsausschnitten  
 Umschließungsausschnitte können mit einer von drei Methoden gestartet werden: mit einer Tastenkombination, über das Menü **Bearbeiten** und über das Kontextmenü.  
  
 Wenn Sie den Ausschnitt eingefügt haben, müssen Sie den Ersetzungstext so ändern, dass eine gültige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung entsteht. Weitere Informationen finden Sie unter [Abschließen von Transact-SQL-Ausschnitten](../../relational-databases/scripting/complete-transact-sql-snippets.md).  
  
#### So fügen Sie einen Umschließungsausschnitt ein  
  
1.  Wählen Sie im [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Abfrage-Editor-Fenster die im Block einzuschließenden Anweisungen aus.  
  
2.  Die Liste der Umschließungsausschnitte können Sie mit einer der folgenden drei Methoden anzeigen:  
  
    -   Drücken Sie STRG+K, STRG+S.  
  
    -   Zeigen Sie im Menü **Bearbeiten** auf **IntelliSense**, und wählen Sie dann den Befehl des **Umschließen mit** aus.  
  
    -   Klicken Sie mit der rechten Maustaste auf den markierten Text, und wählen Sie dann im Kontextmenü den Befehl **Umschließen mit** aus.  
  
3.  Wählen Sie in der Liste den Namen des Ausschnitts (BEGIN, IF oder WHILE) aus, indem Sie die Maus verwenden oder den Namen des Ausschnitts eingeben und TAB oder die EINGABETASTE drücken.  
  
## Siehe auch  
 [Einfügen von Transact-SQL-Ausschnitten](../../relational-databases/scripting/insert-transact-sql-snippets.md)  
  
  