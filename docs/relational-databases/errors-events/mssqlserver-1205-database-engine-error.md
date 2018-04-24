---
title: MSSQLSERVER_1205 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3bab64d23dfa8e865061183d9565b96606b45ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1205"></a>MSSQLSERVER_1205
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1205|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|LK_VICTIM|  
|Meldungstext|Die Transaktion (Prozess-ID %d) befand sich auf %.*ls Ressourcen aufgrund eines anderen Prozesses in einer Deadlocksituation und wurde als Deadlockopfer ausgewählt. Führen Sie die Transaktion erneut aus.|  
  
## <a name="explanation"></a>Erklärung  
Durch separate Transaktionen wird in einer zu Konflikten führenden Reihenfolge auf Ressourcen zugegriffen, was zu einem Deadlock führt. Zum Beispiel:  
  
-   Transaction1 aktualisiert **Table1.Row1** und Transaction2 aktualisiert **Table2.Row2**.  
  
-   Transaction1 versucht **Table2.Row2** zu aktualisieren. Transaction1 wird jedoch blockiert, weil für Transaction2 noch kein Commit ausgeführt wurde.  
  
-   Nun versucht Transaction2, **Table1.Row1** zu aktualisieren. Transaction2 wird jedoch blockiert, weil für Transaction1 noch kein Commit ausgeführt wurde.  
  
-   Es kommt zu einem Deadlock, weil von Transaction1 auf die Beendigung von Transaction2 gewartet wird, während gleichzeitig von Transaction2 auf die Beendigung von Transaction1 gewartet wird.  
  
Dieser Deadlock wird vom System erkannt und eine der beteiligten Transaktionen als "Opfer" ausgewählt. Anschließend wird diese Meldung ausgegeben und für die Transaktion des Opfers ein Rollback ausgeführt.  
  
## <a name="user-action"></a>Benutzeraktion  
Führen Sie die Transaktion erneut aus. Sie können auch die Anwendung überarbeiten, um Deadlocks zu vermeiden. Die Transaktion, die als Opfer ausgewählt wurde, kann erneut ausgeführt werden und wird wahrscheinlich erfolgreich verlaufen, je nachdem, welche Vorgänge gleichzeitig ausgeführt werden.  
  
Wenn Sie Deadlocks verhindern oder vermeiden möchten, sollten alle Transaktionszugriffszeilen in derselben Reihenfolge (**Table1** und dann **Table2**) vorliegen. Auf diese Weise kann es zwar zum Blockieren kommen, ein Deadlock tritt jedoch nicht auf.  
  
