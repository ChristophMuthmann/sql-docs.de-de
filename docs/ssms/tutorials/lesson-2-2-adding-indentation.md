---
title: "Hinzufügen von Einzügen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 9dce05c1-c52f-455d-8b8d-6f303e242760
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: 55241a0b99024f557718654869d0ab728089e569
ms.contentlocale: de-de
ms.lasthandoff: 06/23/2017

---
# <a name="lesson-2-2---adding-indentation"></a>Lektion 2-2: Hinzufügen von Einzügen
Der Abfrage-Editor ermöglicht es Ihnen, mit nur einem Schritt einen Einzug für große Codeabschnitte festzulegen. Außerdem können Sie die Größe des Einzugs ändern.  
  
## <a name="indenting-code"></a>Festlegen von Einzügen für Code  
  
#### <a name="to-indent-multiple-lines-of-code"></a>So legen Sie einen Einzug für mehrere Codezeilen fest  
  
1.  Klicken Sie auf der Symbolleiste auf **Neue Abfrage**.  
  
2.  Erstellen Sie eine zweite Abfrage, über die die Spalten **BusinessEntityID**, FirstName, **MiddleName**und **LastName** aus der Tabelle **Person** der Schemas **Person** ausgewählt werden. Platzieren Sie jede Spalte in eine separate Zeile, sodass der Code wie folgt aussieht:  
  
    ```  
    -- Search for a contact  
    SELECT   
    BusinessEntityID,  
    FirstName,   
    MiddleName,   
    LastName  
    FROM Person.Person  
    WHERE LastName = 'Sanchez';  
    GO  
    ```  
  
3.  Markieren Sie den gesamten Text von `BusinessEntityID` bis `LastName`.  
  
4.  Klicken Sie auf der Symbolleiste **SQL-Editor** auf **Einzug vergrößern** , um für alle Zeilen gleichzeitig einen Einzug festzulegen.  
  
#### <a name="to-change-the-default-indentation"></a>So ändern Sie den Standardeinzug  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
2.  Erweitern Sie **Text-Editor**, erweitern Sie **Alle Sprachen**, und klicken Sie dann auf **Tabstopps** , um die gewünschten Werte für die Einzüge festzulegen. Beachten Sie, dass Sie die Größe des Einzugs und der Tabstopps festlegen können und angeben können, ob Tabstopps in Leerzeichen umgewandelt werden sollen.  
  
    ![Erscheinen des Dialogfelds „Registerkarten“](./media/lesson-2-2-adding-indentation/tabsdialog.gif "Appearance of the Tabs dialog box")  
  
3.  Klicken Sie auf **OK**.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Maximieren des Abfrage-Editors](../../tools/sql-server-management-studio/lesson-2-3-maximizing-query-editor.md)  
  
  
  

