---
title: "Anzeigen von Datenkonflikten für Transaktionsveröffentlichungen (SSMS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
- viewing conflict information
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 966493051334ca3ead4b6412545ab77e97edafc0
ms.lasthandoff: 04/11/2017

---
# <a name="view-data-conflicts-for-transactional-publications-sql-server-management-studio"></a>Anzeigen von Datenkonflikten für Transaktionsveröffentlichungen (SQL Server Management Studio)
  Sie können Konflikte bei der Peer-zu-Peer-Transaktionsreplikation und der Transaktionsreplikation mit Abonnements mit verzögertem Update über eine Warteschlange im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Replikationskonflikt-Viewer anzeigen. Informationen, wie Konflikte erkannt und behoben werden, finden Sie unter [Konflikterkennung bei der Peer-to-Peer-Replikation](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md) und [Festlegen der Konfliktlösungsoptionen für verzögerte Updates über eine Warteschlange &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md).  
  
 Die Verfügbarkeit von Konfliktdaten hängt vom Typ der Replikation und der Beibehaltungsdauer ab:  
  
-   Bei der Peer-zu-Peer-Replikation schlägt der Verteilungs-Agent standardmäßig fehl, wenn er einen Konflikt erkennt. Im Fehlerprotokoll wird ein Konfliktfehler protokolliert, jedoch werden in der Konflikttabelle keine Konfliktdaten erfasst; daher können sie nicht angezeigt werden. Wenn der Verteilungs-Agent fortfahren kann, wird der Konflikt lokal auf jedem Knoten protokolliert, auf dem er erkannt wurde. Weitere Informationen finden Sie im Abschnitt "Konfliktbehandlung" unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
-   Bei Abonnements mit verzögertem Update über eine Warteschlange sind Daten für jeden Konflikt verfügbar. Die Konfliktdaten sind im Replikationskonflikt-Viewer für den Zeitraum verfügbar, der als Beibehaltungsdauer für Konfliktdaten (bei Standardeinstellung 14 Tage) angegeben wurde. Um die Beibehaltungsdauer für Konfliktdaten festzulegen, können Sie auf zweierlei Weise vorgehen:  
  
    -   Geben Sie einen Beibehaltungswert für den Parameter @conflict_retention von [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)an.  
  
    -   Geben Sie den Wert **'conflict_retention'** für den @property -Parameter und einen Beibehaltungswert für den @value von [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md).  
  
### <a name="to-view-conflicts"></a>So zeigen Sie Konflikte an  
  
1.  Stellen Sie die Verbindung zum entsprechenden Server in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]her, und erweitern Sie dann den Serverknoten:  
  
    -   Für die Peer-zu-Peer-Replikation ist dies der Knoten, bei dem der Konflikt aufgetreten ist.  
  
    -   Für Abonnements mit verzögertem Update über eine Warteschlange ist dies der Verleger.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Veröffentlichung, für die Sie die Konflikte anzeigen möchten, und klicken Sie dann auf **Konflikte anzeigen**.  
  
4.  Wählen Sie im Dialogfeld **Konflikttabelle auswählen** eine Datenbank, eine Veröffentlichung und eine Tabelle aus, für die Sie die Konflikte anzeigen möchten.  
  
5.  Im Replikationskonflikt-Viewer können Sie folgende Aktionen ausführen:  
  
    -   Filtern Sie Zeilen mit den Schaltflächen rechts vom oberen Raster.  
  
    -   Wählen Sie eine Zeile im oberen Raster aus, um Informationen zur Zeile im unteren Raster anzuzeigen.  
  
    -   Wählen Sie eine oder mehrere Zeilen im oberen Raster aus, und klicken Sie auf **Entfernen**. Die Zeilen werden dann aus der Metatabelle für Konflikte gelöscht.  
  
    -   Klicken Sie auf die Eigenschaftenschaltfläche (**…**), um weitere Informationen zu einer am Konflikt beteiligten Zeile anzuzeigen.  
  
    -   Aktivieren Sie **Details dieses Konflikts protokollieren** , um Konfliktdaten in einer Datei zu protokollieren. Um einen Speicherort für die Datei anzugeben, zeigen Sie auf das Menü **Ansicht** , und klicken Sie dann auf **Optionen**. Geben Sie einen Wert ein, oder klicken Sie auf die Schaltfläche mit den drei Punkten (**...**), und wechseln Sie in das entsprechende Verzeichnis. Klicken Sie auf **OK** , um das Dialogfeld **Optionen** zu schließen.  
  
6.  Schließen Sie den Replikationskonflikt-Viewer.  
  
## <a name="see-also"></a>Siehe auch  
 [Peer-zu-Peer-Transaktionsreplikation](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
