---
title: "Schreibgeschützte Verfügbarkeitsgruppen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d2d3eb4751cee7ab0258554f3b176b73a7cd12e5
ms.sourcegitcommit: c41e1bf5a53e96855b4424de4e0897153070bb28
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2017
---
# <a name="read-scale-availability-groups"></a>Schreibgeschützte Verfügbarkeitsgruppen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Eine Verfügbarkeitsgruppe ist eine umfassende Lösung, die hohe Verfügbarkeit für SQL Server bereitstellt und darüber hinaus integrierte Skalierungslösungen bietet. In einer typischen Datenbankanwendung führen mehrere Clients verschiedene Arten von Arbeitsauslastung aus. Manchmal können sich Engpässe aufgrund von Ressourceneinschränkungen entwickeln. Sie können Ressourcen freigeben und einen höheren Durchsatz für den OLTP-Workload erreichen. Ferner können Sie höhere Leistung und Skalierung für schreibgeschützte Workloads bereitstellen. Nutzen Sie dazu die schnellste Technologie zur Replikation für SQL Server, und erstellen Sie eine Gruppe replizierter Datenbanken, um die Berichterstellung und Analyseworkloads in schreibgeschützte Replikate auszulagern. 

Mit Verfügbarkeitsgruppen kann mindestens ein sekundäres Replikat so konfiguriert werden, dass es den schreibgeschützten Zugriff auf sekundäre Datenbanken unterstützt.

Die Clientanwendungen, die Analysen durchführen oder Berichte zu Workloads erstellen, können eine direkte Verbindung mit sekundären Datenbanken herstellen. Ferner können Sie eine schreibgeschützte Routingliste einrichten und diese mit der primären Datenbank verbinden. Diese leitet dann die Verbindungsanforderung in Round-Robin-Manier an jedes der in der Routingliste enthaltenen sekundären Replikate weiter.

## <a name="read-scale-availability-groups-without-cluster"></a>Schreibgeschützte Verfügbarkeitsgruppen ohne Cluster

In [!INCLUDE[sssql15-md](..\..\..\includes\sssql15-md.md)] und früher war für alle Verfügbarkeitsgruppen ein Cluster erforderlich. Der Cluster hat für Geschäftskontinuität gesorgt: Hochverfügbarkeit und Notfallwiederherstellung (HADR). Darüber hinaus wurden für Lesevorgänge sekundäre Replikate konfiguriert. Wenn hohe Verfügbarkeit nicht das eigentliche Ziel darstellte, bedeuteten die Konfiguration und der Betrieb eines Clusters einen erheblichen Mehraufwand im Betrieb. SQL Server 2017 führt schreibgeschützte Verfügbarkeitsgruppen ohne Cluster ein. 

Wenn es eine Unternehmensanforderung ist, die Ressourcen unternehmenskritischer Workloads aufrechtzuerhalten, die auf dem primären Replikat ausgeführt werden, können Sie jetzt das schreibgeschützte Routing verwenden oder eine direkte Verbindung zu lesbaren sekundären Replikaten herstellen. Sie müssen sich nicht auf die Integration von Clustertechnologie einlassen. Diese Funktionen sind für SQL Server 2017 unter Windows- und Linux-Plattformen verfügbar.

>[!IMPORTANT]
>Dabei handelt es sich nicht um eine Einrichtung mit hoher Verfügbarkeit. Es gibt keine Infrastruktur zur Überwachung und Koordinierung der Fehlererkennung und eines automatischen Failovers. Ohne einen Cluster kann SQL Server nicht die niedrige Zielsetzung für die Wiederherstellungszeit (RTO, Recovery time objective) gewährleisten, die eine automatisierte Hochverfügbarkeitslösung bereitstellt. Wenn Sie hohe Verfügbarkeit benötigen, verwenden Sie einen Cluster-Manager (Windows Server Failover Clustering unter Windows oder Pacemaker unter Linux). 
>
>Die schreibgeschützte Verfügbarkeitsgruppe kann Funktionen für die Notfallwiederherstellung bereitstellen. Wenn sich die schreibgeschützten Replikate im synchronen Commitmodus befinden, bieten diese eine RPO (Recovery point objective) von 0 (null). Weitere Informationen zum Ausführen eines Failovers einer schreibgeschützten Verfügbarkeitsgruppe finden Sie unter [Ausführen eines Failovers des primären Replikats auf einer schreibgeschützten Verfügbarkeitsgruppe](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md#ReadScaleOutOnly).

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>Verwenden Sie für geografischen Schreibschutz verteilte Verfügbarkeitsgruppen

Geografisch getrennte Lösungen können schreibgeschützte Lösungen mit verteilten Verfügbarkeitsgruppen implementieren. Sie können sie zum Abladen von Leseworkloads von primären Replikaten in lesbare sekundäre Replikate und an Orten verwenden, die der Quelle der Leseworkload näher sind. Durch verteilte Verfügbarkeitsgruppen wird die Ressourcenauslastung für das primäre Replikat verringert. Sie sind auch im Hinblick auf den Lesedurchsatz nützlich, indem sie die Netzwerklatenz verringern und dedizierte Ressourcen nutzen.

Eine einzelne verteilte Verfügbarkeitsgruppe kann bis zu 17 lesbare sekundäre Replikate ausweisen. Für eine erhöhte Skalierbarkeit können Sie mehrere Verfügbarkeitsgruppen miteinander verketten, um die Anzahl an lesbaren Replikaten noch weiter zu erhöhen. Darüber hinaus können Sie zwei verteilte Verfügbarkeitsgruppen aus der gleichen Verfügbarkeitsgruppe für Lesevorgänge mit geringer Wartezeit in geografisch verteilten Umgebungen bereitstellen.




## <a name="next-steps"></a>Nächste Schritte 

[Konfigurieren von schreibgeschützten Verfügbarkeitsgruppen unter Linux](../../../linux/sql-server-linux-availability-group-configure-rs.md)

## <a name="see-also"></a>Siehe auch 
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) 
  
  
