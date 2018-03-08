---
title: "Rechenkapazitätsgrenzen von bestimmten Editionen von SQL Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/06/2017
ms.prod: sql-server
ms.prod_service: sql-non-specified
ms.service: ssdt
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- processors [SQL Server], supported
- number of processors supported
- maximum number of processors supported
ms.assetid: cd308bc9-9468-40cc-ad6e-1a8a69aca6c8
caps.latest.revision: "60"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 02a5a436fdae6d9196359b36e72af3ffc11d2a87
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="compute-capacity-limits-by-edition-of-sql-server"></a>Rechenkapazitätsgrenzen von bestimmten Editionen von SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In diesem Artikel wird erläutert, wie Sie Kapazitätsgrenzen für Editionen von [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] berechnen und wie sie sich in physischen und virtualisierten Umgebungen mit Hyperthreaded-Prozessoren unterscheiden.  
  
 ![Zuordnungen zu Rechenkapazitätsgrenzen](../sql-server/media/compute-capacity-limits.gif "Mappings to compute capacity limits")  
  
 In dieser Tabelle werden die Schreibweisen im vorigen Diagramm beschrieben:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0..1|Null oder Eins|  
|1|Genau eins|  
|1..\*|Ein oder mehr|  
|0..\*|0 oder mehr|  
|1..2|Einer oder zwei|  
  
> [!IMPORTANT]  
> Weitere Details:  
>   
> - Ein virtueller Computer (VM) weist einen oder mehrere virtuelle Prozessoren auf.  
> - Ein oder mehrere virtuelle Prozessoren werden genau einem virtuellem Computer zugeordnet.  
> - 0 (null) oder ein virtueller Prozessor wird null oder mehreren logischen Prozessoren zugeordnet. Die Zuordnung virtueller Prozessoren zu logischen Prozessoren ist wie folgt: 
>     -   1:0 stellt einen ungebundenen logischen, von den Gastbetriebssystemen nicht verwendeten Prozessor dar.  
>     -   1:viele stellt einen Overcommit dar.  
>     -   0:viele stellt die Abwesenheit des virtuellen Computers auf dem Hostsystem dar. Also den Fall, dass virtuelle Computer keine logischen Prozessoren verwenden.  
> - Ein Socket wird null oder mehr Kernen zugeordnet. Die Zuordnung Socket zu Kern kann wie folgt sein:  
>     -   1:0 stellt einen leeren Socket dar. Es ist kein Chip installiert.  
>     -   1:1 stellt einen im Socket installierten Einzelkern-Chip dar. Diese Zuordnung ist heutzutage selten.  
>     -   1:viele stellt einen im Socket installierten Mehrkern-Chip dar. Typische Werte sind 2, 4 und 8.  
> - Ein Kern wird einem oder zwei logischen Prozessoren zugeordnet. Die Zuordnung von Kernen zu logischen Prozessoren ist wie folgt:  
>     -   1:1, Hyperthreading ist aus.  
>     -   1:2, Hyperthreading ist an.  
  
 Die folgenden Definitionen gelten für die in diesem Artikel verwendeten Begriffe:  
  
-   Ein Thread oder logischer Prozessor ist aus der Sicht von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bzw. aus der Sicht des Betriebssystems, einer Anwendung oder eines Treibers ein logisches Computermodul.  
  
-   Ein Kern ist eine Prozessoreinheit. Sie kann aus einem oder mehreren logischen Prozessoren bestehen.  
  
-   Ein physischer Prozessor kann aus einem oder mehreren Kernen bestehen. Ein physischer Prozessor ist das Gleiche wie ein Prozessorpaket oder ein Socket.  
  
Systeme mit mehr als einem physischen Prozessor oder Systeme mit physischen Prozessoren, die mehrere Kerne und/oder Hyperthreads haben, ermöglichen dem Betriebssystem, mehrere Tasks gleichzeitig auszuführen. Jeder Thread der Ausführung wird als logischer Prozessor angezeigt. Wenn Ihr Computer z.B. zwei Quad-Core-Prozessoren mit aktiviertem Hyperthreading und zwei Threads pro Kern aufweist, verfügen Sie über 16 logische Prozessoren: 2 Prozessoren x 4 Kernen pro Prozessor x 2 Threads pro Kern. Beachten Sie dabei Folgendes:  
  
