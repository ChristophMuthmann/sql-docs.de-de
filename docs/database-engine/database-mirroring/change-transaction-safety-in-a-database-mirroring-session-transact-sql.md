---
title: "Ändern der Transaktionssicherheit in einer Datenbank-Spiegelungssitzung (Transact-SQL) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 828a9d7c3bbb7ee46029bcc6bb81dab4477bcd6a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>Ändern der Transaktionssicherheit in einer Datenbank-Spiegelungssitzung (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die Transaktionssicherheit ist das Attribut, das den Betriebsmodus der Sitzung steuert. Der Datenbankbesitzer kann die Transaktionssicherheit jedoch jederzeit ändern. Standardmäßig ist die Sicherheitsstufe für Transaktionen auf FULL (synchroner Betriebsmodus) festgelegt.  
  
 Wird die Transaktionssicherheit deaktiviert, geht die Sitzung in den asynchronen Betriebsmodus über, in dem die Leistung maximiert wird. Falls der Prinzipal nicht mehr verfügbar ist, wird der Spiegel beendet, ist jedoch als betriebsbereit verfügbar (ein Failover erfordert das Erzwingen des Diensts bei möglichem Datenverlust).  
  
### <a name="to-turn-on-transaction-safety"></a>So aktivieren Sie die Transaktionssicherheit  
  
1.  Stellen Sie eine Verbindung mit dem Prinzipalserver her.  
  
2.  Führen Sie die folgende Transact-SQL-Anweisung aus:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     Dabei ist *\<database>* der Name der gespiegelten Datenbank.  
  
### <a name="to-turn-off-transaction-safety"></a>So deaktivieren Sie die Transaktionssicherheit  
  
1.  Stellen Sie eine Verbindung mit dem Prinzipalserver her.  
  
2.  Führen Sie die folgende Anweisung aus:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     Dabei ist *\<database>* die gespiegelte Datenbank.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE-Datenbankspiegelung &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  
