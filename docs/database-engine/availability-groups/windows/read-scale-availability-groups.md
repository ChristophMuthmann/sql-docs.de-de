---
title: "Schreibgeschützte Verfügbarkeitsgruppen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/24/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c607ab320a7deb80fb140ee9f4cc25b798b7fc4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="read-scale-availability-groups"></a>Schreibgeschützte Verfügbarkeitsgruppen
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Nicht nur dass eine Verfügbarkeitsgruppe die besten HA-Funktionen für SQL Server in sich vereint, sie ist auch eine flächendeckende Lösung, die zudem integrierte Skalierungslösungen bietet. In einer typischen Datenbankanwendung gibt es mehrere Client, die verschiedene Typen von Workloads ausführen und die manchmal durch Ressourceneinschränkungen zu Engpässen führen. Sie können Ressourcen verfügbar machen und einen höheren Durchsatz für die OLTP-Workload erzielen oder eine höhere Leistung und Skalierung für schreibgeschützte Workloads. Dies können Sie erreichen, indem Sie die schnellste Technologie zur Replikation für SQL Server einsetzen: Erstellen Sie eine Gruppe replizierter Datenbanken, um die Berichterstellung und Analyseworkloads in schreibgeschützte Replikate auszulagern. 

Mit Verfügbarkeitsgruppen kann mindestens ein sekundäres Replikat so konfiguriert werden, dass es den schreibgeschützten Zugriff auf sekundäre Datenbanken unterstützt.

Die Clientanwendungen, die Analysen durchführen oder Berichte zu Workloads erstellen, können eine direkte Verbindung mit der sekundären Datenbank herstellen. Der Kunde kann auch eine schreibgeschützte Routingliste einrichten und eine Verbindung zur primären Datenbank herstellen, die dann die Verbindungsanforderung an jedes der sekundären Replikate aus der Routingliste im Roundrobinverfahren weiterleitet.

## <a name="read-scale-availability-groups-without-cluster"></a>Schreibgeschützte Verfügbarkeitsgruppen ohne Cluster

In [!INCLUDE[sssql15-md](..\..\..\includes\sssql15-md.md)] und früher war ein Cluster für alle Verfügbarkeitsgruppen erforderlich. Der Cluster hat für Geschäftskontinuität gesorgt: Hochverfügbarkeit und Notfallwiederherstellung (HADR). Darüber hinaus konnten sekundäre Replikate für Lesevorgänge konfiguriert werden. Das Konfigurieren und Betreiben eines Clusters kam mit hohem operativem Aufwand, wenn es nicht die hohe Verfügbarkeit zum Ziel hatte. SQL Server 2017 führt schreibgeschützte Verfügbarkeitsgruppen ohne Cluster ein. 

Wenn es eine Unternehmensanforderung ist, die Ressourcen unternehmenskritischer Workloads aufrechtzuerhalten, die auf dem primären Replikat ausgeführt werden, können Benutzer jetzt das schreibgeschützte Routing verwenden oder eine direkte Verbindung zu lesbaren sekundären Replikaten herstellen, ohne dass eine Abhängigkeit von der Integration in eine Clustertechnologie besteht. Diese Funktionen sind für SQL Server 2017 unter Windows- und Linux-Plattformen verfügbar.

>[!IMPORTANT]
>Dabei handelt es sich nicht um eine Einrichtung mit hoher Verfügbarkeit. Es gibt keine Infrastruktur zur Überwachung und Koordinierung der Fehlererkennung und eines automatischen Failovers. Ohne ein Cluster kann SQL Server nicht die niedrige Zielsetzung für die Wiederherstellungszeit (RTO, Recovery time objective) gewährleisten, die eine automatisierte Hochverfügbarkeitslösung bereitstellt. Verwenden Sie für Benutzer, die Hochverfügbarkeitsfunktionen benötigen, einen Cluster-Manager (WSFC unter Windows oder Pacemaker unter Linux). 
>
>Die schreibgeschützte Verfügbarkeitsgruppe kann Funktionen für die Notfallwiederherstellung bereitstellen. Wenn sich die schreibgeschützten Replikate im synchronen Commitmodus befinden, bieten diese eine RPO (Recovery point objective) von 0 (null). Weitere Informationen zum Ausführen eines Failovers einer schreibgeschützten Verfügbarkeitsgruppe finden Sie unter [Ausführen eines Failovers des primären Replikats auf schreibgeschützten Verfügbarkeitsgruppen](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md#ReadScaleOutOnly).

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>Verwenden Sie für geografischen Schreibschutz verteilte Verfügbarkeitsgruppen

Geografisch getrennte Lösungen können schreibgeschützte Lösungen mit verteilten Verfügbarkeitsgruppen implementieren. Dadurch ist das Abladen von Leseworkloads von primären Replikaten in lesbare sekundäre Replikate und in Orten möglich, die der Quelle der Leseworkload näher sind. Dadurch wird nicht nur die Auslastung von Ressourcen in der primären Datenbank reduziert, sondern der Lesedurchsatz wir verbessert, indem die Wartezeit des Netzwerks reduziert und dedizierte Ressourcen genutzt werden.

Eine einzelne verteilte Verfügbarkeitsgruppe kann bis zu 17 lesbare sekundäre Replikate ausweisen. Für eine erhöhte Skalierbarkeit können Sie mehrere Verfügbarkeitsgruppen miteinander verketten und die Zahl an lesbaren Replikaten noch weiter erhöhen. Darüber hinaus können Sie zwei verteilte Verfügbarkeitsgruppen aus der gleichen Verfügbarkeitsgruppe für Lesevorgänge mit geringer Wartezeit in geografisch verteilten Umgebungen bereitstellen.




## <a name="next-steps"></a>Nächste Schritte 

[Konfigurieren von schreibgeschützten Verfügbarkeitsgruppen unter Linux](../../../linux/sql-server-linux-availability-group-configure-rs.md)

## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
