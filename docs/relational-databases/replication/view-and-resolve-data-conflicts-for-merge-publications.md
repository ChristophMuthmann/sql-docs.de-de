---
title: "Anzeigen und Lösen von Datenkonflikten für Mergeveröffentlichungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
caps.latest.revision: "41"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2bc867c7c3c96d0b90793a14edd51313c5aed941
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="view-and-resolve-data-conflicts-for-merge-publications"></a>Anzeigen und Lösen von Datenkonflikten für Mergeveröffentlichungen
  Konflikte bei der Mergereplikation werden anhand des für den jeweiligen Artikel angegebenen Konfliktlösers gelöst. Standardmäßig werden Konflikte ohne Benutzereingriff gelöst. Konflikte können jedoch im Replikationskonflikt-Viewer von [!INCLUDE[msCoName](../../includes/msconame-md.md)] angezeigt und das Ergebnis der Konfliktlösung kann geändert werden.  
  
 Die Konfliktdaten sind im Replikationskonflikt-Viewer für den Zeitraum verfügbar, der als Beibehaltungsdauer der Konflikte (bei einer Standardeinstellung von 14 Tagen) angegeben wurde. Zum Festlegen der Beibehaltungsdauer der Konflikte haben Sie folgende Möglichkeiten:  
  
-   Geben Sie einen Beibehaltungswert für den Parameter **@conflict_retention** von [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
-   Geben Sie den Wert **conflict_retention** für den **@property**-Parameter und einen Beibehaltungswert für den **@value**-Parameter von [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) an.  
  
 Standardmäßig werden Konfliktinformationen an den folgenden Orten gespeichert:  
  
-   Auf dem Verleger und Abonnenten, wenn die Veröffentlichung mindestens einen Kompatibilitätsgrad von 90RTM aufweist.  
  
-   Auf dem Verleger, wenn die Veröffentlichung einen geringeren Kompatibilitätsgrad als 80RTM aufweist.  
  
-   Auf dem Verleger, wenn auf den Abonnenten [!INCLUDE[ssEW](../../includes/ssew-md.md)]ausgeführt wird. Konfliktdaten dürfen nicht auf Abonnenten mit [!INCLUDE[ssEW](../../includes/ssew-md.md)] gespeichert werden.  
  
 Das Speichern von Konfliktinformationen wird von der **conflict_logging** -Veröffentlichungseigenschaft gesteuert. Weitere Informationen finden Sie unter [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) und [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Konflikte können während der Synchronisierung auch mit dem interaktiven [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Replikationskonfliktlöser gelöst werden. Der interaktive Konfliktlöser ist über die Synchronisierungsverwaltung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows verfügbar. Weitere Informationen finden Sie unter [Synchronisieren eines Abonnements mithilfe der Synchronisierungsverwaltung von Windows &#40;Synchronisierungsverwaltung von Windows&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
### <a name="to-view-and-resolve-conflicts-for-merge-publications"></a>So zeigen Sie Konflikte von Mergeveröffentlichungen an und lösen Sie die Konflikte  
  
1.  Stellen Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger (oder gegebenenfalls Abonnenten) her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Veröffentlichung, für die Sie die Konflikte anzeigen möchten, und klicken Sie dann auf **Konflikte anzeigen**.  
  
    > [!NOTE]  
    >  Wenn für die **conflict_logging** -Eigenschaft der Wert **'subscriber'** angegeben wurde, ist die Menüoption **Konflikte anzeigen** nicht verfügbar. Starten Sie zum Anzeigen von Konflikten ConflictViewer.exe von der Eingabeaufforderung aus. ConflictViewer.exe befindet sich standardmäßig im folgenden Verzeichnis: Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE. Eine Liste der gültigen Startparameter erhalten Sie, wenn Sie ConflictViewer.exe -? ausführen.  
  
4.  Wählen Sie im Dialogfeld **Konflikttabelle auswählen** eine Datenbank, eine Veröffentlichung und eine Tabelle aus, für die Sie die Konflikte anzeigen möchten.  
  
5.  Im Replikationskonflikt-Viewer können Sie folgende Aktionen ausführen:  
  
    -   Filtern Sie Zeilen mit den Schaltflächen rechts vom oberen Raster.  
  
    -   Wählen Sie eine Zeile im oberen Raster aus, um Informationen zur Zeile im unteren Raster anzuzeigen.  
  
    -   Wählen Sie eine oder mehrere Zeilen im oberen Raster aus, und klicken Sie auf **Entfernen**, was dem Klicken auf die Schaltfläche **Gewinner absenden** entspricht (ohne Änderungen an den Daten vorzunehmen).  
  
    -   Klicken Sie auf die Eigenschaftenschaltfläche (**…**), um weitere Informationen zu einer am Konflikt beteiligten Zeile anzuzeigen.  
  
    -   Bearbeiten Sie Daten in den Spalten **Konfliktgewinner** oder **Konfliktverlierer** , bevor Sie die Daten absenden (bei einer grauen Spalte sind die Daten schreibgeschützt).  
  
    -   Klicken Sie auf **Gewinner absenden** , um die als Gewinner des Konflikts ausgewiesene Spalte zu akzeptieren.  
  
    -   Klicken Sie auf **Verlierer absenden** , um die Konfliktlösung zu überschreiben und den als Verlierer des Konflikts ausgewiesenen Wert an alle Knoten der Topologie zu senden.  
  
    -   Aktivieren Sie **Details dieses Konflikts protokollieren** , um Konfliktdaten in einer Datei zu protokollieren. Um einen Speicherort für die Datei anzugeben, zeigen Sie auf das Menü **Ansicht** , und klicken Sie dann auf **Optionen**. Geben Sie einen Wert ein, oder klicken Sie auf die Schaltfläche mit den drei Punkten (**...**), und wechseln Sie in das entsprechende Verzeichnis. Klicken Sie auf **OK** , um das Dialogfeld **Optionen** zu beenden.  
  
6.  Schließen Sie den Replikationskonflikt-Viewer.  
  
## <a name="see-also"></a>Siehe auch  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Angeben eines Mergeartikelkonfliktlösers](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  