-   Die Rechenkapazität eines logischen Prozessors von einem einzelnen Thread eines Hyperthread-Kerns ist geringer als die Rechenkapazität eines logischen Prozessors von diesem gleichen Kern mit deaktiviertem Hyperthreading.  
  
-   Die Rechenkapazität der zwei logischen Prozessoren im Hyperthread-Kern ist größer als die Rechenkapazität des gleichen Kerns mit deaktiviertem Hyperthreading.  
  
Jede Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] hat zwei Rechenkapazitätsgrenzen:  
  
- Die maximale Anzahl von Sockets (oder physischen Prozessoren oder Prozessorpaketen)  
  
- Die maximale Anzahl von Kernen, die vom Betriebssystem gemeldet wird  
  
Diese Begrenzungen gelten für eine einzelne Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sie stellen die maximale Rechenkapazität dar, die eine einzelne Instanz verwendet. Sie schränken den Server nicht ein, auf dem die Instanz möglicherweise bereitgestellt wird. Vielmehr stellt die Bereitstellung mehrerer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanzen auf demselben physischen Server eine effiziente Möglichkeit dar, die Rechenkapazität eines physischen Servers mit mehr Sockets und/oder Kernen zu nutzen, als es die Kapazitätsgrenzen zulassen.  
  
Die folgende Tabelle gibt die Rechenkapazitätsgrenzen für eine einzelne Instanz jeder Edition von [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]an:  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Edition|Maximale Rechenkapazität für eine einzelne Instanz ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)])|Maximale Rechenkapazität für eine einzelne Instanz (AS, RS)|  
|---------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
|Enterprise Edition: Core-basierte Lizenzierung\*|Maximum des Betriebssystems|Maximum des Betriebssystems|  
|Entwickler|Maximum des Betriebssystems|Maximum des Betriebssystems|  
|Standard|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|Beschränkt auf weniger als 4 Sockets oder 24 Kerne|  
|Express|Beschränkt auf weniger als 1 Socket oder 4 Kerne|Beschränkt auf weniger als 1 Socket oder 4 Kerne|  

\*Die Enterprise Edition mit einer Lizenzierung in Form von Serverlizenz + Clientzugriffslizenz (CAL) ist auf maximal 20 Kerne pro [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz beschränkt. (Diese Lizenzierung ist für neue Verträge nicht verfügbar.) Für das auf Prozessorkernen basierende Serverlizenzierungsmodell gelten keine Beschränkungen.  
  
In einer virtualisierten Umgebung beruht die Beschränkung der Rechenkapazität auf der Anzahl der logischen Prozessoren, nicht der Kerne. Dies hat den Grund, dass die Prozessorarchitektur für die Gastanwendungen nicht sichtbar ist. 

Ein Server mit vier Sockets beispielsweise, bestückt mit Quad-Core-Prozessoren und der Fähigkeit, zwei Hyperthreads pro Kern zu aktivieren, enthält mit aktiviertem Hyperthreading 32 logische Prozessoren. Er enthält jedoch mit deaktiviertem Hyperthreading nur 16 logische Prozessoren. Diese logischen Prozessoren können virtuellen Computern auf dem Server zugeordnet werden. Die Rechenlast der virtuellen Computers auf diesem logischen Prozessor wird einem Ausführungs-Thread auf dem physischen Prozessor im Hostserver zugeordnet.  
  
Es kann daher sinnvoll sein, Hyperthreading zu deaktivieren, wenn die Leistung der einzelnen virtuellen Prozessoren wichtig ist. Sie können das Hyperthreading mithilfe einer BIOS-Einstellung für den Prozessor während der BIOS-Einrichtung aktivieren oder deaktivieren. Normalerweise handelt es sich aber um einen Vorgang im Bereich des Servers, der alle auf dem Server ausgeführten Arbeitsauslastungen betrifft. Dies kann dafür sprechen, Arbeitsauslastungen, die in virtualisierten Umgebungen ausgeführt werden, von solchen zu trennen, die in einer physischen Betriebssystemumgebung von der Leistungssteigerung durch Hyperthreading profitieren würden.  
  
## <a name="see-also"></a>Siehe auch  
 [Editionen und Komponenten von SQL Server 2016](../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Spezifikationen der maximalen Kapazität für SQL Server](../sql-server/maximum-capacity-specifications-for-sql-server.md)   
 [Schnellstart-Installation von SQL Server 2016](http://msdn.microsoft.com/library/672afac9-364d-4946-ad5d-8a2d89cf8d81)  
  
  

