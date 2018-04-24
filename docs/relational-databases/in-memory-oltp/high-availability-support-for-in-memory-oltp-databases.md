---
title: Unterstützung für Hochverfügbarkeit für In-Memory OLTP-Datenbanken | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79a681b5ba221049155992283f349dea347e40f7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>Unterstützung für Hochverfügbarkeit für In-Memory OLTP-Datenbanken
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Datenbanken mit speicheroptimierten Tabellen mit bzw. ohne systemeigene kompilierte gespeicherte Prozeduren werden mit AlwaysOn-Verfügbarkeitsgruppen vollständig unterstützt.  Es gibt keinen Unterschied in Konfiguration und Unterstützung zwischen Datenbanken mit [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Objekten und solchen ohne diese Objekte.  
  
 Wenn in der Konfiguration einer AlwaysOn-Verfügbarkeitsgruppe eine In-Memory-OLTP-Datenbank bereitgestellt wird, werden bei Anwendung von REDO Änderungen an speicheroptimierten Tabellen auf dem primären Replikat im Arbeitsspeicher auf die Tabellen auf den sekundären Replikaten angewendet. Dies bedeutet, dass ein Failover zu einem sekundären Replikat sehr schnell erfolgen kann, da sich die Daten bereits im Arbeitsspeicher befinden. Darüber hinaus stehen die Tabellen für Abfragen auf sekundären Replikaten, die für den Lesezugriff konfiguriert wurden, zur Verfügung.  
  
## <a name="always-on-availability-groups-and-in-memory-oltp-databases"></a>AlwaysOn-Verfügbarkeitsgruppen und In-Memory OLTP-Datenbanken  
 Die Konfiguration von Datenbanken mit [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Komponenten ermöglicht Folgendes:  
  
-   **Eine vollständig integrierte Lösung**   
    Sie können Ihre Datenbanken mit speicheroptimierten Tabellen unter Verwendung des gleichen Assistenten mit der gleichen Ebene der Unterstützung für synchrone und asynchrone sekundäre Replikate konfigurieren. Darüber hinaus erfolgt die Systemüberwachung über das vertraute AlwaysOn-Dashboard in SQL Server Management Studio.  
  
-   **Vergleichbare Failoverzeit**   
    Sekundäre Replikate behalten den im Speicher enthaltenen Status der dauerhaften speicheroptimierten Tabellen. Beim automatischen oder erzwungenen Failover ist die Failoverzeit auf dem neuen primären Replikat mit der für datenträgerbasierte Tabellen vergleichbar, da keine Wiederherstellung notwendig ist. Speicheroptimierte Tabellen, die als SCHEMA_ONLY erstellt wurden, werden in dieser Konfiguration unterstützt. Änderungen an diesen Tabellen werden jedoch nicht protokolliert. Deshalb sind in diesen Tabellen keine Daten auf dem sekundären Replikat vorhanden.  
  
-   **Lesbares sekundäres Replikat**   
    Sie können auf speicheroptimierte Tabellen auf dem sekundären Replikat zugreifen und sie abfragen, wenn es für Lesezugriff konfiguriert ist. In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]ist der Lese-Zeitstempel auf dem sekundären Replikat eng mit dem Lese-Zeitstempel auf dem primären Replikat synchronisiert. Änderungen auf dem primären Replikat werden daher sehr schnell auf dem sekundären Replikat sichtbar. Diese enge Synchronisierung unterscheidet sich vom [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] -In-Memory OLTP.  
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>Failoverclustering-Instanz (FCI) und In-Memory OLTP-Datenbanken  
 Um in einer Konfiguration mit freigegebenem Speicher Hochverfügbarkeit zu erreichen, können Sie das Failoverclustering für Instanzen mit mindestens einer Datenbank mit speicheroptimierten Tabellen einrichten. Beim Einrichten einer FCI müssen Sie die folgenden Faktoren berücksichtigen:  
  
-   **Wiederherstellungszeit-Zielsetzung**   
    Die Failoverzeit wird wahrscheinlich höher sein, da speicheroptimierte Tabellen in den Arbeitsspeicher geladen werden müssen, bevor die Datenbank verfügbar gemacht wird.  
  
-   **SCHEMA_ONLY-Tabellen**   
    Beachten Sie, dass SCHEMA_ONLY-Tabellen nach dem Failover ohne Zeilen, also leer sind. Dies ist so von der Anwendung definiert. Es ist genau das gleiche Verhalten wie beim Neustart einer [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Datenbank mit SCHEMA_ONLY-Tabellen.  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>Unterstützung für Transaktionsreplikation in In-Memory OLTP  
 Die Tabellen, die als Transaktionsreplikationsabonnenten fungieren, können (mit Ausnahme der Peer-zu-Peer-Transaktionsreplikation) als speicheroptimierte Tabellen konfiguriert werden. Andere Replikationskonfigurationen sind mit speicheroptimierten Tabellen nicht kompatibel.  Weitere Informationen finden Sie unter [Replikation mit Abonnenten von speicheroptimierten Tabellen](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Always On-Verfügbarkeitsgruppen (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Aktive sekundäre Replikate: Lesbare sekundäre Replikate (AlwaysOn-Verfügbarkeitsgruppen)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Replikation mit Abonnenten von speicheroptimierten Tabellen](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
