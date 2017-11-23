---
title: Herstellen einer Verbindung mit der Appliance-Knoten (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f975aa91-c816-4b29-89bf-923ab5b4abb4
caps.latest.revision: "19"
ms.openlocfilehash: 00db55a8c4835407d9b5aeb2ce7dac30f94eb888
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="connect-to-appliance-nodes"></a>Herstellen einer Verbindung mit der Appliance-Knoten
Dieser Artikel beschreibt die verschiedenen Möglichkeiten, auf die einzelnen Knoten in der Einheit Analytics Platform System herstellen.  
  
## <a name="connecting-with-hadoop"></a>Herstellen einer Verbindung mit Hadoop  
Bitten Sie bevor Hadoop mit SQL Server PDW verwenden Ihre Appliance-Administrator, um die Java Runtime Environment auf SQL Server PDW zu installieren. Anweisungen finden Sie [Konfigurieren von PolyBase-Konnektivität mit externen Daten &#40; Analyseplattformsystem &#41; ](configure-polybase-connectivity-to-external-data.md) in die Appliance Operations Guide.  
  
## <a name="ConnectingToIndividualNodes"></a>Herstellen einer Verbindung mit der Appliance-Knoten  
Jeder Knoten Appliance direkt zugegriffen wird nur unter bestimmten Verwendungsszenarien und nach bestimmten Benutzertypen. Die folgende Tabelle enthält jeder Appliance-Knoten und die Szenarien, die unter denen Benutzer direkt auf dem jeweiligen Knoten hergestellt werden.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  
  
|||  
|-|-|  
|**Knoten**|**Access-Szenarien**|  
|Knoten "Zugriffssteuerung"|Verwenden Sie einen Webbrowser, um die Verwaltungskonsole zugreifen, der auf den Knoten "Zugriffssteuerung" ausgeführt wird. Weitere Informationen finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40; Analyseplattformsystem &#41; ](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Verbinden allen Clientanwendungen und Clienttools mit dem Steuerungsknoten, unabhängig davon, ob die Verbindung Ethernet oder InfiniBand verwendet wird.<br /><br />Verwenden Sie zum Konfigurieren einer Ethernet-Verbindungs mit dem Steuerungsknoten Steuerelement Knoten-Cluster-IP-Adresse und Port **17001**. Z. B. "192.168.0.1,17001".<br /><br />Verwenden Sie zum Konfigurieren einer InfiniBand-Verbindungs mit dem Steuerungsknoten  ***Appliance_domain*-SQLCTL01** und Port **17001**. Mithilfe von  ***Appliance_domain*-SQLCTL01**, der Appliance DNS-Server wird Ihr Server mit aktiven InfiniBand-Netzwerk verbinden. So konfigurieren den nicht-Appliance-Server, um diese Option verwenden, finden Sie unter [InfiniBand-Netzwerkadapter konfigurieren](configure-infiniband-network-adapters.md).<br /><br />Der Appliance-Administrator eine Verbindung mit dem Steuerungsknoten Verwaltungsvorgänge ausführen. Beispielsweise führt der Appliance-Administrator die folgenden Vorgänge aus dem Knoten "Zugriffssteuerung":<br /><br />Konfigurieren von Analytics Platform System mit der **dwconfig.exe** -Konfigurationstool.|  
|Computeknoten|Serverdienste Knotens Verbindungen durch die Knoten "Zugriffssteuerung" weitergeleitet werden. Die IP-Adressen von Compute-Knoten werden nie in Anwendungsbefehle als Parameter eingegeben werden.<br /><br />Für das Laden, Remote Tabelle kopieren und Hadoop, SQL Server PDW Sicherung senden oder Empfangen von Daten parallel zwischen den Computeknoten und nicht-Appliance-Knoten oder Server direkt. Diese Anwendungen, die mit SQL Server PDW durch Herstellen einer Verbindung mit dem Steuerungsknoten hergestellt, und klicken Sie dann der Steuerelementknoten leitet SQL Server PDW um eine Kommunikation zwischen den Computeknoten und dem nicht-Appliance-Server herzustellen.<br /><br />Z. B. vorkommen, diese Vorgänge parallel mit direkten Verbindungen für den Serverknoten:<br /><br />Laden in SQL Server PDW vom Server geladen.<br /><br />Sichern einer Datenbank aus SQL Server PDW dem backup-Server.<br /><br />Wiederherstellen einer Datenbank aus dem backup-Server mit SQL Server PDW.<br /><br />Hadoop-Daten aus SQL Server PDW abgefragt.<br /><br />Exportieren von Daten aus SQL Server PDW in eine externe Hadoop-Tabelle.<br /><br />Das Kopieren einer SQL Server PDW-Tabelle mit einer SMP SQL Server-Remotedatenbank.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>Herstellen einer Verbindung mit dem Ethernet und InfiniBand-Netzwerke  
Remote-Server können über entweder die Appliance InfiniBand-Netzwerk oder über das Ethernet-Netzwerk verbinden. Für die Verbesserung der Leistung beim Laden der Server, Server sichern und Empfangen von Daten über Server **CREATE REMOTE TABLE AS SELECT** -Anweisungen in der Regel Daten über die Appliance InfiniBand-Netzwerk übertragen.  
  
Sie können die nicht-Appliance-Servern zu Ihren eigenen Kunden Arbeitsgruppe oder Domäne gehören konfigurieren und verwenden Sie Ihr eigenes Kundennetzwerk für die Verbindung mit diesen Servern und Übertragen von Daten auf diese. Nicht-Appliance-Servern, die mit dem InfiniBand-Gerät verbunden haben, die Möglichkeit, Daten miteinander über die Appliance InfiniBand-Netzwerk zu übertragen; Achten Sie darauf, dabei, da sie die Leistung von SQL Server PDW verlangsamen kann.  
  
Diese Anweisung fügt z. B. Netzwerkanmeldeinformationen zum Ausführen von Sicherungen über InfiniBand eine backup-Server, die eine InfiniBand IP-Adresse 192.168.0.1 verfügt. Die Appliance-Domäne ist *Mypdw*, und die Anweisung aus dem backup-Server ausgeführt wird. Bevor Sie diese Anweisung ausführen, müssen Sie eigene Parameter ausfüllen.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
Beispielsweise startet ein Laden-Befehl wie folgt:  
  
```  
dwloader –S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
