---
title: Analytics Platform System-Hardwarekomponenten
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Analytics Platform System (APS) verwendet skalierbare Komponenten, sodass Sie die richtige Menge an Verarbeitungs- und Ihren geschäftsanforderungen entsprechend erwerben können.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: aa1cdcc7-cfee-4658-bbce-7d319bfb7483
caps.latest.revision: 17
ms.openlocfilehash: 4b972c4b926463a67588c4ee41ed0157da7cdc80
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="analytics-platform-system-hardware-components"></a>Analytics Platform System-Hardwarekomponenten

Analytics Platform System (APS) verwendet skalierbare Komponenten, sodass Sie die richtige Menge an Verarbeitungs- und Ihren geschäftsanforderungen entsprechend erwerben können. Wenn Sie APS bestellen, benötigen Sie eine Kombination aus diesen Hardware-Kernkomponenten. Bestimmte Hardwarehersteller möglicherweise verschiedene Benennungskonventionen verwenden oder über zusätzliche Komponenten.  
 
  
## <a name="rackandnetwork"></a>Gestell eingesetzt ist und Netzwerk 
 
APS-Komponenten werden alle in einem oder mehreren Racks gespeichert, die in Ihrem Rechenzentrum passen. Jedes Rack enthält zwei InfiniBand-Switches, Stromverteilereinheiten (PDUs) und zwei Ethernet-Switches.  
  
![Gestell eingesetzt ist und Netzwerk](media/rack-and-network.png "APS-Rack Einbauen und Netzwerk")  
  
## <a name="datascaleunit"></a>Daten-Skalierungseinheit
 
Eine Daten-Skalierungseinheit enthält Daten Hosts und direkt angeschlossener Speicher (DAS) zum Verarbeiten und speichern Benutzerdaten. Zum Hinzufügen von Kapazität fügen Sie Daten Skalierungseinheiten entsprechend den Konfigurationen, die von Ihrem Hardwarehersteller unterstützt werden. Mit steigender Anzahl der Skalierungseinheiten Daten müssen Sie zusätzliche Rack hinzufügen & Netzwerkkomponenten sowie nach Bedarf, um weitere bereitzustellen Stromversorgung, Netzwerk und rack-Infrastruktur.  
  
### <a name="data-host"></a>Daten-host  

Ein Daten-Host ist eine zum Verarbeiten von Benutzerdaten dedizierte Server. Parallel Data Warehouse (PDW) einem Compute-Knoten, die auf jedem Host Daten ausgeführt wird. Die Skalierungseinheit Daten hat HPE Appliances zwei Data-Hosts. Dell und Quanta Einheiten hat die Skalierungseinheit Daten drei Data-Hosts.  
  
### <a name="direct-attached-storage"></a>Direkt angeschlossener Speicher
 
Den direkte angeschlossenen Speicher (DAS) ist ein Pool von Datenträgern, die mit den Daten Hosts verbunden sind. Aller Hosts Daten können auf beliebigen Datenträgern zugreifen. Als Teil der shared-Nothing-Architektur, die Compute-Knoten, die auf den Hosts Daten ausgeführt einzelne Datenträger nicht freigeben. Allerdings für hohe Verfügbarkeit der Speicherzugriff freigegeben ist, und jeden Host Daten kann auf beliebigen Datenträgern zugreifen.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>Skalierung Einheit Datenarchitektur - DELL und Quanta
  
![Skalierbarkeitseinheit](media/scalability-unit-dell.png "Dell skalierbarkeitseinheit")  
  
### <a name="data-scale-unit-architecture---hpe"></a>Data-Architektur Einheit skalieren - HPE 
 
![HPE skalierbarkeitseinheit](media/scalability-unit-hpe.png "HPE skalierbarkeitseinheit")  
  
### <a name="data-scale-unit-description"></a>Datenbeschreibung Skalierung-Einheit

