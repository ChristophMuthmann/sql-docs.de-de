---
title: "Ver&#246;ffentlichen der Ausf&#252;hrung einer gespeicherten Prozedur in einer Transaktionsver&#246;ffentlichung (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Veröffentlichen [SQL Server-Replikation], Ausführung von gespeicherten Prozeduren"
  - "Gespeicherte Prozeduren [SQL Server-Replikation], veröffentlichen"
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Ver&#246;ffentlichen der Ausf&#252;hrung einer gespeicherten Prozedur in einer Transaktionsver&#246;ffentlichung (SQL Server Management Studio)
  Gibt an, dass die Ausführung einer gespeicherten Prozedur (und nicht nur ihre Definition) veröffentlicht werden soll die **Artikeleigenschaften - \< Artikel>** (Dialogfeld). Dieses Dialogfeld steht im Assistenten für neue Veröffentlichung und die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
 Die Definition der Prozedur (die CREATE PROCEDURE-Anweisung) wird beim Initialisieren des Abonnements auf den Abonnenten repliziert. Wenn die Prozedur dann auf dem Verleger ausgeführt wird, führt die Replikation auch die entsprechende Prozedur auf dem Abonnenten aus.  
  
### So veröffentlichen Sie die Ausführung einer gespeicherten Prozedur  
  
1.  Auf der **Artikel** Seite des Assistenten für neue Veröffentlichung oder **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld Wählen Sie eine gespeicherte Prozedur.  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Gespeicherte Prozedur-Artikels festlegen**.  
  
3.  In der **Artikeleigenschaften - \< Artikel>** Dialogfeld geben die folgenden Werte für die **replizieren** Option:  
  
    -   **Ausführung der gespeicherten Prozedur**  
  
    -   **Ausführung in einer serialisierten Transaktion**  
  
         Es handelt sich hierbei um die bevorzugte Option, da hier die Prozedurausführung nur repliziert wird, wenn die Prozedur im Kontext einer serialisierbaren Transaktion ausgeführt wird. Falls die gespeicherte Prozedur außerhalb einer serialisierbaren Transaktion ausgeführt wird, werden Änderungen an den Daten in veröffentlichten Tabellen als eine Reihe von DML-Anweisungen (Data Manipulation Language, Datenbearbeitungssprache) repliziert.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Wenn Sie haben die **Veröffentlichungseigenschaften - \< Veröffentlichung>** Klicken Sie im Dialogfeld klicken Sie auf **OK** zum Speichern und schließen das Dialogfeld.  
  
## Siehe auch  
 [Veröffentlichen der Ausführung von gespeicherten Prozeduren in der Transaktionsreplikation](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  