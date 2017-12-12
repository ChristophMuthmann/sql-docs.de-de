---
title: Herstellen einer Verbindung mit dem Abfrage-Editor | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 48725f54-a7b6-4b79-948e-965c1fe4eef1
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5a822268755f46da6775150119b6c7fd771838c8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-2-1---connecting-with-query-editor"></a>Lektion 2-1: Herstellen einer Verbindung mit dem Abfrage-Editor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Sie auch dann Code schreiben oder bearbeiten, wenn Sie nicht mit dem Server verbunden sind. Dies kann nützlich sein, wenn der Server nicht verfügbar ist oder wenn die Ressourcen auf dem Server oder im Netzwerk knapp sind. Sie können auch den Abfrage-Editor mit einer neuen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbinden, ohne ein neues Abfrage-Editorfenster zu öffnen und ohne den Code neu einzugeben.  
  
## <a name="coding-offline"></a>Schreiben von Code offline  
  
#### <a name="to-write-code-offline-and-then-connect-to-different-servers"></a>So schreiben Sie Code offline und stellen dann Verbindungen mit verschiedenen Servern her  
  
1.  Klicken Sie auf der Symbolleiste von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] auf **Datenbankmodul-Abfrage** , um den Abfrage-Editor zu öffnen.  
  
2.  Klicken Sie im Dialogfeld **Verbindung mit Datenbankmodul herstellen** auf **Abbrechen**. Der Abfrage-Editor wird geöffnet, und in der Titelleiste des Abfrage-Editors wird angezeigt, dass Sie mit keiner Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verbunden sind.  
  
3.  Geben Sie im Codebereich folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen ein:  
  
    ```  
    SELECT * FROM Production.Product;  
    GO  
    ```  
  
    An diesem Punkt können Sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen, indem Sie auf **Verbinden**, **Ausführen**, **Analysieren**oder **Geschätzten Ausführungsplan anzeigen**klicken. Alle diese Optionen sind im Menü **Abfrage** , auf der Symbolleiste des Abfrage-Editors oder in dem Kontextmenü verfügbar, das angezeigt wird, wenn Sie mit der rechten Maustaste in das Abfrage-Editorfenster klicken. Im Rahmen dieser Übung verwenden wir die Symbolleiste.  
  
4.  Klicken Sie auf der Symbolleiste auf die Schaltfläche **Ausführen** , um das Dialogfeld **Verbindung mit Datenbankmodul herstellen** zu öffnen.  
  
5.  Geben Sie im Textfeld **Servername** den Namen Ihres Servers ein, und klicken Sie dann auf **Optionen**.  
  
6.  Durchsuchen Sie auf der Registerkarte **Verbindungseigenschaften** in der Liste **Verbindung mit Datenbank herstellen** den Server, um [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] auszuwählen, und klicken Sie dann auf **Verbinden**.  
  
7.  Wenn Sie für dieselbe Verbindung ein weiteres Abfrage-Editorfenster öffnen möchten, klicken Sie auf das Symbolleiste auf **Neue Abfrage**.  
  
8.  Klicken Sie mit der rechten Maustaste auf das Abfrage-Editor-Fenster, zeigen Sie auf **Verbindung**, und klicken Sie anschließend auf **Verbindung ändern**, um die Verbindungen zu ändern.  
  
9. Wählen Sie im Dialogfeld **Verbindung mit SQL Server herstellen** eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (falls verfügbar), und klicken Sie dann auf **Verbinden**.  
  
Diese neue Funktion des Abfrage-Editors ermöglicht es Ihnen, denselben Code auf mehreren Servern auszuführen. Dies kann für Wartungsaktionen nützlich sein, an denen mehrere Server beteiligt sind.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Hinzufügen von Einzügen](../../tools/sql-server-management-studio/lesson-2-2-adding-indentation.md)  
  
  
  
