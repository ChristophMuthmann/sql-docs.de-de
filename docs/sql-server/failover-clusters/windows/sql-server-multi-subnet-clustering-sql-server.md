---
title: SQL Server-Multisubnetzclustering (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stretch cluster
- Availability Groups [SQL Server], WSFC clusters
- failover clustering [SQL Server], AlwaysOn Availability Groups
- multi-site failover cluster
- failover clustering [SQL Server]
ms.assetid: cd909612-99cc-4962-a8fb-e9a5b918e221
caps.latest.revision: 52
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 615d94c4058e25a12ebcd21619928507b928c2d8
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-multi-subnet-clustering-sql-server"></a>SQL Server-Multisubnetzclustering (SQL Server)
  Ein [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Multisubnetz-Failovercluster ist eine Konfiguration, in der jeder Failoverclusterknoten mit einem anderen Subnetz oder einer anderen Gruppe von Subnetzen verbunden ist. Diese Subnetze können am gleichen Standort oder an geografisch verteilten Standorten sein. Das Clustering von weit verstreuten Standorten wird mitunter auch als Stretchcluster bezeichnet. Da kein freigegebener Speicher vorhanden ist, auf den alle Knoten zugreifen können, sollten die Daten zwischen den Datenspeichern in den verschiedenen Subnetzen repliziert werden. Infolge der Datenreplikation ist mehr als eine Kopie der Daten verfügbar. Multisubnetz-Failovercluster bieten somit neben hoher Verfügbarkeit auch eine Lösung zur Wiederherstellung im Notfall.  
  
   
##  <a name="VisualElement"></a> SQL Server-Multisubnetz-Failovercluster (zwei Knoten, zwei Subnetze)  
 In der folgenden Abbildung wird eine Failoverclusterinstanz (FCI) in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]mit zwei Knoten dargestellt.  
  
 ![Multisubnetzarchitektur mit MultiSubnetFailover](../../../sql-server/failover-clusters/windows/media/multi-subnet-architecture-withmultisubnetfailoverparam.gif "Multi-Subnet Architecture with MultiSubnetFailover")  
  
  
##  <a name="Configurations"></a> Konfigurationen einer Multisubnetz-Failoverclusterinstanz  
 Im Folgenden finden Sie einige Beispiele für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -FCIs mit mehreren Subnetzen:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -FCI SQLCLUST1 enthält Node1 und Node2. Node1 ist mit Subnet1 verbunden. Node2 ist mit Subnet2 verbunden. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup betrachtet diese Konfiguration als Multisubnetzcluster und legt die IP-Adressressourcenabhängigkeit auf **OR**fest.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -FCI SQLCLUST1 enthält Node1, Node2 und Node3. Node1 und Node2 sind mit Subnet1 verbunden. Node3 ist mit Subnet2 verbunden. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup betrachtet diese Konfiguration als Multisubnetzcluster und legt die IP-Adressressourcenabhängigkeit auf **OR**fest. Da sich Node1 und Node2 im gleichen Subnetz befinden, bietet diese Konfiguration zusätzlich eine hohe lokale Verfügbarkeit.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -FCI SQLCLUST1 enthält Node1 und Node2. Node1 befindet sich in Subnet1. Node2 befindet sich in Subnet1 und Subnet2. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup betrachtet diese Konfiguration als Multisubnetzcluster und legt die IP-Adressressourcenabhängigkeit auf **OR**fest.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -FCI SQLCLUST1 enthält Node1 und Node2. Node1 ist mit Subnet1 und Subnet2 verbunden. Node2 ist auch mit Subnet1 und Subnet2 verbunden. Die IP-Adressabhängigkeit wird vom Setup von **auf** AND [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] festgelegt.  
  
    > **HINWEIS:** Diese Konfiguration wird nicht als Multisubnetz-Failovercluster-Konfiguration betrachtet, da sich die gruppierten Knoten in der gleichen Subnetzgruppe befinden.  
  
##  <a name="ComponentsAndConcepts"></a> Überlegungen zu IP-Adressressourcen  
 Die IP-Adressen in einer Multisubnetz-Failoverclusterkonfiguration sind nicht im Besitz aller Knoten im Failovercluster und beim Start von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] möglicherweise nicht alle online. Ab [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]können Sie die IP-Adressabhängigkeit auf **OR**festlegen. Dadurch kann [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] online sein, wenn mindestens eine gültige IP-Adresse vorhanden ist, mit der eine Bindung hergestellt werden kann.  
  
> **HINWEIS:** In den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Versionen vor [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]wurde eine Stretch-V-LAN-Technologie in Clusterkonfigurationen mit mehreren Standorten verwendet, um eine einzelne IP-Adresse für standortübergreifende Failover verfügbar zu machen. Durch die neue Möglichkeit zur Gruppierung von Knoten in unterschiedlichen Subnetzen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können Sie jetzt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster an mehreren Standorten ohne Stretch-V-LAN-Technologie konfigurieren.  
  
