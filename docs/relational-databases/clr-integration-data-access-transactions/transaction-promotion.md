---
title: "Transaktionshöherstufung | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f37528588c5d302036bb39d3de4349c44120e86f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="transaction-promotion"></a>Transaktionshöherstufung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Transaktion *heraufstufung* beschreibt eine lokale Transaktion, die zu einer vollständig verteilbaren Transaktion automatisch heraufgestuft werden kann, nach Bedarf. Wird in einer Datenbanktransaktion auf dem Server eine verwaltete gespeicherte Prozedur aufgerufen, wird der CLR-Code (Common Language Runtime, CLR) im Kontext einer lokalen Transaktion ausgeführt.  Wenn in der Datenbanktransaktion eine Verbindung zu einem Remoteserver geöffnet wird, wird die Verbindung in die verteilte Transaktion eingetragen, und die lokale Transaktion wird automatisch zu einer verteilten Transaktion höhergestuft. Dies bedeutet, dass durch die Transaktionhöherstufung der Verarbeitungsaufwand von verteilten Transaktionen reduziert wird, indem diese erst dann erstellt werden, wenn sie gebraucht werden. Die Transaktionshöherstufung ist automatisch, falls diese mithilfe des **Enlist** -Schlüsselworts aktiviert wurde und kein Eingriff seitens des Entwicklers erforderlich ist. Die .NET Framework-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet Unterstützung für die transaktionshöherstufung über die Klassen in .NET Framework **System.Data.SqlClient** Namespace.  
  
## <a name="the-enlist-keyword"></a>Das 'Enlist'-Schlüsselwort  
 Die **ConnectionString** -Eigenschaft eines **SqlConnection** -Objekts unterstützt das **Enlist** -Schlüsselwort, welches angibt, ob **System.Data.SqlClient** den Transaktionskontext erkennt und die Verbindung automatisch in eine verteilte Transaktion einträgt. Wenn für dieses Schlüsselwort true festgelegt wird, wird die Verbindung automatisch im aktuellen Transaktionskontext des öffnenden Threads eingetragen. Wenn für dieses Schlüsselwort false festgelegt wird, interagiert die SqlClient-Verbindung nicht mit einer verteilten Transaktion. Wenn das **Enlist** -Schlüsselwort nicht in der Verbindungszeichenfolge angegeben wird, wird die Verbindung automatisch in eine verteilte Transaktion eingetragen, falls zum Zeitpunkt des Öffnens der Verbindung eine verteilte Transaktion erkannt wurde.  
  
## <a name="distributed-transactions"></a>Verteilte Transaktionen  
 Verteilte Transaktionen nehmen normalerweise beträchtliche Systemressourcen in Anspruch. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) verwaltet diese Transaktionen und integriert alle Ressourcen-Manager, auf die in den Transaktionen zugegriffen wird. Transaktionshöherstufung, auf der anderen Seite ist eine besondere Form einer **System.Transactions** Transaktion, die effektiv die Arbeit in eine einfache delegiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Transaktion. **System.Transactions**, **System.Data.SqlClient**, und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] koordinieren die Arbeit zur Behandlung der Transaktions, die auf eine vollständig verteilte Transaktion Stufen sie bei Bedarf.  
  
 Der Vorteil der Verwendung der Transaktionshöherstufung liegt darin, dass beim Öffnen einer Verbindung, die eine aktive **TransactionScope** -Transaktion aufweist, diese Transaktion als "leichtgewichtige" Transaktion agiert, wenn keine anderen Verbindungen geöffnet sind, anstatt als verteilte Transaktion zusätzliche Ressourcen zu verbrauchen. Weitere Informationen zu **TransactionScope**, finden Sie unter [mithilfe von System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md).  
  
## <a name="see-also"></a>Siehe auch  
 [CLR-Integration und -Transaktionen](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
