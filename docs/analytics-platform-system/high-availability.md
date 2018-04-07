---
title: Analytics Platform System hohe Verfügbarkeit
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
description: Beschreibt, wie das Analytics Platform System (APS) für hohe Verfügbarkeit ausgelegt ist.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 5ab245e9-0316-4d25-a626-4745ce856925
caps.latest.revision: 9
ms.openlocfilehash: 9fd057a4cd673f06034e0093ca93be7ceaf345ea
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="analytics-platform-system-high-availability"></a>Analytics Platform System hohe Verfügbarkeit
Beschreibt, wie das Analytics Platform System (APS) für hohe Verfügbarkeit ausgelegt ist.  
  
## <a name="high-availability-architecture"></a>Hohe Verfügbarkeit-Architektur  
![Anwendungsarchitektur](media/appliance-architecture.png "Anwendungsarchitektur")  
  
## <a name="network"></a>Netzwerk  
Netzwerkverfügbarkeit hat die APS-Appliance zwei InfiniBand-Netzwerke. Wenn eines der InfiniBand-Netzwerke ausfällt, ist der andere Controller weiterhin verfügbar. Darüber hinaus wurde Active Directory-Domänencontroller, um eingehende Anforderungen an das richtige InfiniBand-Netzwerk zu beheben repliziert.  
  
Weitere Informationen finden Sie unter [konfigurieren InfiniBand-Netzwerkadapter](configure-infiniband-network-adapters.md).  
  
## <a name="storage"></a>Speicherung  
Um Daten zu schützen, verwendet die APS RAID 1-Spiegelung, um zwei Kopien der Daten für alle Benutzer zu verwalten. Wenn ein Datenträgerfehler auftritt, wird das Hardwaresystem wird neu erstellt die Daten auf ein Hotspare-Laufwerk und legt eine Warnung, dass ein Fehler auf dem Datenträger vorhanden ist.  
  
Um verfügbaren Daten online zu halten, verwendet APS Speicherplätze und freigegebener Clustervolumes, um die Datenträger für die Daten in den direkt angeschlossenen Speicher zu verwalten. Es ist ein Speicherpool pro Daten Skalierungseinheit, die in freigegebenen Clustervolumes, die Compute-Knoten-Hosts über Bereitstellungspunkte zur Verfügung stehen organisiert.  
  
Um sicherzustellen, dass der Speicherpool online bleibt, hat jeder einzelne Host in der Skalierungseinheit für Daten einen iSCSI-virtuellen Computer, der kein Failover durchgeführt wird. Diese Architektur ist wichtig, da ein Host ausfällt, die Daten über die anderen Hosts in der Skalierungseinheit Daten weiterhin verfügbar sind.  
  
## <a name="hosts"></a>Hosts  
Für hostverfügbarkeit werden alle Hosts in einem Windows-Failovercluster konfiguriert. Jedes Rack hat einen passiven Host. Erste Rack, die SQL Server Parallel Data Warehouse (PDW) und der Appliance-Struktur gesteuert werden, kann optional einen zweiten passiven Host verfügen. Wenn ein Host ausfällt, virtuelle Computer, die für Failover konfiguriert sind wird ein Failover auf einen verfügbaren passiven Host.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW-Knoten und Appliance-fabric  
APS verwendet für hohe Verfügbarkeit der PDW-Knoten und der Appliance-Struktur die Virtualisierung. Für jeden PDW und Appliance Fabric-Komponenten auf einem virtuellen Computer ausführen.  
  
Jeder virtuelle Computer wird als eine Rolle in der Windows-Failovercluster definiert. Bei ein virtuellen Computer ein Fehler auftritt, startet Sie Cluster auf einem verfügbaren passiven Host neu. Bereitstellen der virtuellen Maschinen sind mit System Center Virtual Machine Manager. Wenn ein Failover auftritt, wird auf dem passiven Host ausgeführten virtuellen Computers weiterhin auf ihre Benutzerdaten über dem InfiniBand-Netzwerk zugreifen können.  
  
Der Knoten "Zugriffssteuerung" und Compute-Knoten virtuelle Computer sind jeweils als Cluster mit einzelnem Knoten konfiguriert. Der einzelnen Knoten-Cluster verwaltet InfiniBand-Netzwerke als Clusterressource, um sicherzustellen, dass der Cluster immer das aktive InfiniBand IP verwendet. Einzelknoten-Cluster verwaltet die PDW-Prozesse, die innerhalb des virtuellen Computers ausgeführt. Hat beispielsweise den Einzelknotencluster SQL Server- und Daten Bewegung Service (DMS) als Ressourcen, damit es in der richtigen Reihenfolge gestartet werden kann. Der Knoten "Zugriffssteuerung" VM steuert auch die Startreihenfolge für die anderen virtuellen Computern, die auf der orchestrierungshost ausgeführt.  
  
