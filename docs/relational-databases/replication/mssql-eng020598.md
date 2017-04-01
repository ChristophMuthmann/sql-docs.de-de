---
title: "MSSQL_ENG020598 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG020598 (Fehler)"
ms.assetid: 1c3032f2-23d1-4ead-94ee-16ac4d75cd0c
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020598
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20598|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Die Zeile wurde bei der Anwendung des replizierten Befehls auf dem Abonnenten nicht gefunden.|  
  
## Erklärung  
 Dieser Fehler wird bei der Transaktionsreplikation ausgegeben, wenn der Verteilungs-Agent versucht, eine Zeile auf dem Abonnenten zu aktualisieren, die Zeile jedoch gelöscht bzw. der Primärschlüssel geändert wurde. Standardmäßig sollten Abonnenten von Transaktionsreplikationen schreibgeschützt sein, da Änderungen nicht an den Verleger zurückgegeben werden. Bei der Transaktionsreplikation sollten Benutzeränderungen nur am Abonnenten vorgenommen werden, wenn aktualisierbare Abonnements oder Peer-zu-Peer-Replikationen verwendet werden. Informationen zu diesen Optionen finden Sie unter [aktualisierbare Abonnements für die Transaktionsreplikation](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md) und [Peer-zu-Peer-Transaktionsreplikation](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
## Benutzeraktion  
 **So lösen Sie dieses Problem**  
  
1.  Wenn die Replikation fortgesetzt werden muss, während Sie die Ursache des Fehlers ermitteln, geben Sie den Parameter **- SkipErrors 20598** für den Verteilungs-Agent. Hierdurch kann der Agent Änderungen auslassen, die den Fehler 20598 verursachen, und dennoch zulassen, dass andere Änderungen repliziert werden.  
  
2.  Stellen Sie fest, welche Zeilen auf dem Abonnenten gelöscht wurden bzw. einen anderen Primärschlüssel aufweisen als die Zeilen auf dem Verleger. Verwenden Sie [tablediff Utility](../../tools/tablediff-utility.md) , um zu ermitteln, welche Zeilen sich in den Veröffentlichungs- und Abonnementdatenbanken unterscheiden. Informationen zum Verwenden dieses Hilfsprogramms bei replizierten Datenbanken finden Sie unter [Vergleichen replizierten Tabellen für Unterschiede & #40; Replikationsprogrammierung & #41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
3.  Verbessern Sie die Zeilen auf dem Abonnenten mithilfe des Hilfsprogramms **tablediff** oder einer anderen Methode.  
  
4.  (Optional) Entfernen Sie die **- SkipErrors** Parameter.  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  