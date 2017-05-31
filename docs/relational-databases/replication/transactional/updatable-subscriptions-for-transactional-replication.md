---
title: "Aktualisierbare Abonnements für die Transaktionsreplikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, about updatable subscriptions
- queued updating subscriptions [SQL Server replication]
- immediate updating subscriptions
- subscriptions [SQL Server replication], updatable
- updatable subscriptions
ms.assetid: 8eec95cb-3a11-436e-bcee-bdcd05aa5c5a
caps.latest.revision: 60
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a0ab23e21b8bc503336fe9e10a715fb0da623d2a
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="updatable-subscriptions---for-transactional-replication"></a>Aktualisierbare Abonnements – Für die Transaktionsreplikation
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  Dieses Feature wird in den Versionen von [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] von 2012 bis 2016 weiterhin unterstützt. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Die Transaktionsreplikation unterstützt Updates auf den Abonnenten über aktualisierbare Abonnements und Peer-zu-Peer-Replikation. Es gibt zwei Arten von aktualisierbaren Abonnements:  
  
-   Sofortiges Aktualisieren. Verleger und Abonnent müssen verbunden sein, damit Daten auf dem Abonnenten aktualisiert werden können.  
  
-   Verzögertes Aktualisieren über eine Warteschlange. Verleger und Abonnent müssen nicht verbunden sein, damit Daten auf dem Abonnenten aktualisiert werden können. Updates können ausgeführt werden, während der Verleger oder der Abonnent offline ist.  
  
 Wenn Daten auf einem Abonnenten aktualisiert werden, werden sie zuerst an den Verleger und dann an andere Abonnenten weitergegeben. Beim sofortigen Aktualisieren werden die Änderungen sofort mithilfe des Zweiphasencommit-Protokolls weitergegeben. Beim verzögerten Aktualisieren über eine Warteschlange werden die Änderungen in einer Warteschlange gespeichert und dann immer, wenn eine Netzwerkverbindung verfügbar ist, asynchron auf dem Verleger angewendet. Da die Updates asynchron an den Verleger weitergegeben werden, wurden die gleichen Daten möglicherweise vom Verleger oder von einem anderen Abonnenten aktualisiert. Daher können Konflikte auftreten, wenn die Updates angewendet werden. Konflikte werden nach einer Vorgehensweise zur Konfliktlösung erkannt und gelöst, die beim Erstellen der Veröffentlichung festgelegt wird.  
  
 Wenn Sie im Assistenten für neue Veröffentlichung eine Transaktionsveröffentlichung mit aktualisierbaren Abonnements erstellen, werden sowohl das sofortige Aktualisieren als auch das verzögerte Aktualisieren über eine Warteschlange aktiviert. Beim Erstellen einer Veröffentlichung mit gespeicherten Prozeduren können Sie eine oder beide Optionen aktivieren. Wenn Sie ein Abonnement für die Veröffentlichung erstellen, geben Sie an, welcher Updatemodus verwendet wird. Sie können dann gegebenenfalls den Updatemodus wechseln. Weitere Informationen finden Sie im folgenden Abschnitt zum Wechseln des Updatemodus.  
  
 Informationen zum Aktivieren aktualisierbarer Abonnements für Transaktionsveröffentlichungen finden Sie unter [Enable Updating Subscriptions for Transactional Publications](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).  
  
 Informationen zum Erstellen aktualisierbarer Abonnements für Transaktionsveröffentlichungen finden Sie unter [Erstellen eines aktualisierbaren Abonnements für eine Transaktionsveröffentlichung (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md). 
  
## <a name="switching-between-update-modes"></a>Wechseln des Updatemodus  
 Bei der Verwendung aktualisierbarer Abonnements können Sie den Updatemodus für ein Abonnement angeben und dann bei Bedarf in den anderen Modus wechseln. Sie können z. B. angeben, dass das sofortige Aktualisieren für ein Abonnement verwendet wird. Wenn dann jedoch die Netzwerkverbindung aufgrund eines Systemfehlers unterbrochen wird, können Sie auf das verzögerte Aktualisieren über eine Warteschlange wechseln.  
  
> [!NOTE]  
>  Bei der Replikation erfolgt kein automatischer Wechsel zwischen den Updatemodi. Sie müssen den Updatemodus über SQL Server Management Studio festlegen, oder die Anwendung muss für einen Moduswechsel [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md) aufrufen.  
  
 Wenn Sie vom sofortigen Aktualisieren zum verzögerten Aktualisieren über eine Warteschlange wechseln, können Sie erst wieder zum sofortigen Aktualisieren wechseln, wenn der Abonnent und der Verleger verbunden sind und der Warteschlangenlese-Agent alle ausstehenden Nachrichten in der Warteschlange auf den Verleger angewendet hat.  
  
 **So wechseln Sie den Updatemodus**  
  
 Zum Wechseln des Updatemodus müssen Sie die Veröffentlichung und das Abonnement für beide Modi aktivieren und zwischen beiden nach Bedarf wechseln. Weitere Informationen finden Sie unter  
[Switch Between Update Modes for an Updatable Transactional Subscription](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).  
  
### <a name="considerations-for-using-updatable-subscriptions"></a>Überlegungen zur Verwendung von aktualisierbaren Abonnements  
  
-   Nachdem eine Veröffentlichung für Abonnements mit sofortigem Update oder Abonnements mit verzögertem Update über eine Warteschlange aktiviert wurde, kann die Option nicht für die Veröffentlichung deaktiviert werden (obwohl die Abonnements sie nicht verwenden müssen). Zum Deaktivieren der Option muss die Veröffentlichung gelöscht und dann eine neue Veröffentlichung erstellt werden.  
  
-   Das erneute Veröffentlichen von Daten wird nicht unterstützt.  
  
-   Bei der Replikation wird die **msrepl_tran_version** -Spalte veröffentlichten Tabellen für das Nachverfolgen hinzugefügt. Wegen dieser zusätzlichen Spalte sollten alle **INSERT** -Anweisungen eine Spaltenliste enthalten.  
  
-   Wenn Sie das Schema einer Tabelle in einer Veröffentlichung ändern möchten, die das Aktualisieren von Abonnements unterstützt, müssen alle Aktivitäten an der Tabelle auf dem Verleger und dem Abonnenten angehalten werden. Außerdem müssen ausstehende Datenänderungen vor einer Schemaänderung an alle Knoten weitergegeben werden. Dadurch wird sichergestellt, dass unbeendete Transaktionen keinen Konflikt mit der ausstehenden Schemaänderung auslösen. Nach der Weitergabe der Schemaänderungen an alle Knoten können die Aktivitäten an den veröffentlichten Tabellen fortgesetzt werden. Weitere Informationen finden Sie unter [Versetzen einer Replikationstopologie in einen inaktiven Status &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
-   Wenn Sie den Updatemodus wechseln möchten, muss der Warteschlangenlese-Agent nach der Initialisierung des Abonnements mindestens einmal ausgeführt werden (standardmäßig wird der Warteschlangenlese-Agent fortlaufend ausgeführt).  
  
-   Ist die Abonnentendatenbank horizontal partitioniert und die Partition enthält Zeilen, die auf dem Abonnenten, aber nicht auf dem Verleger vorhanden sind, kann der Abonnent die bereits vorhandenen Zeilen nicht aktualisieren. Bei dem Versuch, diese Zeilen zu aktualisieren, wird ein Fehler zurückgegeben. Die Zeilen sollten aus der Tabelle gelöscht und dann auf dem Verleger hinzugefügt werden.  

-   Transaktionsreplikation mit aktualisierbaren Abonnenten in der Warteschlange kann die Leistung beeinträchtigen, wenn eindeutige, gefilterte Indizes verwendet werden. Wenn ein Konflikt bei einem Artikel mit eindeutig gefilterten Indizes auftritt, führt die Konfliktlösung zu zusätzlichen Löschvorgängen und Einfügungen im Abonnenten für die Zeilen, die nicht vom eindeutig gefilterten Index abgedeckt werden.
  
### <a name="updates-at-the-subscriber"></a>Updates auf dem Abonnenten  
  
-   Updates auf dem Abonnenten werden auch dann an den Verleger weitergegeben, wenn ein Abonnement abgelaufen oder inaktiv ist. Stellen Sie sicher, dass Abonnements dieser Art gelöscht oder erneut initialisiert werden.  
  
-   Wenn die Spalten **TIMESTAMP** oder **IDENTITY** verwendet und als Basisdatentypen repliziert werden, sollten die Werte in diesen Spalten nicht auf dem Abonnenten aktualisiert werden.  
  
-   Abonnenten können keine **text**-, **ntext** - oder **image** -Werte aktualisieren oder einfügen, da das Lesen eingefügter oder gelöschter Tabellen innerhalb der Änderungsprotokollierungstrigger der Replikation nicht möglich ist. Ebenso können Abonnenten keine **text** - oder **image** -Werte mithilfe von **WRITETEXT** oder **UPDATETEXT** aktualisieren oder einfügen, da die Daten vom Verleger überschrieben werden. Stattdessen können Sie die **text** - und **image** -Spalten in eine separate Tabelle partitionieren und die beiden Tabellen in einer Transaktion ändern.  
  
     Verwenden Sie zum Aktualisieren großer Objekte für einen Abonnenten die Datentypen **varchar(max)**, **nvarchar(max)**, **varbinary(max)** anstelle der Datentypen **text**, **ntext**, und **image** .  
  
-   Updates an eindeutigen Schlüsseln (einschließlich Primärschlüssel), die Duplikate generieren (z. B. ein Update der Form `UPDATE <column> SET <column> =<column>+1` ), sind nicht zulässig und werden aufgrund eines Verstoßes gegen die Eindeutigkeit abgelehnt. Dies ist darin begründet, dass Updates von Zeilengruppen auf dem Abonnenten durch die Replikation als einzelne **UPDATE** -Anweisungen für jede betroffene Zeile weitergegeben werden.  
  
-   Ist die Abonnentendatenbank horizontal partitioniert und die Partition enthält Zeilen, die auf dem Abonnenten, aber nicht auf dem Verleger vorhanden sind, kann der Abonnent die bereits vorhandenen Zeilen nicht aktualisieren. Bei dem Versuch, diese Zeilen zu aktualisieren, wird ein Fehler zurückgegeben. Die Zeilen sollten aus der Tabelle gelöscht und erneut eingefügt werden.  
  
### <a name="user-defined-triggers"></a>Benutzerdefinierte Trigger  
  
-   Wenn die Anwendung Trigger auf dem Abonnenten erfordert, definieren Sie die Trigger mithilfe der `NOT FOR REPLICATION` -Option auf dem Verleger und dem Abonnenten. Dadurch wird sichergestellt, dass Trigger nur für die ursprüngliche Datenänderung und nicht bei der Replikation dieser Änderung ausgelöst werden.  
  
     Stellen Sie sicher, dass der benutzerdefinierte Trigger nicht ausgelöst wird, wenn der Replikationstrigger die Tabelle aktualisiert. Dies wird erreicht, indem die **sp_check_for_sync_trigger** -Prozedur im Rumpf des benutzerdefinierten Triggers aufgerufen wird. Weitere Informationen finden Sie unter [sp_check_for_sync_trigger &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-check-for-sync-trigger-transact-sql.md).  
  
### <a name="immediate-updating"></a>Sofortige Updates  
  
-   Für sofort aktualisierbare Abonnements werden Änderungen auf dem Abonnenten an den Verleger weitergegeben und mithilfe von MS DTC (Microsoft Distributed Transaction Coordinator) angewendet. Stellen Sie sicher, dass MS DTC auf dem Verleger und Abonnenten installiert und konfiguriert ist. Weitere Informationen finden Sie in der Windows-Dokumentation.  
  
-   Die Trigger, die für sofort aktualisierbare Abonnements verwendet werden, erfordern eine Verbindung mit dem Verleger, damit Änderungen repliziert werden können.  
  
-   Wenn die Veröffentlichung sofort aktualisierbare Abonnements zulässt und ein Artikel in der Veröffentlichung einen Spaltenfilter aufweist, können Sie Spalten ungleich NULL ohne Standardwerte nicht herausfiltern.  
  
### <a name="queued-updating"></a>Verzögerte Updates über eine Warteschlange  
  
-   In einer Mergeveröffentlichung eingeschlossene Tabellen können nicht als Teil einer Transaktionsveröffentlichung veröffentlicht werden, die Abonnements mit verzögertem Update über eine Warteschlange zulässt.  
  
-   Updates an Primärschlüsselspalten werden beim Verwenden des verzögerten Aktualisierens über eine Warteschlange nicht empfohlen, da der Primärschlüssel verwendet wird, um Datensätze für alle Abfragen zu suchen. Wenn die Vorgehensweise zur Konfliktlösung so festgelegt ist, dass der Abonnent gewinnt, sollten Updates an Primärschlüsseln mit Vorsicht vorgenommen werden. Wenn Updates am Primärschlüssel auf dem Verleger und dem Abonnenten vorgenommen werden, handelt es sich beim Ergebnis um zwei Zeilen mit unterschiedlichen Primärschlüsseln.  
  
-   Für Spalten des Datentyps **SQL_VARIANT**: Daten werden beim Einfügen oder Aktualisieren auf dem Abonnenten vom Warteschlangenlese-Agent auf die folgende Weise zugeordnet, wenn sie vom Abonnenten in die Warteschlange kopiert werden:  
  
    -   **BIGINT**, **DECIMAL**, **NUMERIC**, **MONEY**und **SMALLMONEY** werden **NUMERIC**zugeordnet.  
  
    -   **BINARY** und **VARBINARY** werden **VARBINARY** -Daten zugeordnet.  
  
### <a name="conflict-detection-and-resolution"></a>Konflikterkennung und -lösung  
  
-   Für die Konfliktlösungsrichtlinie Abonnent gewinnt gilt: Die Konfliktlösung wird bei Updates an Primärschlüsselspalten nicht unterstützt.  
  
-   Konflikte aufgrund von Fehlern der FOREIGN KEY-Einschränkung werden durch die Replikation nicht aufgelöst:  
  
    -   Wenn Konflikte nicht zu erwarten und die Daten optimal partitioniert sind (Abonnenten aktualisieren nicht dieselben Zeilen), können Sie FOREIGN KEY-Einschränkungen auf dem Verleger und den Abonnenten verwenden.  
  
    -   Wenn Konflikte zu erwarten sind, gehen Sie folgendermaßen vor: Verwenden Sie keine FOREIGN KEY-Einschränkungen auf dem Verleger oder dem Abonnenten, wenn Sie die Konfliktlösung "Abonnent gewinnt" verwenden; verwenden Sie keine FOREIGN KEY-Einschränkungen auf dem Abonnenten, wenn Sie die Konfliktlösung "Verleger gewinnt" verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Peer-zu-Peer-Transaktionsreplikation](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Veröffentlichungstypen der Transaktionsreplikation](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  

