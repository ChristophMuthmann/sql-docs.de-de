---
title: Failoverclusterinstanzen - SQLServer on Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: Inactive
ms.openlocfilehash: f47d5695d2c67a0a5d20df9288854d72ad98be97
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>Failoverclusterinstanzen - SQLServer on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieser Artikel beschreibt die Konzepte im Zusammenhang mit SQL Server Failoverclusterinstanzen (FCI) unter Linux. 

Zum Erstellen einer SQL Server-FCI für Linux finden Sie unter [Konfigurieren von SQL Server-FCI unter Linux](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>Der Clustering-Ebene

* In RHEL, basiert die clustering-Ebene auf Red Hat Enterprise Linux (RHEL) [HA-Add-On](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf). 

    > [!NOTE] 
    > Zugriff auf Red Hat-HA-Add-On und Dokumentation erfordert ein Abonnement. 

* In SLES, basiert die clustering-Ebene unter SUSE Linux Enterprise [hohe Verfügbarkeit Erweiterung (HAE)](https://www.suse.com/products/highavailability).

    Weitere Informationen für die Clusterkonfiguration, Ressourcenoptionen-Agent, Management, best Practices und Empfehlungen finden Sie unter [SUSE Linux Enterprise hohe Verfügbarkeit Erweiterung 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

Das Add-on RHEL mit hoher Verfügbarkeit und die SUSE HAE basieren auf [Schrittmacher](http://clusterlabs.org/).

Wie das folgende Diagramm zeigt, wird der Speicher auf zwei Servern angezeigt. Komponenten - Corosync "und" Schrittmacher - Kommunikation und ressourcenverwaltung koordiniert werden. Einer der Server hat die aktive Verbindung mit der Speicherressourcen und SQL Server. Wenn Schrittmacher einen Fehler erkennt verwalten die Clusterkomponenten, die Ressourcen auf den anderen Knoten verschoben.  

![Red Hat Enterprise Linux 7 freigegebene Datenträgercluster für SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> SQL Server Integration in Schrittmacher unter Linux ist an diesem Punkt nicht als gekoppelten als mit WSFC unter Windows. Aus SQL, besteht keine Kenntnisse über das Vorhandensein des Clusters, alle Orchestrierung befindet sich im außerhalb und der Dienst wird als eigenständige Instanz von Schrittmacher gesteuert. Außerdem virtuellen Netzwerknamen bezieht sich auf WSFC, es gibt keine Entsprechung in Schrittmacher identisch. Es wird erwartet, @@servername und sys.servers des Knotennamens zurückgegeben, während der Cluster Dmvs Sys. dm_os_cluster_nodes und dm_os_cluster_properties keine Datensätze werden. Zum Verwenden einer Verbindungszeichenfolge, die auf einem Zeichenfolgennamen für den Server verweist, und die IP-Adresse verwenden, müssen sie in ihrer DNS-Server die IP-Adresse verwendet, um die virtuelle IP-Adressressource erstellen (wie in den folgenden Abschnitten erläutert wird) mit dem ausgewählten Server registrieren.

## <a name="number-of-instances-and-nodes"></a>Anzahl der Instanzen und Knoten

Einer der Hauptunterschiede mit SQL Server on Linux ist, dass es darf nur eine Installation von SQL Server / Linux-Server vorhanden sein. Die Installation wird eine Instanz aufgerufen. Dies bedeutet, dass im Gegensatz zu Windows Server unterstützt bis zu 25 FCIs pro Windows Server-Failovercluster (WSFC), eine Linux-basierten FCI nur eine einzelne Instanz aufweisen. Diese eine Instanz ist auch eine Standardinstanz. Es gibt kein Konzept für eine benannte Instanz unter Linux. 

Einen Schrittmacher Cluster kann nur bis zu 16 Knoten haben Wenn Corosync beteiligt ist, damit eine einzelne FCI bis zu 16 Server erstrecken kann. Eine FCI implementiert, mit der Standard Edition von SQL Server unterstützt bis zu zwei Knoten eines Clusters, auch wenn das Cluster Schrittmacher maximal 16 Knoten hat.

In einer SQL Server-FCI ist SQL Server-Instanz auf einem "Node" oder anderen aktiv.

## <a name="ip-address-and-name"></a>IP-Adresse und den Namen
In einem Cluster mit Linux Schrittmacher benötigt jede SQL Server-FCI eigene eindeutige IP-Adresse und den Namen. Wenn die FCI-Konfiguration über mehrere Subnetze erstreckt, wird eine IP-Adresse pro Subnetz erforderlich. Der eindeutige Name und IP-Adressen werden verwendet, um der FCI zuzugreifen, sodass Anwendungen und Endbenutzern nicht wissen, welche zugrunde liegenden Schrittmacher Cluster-Server müssen.

Der Name der FCI in DNS muss identisch mit den Namen der FCI-Ressource, die im Cluster Schrittmacher erstellt wird.
Der Name und die IP-Adresse müssen in DNS registriert werden.

## <a name="shared-storage"></a>Freigegebener Speicher
Alle FCIs erfordern, ob sie unter Linux oder Windows Server sind eine Form von freigegebenem Speicher. Dieser Speicher wird angezeigt, auf allen Servern, die möglicherweise die FCI gehostet werden können, aber nur ein einziger Server kann den Speicher für die FCI verwenden, zu einem beliebigen Zeitpunkt. Die Optionen für den freigegebenen Speicher unter Linux verfügbar sind:

- iSCSI
- Network File System (NFS)
- Server Message Block (SMB) unter Windows Server leicht unterschiedliche Optionen stehen. Eine Möglichkeit, die derzeit nicht unterstützt für Linux-basierte FCIs ist die Fähigkeit, einen Datenträger verwenden, der lokal auf den Knoten für die tempdb-Datenbank ist die temporäre SQL-Server-Arbeitsbereich ist.

In einer Konfiguration, die mehrere Standorte umfasst, muss die in einem Rechenzentrum gespeicherten mit den anderen synchronisiert werden. Im Fall eines Failovers die FCI wird in der Lage, online geschaltet werden kann, und der Speicher wird angezeigt, identisch sein. Erreichen Sie dies erfordern eine externe Methode für die Speicherreplikation, ob es über die zugrunde liegenden Speicherhardware oder ein Programm softwarebasierten vorgenommen wird. 

>[!NOTE]
>Für SQL Server 2017 müssen Linux-basierten Bereitstellungen mithilfe von Datenträgern, die angezeigt wird, direkt auf einem Server mit XFS oder EXT4 formatiert werden. Andere Dateisysteme werden derzeit nicht unterstützt. Alle Änderungen werden hier berücksichtigt.

Der Prozess zum Darstellen von freigegebenen Speichers gilt für die verschiedenen unterstützten Methoden:

- Konfigurieren Sie den freigegebenen Speicher
- Bereitstellen Sie den Speicher als Ordner auf den Servern, die als Knoten des Clusters Schrittmacher, für die FCI fungieren soll
- Falls erforderlich, verschieben Sie die SQL Server-Systemdatenbanken in freigegebenen Speicher
- Tests, der SQL Server von jedem Server arbeitet mit den freigegebenen Speicher verbunden

Ein Hauptunterschied mit SQL Server on Linux ist, dass Sie können konfigurieren, dass den Benutzer Daten- und Protokolldateien Standardspeicherort, der Systemdatenbanken stets am vorhanden sein müssen `/var/opt/mssql/data`. Unter Windows Server besteht die Möglichkeit zum Verschieben von Systemdatenbanken einschließlich TempDB zur Verfügung. Dies spielt in wie freigegebenen Speicher für eine FCI konfiguriert ist.

Der Standardpfad für nicht-Systemdatenbanken können geändert werden, mithilfe der `mssql-conf` Hilfsprogramm. Informationen zum Ändern der Standardeinstellungen [ändern Sie das Standardverzeichnis Daten- oder Protokolldatei](sql-server-linux-configure-mssql-conf.md#datadir). Sie können auch SQL Server-Daten und Transaktionsprotokolle an anderen Orten speichern, solange sie die richtigen Sicherheitseinstellungen besitzen, auch wenn es sich nicht um einen Standardspeicherort ist; der Speicherort muss angegeben werden.

In den folgenden Themen wird erläutert, wie so konfigurieren Sie unterstützten Speichertypen für ein Linux-SQL Server-FCI basierte wird:

- [Konfigurieren der Failover-Clusterinstanz - iSCSI - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Konfigurieren Sie Failoverclusterinstanz – NFS - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Konfigurieren der Failover-Clusterinstanz - SMB - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
