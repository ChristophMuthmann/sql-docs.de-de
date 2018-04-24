---
title: Leistungsoptimierung für Oracle-Verleger | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], performance tuning
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fefeadc5a03c9e00223b7b551a7702aca90b75fc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="performance-tuning-for-oracle-publishers"></a>Leistungsoptimierung für Oracle-Verleger
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die Oracle-Veröffentlichungsarchitektur ist ähnlich aufgebaut wie diejenige von [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Aus diesem Grund sind im ersten Schritt der Leistungsoptimierung der Oracle-Replikation die allgemeinen Optimierungsempfehlungen unter [Enhance General Replication Performance](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)zu beachten.  
  
 Darüber hinaus stehen zwei Optionen für Oracle-Verleger zur Verfügung, die im Zusammenhang mit der Leistung stehen:  
  
-   Angeben der entsprechenden Veröffentlichungsoption: Oracle oder Oracle-Gateway.  
  
-   Konfigurieren des Transaktionssatz-Auftrags, mit dem Änderungen am Verleger in angemessenen Abständen verarbeitet werden.  
  
## <a name="specifying-the-appropriate-publishing-option"></a>Angeben der entsprechenden Veröffentlichungsoption  
 Die Option Oracle (Gateway) bietet eine bessere Leistung im Vergleich zur Option Oracle (Vollständig), allerdings ist es mit dieser Option nicht möglich, dieselbe Tabelle in mehreren Transaktionsveröffentlichungen zu veröffentlichen. Eine Tabelle kann in höchstens eine Transaktionsveröffentlichung und in beliebig viele Momentaufnahmeveröffentlichungen aufgenommen werden. Wenn Sie dieselbe Tabelle in mehreren Transaktionsveröffentlichungen veröffentlichen müssen, wählen Sie die Option Oracle (Vollständig) aus. Geben Sie diese Option an, wenn Sie den Oracle-Verleger beim [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler festlegen. Weitere Informationen finden Sie unter [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
## <a name="configuring-the-transaction-set-job"></a>Konfigurieren des Transaktionssatz-Auftrags  
 Änderungen an veröffentlichten Oracle-Tabellen werden in Gruppen verarbeitet, den so genannten Transaktionssätzen. Um die Transaktionskonsistenz sicherzustellen, wird jeder Transaktionssatz als einzelne Transaktion an die Verteilungsdatenbank übermittelt. Wird der Transaktionssatz zu groß, kann er nicht mehr effizient als einzelne Transaktion verarbeitet werden.  
  
 Standardmäßig werden Transaktionssätze nur durch den Protokolllese-Agent erstellt. Falls der Protokolllese-Agent in Phasen umfangreicher Änderungsaktivitäten nicht ausgeführt wird oder keine Verbindung vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler zum Oracle-Verleger aufbauen kann, werden die Transaktionssätze möglicherweise unüberschaubar groß. Um dieses Problem zu vermeiden, stellen Sie sicher, dass Transaktionssätze in regelmäßigen Abständen erstellt werden, selbst wenn der Protokolllese-Agent nicht ausgeführt wird oder keine Verbindung mit dem Oracle-Verleger aufbauen kann.  
  
 Transaktionssätze können mit dem Xactset Job erstellt werden (Oracle-Datenbankauftrag, der bei der Replikation installiert wird), bei dem die Sätze mit demselben Mechanismus erstellt angelegt werden wie beim Protokolllese-Agent. Bei jeder Ausführung des Auftrags wird ein neuer Transaktionssatz erstellt. Beim nächsten Ausführen des Protokolllese-Agents werden alle erstellten Sätze durch den Agent verarbeitet. Stehen weiterhin Änderungen aus, nachdem alle vorhandenen Transaktionssätze verarbeitet wurden, erstellt und verarbeitet der Protokolllese-Agent mindestens einen weiteren Transaktionssatz.  
  
 Informationen zum Transaktionssatz-Auftrag finden Sie unter [Konfigurieren des Transaktionssatz-Auftrags für einen Oracle-Verleger &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Veröffentlichungen mit Oracle (Übersicht)](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
