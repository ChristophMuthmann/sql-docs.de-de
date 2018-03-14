---
title: Replikationskonflikt-Viewer von Microsoft (Mergereplikation) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.replconflictviewer.cvmerge.f1
ms.assetid: bfef5e21-ac04-4bc5-a55e-595421e34923
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4fbbfbe441da04c73f39e653fc9b12a6169eaea3
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="microsoft-replication-conflict-viewer-merge-replication"></a>Replikationskonflikt-Viewer von Microsoft (Mergereplikation)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Der Replikationskonflikt-Viewer ermöglicht die Anzeige aller Konflikte, die während der Replikationssynchronisierung auftreten. Konflikte treten auf, wenn dieselben Daten auf zwei verschiedenen Servern bearbeitet werden, z. B. auf einem Verleger und einem Abonnenten, oder aber auf zwei verschiedenen Abonnenten. Die Replikation löst Konflikte automatisch mithilfe des Konfliktlösers, der beim Erstellen des Artikels ausgewählt wurde. Der Replikationskonflikt-Viewer ermöglicht es Ihnen aber auch, ggf. eine andere Lösung für den Konflikt zu wählen. Die folgenden Konflikte sind möglich:  
  
-   Updatekonflikte. Updatekonflikte treten auf, wenn dieselben Daten an zwei verschiedenen Speicherorten geändert werden. Eine Änderung setzt sich dabei unbeabsichtigt gegen eine andere durch. Sie haben die Möglichkeit, die vorhandenen Daten (die Daten, die gewonnen haben) beizubehalten, die vorhandenen Daten mit den Daten zu überschreiben, die einen Konflikt mit ihnen ausgelöst haben (die Daten, die verloren haben) oder die Daten zusammenzuführen (die Daten, die gewonnen haben, und die, die verloren haben) und die vorhandenen Daten zu aktualisieren.  
  
-   Einfügekonflikte. Einfügekonflikte treten auf, wenn eine Zeile an einem Speicherort eingefügt wird, an dem sie beim Zusammenführen mit Änderungen an anderen Speicherorten Datenkonsistenzregeln verletzt. Sie haben die Möglichkeit, die vorhandenen Daten (die Daten, die gewonnen haben) beizubehalten, die vorhandenen Daten mit den Daten zu überschreiben, die einen Konflikt mit ihnen ausgelöst haben (die Daten, die verloren haben) oder die Daten zusammenzuführen (die Daten, die gewonnen haben, und die, die verloren haben) und die vorhandenen Daten zu aktualisieren.  
  
-   Löschkonflikte. Diese Konflikte treten auf, wenn dieselbe Zeile an einem Speicherort gelöscht und an einem anderen bearbeitet wird.  
  
 Wenn Konflikte während der Synchronisierung gelöst werden, werden die Daten aus der verlierenden Zeile in eine Konflikttabelle geschrieben. Unabhängig davon, ob Sie die ursprüngliche Lösung akzeptieren oder eine andere Lösung für den Konflikt wählen, wird die protokollierte Konfliktzeile aus der Konflikttabelle gelöscht. Sie sollten deshalb in regelmäßigen Abständen Konflikte überprüfen, um die Größe der Konfliktnachverfolgungstabellen zu verringern.  
  
