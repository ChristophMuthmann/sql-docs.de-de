---
title: "Anzeigen und L&#246;sen von Datenkonflikten f&#252;r Mergever&#246;ffentlichungen (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Konfliktlösung bei der Mergereplikation [SQL Server-Replikation], Anzeigen von Konflikten"
  - "Anzeigen von Konfliktinformationen"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Anzeigen und L&#246;sen von Datenkonflikten f&#252;r Mergever&#246;ffentlichungen (SQL Server Management Studio)
  Konflikte bei der Mergereplikation werden anhand des für den jeweiligen Artikel angegebenen Konfliktlösers gelöst. Standardmäßig werden Konflikte ohne Benutzereingriff gelöst. Konflikte können jedoch im Replikationskonflikt-Viewer von [!INCLUDE[msCoName](../../includes/msconame-md.md)] angezeigt und das Ergebnis der Konfliktlösung kann geändert werden.  
  
 Die Konfliktdaten sind im Replikationskonflikt-Viewer für den Zeitraum verfügbar, der als Beibehaltungsdauer der Konflikte (bei einer Standardeinstellung von 14 Tagen) angegeben wurde. Zum Festlegen der Beibehaltungsdauer der Konflikte haben Sie folgende Möglichkeiten:  
  
-   Geben Sie einen Wert für die Beibehaltungsdauer für die **@conflict_retention** Parameter [Sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
-   Geben Sie den Wert **Conflict_retention** für die **@property** Parameter und eine Beibehaltungsdauer Wert für die **@value** Parameter [Sp_changemergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Standardmäßig werden Konfliktinformationen an den folgenden Orten gespeichert:  
  
-   Auf dem Verleger und Abonnenten, wenn die Veröffentlichung mindestens einen Kompatibilitätsgrad von 90RTM aufweist.  
  
-   Auf dem Verleger, wenn die Veröffentlichung einen geringeren Kompatibilitätsgrad als 80RTM aufweist.  
  
-   Auf dem Verleger, wenn auf den Abonnenten [!INCLUDE[ssEW](../../includes/ssew-md.md)]ausgeführt wird. Konfliktdaten dürfen nicht auf Abonnenten mit [!INCLUDE[ssEW](../../includes/ssew-md.md)] gespeichert werden.  
  
 Speichern von Konfliktinformationen wird gesteuert, indem die **Conflict_logging** veröffentlichungseigenschaft. Weitere Informationen finden Sie unter [Sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) und [Sp_changemergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Konflikte können während der Synchronisierung auch mit dem interaktiven [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Replikationskonfliktlöser gelöst werden. Der interaktive Konfliktlöser ist über die Synchronisierungsverwaltung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows verfügbar. Weitere Informationen finden Sie unter [synchronisieren Sie ein Abonnement mithilfe von Windows Synchronization Manager & #40; Windows-Synchronisierungs-Manager & #41;](../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md).  
  
### So zeigen Sie Konflikte von Mergeveröffentlichungen an und lösen Sie die Konflikte  
  
1.  Verbinden mit dem Verleger (oder gegebenenfalls Abonnenten) in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Mit der rechten Maustaste in der Veröffentlichung, für die Sie Konflikte anzeigen, und klicken Sie dann auf möchten **Konflikte anzeigen**.  
  
    > [!NOTE]  
    >  Wenn Sie einen Wert von angegeben **'Subscriber'** für die **Conflict_logging** -Eigenschaft, die **Konflikte anzeigen** Menüoption ist nicht verfügbar. Starten Sie zum Anzeigen von Konflikten ConflictViewer.exe von der Eingabeaufforderung aus. ConflictViewer.exe befindet sich standardmäßig im folgenden Verzeichnis: Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE. Eine Liste der gültigen Startparameter erhalten Sie, wenn Sie ConflictViewer.exe -? ausführen.  
  
4.  Wählen Sie im Dialogfeld **Konflikttabelle auswählen** eine Datenbank, eine Veröffentlichung und eine Tabelle aus, für die Sie die Konflikte anzeigen möchten.  
  
5.  Im Replikationskonflikt-Viewer können Sie folgende Aktionen ausführen:  
  
    -   Filtern Sie Zeilen mit den Schaltflächen rechts vom oberen Raster.  
  
    -   Wählen Sie eine Zeile im oberen Raster aus, um Informationen zur Zeile im unteren Raster anzuzeigen.  
  
    -   Wählen Sie eine oder mehrere Zeilen im oberen Raster aus, und klicken Sie dann auf **Entfernen**, dies entspricht dem Klicken auf die **Gewinner Absenden** Schaltfläche (ohne Änderungen an den Daten vorzunehmen).  
  
    -   Klicken Sie auf die Eigenschaftenschaltfläche (**...**) zum Anzeigen weiterer Informationen für eine Spalte einen Konflikt beteiligt.  
  
    -   Bearbeiten von Daten in die **Konfliktgewinner** oder **konfliktverlierer** Spalte vor dem Senden der Daten (Daten sind schreibgeschützt, wenn die Spalte Grau ist).  
  
    -   Klicken Sie auf **Gewinner absenden** , um die als Gewinner des Konflikts ausgewiesene Spalte zu akzeptieren.  
  
    -   Klicken Sie auf **Verlierer absenden** , um die Konfliktlösung zu überschreiben und den als Verlierer des Konflikts ausgewiesenen Wert an alle Knoten der Topologie zu senden.  
  
    -   Aktivieren Sie **Details dieses Konflikts protokollieren** , um Konfliktdaten in einer Datei zu protokollieren. Um einen Speicherort für die Datei anzugeben, zeigen Sie auf das Menü **Ansicht** , und klicken Sie dann auf **Optionen**. Geben Sie einen Wert aus, oder klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), und navigieren Sie zu der entsprechenden Datei. Klicken Sie auf **OK** , um das Dialogfeld **Optionen** zu beenden.  
  
6.  Schließen Sie den Replikationskonflikt-Viewer.  
  
## Siehe auch  
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Angeben eines Mergeartikelkonfliktlösers](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  