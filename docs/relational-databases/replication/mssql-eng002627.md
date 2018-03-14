---
title: MSSQL_ENG002627 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG002627 error
ms.assetid: 7f4136ac-3784-4a41-a98c-8a02308e4883
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b8971bc0f4dd889d59c15702851fe13c079d2e9
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="mssqleng002627"></a>MSSQL_ENG002627
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2627|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name|–|  
|Meldungstext|Verletzung der %1!s!-Einschränkung '%2!s!'. Ein doppelter Schlüssel kann nicht in das '%.\*ls'-Objekt eingefügt werden.|  
  
## <a name="explanation"></a>Erklärung  
 Das ist ein allgemeiner Fehler, der unabhängig davon ausgelöst werden kann, ob eine Datenbank repliziert wird. Bei replizierten Datenbanken wird der Fehler in der Regel ausgelöst, weil Primärschlüssel in der Topologie nicht richtig verwaltet wurden. In einer verteilten Umgebung muss unbedingt sichergestellt werden, dass in mehreren Knoten nicht der gleiche Wert in eine Primärschlüsselspalte oder eine andere eindeutige Spalte eingefügt wird. Die folgenden Ursachen können zugrunde liegen:  
  
-   Einfügungen und Updates an einer Zeile finden in mehreren Knoten statt. Die Mergereplikation und aktualisierbare Abonnements für Transaktionsreplikationen stellen jeweils eine Konflikterkennung und -lösung bereit. Dennoch ist es besser, eine bestimmte Zeile nur in einem Knoten einzufügen oder zu aktualisieren. Die Peer-zu-Peer-Transaktionsreplikation stellt keine Konflikterkennung und -lösung bereit. Einfügungen und Updates müssen partitioniert werden.  
  
-   Auf einem Abonnenten wurde eine Zeile eingefügt, die schreibgeschützt sein sollte. Abonnenten von Momentaufnahmeveröffentlichungen sollten als schreibgeschützt behandelt werden, ebenso wie Abonnenten von Transaktionsveröffentlichungen, außer es werden aktualisierbare Abonnements oder die Peer-zu-Peer-Transaktionsreplikation verwendet.  
  
-   Es wird eine Tabelle mit einer Identitätsspalte verwendet, die Spalte wird jedoch nicht ordnungsgemäß verwaltet.  
  
## <a name="user-action"></a>Benutzeraktion  
 Die erforderliche Aktion hängt davon ab, weshalb der Fehler ausgelöst wurde:  
  
-   Einfügungen und Updates an einer Zeile finden in mehreren Knoten statt.  
  
     Unabhängig vom Typ der verwendeten Replikation wird empfohlen, Einfügungen und Updates möglichst zu partitionieren, da dies den Verarbeitungsaufwand bei der Konflikterkennung und -lösung reduziert. Bei der Peer-zu-Peer-Transaktionsreplikation ist eine Partitionierung von Einfügungen und Updates erforderlich. Weitere Informationen finden Sie unter [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
-   Auf einem Abonnenten wurde eine Zeile eingefügt, die schreibgeschützt sein sollte.  
  
     Fügen Sie auf dem Abonnenten keine Zeilen ein und aktualisieren Sie keine Zeilen, es sei denn Sie verwenden die Mergereplikation, die Transaktionsreplikation mit aktualisierbaren Abonnements oder die Peer-zu-Peer-Transaktionsreplikation.  
  
-   Es wird eine Tabelle mit einer Identitätsspalte verwendet, die Spalte wird jedoch nicht ordnungsgemäß verwaltet.  
  
     Bei der Mergereplikation und der Transaktionsreplikation mit aktualisierbaren Abonnements sollten Identitätsspalten automatisch durch die Replikation verwaltet werden. Bei der Peer-zu-Peer-Transaktionsreplikation müssen sie manuell verwaltet werden. Weitere Informationen finden Sie unter [Replizieren von Identitätsspalten](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Mergereplikation](../../relational-databases/replication/merge/merge-replication.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Aktualisierbare Abonnements für die Transaktionsreplikation](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
