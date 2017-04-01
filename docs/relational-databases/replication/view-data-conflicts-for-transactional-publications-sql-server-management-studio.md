---
title: "Anzeigen von Datenkonflikten f&#252;r Transaktionsver&#246;ffentlichungen (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Konfliktlösung [SQL Server-Replikation], Abonnements mit verzögertem Update über eine Warteschlange"
  - "Abonnements mit verzögertem Update über eine Warteschlange [SQL Server-Replikation]"
  - "Anzeigen von Konfliktinformationen"
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Anzeigen von Datenkonflikten f&#252;r Transaktionsver&#246;ffentlichungen (SQL Server Management Studio)
  Sie können Konflikte bei der Peer-zu-Peer-Transaktionsreplikation und der Transaktionsreplikation mit Abonnements mit verzögertem Update über eine Warteschlange im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Replikationskonflikt-Viewer anzeigen. Informationen, wie Konflikte erkannt und behoben werden können, finden Sie unter [Konflikterkennung bei der Peer-to-Peer-Replikation](../../relational-databases/replication/transactional/conflict-detection-in-peer-to-peer-replication.md) und [Legen Sie in der Warteschlange aktualisieren Konfliktlösungsoptionen & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md).  
  
 Die Verfügbarkeit von Konfliktdaten hängt vom Typ der Replikation und der Beibehaltungsdauer ab:  
  
-   Bei der Peer-zu-Peer-Replikation schlägt der Verteilungs-Agent standardmäßig fehl, wenn er einen Konflikt erkennt. Im Fehlerprotokoll wird ein Konfliktfehler protokolliert, jedoch werden in der Konflikttabelle keine Konfliktdaten erfasst; daher können sie nicht angezeigt werden. Wenn der Verteilungs-Agent fortfahren kann, wird der Konflikt lokal auf jedem Knoten protokolliert, auf dem er erkannt wurde. Weitere Informationen finden Sie unter "Konfliktbehandlung" in [Erkennung in der Peer-to-Peer-Replikation](../../relational-databases/replication/transactional/conflict-detection-in-peer-to-peer-replication.md).  
  
-   Bei Abonnements mit verzögertem Update über eine Warteschlange sind Daten für jeden Konflikt verfügbar. Die Konfliktdaten sind im Replikationskonflikt-Viewer für den Zeitraum verfügbar, der als Beibehaltungsdauer für Konfliktdaten (bei Standardeinstellung 14 Tage) angegeben wurde. Um die Beibehaltungsdauer für Konfliktdaten festzulegen, können Sie auf zweierlei Weise vorgehen:  
  
    -   Geben Sie einen Beibehaltungswert für den @conflict_retention-Parameter der [Sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
    -   Geben Sie den Wert **'Conflict_retention'** für den Parameter @property und einen Beibehaltungswert für den Parameter @value von [Sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md).  
  
### So zeigen Sie Konflikte an  
  
1.  Stellen Sie die Verbindung zum entsprechenden Server in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]her, und erweitern Sie dann den Serverknoten:  
  
    -   Für die Peer-zu-Peer-Replikation ist dies der Knoten, bei dem der Konflikt aufgetreten ist.  
  
    -   Für Abonnements mit verzögertem Update über eine Warteschlange ist dies der Verleger.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Mit der rechten Maustaste in der Veröffentlichung, für die Sie Konflikte anzeigen, und klicken Sie dann auf möchten **Konflikte anzeigen**.  
  
4.  Wählen Sie im Dialogfeld **Konflikttabelle auswählen** eine Datenbank, eine Veröffentlichung und eine Tabelle aus, für die Sie die Konflikte anzeigen möchten.  
  
5.  Im Replikationskonflikt-Viewer können Sie folgende Aktionen ausführen:  
  
    -   Filtern Sie Zeilen mit den Schaltflächen rechts vom oberen Raster.  
  
    -   Wählen Sie eine Zeile im oberen Raster aus, um Informationen zur Zeile im unteren Raster anzuzeigen.  
  
    -   Wählen Sie eine oder mehrere Zeilen im oberen Raster aus, und klicken Sie auf **Entfernen**. Die Zeilen werden dann aus der Metatabelle für Konflikte gelöscht.  
  
    -   Klicken Sie auf die Eigenschaftenschaltfläche (**...**) zum Anzeigen weiterer Informationen für eine Spalte einen Konflikt beteiligt.  
  
    -   Aktivieren Sie **Details dieses Konflikts protokollieren** , um Konfliktdaten in einer Datei zu protokollieren. Um einen Speicherort für die Datei anzugeben, zeigen Sie auf das Menü **Ansicht** , und klicken Sie dann auf **Optionen**. Geben Sie einen Wert aus, oder klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), und navigieren Sie zu der entsprechenden Datei. Klicken Sie auf **OK** , um das Dialogfeld **Optionen** zu schließen.  
  
6.  Schließen Sie den Replikationskonflikt-Viewer.  
  
## Siehe auch  
 [Peer-zu-Peer-Transaktionsreplikation](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Konflikterkennung und -lösung beim verzögerten Update über eine Warteschlange](../../relational-databases/replication/transactional/queued-updating-conflict-detection-and-resolution.md)  
  
  