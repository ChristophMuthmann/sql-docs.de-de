---
title: "Veröffentlichen der Ausführung der gespeicherten Prozedur in einer Transaktionspublikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a709463393f37dd3d6ac3af64f62fe70a8556cad
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="publish-execution-of-stored-procedure-in-transactional-publication"></a>Veröffentlichen der Ausführung der gespeicherten Prozedur in einer Transaktionspublikation
  Im Dialogfeld **Artikeleigenschaften - \<Article>** können Sie angeben, dass die Ausführung einer gespeicherten Prozedur (und nicht nur ihre Definition) veröffentlicht werden soll. Dieses Dialogfeld ist im Assistenten für neue Veröffentlichung sowie über das Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** verfügbar. Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen Sie eine Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
 Die Definition der Prozedur (die CREATE PROCEDURE-Anweisung) wird beim Initialisieren des Abonnements auf den Abonnenten repliziert. Wenn die Prozedur dann auf dem Verleger ausgeführt wird, führt die Replikation auch die entsprechende Prozedur auf dem Abonnenten aus.  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>So veröffentlichen Sie die Ausführung einer gespeicherten Prozedur  
  
1.  Wählen Sie auf der Seite **Artikel** des Assistenten für neue Veröffentlichung oder im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** eine gespeicherte Prozedur aus.  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Gespeicherte Prozedur-Artikels festlegen**.  
  
3.  Geben Sie im Dialogfeld **Artikeleigenschaften - \<Article>** einen der folgenden Werte für die Option **Replizieren** an:  
  
    -   **Ausführung der gespeicherten Prozedur**  
  
    -   **Ausführung in einer serialisierten Transaktion**  
  
         Es handelt sich hierbei um die bevorzugte Option, da hier die Prozedurausführung nur repliziert wird, wenn die Prozedur im Kontext einer serialisierbaren Transaktion ausgeführt wird. Falls die gespeicherte Prozedur außerhalb einer serialisierbaren Transaktion ausgeführt wird, werden Änderungen an den Daten in veröffentlichten Tabellen als eine Reihe von DML-Anweisungen (Data Manipulation Language, Datenbearbeitungssprache) repliziert.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Wenn Sie sich im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** befinden, klicken Sie auf **OK**, um eine Speicherung vorzunehmen und das Dialogfeld zu schließen.  
  
## <a name="see-also"></a>Siehe auch  
 [Veröffentlichen der Ausführung von gespeicherten Prozeduren in der Transaktionsreplikation](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
