---
title: Replikationskonflikt-Viewer von Microsoft (Transaktionsreplikation) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.replconflictviewer.cvqueued.f1
ms.assetid: eec59d8e-cadb-4623-a31f-9f42ec09c97f
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8ee6e349e5627a169d38ece1d90a9b68ebca6593
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="microsoft-replication-conflict-viewer-transactional-replication"></a>Replikationskonflikt-Viewer von Microsoft (Transaktionsreplikation)
  Mit dem Replikationskonflikt-Viewer können Sie Konflikte anzeigen, die bei der Synchronisierung für die Peer-zu-Peer-Transaktionsreplikation und die Transaktionsreplikation mit Abonnements mit verzögertem Update über eine Warteschlange aufgetreten sind. Weitere Informationen finden Sie unter [Anzeigen von Datenkonflikten für Transaktionsveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md).  
  
> [!NOTE]  
>  Der Replikationskonflikt-Viewer zeigt Konflikte an, die bei der Mergereplikation und der Transaktionsreplikation auftreten. Bei der Transaktionsreplikation können Sie den Replikationskonflikt-Viewer verwenden, um Konfliktdaten anzuzeigen, aber Sie können keine andere Lösung für den Konflikt auswählen.  
  
## <a name="options"></a>Optionen  
 Der Replikationskonflikt-Viewer ist in zwei Abschnitte unterteilt. Der obere Abschnitt des Dialogfelds zeigt die Konfliktliste für die ausgewählte Tabelle. Wenn Sie auf ein Element in der Konfliktliste klicken, werden die Details des Konflikts im unteren Abschnitt des Dialogfelds angezeigt.  
  
 Die Konfliktdaten im unteren Abschnitt werden in zwei entsprechenden Spalten angezeigt (**Konfliktgewinner** und **Konfliktverlierer**). Wenn ein Konflikt zwischen aktualisierten und gelöschten Daten vorhanden ist, können möglicherweise keine Daten für die gelöschte Seite des Konflikts angezeigt werden. In diesem Fall zeigt der Replikationskonflikt-Viewer eine Meldung in einer der beiden Spalten an, die die Zeile angibt, die an einem Speicherort gelöscht und an einem anderen aktualisiert wurde. Sie gibt außerdem die vorgeschlagene Lösung an.  
  
 **Datenbank**  
 Wählen Sie eine Datenbank aus, die Veröffentlichungen mit Konflikten enthält.  
  
 **Veröffentlichung**  
 Wählen Sie eine Veröffentlichung aus, die Tabellen mit Konflikten enthält.  
  
 **Tabelle**  
 Wählen Sie eine Tabelle aus, die Konflikte enthält.  
  
 **Filter definieren**  
 Klicken Sie auf diese Option, um das Dialogfeld **Filter definieren** zu öffnen.  
  
 **Filter anwenden oder entfernen**  
 Klicken Sie auf diese Option, um einen Filter anzuwenden oder zu entfernen, der im Dialogfeld **Filter definieren** definiert wurde.  
  
 **Alles auswählen**  
 Wählt alle Konflikte aus, die im Raster aufgeführt sind.  
  
 **Keine auswählen**  
 Macht die Auswahl für alle Konflikte rückgängig, die im Raster aufgeführt sind.  
  
 **Entfernen**  
 Entfernt die ausgewählten Konflikte aus dem Viewer und die zugeordneten Metadaten aus den Replikationssystemtabellen.  
  
 **Alle Spalten anzeigen**  
 Zeigt alle Spalten der Tabelle an.  
  
 **Die ersten fünf Spalten und Spalten mit Konfliktdaten anzeigen**  
 Zeigt die ersten fünf Spalten und alle Spalten mit Konflikten an. Diese Option ist hilfreich, wenn die Tabelle über eine große Anzahl von Spalten verfügt, Sie aber nur diejenigen anzeigen möchten, die für die Konfliktlösung am wichtigsten sind. Die ersten fünf Spalten sind in diese Sicht immer einbezogen, da Felder zum Kennzeichnen einer Zeile, z. B. der Primärschlüssel oder Namensfelder, sich oft in den ersten Spalten einer Tabelle befinden.  
  
 **Spalteninformationen anzeigen** (**…**)  
 Zeigt die Spalteninformationen an: **Tabellenname**, **Spaltenname**, **Datentyp**und **Spaltenwert**.  
  
 **Details dieses Konflikts protokollieren**  
 Aktivieren Sie dieses Kontrollkästchen, um die Details eines Konflikts in eine Datei zu speichern. Zeigen Sie auf das Menü **Ansicht** , und klicken Sie auf **Optionen**, um einen Speicherort für die Datei anzugeben. Geben Sie einen Wert ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), und navigieren Sie zur entsprechenden Datei. Klicken Sie auf **OK** , um das Dialogfeld **Optionen** zu beenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Konflikterkennung bei der Peer-zu-Peer-Replikation](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [Anzeigen von Datenkonflikten für Transaktionsveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
  
