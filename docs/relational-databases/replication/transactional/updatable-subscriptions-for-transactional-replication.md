---
title: "Aktualisierbare Abonnements f&#252;r die Transaktionsreplikation | Microsoft Docs"
ms.custom: ""
ms.date: "07/21/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Transaktionsreplikation, aktualisierbare Abonnements"
  - "Aktualisierbare Abonnements, Informationen zu aktualisierbaren Abonnements"
  - "Abonnements mit verzögertem Update über eine Warteschlange [SQL Server-Replikation]"
  - "Sofort aktualisierbare Abonnements"
  - "Abonnements [SQL Server-Replikation], aktualisierbar"
  - "updatable subscriptions"
ms.assetid: 8eec95cb-3a11-436e-bcee-bdcd05aa5c5a
caps.latest.revision: 60
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 60
---
# Aktualisierbare Abonnements f&#252;r die Transaktionsreplikation
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  Dieses Feature wird in den Versionen von [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] von 2012 bis 2016 weiterhin unterstützt. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Die Transaktionsreplikation unterstützt Updates auf den Abonnenten über aktualisierbare Abonnements und Peer-zu-Peer-Replikation. Es gibt zwei Arten von aktualisierbaren Abonnements:  
  
-   Sofortiges Aktualisieren. Verleger und Abonnent müssen verbunden sein, damit Daten auf dem Abonnenten aktualisiert werden können.  
  
-   Verzögertes Aktualisieren über eine Warteschlange. Verleger und Abonnent müssen nicht verbunden sein, damit Daten auf dem Abonnenten aktualisiert werden können. Updates können ausgeführt werden, während der Verleger oder der Abonnent offline ist.  
  
 Wenn Daten auf einem Abonnenten aktualisiert werden, werden sie zuerst an den Verleger und dann an andere Abonnenten weitergegeben. Beim sofortigen Aktualisieren werden die Änderungen sofort mithilfe des Zweiphasencommit-Protokolls weitergegeben. Beim verzögerten Aktualisieren über eine Warteschlange werden die Änderungen in einer Warteschlange gespeichert und dann immer, wenn eine Netzwerkverbindung verfügbar ist, asynchron auf dem Verleger angewendet. Da die Updates asynchron an den Verleger weitergegeben werden, wurden die gleichen Daten möglicherweise vom Verleger oder von einem anderen Abonnenten aktualisiert. Daher können Konflikte auftreten, wenn die Updates angewendet werden. Konflikte werden nach einer Vorgehensweise zur Konfliktlösung erkannt und gelöst, die beim Erstellen der Veröffentlichung festgelegt wird.  
  
 Wenn Sie im Assistenten für neue Veröffentlichung eine Transaktionsveröffentlichung mit aktualisierbaren Abonnements erstellen, werden sowohl das sofortige Aktualisieren als auch das verzögerte Aktualisieren über eine Warteschlange aktiviert. Beim Erstellen einer Veröffentlichung mit gespeicherten Prozeduren können Sie eine oder beide Optionen aktivieren. Wenn Sie ein Abonnement für die Veröffentlichung erstellen, geben Sie an, welcher Updatemodus verwendet wird. Sie können dann gegebenenfalls den Updatemodus wechseln. Weitere Informationen finden Sie im folgenden Abschnitt zum Wechseln des Updatemodus.  
  
 Informationen zum Aktivieren aktualisierbarer Abonnements für Transaktionsveröffentlichungen finden Sie unter [Enable Updating Subscriptions for Transactional Publications](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).  
  
 Aktualisierbare Abonnements für eine Transaktionspublikation erstellen, finden Sie unter [Erstellen eines aktualisierbaren Abonnements für eine Transaktionsveröffentlichung (Management Studio)](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md) 
  
## Wechseln des Updatemodus  
 Bei der Verwendung aktualisierbarer Abonnements können Sie den Updatemodus für ein Abonnement angeben und dann bei Bedarf in den anderen Modus wechseln. Sie können z. B. angeben, dass das sofortige Aktualisieren für ein Abonnement verwendet wird. Wenn dann jedoch die Netzwerkverbindung aufgrund eines Systemfehlers unterbrochen wird, können Sie auf das verzögerte Aktualisieren über eine Warteschlange wechseln.  
  
> [!NOTE]  
>  Bei der Replikation erfolgt kein automatischer Wechsel zwischen den Updatemodi. Sie müssen den Aktualisierungsmodus über SQL Server Management Studio oder Ihre Anwendung aufrufen muss [Sp_setreplfailovermode &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md) um zwischen den Modi zu wechseln.  
  
 Wenn Sie vom sofortigen Aktualisieren zum verzögerten Aktualisieren über eine Warteschlange wechseln, können Sie erst wieder zum sofortigen Aktualisieren wechseln, wenn der Abonnent und der Verleger verbunden sind und der Warteschlangenlese-Agent alle ausstehenden Nachrichten in der Warteschlange auf den Verleger angewendet hat.  
  
 **So wechseln Sie den Updatemodus**  
  
 Zum Wechseln des Updatemodus müssen Sie die Veröffentlichung und das Abonnement für beide Modi aktivieren und zwischen beiden nach Bedarf wechseln. Weitere Informationen finden Sie unter  
