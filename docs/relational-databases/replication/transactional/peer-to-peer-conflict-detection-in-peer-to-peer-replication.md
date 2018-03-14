---
title: Konflikterkennung bei der Peer-zu-Peer-Replikation |Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
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
helpviewer_keywords:
- transactional replication, peer-to-peer replication
- peer-to-peer transactional replication, conflict detection
ms.assetid: 754a1070-59bc-438d-998b-97fdd77d45ca
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1df7460cea4142e8f64f956a8b8dde852c47a165
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="peer-to-peer---conflict-detection-in-peer-to-peer-replication"></a>Peer-zu-Peer - Konflikterkennung bei der Peer-zu-Peer-Replikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Bei der Peer-zu-Peer-Transaktionsreplikation können Sie an einem beliebigen Knoten in der Topologie Daten einfügen, aktualisieren oder löschen, und Datenänderungen können an andere Knoten übermittelt werden. Da Sie Daten an einem beliebigen Knoten ändern können, können Datenänderungen an verschiedenen Knoten untereinander in Konflikt stehen. Wird eine Zeile an mehr als einem Knoten geändert, kann es zu einem Konflikt kommen, oder das Update kann sogar verloren gehen, wenn die Zeile an andere Knoten übermittelt wird.  
  
 Die Peer-zu-Peer-Replikation in [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] und neueren Versionen bietet die Option, die Konflikterkennung für eine gesamte Peer-zu-Peer-Topologie zu aktivieren. Mithilfe dieser Option kann Problemen vorgebeugt werden, die durch nicht erkannte Konflikte, einschließlich inkonsistentem Verhalten von Anwendungen und verlorenen Updates, entstehen. Standardmäßig wird, wenn diese Option aktiviert ist, eine konfliktverursachende Änderung als ein schwerwiegender Fehler betrachtet, der zu einem Fehler des Verteilungs-Agents führt. Bei einem Konflikt verbleibt die Topologie so lange in einem inkonsistenten Zustand, bis der Konflikt gelöst und die Datenkonsistenz in der Topologie wiederhergestellt wurde.  
  
> [!NOTE]  
>  Stellen Sie, um inkonsistente Daten zu vermeiden, in einer Peer-zu-Peer-Topologie sicher, dass keine Konflikte auftreten, auch wenn die Konflikterkennung aktiviert ist. Damit sichergestellt ist, dass Schreibvorgänge für eine bestimmte Zeile nur an einem Knoten durchgeführt werden, müssen Anwendungen, die auf Daten zugreifen und diese ändern, Einfügungen, Updates und Löschungen partitionieren. Diese Partitionierung gewährleistet, dass Änderungen an einer bestimmten Zeile, die von einem Knoten stammt, mit allen anderen Knoten in der Topologie synchronisiert werden, bevor die Zeile von einem anderen Knoten geändert wird. Wenn eine Anwendung ausgereifte Fähigkeiten zur Konflikterkennung und -lösung erfordert, verwenden Sie die Mergereplikation. Weitere Informationen finden Sie unter [Merge Replication](../../../relational-databases/replication/merge/merge-replication.md) und [Resolve Merge Replication Conflicts](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md).  
  
