---
title: Replikation mit Abonnenten von speicheroptimierten Tabellen | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
caps.latest.revision: "23"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c69235ed7926219dc306764b3b2ba80a2c35bb1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>Replikation mit Abonnenten von speicheroptimierten Tabellen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Die Tabellen, die als Momentaufnahmen- und Transaktionsreplikationsabonnenten fungieren, können (mit Ausnahme der Peer-zu-Peer-Transaktionsreplikation) als speicheroptimierte Tabellen konfiguriert werden. Andere Replikationskonfigurationen sind mit speicheroptimierten Tabellen nicht kompatibel. Diese Funktion ist ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]verfügbar.  
  
## <a name="two-configurations-are-required"></a>Zwei Konfigurationen sind erforderlich.  
  
-   **Konfigurieren der Abonnentendatenbank für die Unterstützung der Replikation in speicheroptimierte Tabellen**  
  
     Legen Sie die **@memory_optimized**-Eigenschaft auf **true** fest, indem Sie [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) oder [sp_changesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) verwenden.  
  
-   **Konfigurieren des Artikels für die Unterstützung der Replikation in speicheroptimierte Tabellen**  
  
     Legen Sie die `@schema_option = 0x40000000000`-Option für den Artikel mit [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) oder [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) fest.  
  
#### <a name="to-configure-a-memory-optimized-table-as-a-subscriber"></a>So konfigurieren Sie eine speicheroptimierte Tabelle als Abonnent  
  
1.  Erstellen Sie eine Transaktionsveröffentlichung. Weitere Informationen finden Sie unter [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Fügen Sie der Veröffentlichung Artikel hinzu. Weitere Informationen finden Sie unter [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
     Falls Sie die Konfiguration mit [!INCLUDE[tsql](../../includes/tsql-md.md)] set the **@schema_option** der gespeicherten **sp_addarticle** -Prozedur auf   
    **0x40000000000**verfügbar.  
  
3.  Legen Sie im Fenster mit den Artikeleigenschaften **Enable Memory optimization** auf **true**fest.  
  
4.  Starten Sie den Auftrag des Momentaufnahme-Agents, um die Anfangsmomentaufnahme für diese Veröffentlichung zu generieren. Weitere Informationen finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
5.  Erstellen Sie dann ein neues Abonnement. Legen Sie im **Assistenten für neue Abonnements** **Memory Optimized Subscription** auf **true**fest.  
  
 Speicheroptimierte Tabellen empfangen nun Updates vom Verleger.  
  
#### <a name="reconfigure-an-existing-transaction-replication"></a>Neukonfiguration einer vorhandenen Transaktionsreplikation  
  
1.  Gehen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] zu den Abonnementeigenschaften, und legen Sie **Memory Optimized Subscription** auf **true**fest. Die Änderungen werden erst nach der erneuten Initialisierung des Abonnements wirksam.  
  
     Falls Sie die Konfiguration mit [!INCLUDE[tsql](../../includes/tsql-md.md)] vornehmen, legen Sie den neuen **@memory_optimized** der gespeicherten **sp_addsubscription** -Prozedur auf "true" fest.  
  
2.  Gehen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] zu den Artikeleigenschaften einer Veröffentlichung, und legen Sie **Enable Memory optimization** auf "true" fest.  
  
     Falls Sie die Konfiguration mit [!INCLUDE[tsql](../../includes/tsql-md.md)] set the **@schema_option** der gespeicherten **sp_addarticle** -Prozedur auf   
    **0x40000000000**verfügbar.  
  
3.  Speicheroptimierte Tabellen unterstützen keine gruppierten Indizes. Daher müssen gruppierte Indizes bei der Replikation auf dem Ziel in nicht gruppierte Indizes konvertiert werden. Hierzu muss der Parameter **Convert clustered index to nonclustered for memory optimized article** auf "true" festgelegt werden.  
  
     Falls Sie die Konfiguration mit [!INCLUDE[tsql](../../includes/tsql-md.md)] set the **@schema_option** der gespeicherten **sp_addarticle** -Prozedur auf  **0x0000080000000000**verfügbar.  
  
4.  Generieren Sie die Momentaufnahme erneut.  
  
5.  Initialisieren Sie das Abonnement erneut.  
  
## <a name="remarks-and-restrictions"></a>Hinweise und Einschränkungen  
 Es wird nur die unidirektionale Transaktionsreplikation unterstützt. Die Peer-zu-Peer-Transaktionsreplikation wird nicht unterstützt.  
  
 Speicheroptimierte Tabellen können nicht veröffentlicht werden.  
  
 Replikationstabellen auf dem Verteiler können nicht als speicheroptimierte Tabellen konfiguriert werden.  
  
 Die Mergereplikation kann speicheroptimierte Tabellen einschließen.  
  
 Auf dem Abonnenten können die Tabellen, die bei einer Transaktionsreplikation berücksichtigt werden, als speicheroptimierte Tabellen konfiguriert werden. Die Abonnententabellen müssen jedoch die Anforderungen für speicheroptimierte Tabellen erfüllen. Dies erfordert folgende Einschränkungen.  
 
-   Tabellen, die mit speicheroptimierten Tabellen auf Abonnenten repliziert werden, sind auf die Datentypen beschränkt, die für speicheroptimierte Tabellen zulässig sind. Weitere Informationen finden Sie unter [Unterstützte Datentypen für In-Memory OLTP](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md).  
  
-   Nicht alle Transact-SQL-Funktionen werden von speicheroptimierten Tabellen unterstützt. Weitere Einzelheiten finden Sie unter [Transact-SQL Constructs Not Supported by In-Memory OLTP](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) .  
  
##  <a name="Schema"></a> Ändern einer Schemadatei  
  
-   Bei Verwendung der Option für speicheroptimierte Tabellen `DURABILITY = SCHEMA_AND_DATA` muss die Tabelle einen nicht gruppierten Primärschlüsselindex aufweisen.  
  
-   ANSI_PADDING muss auf ON festgelegt sein.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Replikationsfunktionen und -tasks](../../relational-databases/replication/replication-features-and-tasks.md)  
  
  