> [!NOTE]  
>  Konflikte, die logische Datensätze einschließen, werden im Konflikt-Viewer nicht angezeigt. Mit den gespeicherten Replikationsprozeduren können Informationen zu diesen Konflikten angezeigt werden. Weitere Informationen finden Sie unter [Anzeigen von Konfliktinformationen zu Mergeveröffentlichungen &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
## <a name="options"></a>Tastatur  
 Der Replikationskonflikt-Viewer ist in zwei Abschnitte unterteilt. Der obere Abschnitt des Dialogfelds zeigt die Konfliktliste für die ausgewählte Tabelle. Wenn Sie auf ein Element in der Konfliktliste klicken, werden die Details des Konflikts im unteren Abschnitt des Dialogfelds angezeigt.  
  
 Informationen zur Ursache des Konflikts (dieselbe Zeile wurde z. B. auf dem Verleger und auf dem Abonnenten aktualisiert) werden im unteren Abschnitt des Dialogfelds angezeigt. Die Konfliktdaten im unteren Abschnitt werden in zwei entsprechenden Spalten angezeigt (**Konfliktgewinner** und **Konfliktverlierer**). Wenn ein Konflikt zwischen aktualisierten und gelöschten Daten vorhanden ist, können möglicherweise keine Daten für die gelöschte Seite des Konflikts angezeigt werden. In diesem Fall zeigt der Replikationskonflikt-Viewer eine Meldung in einer der beiden Spalten an, die anzeigt, dass die Zeile an einem Speicherort gelöscht und an einem anderen aktualisiert wurde. Sie gibt außerdem die vorgeschlagene Lösung an.  
  
 Daten, die nicht im Replikationskonflikt-Viewer bearbeitet werden können (z. B. **rowguid** -Daten) werden schreibgeschützt in einem schattierten Feld angezeigt.  
  
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
 Entfernt die ausgewählten Konflikte aus dem Viewer und die zugeordneten Metadaten aus den Replikationssystemtabellen. Gleichbedeutend mit dem Klicken auf die Schaltfläche Gewinner absenden (ohne an den Daten Änderungen vorzunehmen) für jeden ausgewählten Konflikt.  
  
 **Alle Spalten anzeigen**  
 Zeigt alle Spalten der Tabelle an.  
  
 **Die ersten fünf Spalten und Spalten mit Konfliktdaten anzeigen**  
 Zeigt die ersten fünf Spalten und alle Spalten mit Konflikten an. Diese Option ist hilfreich, wenn die Tabelle über eine große Anzahl von Spalten verfügt, Sie aber nur diejenigen anzeigen möchten, die für die Konfliktlösung am wichtigsten sind. Die ersten fünf Spalten sind in diese Sicht immer einbezogen, da Felder zum Kennzeichnen einer Zeile, z. B. der Primärschlüssel oder Namensfelder, sich oft in den ersten Spalten einer Tabelle befinden.  
  
 **Spalteninformationen anzeigen** (**…**)  
 Zeigt die Spalteninformationen an: **Tabellenname**, **Spaltenname**, **Datentyp**und **Spaltenwert**. **Spaltenwert** kann bearbeitet werden, sofern der Wert nicht als schreibgeschützt angezeigt wird.  
  
 **Gewinner absenden**  
 Klicken Sie auf diese Option, um die Zeile beizubehalten, die vom Konfliktlöser als Gewinner bestimmt wurde. Der Wert jeder nicht als schreibgeschützt angezeigten Spalte kann vor dem Klicken auf diese Schaltfläche geändert werden.  
  
 **Verlierer absenden**  
 Klicken Sie auf diese Option, um die Zeile zu akzeptieren, die vom Konfliktlöser als Verlierer bestimmt wurde. Der Wert jeder nicht als schreibgeschützt angezeigten Spalte kann vor dem Klicken auf diese Schaltfläche geändert werden.  
  
 **Details dieses Konflikts protokollieren**  
 Aktivieren Sie dieses Kontrollkästchen, um die Details eines Konflikts in eine Datei zu speichern. Zeigen Sie auf das Menü **Ansicht** , und klicken Sie auf **Optionen**, um einen Speicherort für die Datei anzugeben. Geben Sie einen Wert ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), und navigieren Sie zur entsprechenden Datei. Klicken Sie auf **OK** , um das Dialogfeld **Optionen** zu beenden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anzeigen und Lösen von Datenkonflikten für Mergeveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Advanced Merge Replication Conflict Detection and Resolution (Erweiterte Konflikterkennung und -lösung bei der Mergereplikation)](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
