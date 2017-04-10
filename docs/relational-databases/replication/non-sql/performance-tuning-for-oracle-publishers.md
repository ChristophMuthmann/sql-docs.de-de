---
title: "Leistungsoptimierung f&#252;r Oracle-Verleger | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Veröffentlichungen mit Oracle [SQL Server-Replikation], Leistungsoptimierung"
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Leistungsoptimierung f&#252;r Oracle-Verleger
  Der Oracle-veröffentlichungsarchitektur ähnlich wie ist die [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Veröffentlichen Architektur; der erste Schritt bei der Feineinstellung von Oracle-Replikation erfordert deshalb folgen die allgemeinen optimierungsempfehlungen finden Sie in [General Replication Performance verbessern](../../../relational-databases/replication/administration/enhance-general-replication-performance.md).  
  
 Darüber hinaus stehen zwei Optionen für Oracle-Verleger zur Verfügung, die im Zusammenhang mit der Leistung stehen:  
  
-   Angeben der entsprechenden Veröffentlichungsoption: Oracle oder Oracle-Gateway.  
  
-   Konfigurieren des Transaktionssatz-Auftrags, mit dem Änderungen am Verleger in angemessenen Abständen verarbeitet werden.  
  
## Angeben der entsprechenden Veröffentlichungsoption  
 Die Option Oracle (Gateway) bietet eine bessere Leistung im Vergleich zur Option Oracle (Vollständig), allerdings ist es mit dieser Option nicht möglich, dieselbe Tabelle in mehreren Transaktionsveröffentlichungen zu veröffentlichen. Eine Tabelle kann in höchstens eine Transaktionsveröffentlichung und in beliebig viele Momentaufnahmeveröffentlichungen aufgenommen werden. Wenn Sie dieselbe Tabelle in mehreren Transaktionsveröffentlichungen veröffentlichen müssen, wählen Sie die Option Oracle (Vollständig) aus. Geben Sie diese Option an, wenn Sie den Oracle-Verleger beim [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler festlegen. Weitere Informationen finden Sie unter [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
## Konfigurieren des Transaktionssatz-Auftrags  
 Änderungen an veröffentlichten Oracle-Tabellen werden in Gruppen verarbeitet, den so genannten Transaktionssätzen. Um die Transaktionskonsistenz sicherzustellen, wird jeder Transaktionssatz als einzelne Transaktion an die Verteilungsdatenbank übermittelt. Wird der Transaktionssatz zu groß, kann er nicht mehr effizient als einzelne Transaktion verarbeitet werden.  
  
 Standardmäßig werden Transaktionssätze nur durch den Protokolllese-Agent erstellt. Falls der Protokolllese-Agent in Phasen umfangreicher Änderungsaktivitäten nicht ausgeführt wird oder keine Verbindung vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler zum Oracle-Verleger aufbauen kann, werden die Transaktionssätze möglicherweise unüberschaubar groß. Um dieses Problem zu vermeiden, stellen Sie sicher, dass Transaktionssätze in regelmäßigen Abständen erstellt werden, selbst wenn der Protokolllese-Agent nicht ausgeführt wird oder keine Verbindung mit dem Oracle-Verleger aufbauen kann.  
  
 Transaktionssätze können mit dem Xactset Job erstellt werden (Oracle-Datenbankauftrag, der bei der Replikation installiert wird), bei dem die Sätze mit demselben Mechanismus erstellt angelegt werden wie beim Protokolllese-Agent. Bei jeder Ausführung des Auftrags wird ein neuer Transaktionssatz erstellt. Beim nächsten Ausführen des Protokolllese-Agents werden alle erstellten Sätze durch den Agent verarbeitet. Stehen weiterhin Änderungen aus, nachdem alle vorhandenen Transaktionssätze verarbeitet wurden, erstellt und verarbeitet der Protokolllese-Agent mindestens einen weiteren Transaktionssatz.  
  
 Konfigurieren des Transaktionssatz-Auftrags finden Sie in [Konfigurieren Sie die Transaktionssatz-Auftrags für einen Oracle-Verleger & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/administration/configure the transaction set job for an oracle publisher.md).  
  
## Siehe auch  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Veröffentlichungen mit Oracle (Übersicht)](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  