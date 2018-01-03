---
title: "Hinzufügen von Einzügen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 9dce05c1-c52f-455d-8b8d-6f303e242760
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5559f970627449d56863f4c9d933d5e6636f0bd2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="lesson-2-2---adding-indentation"></a>Lektion 2-2: Hinzufügen von Einzügen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Der Abfrage-Editor ermöglicht es Ihnen, mit nur einem Schritt einen Einzug für große Codeabschnitte festzulegen. Außerdem können Sie die Größe des Einzugs ändern.  
  
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
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Maximieren des Abfrage-Editors](../../tools/sql-server-management-studio/lesson-2-3-maximizing-query-editor.md)  
  
  
  
