---
title: "Konfigurieren des Transaktionssatz-Auftrags f&#252;r einen Oracle-Verleger (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_publisherproperty"
  - "Veröffentlichungen mit Oracle [SQL Server-Replikation], konfigurieren"
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Konfigurieren des Transaktionssatz-Auftrags f&#252;r einen Oracle-Verleger (Replikationsprogrammierung mit Transact-SQL)
  Der **Xactset** -Auftrag ist ein Oracle-Datenbankauftrag, der bei der Replikation erstellt und auf einem Oracle-Verleger ausgeführt wird, um Transaktionssätze zu erstellen, wenn der Protokolllese-Agent nicht mit dem Verleger verbunden ist. Sie können diesen Auftrag auf dem Verteiler programmgesteuert mithilfe gespeicherter Replikationsprozeduren aktivieren und konfigurieren. Weitere Informationen finden Sie unter [Performance-Optimierung für Oracle-Verleger](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md).  
  
### So aktivieren Sie den Transaktionssatz-Auftrag  
  
1.  Legen Sie auf dem Oracle-Verleger, die **Job_queue_processes** -Initialisierungsparameter auf einen Wert auf die Ausführung des Xactset-Auftrags zulässt. Weitere Informationen zu diesem Parameter finden Sie in der Datenbankdokumentation für den Oracle-Verleger.  
  
2.  Führen Sie auf dem Verteiler [Sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Geben Sie den Namen des Oracle-Verlegers für **@publisher**, einen Wert **xactsetbatching** für **@propertyname**und einen Wert **enabled** für **@propertyvalue**an.  
  
3.  Führen Sie auf dem Verteiler [Sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Geben Sie den Namen des Oracle-Verlegers für **@publisher**, einen Wert **xactsetjobinterval** für **@propertyname**und das Auftragsintervall in Minuten für **@propertyvalue**an.  
  
4.  Führen Sie auf dem Verteiler [Sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Geben Sie den Namen des Oracle-Verlegers für **@publisher**, einen Wert **xactsetjob** für **@propertyname**und einen Wert **enabled** für **@propertyvalue**an.  
  
### So konfigurieren Sie den Transaktionssatz-Auftrag  
  
1.  (Optional) Führen Sie auf dem Verteiler [Sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Geben Sie den Namen des Oracle-Verlegers für **@publisher**an. Dadurch werden die Eigenschaften des **Xactset** -Auftrags auf dem Verleger zurückgegeben.  
  
2.  Führen Sie auf dem Verteiler [Sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Geben Sie den Namen des Oracle-Verlegers für **@publisher**, den Namen der Xactset-Auftragseigenschaft, die für **@propertyname**festgelegt ist, und eine neue Einstellung für **@propertyvalue**an.  
  
3.  (Optional) Wiederholen Sie Schritt 2 für jede festgelegte Xactset-Auftragseigenschaft. Beim Ändern der **xactsetjobinterval** -Eigenschaft müssen Sie den Auftrag auf dem Oracle-Verleger neu starten, damit das neue Intervall wirksam wird.  
  
### So zeigen Sie die Eigenschaften des Transaktionssatz-Auftrags an  
  
1.  Führen Sie auf dem Verteiler [Sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md). Geben Sie den Namen des Oracle-Verlegers für **@publisher**an.  
  
### So deaktivieren Sie den Transaktionssatz-Auftrag  
  
1.  Führen Sie auf dem Verteiler [Sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Geben Sie den Namen des Oracle-Verlegers für **@publisher**, einen Wert **xactsetjob** für **@propertyname**und einen Wert **disabled** für **@propertyvalue**an.  
  
## Beispiel  
 Im folgenden Beispiel wird der `Xactset` -Auftrag aktiviert und ein Intervall von drei Minuten zwischen den Ausführungen festgelegt.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure the transactio_1.sql)]  
  
## Siehe auch  
 [Leistungsoptimierung für Oracle-Verleger](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  