### <a name="ip-address-resource-or-dependency-considerations"></a>Überlegungen zur IP-Adressabhängigkeit OR  
 Wenn Sie die IP-Adressabhängigkeit auf **OR**festlegen, können Sie das folgende Failoververhalten in Betracht ziehen:  
  
-   Bei einem Fehler in einer IP-Adresse im Knoten, in dessen Besitz sich die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Clusterressourcengruppe derzeit befindet, wird nicht automatisch ein Failover ausgelöst, solange nicht alle gültigen IP-Adressen in diesem Knoten ausgefallen sind.  
  
-   Wenn ein Failover auftritt, wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] online geschaltet, wenn eine Bindung zu mindestens einer gültigen IP-Adresse im aktuellen Knoten hergestellt werden kann. Die IP-Adressen, für die beim Start von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] keine Bindung hergestellt werden konnte, werden im Fehlerprotokoll aufgeführt.  
  
   
 Wenn eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -FCI und eine eigenständige [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]-Instanz parallel installiert sind, achten Sie darauf, dass Konflikte mit TCP-Portnummern für die IP-Adressen vermieden werden. Konflikte treten in der Regel auf, wenn in zwei [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Instanzen die Verwendung des TCP-Standartports (1433) konfiguriert wurde. Um Konflikte zu vermeiden, konfigurieren Sie in einer Instanz die Verwendung eines nicht standardmäßigen festen Ports. Die Konfiguration eines festen Ports kann in der Regel in der eigenständigen Instanz am einfachsten vorgenommen werden. Wenn [!INCLUDE[ssDE](../../../includes/ssde-md.md)] für die Verwendung anderer Ports konfiguriert wird, wird verhindert, dass ein unerwarteter IP-Adressen-/TCP-Port-Konflikt auftritt, der den Start einer Instanz blockiert, wenn eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -FCI ein Failover zu dem Standbyknoten ausführt.  
  
##  <a name="DNS"></a> Clientwiederherstellungs-Latenzzeit während der Failover  
 Die RegisterAllProvidersIP-Clusterressource wird von einer Multisubnetz-FCI für den Netzwerknamen standardmäßig aktiviert. In einer Multisubnetzkonfiguration werden die Online- und Offline-IP-Adressen des Netzwerknamens beim DNS-Server registriert. Die Clientanwendung ruft dann alle registrierten IP-Adressen vom DNS-Server ab und versucht, entweder geordnet oder parallel eine Verbindung mit den Adressen herzustellen. Demnach hängt die Clientwiederherstellungszeit in Multisubnetz-Failovern nicht länger von DNS-Aktualisierungs-Wartezeiten ab. Standardmäßig versucht der Client die IP-Adressen geordnet abzurufen. Wenn der Client den neuen optionalen **MultiSubnetFailover=True** -Parameter in seiner Verbindungszeichenfolge verwendet, versucht er stattdessen gleichzeitig die IP-Adressen abzurufen und stellt eine Verbindung mit dem ersten antwortenden Server her. Dadurch kann die Clientwiederherstellungs-Latenzzeit minimiert werden, wenn Failover auftreten. Weitere Informationen finden Sie unter [Always On-Clientkonnektivität (SQL Server)](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md) und [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners (SQL Server)](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
 Bei Legacyclientbibliotheken oder Drittanbieterdatenanbietern können Sie den **MultiSubnetFailover** -Parameter in der Verbindungszeichenfolge nicht verwenden. Versuchen Sie, den Verbindungstimeout in der Clientverbindungszeichenfolge um 21 Sekunden für jede zusätzliche IP-Adresse anzupassen, damit sichergestellt wird, dass Ihre Clientanwendung optimal mit dem Multisubnetz-FCI in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]interagiert. Dadurch wird sichergestellt, dass der Wiederverbindungsversuch des Clients nicht zu einem Timeout führt, bevor es in der Lage ist, alle IP-Adressen in der Multisubnetz-FCI durchzugehen.  
  
 Der standardmäßige Timeoutzeitraum für Clientverbindungen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio und **sqlcmd** ist 15 Sekunden.  
  
   
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
|Inhaltsbeschreibung|Thema|  
|-------------------------|-----------|  
|Installieren eines SQL Server-Failoverclusters|[Erstellen eines neuen SQL Server-Failoverclusters (Setup)](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Direktes Upgrade des vorhandenen SQL Server-Failoverclusters|[Aktualisieren einer SQL Server-Failoverclusterinstanz &#40;Setup&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|Beibehalten des vorhandenen SQL Server-Failoverclusters|[Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
|Verwenden des Failovercluster-Verwaltungs-Snap-ins zum Anzeigen von WSFC-Ereignissen und -Protokollen|[Anzeigen von Ereignissen und Protokollen für einen Failovercluster](http://technet.microsoft.com/library/cc772342\(WS.10\).aspx)|  
|Verwenden von Windows PowerShell zum Erstellen einer Protokolldatei für alle Knoten (oder einen bestimmten Knoten) in einem WSFC-Failovercluster|[Get-ClusterLog-Failovercluster-Cmdlet](http://technet.microsoft.com/library/ee461045.aspx)|  
  

  
  