## <a name="understanding-conflicts-and-conflict-detection"></a>Grundlegendes zu Konflikten und der Konflikterkennung  
 In einer einzelnen Datenbank verursachen Änderungen, die von verschiedenen Anwendungen an derselben Zeile vorgenommen werden, keinen Konflikt. Der Grund dafür ist, dass Transaktionen serialisiert und gleichzeitige Änderungen mithilfe von Sperren behandelt werden. In einem asynchronen verteilten System wie der Peer-zu-Peer-Replikation agieren Transaktionen unabhängig voneinander auf jedem Knoten, und es gibt keinen Mechanismus dafür, Transaktionen über mehrere Knoten zu serialisieren. Ein Protokoll wie Zweiphasencommit könnte verwendet werden, aber dies hat deutliche Auswirkungen auf die Leistung.  
  
 In Systemen wie der Peer-zu-Peer-Replikation werden Konflikte nicht erkannt, wenn für Änderungen ein Commit auf einzelnen Peers ausgeführt wird. Sie werden erst erkannt, wenn diese Änderungen repliziert und auf anderen Peers übernommen werden. Bei der Peer-zu-Peer-Replikation werden Konflikte von den gespeicherten Prozeduren erkannt, die Änderungen an jedem Knoten übernehmen, und zwar basierend auf einer ausgeblendeten Spalte in jeder veröffentlichten Tabelle. In dieser ausgeblendeten Spalte ist eine ID gespeichert, die eine *Absender-ID* , die Sie für jeden Knoten angeben, mit der Version der Zeile kombiniert. Während der Synchronisierung führt der Verteilungs-Agent Prozeduren für jede Tabelle aus. Diese Prozeduren übernehmen Einfüge-, Update- und Löschvorgänge von anderen Peers. Wenn eine der Prozeduren beim Lesen des Werts der ausgeblendeten Spalte einen Konflikt erkennt, wird Fehler 22815 mit einem Schweregrad von 16 ausgelöst:  
  
 `A conflict of type '%s' was detected at peer %d between peer %d (incoming), transaction id %s  and peer %d (on disk), transaction id %s`  
  
 Standardmäßig führt dieser Fehler dazu, dass der Verteilungs-Agent das Übernehmen von Änderungen für diesen Knoten beendet. Informationen zum Behandeln der erkannten Konflikte finden Sie unter "Konfliktbehandlung" weiter unten in diesem Thema.  
  
> [!NOTE]  
>  Der Zugriff auf die ausgeblendete Spalte ist nur durch einen Benutzer möglich, der sich über die dedizierte Administratorverbindung (DAC) angemeldet hat. Weitere Informationen zu DAC finden Sie unter [Diagnoseverbindung für Datenbankadministratoren](../../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
 Die Peer-zu-Peer-Replikation erkennt die folgenden Typen von Konflikten:  
  
-   Insert-insert  
  
     Alle Zeilen in einer Tabelle, die an der Peer-zu-Peer-Replikation beteiligt sind, werden mithilfe von Primärschlüsselwerten eindeutig identifiziert. Ein Konflikt vom Typ "insert-insert" tritt auf, wenn eine Zeile mit demselben Schlüsselwert an mehreren Knoten eingefügt wurde.  
  
-   Update-update  
  
     Tritt auf, wenn eine Zeile an mehreren Knoten aktualisiert wurde.  
  
-   Insert-update  
  
     Tritt auf, wenn eine Zeile an einem Knoten aktualisiert wurde, diese Zeile aber gelöscht und dann an einem anderen Knoten erneut eingefügt wurde.  
  
-   Insert-delete  
  
     Tritt auf, wenn eine Zeile an einem Knoten gelöscht wurde, diese Zeile aber gelöscht und dann an einem anderen Knoten erneut eingefügt wurde.  
  
-   Update-delete  
  
     Tritt auf, wenn eine Zeile an einem Knoten aktualisiert wurde, diese Zeile aber an einem anderen Knoten gelöscht wurde.  
  
-   Delete-delete  
  
     Tritt auf, wenn eine Zeile an mehreren Knoten gelöscht wurde.  
  
## <a name="enabling-conflict-detection"></a>Aktivieren der Konflikterkennung  
 Zur Verwendung der Konflikterkennung muss auf allen Knoten [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] oder eine höhere Version ausgeführt werden, und die Erkennung muss für alle Knoten aktiviert sein. In [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] und höheren Versionen ist die Konflikterkennung in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]standardmäßig aktiviert. Es wird empfohlen, die Konflikterkennung auch in Szenarien zu aktivieren, in denen Sie keine Konflikte erwarten. Die Konflikterkennung kann in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] oder mithilfe der gespeicherten Prozeduren in [!INCLUDE[tsql](../../../includes/tsql-md.md)] aktiviert und deaktiviert werden:  
  
