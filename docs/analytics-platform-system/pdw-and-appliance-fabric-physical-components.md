---
title: Appliance physische Komponenten – Analytics Platform System | Microsoft Docs
description: Namen und Beschreibungen für die PDW und Appliance, physischen Fabric-Komponenten.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0adbd92d1a29a98a80de65268c53ea63e3941d07
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="appliance-physical-components---analytics-platform-system"></a>Physische Komponenten der Appliance - Analyseplattformsystem
Namen und Beschreibungen für die PDW und Appliance, physischen Fabric-Komponenten. 
  
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
*Appliance_domain*- Windows-Bereitstellungsdienste  
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
  