[Umschalten zwischen Updatemodi für ein aktualisierbares Transaktionsabonnement](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).  
  
### Überlegungen zur Verwendung von aktualisierbaren Abonnements  
  
-   Nachdem eine Veröffentlichung für Abonnements mit sofortigem Update oder Abonnements mit verzögertem Update über eine Warteschlange aktiviert wurde, kann die Option nicht für die Veröffentlichung deaktiviert werden (obwohl die Abonnements sie nicht verwenden müssen). Zum Deaktivieren der Option muss die Veröffentlichung gelöscht und dann eine neue Veröffentlichung erstellt werden.  
  
-   Das erneute Veröffentlichen von Daten wird nicht unterstützt.  
  
-   Fügt der Replikation der **Msrepl_tran_version** -Spalte zu veröffentlichten Tabellen für das nachverfolgen. Wegen dieser zusätzlichen Spalte sollten alle **INSERT** -Anweisungen eine Spaltenliste enthalten.  
  
-   Wenn Sie das Schema einer Tabelle in einer Veröffentlichung ändern möchten, die das Aktualisieren von Abonnements unterstützt, müssen alle Aktivitäten an der Tabelle auf dem Verleger und dem Abonnenten angehalten werden. Außerdem müssen ausstehende Datenänderungen vor einer Schemaänderung an alle Knoten weitergegeben werden. Dadurch wird sichergestellt, dass unbeendete Transaktionen keinen Konflikt mit der ausstehenden Schemaänderung auslösen. Nach der Weitergabe der Schemaänderungen an alle Knoten können die Aktivitäten an den veröffentlichten Tabellen fortgesetzt werden. Weitere Informationen finden Sie unter [Versetzen einer Replikationstopologie in einen inaktiven Status &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
-   Wenn Sie den Updatemodus wechseln möchten, muss der Warteschlangenlese-Agent nach der Initialisierung des Abonnements mindestens einmal ausgeführt werden (standardmäßig wird der Warteschlangenlese-Agent fortlaufend ausgeführt).  
  
-   Ist die Abonnentendatenbank horizontal partitioniert und die Partition enthält Zeilen, die auf dem Abonnenten, aber nicht auf dem Verleger vorhanden sind, kann der Abonnent die bereits vorhandenen Zeilen nicht aktualisieren. Bei dem Versuch, diese Zeilen zu aktualisieren, wird ein Fehler zurückgegeben. Die Zeilen sollten aus der Tabelle gelöscht und dann auf dem Verleger hinzugefügt werden.  

-   Transaktionsreplikation mit aktualisierbaren Abonnenten, die in der Warteschlange kann dadurch die Leistung beeinträchtigt, wenn gefilterte Indizes verwendet werden. Auf ein Konflikt auftritt, wird ein Artikel, der gefilterte Indizes verfügt, und klicken Sie dann die Auflösung des Konflikts zwischen zusätzlichen führen würde löscht und fügt auf dem Abonnenten für die Zeilen, die nicht durch den eindeutigen gefilterten Index abgedeckt werden.
  
### Updates auf dem Abonnenten  
  
-   Updates auf dem Abonnenten werden auch dann an den Verleger weitergegeben, wenn ein Abonnement abgelaufen oder inaktiv ist. Stellen Sie sicher, dass Abonnements dieser Art gelöscht oder erneut initialisiert werden.  
  
-   Wenn die Spalten **TIMESTAMP** oder **IDENTITY** verwendet und als Basisdatentypen repliziert werden, sollten die Werte in diesen Spalten nicht auf dem Abonnenten aktualisiert werden.  
  
-   Abonnenten können nicht aktualisiert oder eingefügt **Text**, **Ntext** oder **Image** Werte, da es nicht möglich, aus den eingefügten oder gelöschten Tabellen innerhalb der Änderungsprotokollierungstrigger der Replikation zu lesen ist. Ebenso können Abonnenten keine **text** - oder **image** -Werte mithilfe von **WRITETEXT** oder **UPDATETEXT** aktualisieren oder einfügen, da die Daten vom Verleger überschrieben werden. Stattdessen können Sie die **text** - und **image** -Spalten in eine separate Tabelle partitionieren und die beiden Tabellen in einer Transaktion ändern.  
  
     Verwenden Sie zum Aktualisieren großer Objekte auf einem Abonnenten die Datentypen **varchar(max)**, **nvarchar(max)**, **varbinary(max)** anstelle von **Text**, **Ntext**, und **Image** Datentypen.  
  
-   Updates an eindeutigen Schlüsseln (einschließlich Primärschlüssel), die Duplikate generieren (z. B. ein Update des Formulars `UPDATE <column> SET <column> =<column>+1` sind nicht zulässig und werden aufgrund eines Verstoßes gegen die abgelehnt. Dies ist darin begründet, dass Updates von Zeilengruppen auf dem Abonnenten durch die Replikation als einzelne **UPDATE** -Anweisungen für jede betroffene Zeile weitergegeben werden.  
  
-   Ist die Abonnentendatenbank horizontal partitioniert und die Partition enthält Zeilen, die auf dem Abonnenten, aber nicht auf dem Verleger vorhanden sind, kann der Abonnent die bereits vorhandenen Zeilen nicht aktualisieren. Bei dem Versuch, diese Zeilen zu aktualisieren, wird ein Fehler zurückgegeben. Die Zeilen sollten aus der Tabelle gelöscht und erneut eingefügt werden.  
  
### Benutzerdefinierte Trigger  
  
-   Wenn die Anwendung Trigger auf dem Abonnenten erfordert, definieren Sie die Trigger mithilfe der `NOT FOR REPLICATION` -Option auf dem Verleger und dem Abonnenten. Dadurch wird sichergestellt, dass Trigger nur für die ursprüngliche Datenänderung und nicht bei der Replikation dieser Änderung ausgelöst werden.  
  
     Stellen Sie sicher, dass der benutzerdefinierte Trigger nicht ausgelöst wird, wenn der Replikationstrigger die Tabelle aktualisiert. Dies erfolgt durch Aufrufen der Prozedur **Sp_check_for_sync_trigger** im Text des benutzerdefinierten Triggers. Weitere Informationen finden Sie unter [Sp_check_for_sync_trigger &#40; Transact-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-check-for-sync-trigger-transact-sql.md).  
  
### Sofortige Updates  
  
-   Für sofort aktualisierbare Abonnements werden Änderungen auf dem Abonnenten an den Verleger weitergegeben und mithilfe von MS DTC (Microsoft Distributed Transaction Coordinator) angewendet. Stellen Sie sicher, dass MS DTC auf dem Verleger und Abonnenten installiert und konfiguriert ist. Weitere Informationen finden Sie in der Windows-Dokumentation.  
  
-   Die Trigger, die für sofort aktualisierbare Abonnements verwendet werden, erfordern eine Verbindung mit dem Verleger, damit Änderungen repliziert werden können.  
  
-   Wenn die Veröffentlichung sofort aktualisierbare Abonnements zulässt und ein Artikel in der Veröffentlichung einen Spaltenfilter aufweist, können Sie Spalten ungleich NULL ohne Standardwerte nicht herausfiltern.  
  
### Verzögerte Updates über eine Warteschlange  
  
-   In einer Mergeveröffentlichung eingeschlossene Tabellen können nicht als Teil einer Transaktionsveröffentlichung veröffentlicht werden, die Abonnements mit verzögertem Update über eine Warteschlange zulässt.  
  
-   Updates an Primärschlüsselspalten werden beim Verwenden des verzögerten Aktualisierens über eine Warteschlange nicht empfohlen, da der Primärschlüssel verwendet wird, um Datensätze für alle Abfragen zu suchen. Wenn die Vorgehensweise zur Konfliktlösung so festgelegt ist, dass der Abonnent gewinnt, sollten Updates an Primärschlüsseln mit Vorsicht vorgenommen werden. Wenn Updates am Primärschlüssel auf dem Verleger und dem Abonnenten vorgenommen werden, handelt es sich beim Ergebnis um zwei Zeilen mit unterschiedlichen Primärschlüsseln.  
  
-   Für Spalten des Datentyps **SQL_VARIANT**: Wenn Daten eingefügt oder auf dem Abonnenten aktualisiert werden, ist zugeordnet wie folgt durch den Warteschlangenlese-Agent, die vom Abonnenten in die Warteschlange kopiert wird:  
  
    -   **BIGINT**, **DECIMAL**, **NUMERIC**, **MONEY**und **SMALLMONEY** werden **NUMERIC**zugeordnet.  
  
    -   **BINARY** und **VARBINARY** werden **VARBINARY** -Daten zugeordnet.  
  
### Konflikterkennung und -lösung  
  
-   Für die Konfliktlösungsrichtlinie Abonnent gewinnt gilt: Die Konfliktlösung wird bei Updates an Primärschlüsselspalten nicht unterstützt.  
  
-   Konflikte aufgrund von Fehlern der FOREIGN KEY-Einschränkung werden durch die Replikation nicht aufgelöst:  
  
    -   Wenn Konflikte nicht zu erwarten und die Daten optimal partitioniert sind (Abonnenten aktualisieren nicht dieselben Zeilen), können Sie FOREIGN KEY-Einschränkungen auf dem Verleger und den Abonnenten verwenden.  
  
    -   Wenn Konflikte zu erwarten sind, gehen Sie folgendermaßen vor: Verwenden Sie keine FOREIGN KEY-Einschränkungen auf dem Verleger oder dem Abonnenten, wenn Sie die Konfliktlösung "Abonnent gewinnt" verwenden; verwenden Sie keine FOREIGN KEY-Einschränkungen auf dem Abonnenten, wenn Sie die Konfliktlösung "Verleger gewinnt" verwenden.  
  
## Siehe auch  
 [Peer-zu-Peer-Transaktionsreplikation](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Veröffentlichungstypen der Transaktionsreplikation](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  