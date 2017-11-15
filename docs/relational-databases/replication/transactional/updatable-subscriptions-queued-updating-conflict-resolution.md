---
title: "Konflikterkennung und -lösung beim verzögerten Update über eine Warteschlange | Microsoft.Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- viewing queued updating conflicts
- conflict resolution [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
- articles [SQL Server replication], conflict resolution
ms.assetid: 084ac587-25e7-4bd0-a385-556bbe07d02f
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30768bae36208218fc5529c64744abc7e1b12a44
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="updatable-subscriptions---queued-updating-conflict-resolution"></a>Aktualisierbare Abonnements – Konfliktlösungsoptionen für das verzögerte Update über eine Warteschlange
  Da die verzögerte Aktualisierung von Abonnements über eine Warteschlange Änderungen an denselben Daten an mehreren Standorten zulässt, können Konflikte auftreten, wenn die Daten auf dem Verleger synchronisiert werden. Die Replikation erkennt alle Konflikte, wenn Änderungen mit dem Verleger synchronisiert werden, und löst die Konflikte anhand der Richtlinie zur Konfliktlösung, die Sie beim Erstellen der Veröffentlichung ausgewählt haben. Die folgenden Konflikte sind möglich:  
  
-   Update- und Einfügekonflikte. Diese Konflikte treten auf, wenn dieselben Daten an zwei verschiedenen Speicherorten geändert werden. Eine Änderung setzt sich dabei unbeabsichtigt gegen eine andere durch.  
  
-   Löschkonflikte. Diese Konflikte treten auf, wenn dieselbe Zeile an einem Speicherort gelöscht und an einem anderen bearbeitet wird.  
  
 Die Konflikterkennung und -lösung kann ein zeitaufwändiger und ressourcenintensiver Prozess sein. Daher sollten Konflikte in der Anwendung, sofern möglich, minimiert werden, indem Sie Datenpartitionen erstellen, sodass die unterschiedlichen Abonnenten andere Datenteilmengen ändern.  
  
## <a name="detecting-conflicts"></a>Erkennen von Konflikten  
 Beim Erstellen einer Veröffentlichung und beim Aktivieren des verzögerten Updates über eine Warteschlange fügt die Replikation eine **uniqueidentifier** -Spalte (**msrepl_tran_version**) mit dem Standardwert **newid()** der zugrunde liegenden Tabelle hinzu. Werden veröffentlichte Daten auf dem Verleger oder dem Abonnenten geändert, erhält die Zeile einen neuen Globally Unique Identifier (GUID), um anzuzeigen, dass eine neue Zeilenversion vorhanden ist. Der Warteschlangenlese-Agent verwendet diese Spalte während der Synchronisierung, um zu bestimmen, ob ein Konflikt vorhanden ist.  
  
 Eine Transaktion in einer Warteschlange behält die alten und neuen Zeilenversionswerte bei. Wird die Transaktion auf dem Verleger angewendet, werden die GUIDs von der Transaktion und der GUID in der Veröffentlichung verglichen. Wenn der alte in der Transaktion gespeicherte GUID mit dem GUID in der Veröffentlichung übereinstimmt, wird die Veröffentlichung aktualisiert, und der Zeile wird der neue GUID zugewiesen, der vom Abonnenten generiert wurde. Durch Aktualisieren der Veröffentlichung mit dem GUID der Transaktion finden Sie übereinstimmende Zeilenversionen in der Veröffentlichung und der Transaktion.  
  
 Wenn der alte in der Transaktion gespeicherte GUID nicht mit dem GUID in der Veröffentlichung übereinstimmt, wird ein Konflikt erkannt. Der neue GUID in der Veröffentlichung zeigt an, dass zwei verschiedene Zeilenversionen vorhanden sind: eine in der Transaktion, die vom Abonnenten gesendet wird, und eine neuere, die beim Verleger vorhanden ist. In diesem Fall hat ein anderer Abonnent oder der Verleger dieselbe Zeile in der Veröffentlichung aktualisiert, bevor diese Abonnententransaktion synchronisiert wurde.  
  
 Im Gegensatz zur Mergereplikation wird eine GUID-Spalte nicht zur Identifikation der eigentlichen Zeile verwendet, sondern um zu überprüfen, ob sich die Zeile geändert hat.  
  
## <a name="resolving-conflicts"></a>Lösen von Konflikten  
 Beim Erstellen einer Veröffentlichung über ein verzögertes Update wählen Sie einen Konfliktlöser aus, der verwendet werden soll, wenn Konflikte erkannt werden. Durch den Konfliktlöser wird bestimmt, wie der Warteschlangenlese-Agent unterschiedliche Versionen derselben Zeile behandelt, die während der Synchronisierung auftreten. Sie können die Vorgehensweise zur Konfliktlösung nach dem Erstellen der Veröffentlichung ändern, sofern keine Abonnements der Veröffentlichung vorhanden sind. Die Wahlmöglichkeiten für den Konfliktlöser sind Folgende:  
  
-   Verleger gewinnt (Standardeinstellung)  
  
-   Verleger gewinnt, und das Abonnement wird erneut initialisiert  
  
-   Abonnent gewinnt  
  
 Konflikte werden aufgezeichnet und können mithilfe des Konflikt-Viewers angezeigt werden.  
  
 **So legen Sie die Vorgehensweise zur Konfliktlösung für das verzögerte Update über eine Warteschlange fest**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Festlegen der Konfliktlösungsoptionen für verzögerte Updates über eine Warteschlange &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)  
  