Eine Skalierungseinheit für Daten muss ein Server (Host) für jeden Knoten Compute und einen direkt angeschlossenen Datenträger-Array, das mit Serial Attached SCSI (SAS) angeschlossen ist. In der CAB-Speicher ist die Datenträgergruppe in zwei Hälften unterteilt, redundante Stromversorgungen aufweisen. Windows Server-Speicherplätze verwaltet Benutzerdaten durch Duplizieren von Daten über RAID 1 gespiegelte Datenträger-Paare. Die Datenträger in jedes Paar Datenträger werden in verschiedenen Hälften der Laufwerkgruppe gespeichert.  
  
Die Datenträgergruppe enthält auch hot-spare-Laufwerke und eine Systemdatenträger. Bei Ausfall eines Datenträgers verwendet Speicherplätze die intakten Kopie der Daten auf dem Datenträger funktioniert so erstellen Sie eine Kopie der Daten auf einen hot-Spare neu an. Dies ist eine wichtige Selbstheilende-Funktion, die trägt zum Schutz vor Datenverlust.  
  
Die Gesamtanzahl der Datenträger für die Serverknoten:  
  
-   DELL ist 96 Festplatten = (3 Server) * (16 Datenträger pro Server) \* (für redundante Datenträger 2).  
  
-   HPE umfasst 64 Datenträger = (2 Server) * (16 Datenträger pro Server) \* (für redundante Datenträger 2).  
  
-   Darüber hinaus weist jede Laufwerkgruppe hot-spare-Laufwerke und eine Systemdatenträger.  
  
**Für hohe Verfügbarkeit**, wenn ein Knoten Failover Compute funktionieren weiterhin und Zugriff auf ihre Benutzerdaten über die anderen Hosts in den Daten-Skalierungseinheit kann. Mindestens eines direkt angeschlossenen physischen Hosts ausgeführt werden muss, oder den Datenzugriff auf den Speicher verloren gegangen ist.  
  
**Für Datenträgergrößen**, 1, 2 oder 3 Terabyte-Laufwerke direkte angeschlossener Speicher möglich. Alle Daten Skalierungseinheiten müssen die Datenträger mit derselben Größe zu vorhanden sein.  
  
## <a name="basescaleunit"></a>Grundlegende Skalierungseinheit 
 
Die Basis-Skalierungseinheit enthält die minimale Anzahl von Brain-Power-Hosts, Daten-Hosts und direkt angeschlossener Speicher, der für die Anwendung erforderlich ist. Es umfasst folgende Komponenten.  
  
### <a name="orchestration-host"></a>orchestrierungshost  
Dieser Server führt des Gehirns PDW.
  
### <a name="passive-host"></a>passive host  
Dieser Server bietet eine hohe Verfügbarkeit. Es ist online und zum Ausführen von Aufträgen im Fall ein Fehlers auf die Orchestrierung oder den Zielhost von Daten bereit. Orchestrierungshost, passive Host- und Daten skalieren Einheit Server werden als ein Windows-Failovercluster konfiguriert. Jedes Rack in die Anwendung erfordert eine passive Host.  
  
### <a name="optional-passive-host"></a>Optionale passiven host  
Um Redundanz Weitere hinzufügen zu können, müssen Sie die Option zum Hinzufügen eines zweiten passiven Hosts auf der Basis-Skalierungseinheit.  
  
### <a name="data-scale-unit"></a>Daten-Skalierungseinheit  
Die Basis-Skalierungseinheit umfasst einen Daten-Skalierungseinheit das am unteren Rand der Rack platziert wird.  
  
Dieses Diagramm zeigt die Basis-Skalierungseinheit sowie das Gestell eingesetzt ist und Netzwerk. Dies ist die minimale Konfiguration für eine Einheit Analytics Platform System.  
  
![Grundlegende Skalierungseinheit](media/base-scale-unit.png "Base-Skalierungseinheit")  
 
