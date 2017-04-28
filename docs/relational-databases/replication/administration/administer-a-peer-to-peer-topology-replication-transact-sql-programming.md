---
title: Verwalten einer Peer-zu-Peer-Topologie (Replikationsprogrammierung mit Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, peer-to-peer replication
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c4ee67601036ff703687015ae3b4b89c822f7054
ms.lasthandoff: 04/11/2017

---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>Verwalten einer Peer-zu-Peer-Topologie (Replikationsprogrammierung mit Transact-SQL)
  Das Verwalten einer Peer-zu-Peer-Topologie ist mit dem Verwalten einer typischen Transaktionsreplikationstopologie zu vergleichen, allerdings sind für einige Bereiche Besonderheiten zu beachten. Der Hauptunterschied beim Verwalten einer Peer-zu-Peer-Topologie besteht darin, dass das System aufgrund einiger Änderungen *in einen inaktiven Status versetzt werden muss*. Um das System in einen inaktiven Status zu versetzen, beenden Sie alle Aktivitäten in veröffentlichten Tabellen auf allen Knoten, und stellen Sie sicher, dass jeder Knoten alle Änderungen sämtlicher anderen Knoten empfangen hat. Weitere Informationen finden Sie unter [Versetzen einer Replikationstopologie in einen inaktiven Status &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
> [!NOTE]  
>  In einer Peer-zu-Peer-Topologie kann der Verteiler keine frühere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Version verwenden als ein Pullabonnent.  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>So fügen Sie einer vorhandenen Konfiguration einen Artikel hinzu  
  
1.  Versetzen Sie das System in einen inaktiven Status.  
  
2.  Beenden Sie den Verteilungs-Agent in jedem Knoten in der Topologie. Weitere Informationen finden Sie unter [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) oder [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Führen Sie die CREATE TABLE-Anweisung aus, um die neue Tabelle in jedem Knoten in der Topologie hinzuzufügen.  
  
4.  Kopieren Sie die Daten mithilfe des [Hilfsprogramms "bcp"](../../../tools/bcp-utility.md)in einem Massenkopiervorgang für die neue Tabelle manuell in alle Knoten.  
  
5.  Führen Sie [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) aus, um den neuen Artikel in jedem Knoten in der Topologie zu erstellen. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Nach dem Ausführen von [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) fügt die Replikation den Artikel automatisch den Abonnements in der Topologie hinzu.  
  
6.  Starten Sie die Verteilungs-Agents in jedem Knoten in der Topologie neu.  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>So nehmen Sie an einer Veröffentlichungsdatenbank Schemaänderungen vor  
  
1.  Versetzen Sie das System in einen inaktiven Status.  
  
2.  Führen Sie die DDL-Anweisungen (Data Definition Language) aus, um das Schema veröffentlichter Tabellen zu ändern. Weitere Informationen zu unterstützten Schemaänderungen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
3.  Versetzen Sie das System erneut in einen inaktiven Status, bevor Sie die Aktivitäten an veröffentlichten Tabellen fortsetzen. So kann sichergestellt werden, dass alle Knoten die Schemaänderungen erhalten haben, bevor neue Datenänderungen repliziert werden.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das Hinzufügen eines neuen Tabellenartikels zu einer vorhandenen Peer-zu-Peer-Topologie mit zwei Knoten veranschaulicht:  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_1.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_2.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_3.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verwaltung &#40;Replikation&#41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Peer-zu-Peer-Transaktionsreplikation](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