-   Replikationsprogrammierung mit Transact-SQL: [Aktivieren des Aktualisierens von Abonnements für Transaktionsveröffentlichungen](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
 **So zeigen Sie Datenkonflikte an**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Anzeigen von Datenkonflikten für Transaktionsveröffentlichungen &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
### <a name="publisher-wins"></a>Verleger gewinnt  
 Wenn die Konfliktlösung auf das Gewinnen des Verlegers festgelegt ist, wird die Transaktionskonsistenz basierend auf den Daten auf dem Verleger beibehalten. Es wird ein Rollback für die konfliktverursachende Transaktion auf dem Abonnenten ausgeführt, der die Transaktion initialisiert hat.  
  
 Der Warteschlangenlese-Agent erkennt einen Konflikt, und kompensierende Befehle werden generiert und an den Abonnenten weitergegeben, indem sie in der Verteilungsdatenbank bereitgestellt werden. Der Verteilungs-Agent wendet die kompensierenden Befehle dann auf den Abonnenten an, von dem die konfliktverursachende Transaktion stammt. Durch die kompensierenden Aktionen werden die Zeilen auf dem Abonnenten so aktualisiert, dass sie mit den Zeilen auf dem Verleger übereinstimmen.  
  
 Bis zum Anwenden der kompensierenden Befehle können die Ergebnisse einer Transaktion gelesen werden, für die schließlich ein Rollback auf dem Abonnenten ausgeführt wird. Dies entspricht einem Dirty Read (Isolationsstufe Read uncommitted). Eine Kompensation für die nachfolgenden abhängigen Transaktionen, die auftreten können, ist nicht vorhanden. Die Transaktionsgrenzen werden jedoch berücksichtigt, und für alle Aktionen in einer Transaktion wird ein Commit oder bei einem Konflikt ein Rollback ausgeführt.  
  
### <a name="publisher-wins-and-the-subscription-is-reinitialized"></a>Verleger gewinnt, und das Abonnement wird erneut initialisiert  
 Das erneute Initialisieren des Abonnenten zur Konfliktlösung behält eine strenge Transaktionskonsistenz auf dem Abonnenten bei, kann jedoch zeitaufwändig sein, wenn die Veröffentlichung viele Daten enthält.  
  
 Erkennt der Warteschlangenlese-Agent einen Konflikt, werden alle restlichen Transaktionen in der Warteschlange (einschließlich der Transaktion mit dem Konflikt) zurückgewiesen, und der Abonnent wird zur erneuten Initialisierung markiert. Die nächste Momentaufnahme, die für die Veröffentlichung generiert wird, wird vom Verteilungs-Agent auf den Abonnenten angewendet.  
  
### <a name="subscriber-wins"></a>Abonnent gewinnt  
 Die Konflikterkennung unter der Richtlinie Abonnent gewinnt bedeutet, dass die letzte Abonnententransaktion gewinnt, die den Verleger aktualisiert. Wird ein Konflikt erkannt, wird in diesem Fall die vom Abonnenten gesendete Transaktion weiterhin verwendet, und der Verleger wird aktualisiert. Diese Vorgehensweise eignet sich für Anwendungen, in denen die Datenintegrität durch diese Änderungen nicht gefährdet wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
