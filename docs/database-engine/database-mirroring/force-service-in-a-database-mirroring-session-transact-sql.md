---
title: Erzwingen des Diensts in einer Datenbank-Spiegelungssitzung (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- forced service [SQL Server]
- database mirroring [SQL Server], forcing service
ms.assetid: 8b6ffe77-35f3-4e2a-a658-8a38a8e1c794
caps.latest.revision: 40
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a4eb1bfb3302d7ca5feeec1467315d26078a078
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="force-service-in-a-database-mirroring-session-transact-sql"></a>Erzwingen des Diensts in einer Datenbank-Spiegelungssitzung (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Wenn der Prinzipalserver im Modus für hohe Leistung und im Modus für hohe Sicherheit ohne automatisches Failover ausfällt, der Spiegelserver jedoch zur Verfügung steht, kann der Datenbankbesitzer die Datenbank verfügbar machen, indem er ein Failover des Diensts auf die Spiegeldatenbank (bei möglichem Datenverlust) erzwingt. Diese Option steht nur zur Verfügung, wenn alle der folgenden Bedingungen erfüllt sind:  
  
-   Der Prinzipalserver ist ausgefallen.  
  
-   WITNESS ist auf OFF festgelegt oder ist mit dem Spiegelserver verbunden.  
  
> [!CAUTION]  
>  Das Erzwingen des Diensts ist eine Methode, die ausschließlich der Wiederherstellung in einem Notfall dient. Das Erzwingen des Diensts kann Datenverluste zur Folge haben. Sie sollten den Dienst daher nur erzwingen, wenn Sie bereit sind, Datenverluste in Kauf zu nehmen, um den Dienst für die Datenbank unverzüglich wiederherzustellen. Wenn es beim Erzwingen des Diensts zum Verlust wichtiger Daten kommen kann, wird empfohlen, die Spiegelung zu beenden und die Datenbanken manuell neu zu synchronisieren. Weitere Informationen zu den Risiken beim Erzwingen des Diensts finden Sie unter [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 Durch das Erzwingen des Diensts wird die Sitzung angehalten und ein neuer Wiederherstellungszweig gestartet. Die Auswirkungen aus dem Erzwingen des Diensts sind vergleichbar mit dem Entfernen der Spiegelung und dem Wiederherstellen der vorherigen Prinzipaldatenbank. Durch das Erzwingen des Diensts wird jedoch das erneute Synchronisieren der Datenbanken (bei möglichem Datenverlust) vereinfacht, wenn die Spiegelung fortgesetzt wird.  
  
### <a name="to-force-service-in-a-database-mirroring-session"></a>So erzwingen Sie den Dienst in einer Datenbank-Spiegelungssitzung  
  
1.  Stellen Sie eine Verbindung zum Spiegelserver her.  
  
2.  Führen Sie die folgende Anweisung aus:  
  
     ALTER DATABASE *<database_name>* SET PARTNER FORCE_SERVICE_ALLOW_DATA_LOSS  
  
     Dabei ist *<database_name>* die gespiegelte Datenbank.  
  
     Der Spiegelserver wird unverzüglich zum Prinzipalserver, und die Spiegelung wird unterbrochen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  
