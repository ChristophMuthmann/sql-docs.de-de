---
title: Wichtige Änderungen an Funktionen des Datenbankmoduls in SQL Server 2016 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/15/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
caps.latest.revision: 144
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9af073b3040ff6d821d9cbbba52640559fd1f145
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>Fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden wichtige Änderungen in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] und den früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]beschrieben. Diese Änderungen können u. U. zur Funktionsunfähigkeit von Anwendungen, Skripts oder Funktionen führen, die auf früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]basieren. Diese Probleme können nach einem Upgrade auftreten.  
  
##  <a name="SQL15"></a> Wichtige Änderungen in [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
-   Die Spalte sample_ms von sys.dm_io_virtual_file_stats wurde aus einem **int** - zu einem **bigint** -Datentyp erweitert.  
  
-   Die Spalte TimeStamp von sys.fn_virtualfilestats wurde aus einem **int** - zu einem **bigint** -Datentyp erweitert.  

-   Mithilfe der Hashalgorithmen MD2, MD4, MD5, SHA und SHA1 (nicht empfohlen) erfordert die Einstellung des Datenbankkompatibilitätsgrads auf früher als Versionsnummer 130.  

-   Unter dem Datenbankkompatibilitätsgrad 130 ergibt sich bei einer impliziten Konvertierung aus dem Datentyp **datetime** in den Datentyp **datetime2** eine verbesserte Genauigkeit, indem die Bruchteile von Millisekunden berücksichtigt werden, wodurch sich unterschiedliche konvertierte Werte ergeben. Verwenden Sie explizite Umwandlung in den Datentyp „datetime2“, wenn ein Vergleich so gestaltet ist, dass zwischen den Datentypen „datetime“ und „datetime2“ verglichen wird. Weitere Informationen finden Sie im folgenden [Microsoft-Support-Artikel](http://support.microsoft.com/help/4010261).
  
## <a name="previous-versions"></a>Vorgängerversionen  
  
-   [Fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2014](https://msdn.microsoft.com/library/ms143179\(v=sql.120\))  
  
-   [Fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2012](https://msdn.microsoft.com/library/ms143179\(v=sql.110\))  
  
-   [Fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2008](https://msdn.microsoft.com/library/ms143179\(v=sql.100\))  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Als veraltet markierte Funktionen des Datenbankmoduls in SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Nicht mehr unterstützte Datenbankmodul-Funktionalität in SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Abwärtskompatibilität des SQL Server-Datenbankmoduls](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [SQL Server 2016 or SQL Server 2017 on Windows improvements in handling some data types and uncommon operations (Verbesserungen der Verarbeitung einiger Datentypen und ungewöhnlicher Vorgänge für SQL Server 2016 oder SQL Server 2017 unter Windows)](http://support.microsoft.com/help/4010261).
  
  
