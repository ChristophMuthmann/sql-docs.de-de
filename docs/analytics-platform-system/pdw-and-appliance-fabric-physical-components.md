---
title: PDW Appliance Fabric physische Komponenten und (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7748d3da-0b7c-4ec6-9c22-4897758ba573
caps.latest.revision: 17
ms.openlocfilehash: 64a594c84d7be91939362ff0886a994147b76d93
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="pdw-and-appliance-fabric-physical-components"></a>Physische PDW und Appliance-Fabric-Komponenten
Namen und Beschreibungen für die PDW und Appliance, physischen Fabric-Komponenten. PDW-Region enthält alle diese Komponenten.  
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Komponentendiagramme  
Dies zeigt die Namen der physischen Komponenten und, in dem sie in das erste Rack einer Appliance 6-Compute-Knoten befinden.  
  
![Komponentennamen für PDW-Region – HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
Der tatsächliche Name für PDW-Komponenten wird der Name der PDW-Region, gefolgt von einem Bindestrich, gefolgt vom Komponentennamen. Beispielsweise ist der Name der PDW-Region PDW123, sind die tatsächlichen Namen **PDW123 CTL01**, **PDW123 CMP01**usw.  
  
Auf ähnliche Weise wird der tatsächliche Name für die Appliance Fabric-Komponenten der Appliance-Domäne, gefolgt von einem Bindestrich, gefolgt vom Komponentennamen. Wenn die Domäne der Anwendung FSW123 ist, die Appliance Fabric VMs sind beispielsweise **FSW123 WDS**, **FSW123 AD01**, **FSW123 VMM**usw.  
  
Hier ist eine konsolidierte Sicht der PDW-Region mit 6 Serverknoten aus.  
  
![PDW-Komponentennamen](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW-Komponenten  
PDW-VMs sind Teil der PDW-Region.  
  
*PDW_region*-CTL01  
Ein virtueller Computer, der den Knoten "Zugriffssteuerung" ausgeführt wird. Dies wird auf HST01 ausgeführt und kann ein Failover auf HST02.  
  
> [!WARNING]  
> SQL Server PDW unterstützt nicht die Erstellung einer Momentaufnahme des virtuellen Computers CTL01 mit Hyper-V-Manager. Momentaufnahmen basieren auf dem lokalen Speicher, der wodurch Fehler gehindert wird, wenn der virtuelle Computer versucht, ein Failover zu der Sicherung. Erstellen einer Momentaufnahme kann auch Zuverlässigkeitsprobleme ausgerichtet sind mit der anderen virtuellen Maschine, dass ein Failover zum passiven Server führen.  
  
*PDW_region*-CMP01 über *PDW_Region*-CMP06  
Ein virtueller Computer, der den Compute-Knoten ausgeführt wird. In diesem Diagramm 6-Serverknoten berechnen den Hosts HSA01 über HSA06 ausführen bzw. Knoten VMs CMP01 über CMP06.  
  
## <a name="fabric"></a>Appliance-Fabric-Komponenten  
Diese Komponenten sind Bestandteil des Fabrics Appliance.  
  
### <a name="virtual-machines"></a>Virtuelle Computer  
*appliance_domain*-WDS  
Dieses Hosts für virtuelle Maschinen Windows Deployment Services (WDS), das Analytics Platform System verwendet werden Windows-Betriebssystemen über das Anwendungsnetzwerk bereitstellen. Außerdem wird den DHCP-Dienst, wodurch die Appliance-Hosts für die Appliance-Netzwerk ohne eine vorkonfiguriert, dass IP-Adresse hostet.  
  
Die *Appliance_domain*- WDS-VM auf HST01 ausgeführt wird und ein Failover zu HST02. Die WDS-VM und der VMM-VM Bereitstellen von Windows auf physischen Hosts während der Installation der Anwendung. Führen Sie während des Lebenszyklus Appliance WDS "und" VMM Vorgänge wie das Ersetzen eines Hosts.  
  
*appliance_domain*-VMM  
Die Virtual Machine Manager (VMM) auf einem virtuellen Computer ausgeführt wird, und es kann ein Failover auf HST02. VMM hostet System Center zur Bereitstellung des Betriebssystems auf physischen Hosts. VMM bietet auch Windows Server Update Services (WSUS), um anwenden oder Entfernen von Windows-Updates auf allen Hosts und virtuellen Maschinen.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
Active Directory-Domänendienste, die der Domain Name System (DNS) enthält, wird auf einem virtuellen Computer auf HST01 und HST02 ausgeführt. Für hohe Verfügbarkeit des Geräts AD01 und AD02 replizierten Domänencontroller sind, und führen Sie kein Failover. Wenn ein Vorgang fehlschlägt, ist eine andere bereits durch die richtigen Daten verfügbar.  
  
*appliance_domain*-ISCSI01  
Ein iSCSI-virtueller Computer wird auf jeden einzelnen Host mit Speicher verbunden ist (HSA01 HSA06) ausgeführt. Dieser virtuelle Computer ist kein Failover.  
  
### <a name="hosts"></a>Hosts  
*Appliance_domain*-HST01 über *Appliance_domain*-HST06  
Die Hosts für die PDW-Steuerelement Knoten und dem Gerät Fabric virtuelle Maschinen. HST03 ist eine optionale passiven Host.  
  
*Appliance_domain*-HSA01 über *Appliance_domain*-HSA08  
Die Hosts mit Speicher verbunden ist (HSA). Jede HAS Host führt eine virtuellen serverknotencomputer und eine ISCSI VM.  
  
### <a name="cluster-for-pdw"></a>Cluster für PDW  
*appliance_domain*-WFOHST01  
PDW-Cluster wird WFOHST01 genannt. Er verwaltet alle physischen Hosts und virtuellen Computern, die mit PDW gehören.  
  
### <a name="direct-attached-storage"></a>Direkt angeschlossener Speicher  
*Appliance_domain*-DAS01 über *Appliance_domain*-DAS03  
Dies ist die direkt angeschlossener Speicher, der für die Serverknoten verbunden ist. HP verfügt über eine Angeschlossenem für jede zwei Serverknoten. Dell und Quanta verfügen über eine Angeschlossenem für alle drei Serverknoten aus.  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[Anwendungskonfiguration &#40;Analyseplattformsystem&#41;](appliance-configuration.md)  
[Appliance-Verwaltungsaufgaben &#40;Analyseplattformsystem&#41;](appliance-management-tasks.md)  
  