-   Sie können die Konflikterkennung in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] entweder auf der Seite **Abonnementoptionen** im Dialogfeld **Veröffentlichungseigenschaften** oder auf der Seite **Topologie konfigurieren** des Assistenten zum Konfigurieren der Peer-zu-Peer-Topologie aktivieren und deaktivieren. Weitere Informationen finden Sie unter [Conflict Detection in Peer-to-Peer Replication](../../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
     Wenn Sie die Konflikterkennung mithilfe von [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]konfigurieren, wird der Verteilungs-Agent so konfiguriert, dass er bei Erkennung eines Konflikts das Übernehmen von Änderungen beendet.  
  
-   Sie können die Konflikterkennung auch mithilfe der folgenden gespeicherten Prozeduren aktivieren und deaktivieren: [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) oder [sp_configure_peerconflictdetection](../../../relational-databases/system-stored-procedures/sp-configure-peerconflictdetection-transact-sql.md).  
  
     Wenn Sie die Konflikterkennung mithilfe gespeicherter Prozeduren konfigurieren, können Sie angeben, ob der Verteilungs-Agent bei Erkennung eines Konflikts das Übernehmen von Änderungen beenden soll. Standardmäßig beendet der Agent diese Aufgabe. Es wird empfohlen, die Standardeinstellung zu verwenden.  
  
## <a name="handling-conflicts"></a>Konfliktbehandlung  
 Wenn ein Konflikt in der Peer-zu-Peer-Replikation auftritt, wird die Peer-zu-Peer Konflikterkennungswarnung ausgelöst. Es wird empfohlen, diese Warnung so zu konfigurieren, dass Sie benachrichtigt werden, wenn ein Konflikt auftritt. Weitere Informationen über Warnungen finden Sie unter [Verwenden von Warnungen für Replikations-Agentereignisse](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
 Verwenden Sie eine der folgenden Vorgehensweisen, um den aufgetretenen Konflikt zu behandeln, nachdem der Verteilungs-Agent beendet und die Warnung ausgelöst wurde:  
  
-   Initialisieren Sie den Knoten, an dem der Konflikt erkannt wurde, erneut aus der Sicherung eines Knotens, der die erforderlichen Daten aufweist (empfohlene Vorgehensweise). Mithilfe dieser Methode wird sichergestellt, dass sich die Daten in einem konsistenten Status befinden.  
  
-   Versuchen Sie, den Knoten wieder zu synchronisieren, indem Sie den Verteilungs-Agent aktivieren, damit dieser das Übernehmen von Änderungen fortsetzt:  
  
    1.  Führen Sie [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) aus: Geben Sie 'p2p_continue_onconflict' für den @property-Parameter und **true** für den @value-Parameter an.  
  
    2.  Starten Sie den Verteilungs-Agent neu.  
  
    3.  Überprüfen Sie die erkannten Konflikte im Konflikt-Viewer, und bestimmen Sie die beteiligten Zeilen, den Konflikttyp und den Gewinner. Der Konflikt wird anhand des Werts der Absender-ID aufgelöst, den Sie während der Konfiguration angegeben haben: Die Zeile, die von dem Knoten mit der höchsten ID stammt, gewinnt den Konflikt. Weitere Informationen finden Sie unter [Anzeigen von Datenkonflikten für Transaktionsveröffentlichungen &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md).  
  
    4.  Führen Sie eine Überprüfung aus, um sicherzustellen, dass die miteinander in Konflikt stehenden Zeilen ordnungsgemäß konvergiert wurden. Weitere Informationen finden Sie unter [Validate Replicated Data](../../../relational-databases/replication/validate-replicated-data.md).  
  
        > [!NOTE]  
        >  Wenn die Daten nach Ausführung dieses Schritts inkonsistent sind, müssen Sie die Zeilen auf dem Knoten mit der höchsten Priorität manuell aktualisieren und dann die Änderungen von diesem Knoten übertragen. Wenn die Topologie keine weiteren miteinander in Konflikt stehenden Änderungen aufweist, werden alle Knoten in einen konsistenten Status gebracht.  
  
    5.  Führen Sie [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) aus: Geben Sie 'p2p_continue_onconflict' für den @property-Parameter und **false** für den @value-Parameter an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
