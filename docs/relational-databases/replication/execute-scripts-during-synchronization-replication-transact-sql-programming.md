---
title: Ausführen von Skripts während der Synchronisierung (Replikationsprogrammierung mit Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a7a7aa93de8e03651de8525a4aa1050e8e90e4fb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>Ausführen von Skripts während der Synchronisierung (Replikationsprogrammierung mit Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Die Replikation unterstützt die bedarfsgesteuerte Ausführung von Skripts für Abonnenten von Transaktions- und Mergeveröffentlichungen. Diese Funktionalität kopiert das Skript in das Replikationsarbeitsverzeichnis und wendet das Skript dann mithilfe von **sqlcmd** auf dem Abonnenten an. Standardmäßig wird der Verteilungs-Agent beendet, wenn beim Anwenden des Skripts auf ein Abonnement für eine Transaktionsveröffentlichung ein Fehler auftritt. Mithilfe von gespeicherten Replikationsprozeduren können Sie ein [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript angeben, das programmgesteuert ausgeführt werden soll.  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>So geben Sie ein Skript an, das für alle Abonnenten einer Momentaufnahme-, Transaktions- oder Mergeveröffentlichung ausgeführt werden soll  
  
1.  Erstellen und testen Sie das [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript, das bedarfsgesteuert ausgeführt wird.  
  
2.  Speichern Sie die Skriptdatei an einem Speicherort, auf den der Momentaufnahme-Agent für die Veröffentlichung zugreifen kann.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addscriptexec &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md) aus. Geben Sie **@publication**, den Namen der Skriptdatei mit dem vollständigen, in Schritt 2 erstellten UNC-Pfad für **@scriptfile**und einen der folgenden Werte für **@skiperror**ein:  
  
    -   **0** &ndash; der Agent beendet die Ausführung des Skripts, wenn ein Fehler auftritt.  
  
    -   **1** &ndash; der Agent protokolliert Fehler und setzt die Ausführung des Skripts fort, wenn Fehler auftreten.  
  
4.  Das angegebene Skript wird auf jedem Abonnenten ausgeführt, wenn der Agent das nächste Mal zur Synchronisierung des Abonnements ausgeführt wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Synchronisieren von Daten](../../relational-databases/replication/synchronize-data.md)  
  
  
