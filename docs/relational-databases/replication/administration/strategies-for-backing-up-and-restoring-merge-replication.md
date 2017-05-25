---
title: Strategien zum Sichern und Wiederherstellen einer Mergereplikation | Microsoft Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- recovery [SQL Server replication], merge replication
- backups [SQL Server replication], merge replication
- restoring [SQL Server replication], merge replication
- merge replication [SQL Server replication], backup and restore
ms.assetid: b8ae31c6-d76f-4dd7-8f46-17d023ca3eca
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b518488e5ac42e28487f984bfd65ca196dfbe723
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="strategies-for-backing-up-and-restoring-merge-replication"></a>Strategien zum Sichern und Wiederherstellen einer Mergereplikation
  Sichern Sie bei Mergereplikationen regelmäßig die folgenden Datenbanken:  
  
-   Veröffentlichungsdatenbank auf dem Verleger  
  
-   Verteilungsdatenbank auf dem Verteiler  
  
-   Abonnementdatenbank auf den einzelnen Abonnenten  
  
-   Die Systemdatenbanken **master** und **msdb** auf dem Verleger, Verteiler und allen Abonnenten. Diese Datenbanken sollten zur selben Zeit wie alle anderen Datenbanken und die entsprechende Replikationsdatenbank gesichert werden. Sichern Sie also z. B. die **master** - und **msdb** -Datenbanken auf dem Verleger immer dann, wenn Sie auch die Veröffentlichungsdatenbank sichern. Beim Wiederherstellen der Veröffentlichungsdatenbank müssen Sie sicherstellen, dass die **master** - und **msdb** -Datenbanken hinsichtlich der Replikationskonfiguration und der Replikationseinstellungen mit der Veröffentlichungsdatenbank übereinstimmen.  
  
 Wenn Sie regelmäßige Protokollsicherungen ausführen, sollten in den Protokollsicherungen auch alle replikationsrelevanten Änderungen erfasst werden. Wenn Sie keine Protokollsicherungen ausführen, sollte immer dann eine Sicherung erfolgen, wenn eine replikationsrelevante Änderung vorgenommen wurde. Weitere Informationen finden Sie unter [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
 Entscheiden Sie sich zum Sichern und Wiederherstellen der Veröffentlichungsdatenbank für eine der unten genannten Herangehensweisen, und befolgen Sie dann die entsprechenden Empfehlungen für die Verteilungsdatenbank und die Abonnementdatenbanken.  
  
## <a name="backing-up-and-restoring-the-publication-database"></a>Sichern und Wiederherstellen der Veröffentlichungsdatenbank  
 Für die Wiederherstellung einer Mergeveröffentlichungs-Datenbank gibt es zwei Herangehensweisen. Nach dem Wiederherstellen der Veröffentlichungsdatenbank aus einer Sicherung müssen Sie sich für eine der folgenden beiden Varianten entscheiden:  
  
-   Synchronisieren der Veröffentlichungsdatenbank mit einer Abonnementdatenbank  
  
-   Erneutes Initialisieren aller Abonnements der Veröffentlichungen in der Veröffentlichungsdatenbank  
  
 Durch die Verwendung dieser Methoden wird sichergestellt, dass nach einer Wiederherstellung der Verleger und alle Abonnenten synchronisiert werden.  
  
> [!NOTE]  
>  Wenn Tabellen Identitätsspalten enthalten, müssen Sie sicherstellen, dass nach einer Wiederherstellung die richtigen Identitätsbereiche zugewiesen werden. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
### <a name="synchronizing-the-publication-database"></a>Synchronisieren der Veröffentlichungsdatenbank  
 Durch das Synchronisieren einer Veröffentlichungsdatenbank mit einer Abonnementdatenbank können Sie aus einer oder mehreren Abonnementdatenbank(en) jene Änderungen hochladen, die zuvor in der Veröffentlichungsdatenbank zwar vorgenommen, aber in der wiederhergestellten Sicherung nicht vorhanden sind. Welche Daten dabei hochgeladen werden können, hängt davon ab, wie die Veröffentlichung gefiltert wird:  
  
-   Wird die Veröffentlichung gar nicht gefiltert, sollten Sie die Veröffentlichungsdatenbank durch Synchronisieren mit einem aktuellen Abonnenten auf den neuesten Stand bringen.  
  
-   Wenn die Veröffentlichung gefiltert ist, können Sie möglicherweise die Veröffentlichungsdatenbank nicht auf den aktuellen Stand bringen. Nehmen wir einmal an, es gibt eine Tabelle, die so partitioniert ist, dass jedes Abonnement nur die Kundendaten für eine der folgenden Verkaufsregionen erhält: Nord, Ost, Süd und West. Wenn für jede Datenpartition mindestens ein Abonnent vorhanden ist, würde es reichen, die Veröffentlichungsdatenbank mit einem Abonnenten für jede Partition zu synchronisieren, um sie auf den neuesten Stand zu bringen. Wenn aber beispielsweise die Daten in der Partition West auf keinen Abonnenten repliziert wurden, können diese Daten auf dem Verleger nicht auf den aktuellen Stand gebracht werden.  
  
> [!IMPORTANT]  
>  Wenn eine Veröffentlichungsdatenbank mit einer Abonnementdatenbank synchronisiert wird, kann es passieren, dass veröffentlichte Tabellen nach dem Wiederherstellen aus der Sicherung einen neueren Stand aufweisen als nicht veröffentlichte Tabellen.  
  
 Wenn Sie die Veröffentlichungsdatenbank mit einem Abonnenten synchronisieren, auf dem eine frühere Version von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] als [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ausgeführt wird, kann das Abonnement nicht anonym sein – es muss sich um ein Clientabonnement oder ein Serverabonnement handeln (in früheren Versionen als lokales Abonnement bzw. globales Abonnement bezeichnet).  
  
 Informationen zum Synchronisieren eines Abonnements finden Sie unter [Synchronisieren eines Pushabonnements](../../../relational-databases/replication/synchronize-a-push-subscription.md) und [Synchronisieren eines Pullabonnements](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
### <a name="reinitializing-all-subscriptions"></a>Erneutes Initialisieren aller Abonnements  
 Durch das erneute Initialisieren aller Abonnements wird sichergestellt, dass alle Abonnenten konsistent mit der wiederhergestellten Veröffentlichungsdatenbank sind. Diese Herangehensweise sollten Sie verwenden, wenn Sie eine ganze Topologie auf den früheren Status zurücksetzen möchten, der in einer bestimmten Sicherung der Veröffentlichungsdatenbank festgehalten ist. So kann es z. B. erforderlich sein, alle Abonnements neu zu initialisieren, wenn Sie nach einer fehlerhaft ausgeführten Batchoperation einen früheren Zustand Ihrer Veröffentlichungsdatenbank wiederherstellen möchten.  
  
 Generieren Sie bei Wahl dieser Option direkt nach dem Wiederherstellen der Veröffentlichungsdatenbank eine neue Momentaufnahme, die an die erneut initialisierten Abonnenten übertragen wird.  
  
 Informationen zum erneuten Initialisieren eines Abonnement finden Sie unter [Erneutes Initialisieren eines Abonnements](../../../relational-databases/replication/reinitialize-a-subscription.md).  
  
 Informationen zum Erstellen und Anwenden einer Momentaufnahme finden Sie unter [Erstellen und Anwenden der Anfangsmomentaufnahme](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md) und [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="backing-up-and-restoring-the-distribution-database"></a>Sichern und Wiederherstellen der Verteilungsdatenbank  
 Bei einer Mergereplikation sollte die Verteilungsdatenbank in regelmäßigen Abständen gesichert werden. Wenn die Sicherung nicht älter als die kürzeste Beibehaltungsdauer aller Veröffentlichungen ist, die den Verteiler verwenden, kann die Verteilungsdatenbank jederzeit problemlos wiederhergestellt werden. Wenn es z. B. drei Veröffentlichungen mit Beibehaltungsdauerwerten von 10, 20 und 30 Tagen gibt, sollte die zum Wiederherstellen der Datenbank verwendete Sicherung höchstens 10 Tage alt sein. Die Verteilungsdatenbank spielt in einer Mergereplikation nur eine begrenzte Rolle: Sie speichert keine Daten, die bei der Änderungsnachverfolgung verwendet werden, und sie bietet auch keine temporäre Speicherung von Mergereplikationsänderungen, die an Abonnementdatenbanken weitergeleitet werden (wie dies bei Transaktionsreplikationen der Fall ist).  
  
## <a name="backing-up-and-restoring-a-subscription-database"></a>Sichern und Wiederherstellen einer Abonnementdatenbank  
 Um die erfolgreiche Wiederherstellung einer Abonnementdatenbank sicherzustellen, sollten die Abonnenten eine Synchronisierung mit dem Verleger vornehmen, bevor die Abonnementdatenbank gesichert wird. Auch nach dem Wiederherstellen der Abonnementdatenbank sollte eine Synchronisierung vorgenommen werden:  
  
-   Durch das Synchronisieren mit dem Verleger vor dem Sichern der Abonnementdatenbank wird sichergestellt, dass sich das Abonnement noch in der Beibehaltungsdauer der Veröffentlichung befindet, wenn der Abonnent wiederhergestellt wird. Nehmen wir beispielsweise an, dass eine Veröffentlichung mit einer Beibehaltungsdauer von 10 Tagen vorliegt. Die letzte Synchronisierung liegt 8 Tage zurück, und jetzt wird die Sicherung ausgeführt. Wenn die Sicherung 4 Tage später wiederhergestellt wird, ist die letzte Synchronisierung 12 Tage her. Dies überschreitet die Beibehaltungsdauer. In diesem Fall müssten Sie den Abonnenten erneut initialisieren. Wenn vor der Sicherung eine Synchronisierung mit dem Abonnenten stattgefunden hätte, würde sich die Abonnementdatenbank noch in der Beibehaltungsdauer befinden.  
  
     Das Alter der Sicherung darf die kürzeste Beibehaltungsdauer aller vom Abonnenten abonnierten Veröffentlichungen nicht überschreiten. Wenn ein Abonnent beispielsweise drei Veröffentlichungen abonniert, deren Beibehaltungsdauerwerte 10, 20 und 30 Tage betragen, sollte die zum Wiederherstellen der Datenbank verwendete Sicherung höchstens 10 Tage alt sein.  
  
-   Durch Synchronisieren der Abonnementdatenbank mit allen ihren Veröffentlichungen nach einer erfolgten Wiederherstellung wird sichergestellt, dass der Abonnent alle Änderungen auf dem Verleger übernehmen kann.  
  
 Weitere Informationen zum Festlegen der Beibehaltungsdauer der Veröffentlichung finden Sie unter [Festlegen des Ablaufdatums für Abonnements](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md).  
  
 Informationen zum Synchronisieren eines Abonnements finden Sie unter [Synchronisieren eines Pushabonnements](../../../relational-databases/replication/synchronize-a-push-subscription.md) und [Synchronisieren eines Pullabonnements](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
## <a name="backing-up-and-restoring-a-republishing-database"></a>Sichern und Wiederherstellen einer Wiederveröffentlichungs-Datenbank  
 Wenn eine Datenbank Daten von einem Verleger abonniert und dieselben Daten selbst auf anderen Abonnementdatenbanken veröffentlicht, wird sie als Wiederveröffentlichungs-Datenbank bezeichnet. Befolgen Sie beim Wiederherstellen einer Wiederveröffentlichungs-Datenbank die in diesem Thema in den Abschnitten zum Sichern und Wiederherstellen einer Veröffentlichungsdatenbank sowie zum Sichern und Wiederherstellen einer Abonnementdatenbank beschriebenen Richtlinien.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Sichern und Wiederherstellen von replizierten Datenbanken](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  
