---
title: "Konfigurieren des Transaktionssatz-Auftrags für einen Oracle-Verleger | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 596351a92f5b5cbbf69c207c66f66477264b0389
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher"></a>Konfigurieren des Transaktionssatz-Auftrags für einen Oracle-Verleger
  Der **Xactset** -Auftrag ist ein Oracle-Datenbankauftrag, der bei der Replikation erstellt und auf einem Oracle-Verleger ausgeführt wird, um Transaktionssätze zu erstellen, wenn der Protokolllese-Agent nicht mit dem Verleger verbunden ist. Sie können diesen Auftrag auf dem Verteiler programmgesteuert mithilfe gespeicherter Replikationsprozeduren aktivieren und konfigurieren. Weitere Informationen finden Sie unter [Leistungsoptimierung für Oracle-Verleger](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md).  
  
### <a name="to-enable-the-transaction-set-job"></a>So aktivieren Sie den Transaktionssatz-Auftrag  
  
1.  Legen Sie auf dem Oracle-Verleger den **job_queue_processes** -Initialisierungsparameter auf einen Wert fest, der die Ausführung des Xactset-Auftrags zulässt. Weitere Informationen zu diesem Parameter finden Sie in der Datenbankdokumentation für den Oracle-Verleger.  
  
2.  Führen Sie auf dem Verteiler [Sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) aus. Geben Sie den Namen des Oracle-Verlegers für **@publisher**, einen Wert **xactsetbatching** für **@propertyname**und einen Wert **enabled** für **@propertyvalue**.  
  
3.  Führen Sie auf dem Verteiler [Sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) aus. Geben Sie den Namen des Oracle-Verlegers für **@publisher**, einen Wert **xactsetjobinterval** für **@propertyname**und das Auftragsintervall in Minuten für **@propertyvalue**.  
  
4.  Führen Sie auf dem Verteiler [Sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) aus. Geben Sie den Namen des Oracle-Verlegers für **@publisher**, einen Wert **xactsetjob** für **@propertyname**und einen Wert **enabled** für **@propertyvalue**.  
  
### <a name="to-configure-the-transaction-set-job"></a>So konfigurieren Sie den Transaktionssatz-Auftrag  
  
1.  (Optional) Führen Sie auf dem Verteiler [Sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) aus. Geben Sie den Namen des Oracle-Verlegers für **@publisher**. Dadurch werden die Eigenschaften des **Xactset** -Auftrags auf dem Verleger zurückgegeben.  
  
2.  Führen Sie auf dem Verteiler [Sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) aus. Geben Sie den Namen des Oracle-Verlegers für **@publisher**, den Namen der Xactset-Auftragseigenschaft, die für **@propertyname**festgelegt ist, und eine neue Einstellung für **@propertyvalue**.  
  
3.  (Optional) Wiederholen Sie Schritt 2 für jede festgelegte Xactset-Auftragseigenschaft. Beim Ändern der **xactsetjobinterval** -Eigenschaft müssen Sie den Auftrag auf dem Oracle-Verleger neu starten, damit das neue Intervall wirksam wird.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>So zeigen Sie die Eigenschaften des Transaktionssatz-Auftrags an  
  
1.  Führen Sie auf dem Verteiler [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md)aus. Geben Sie den Namen des Oracle-Verlegers für **@publisher**.  
  
### <a name="to-disable-the-transaction-set-job"></a>So deaktivieren Sie den Transaktionssatz-Auftrag  
  
1.  Führen Sie auf dem Verteiler [Sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md) aus. Geben Sie den Namen des Oracle-Verlegers für **@publisher**, einen Wert **xactsetjob** für **@propertyname**und einen Wert **disabled** für **@propertyvalue**.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der `Xactset` -Auftrag aktiviert und ein Intervall von drei Minuten zwischen den Ausführungen festgelegt.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure-the-transactio_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Leistungsoptimierung für Oracle-Verleger](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
