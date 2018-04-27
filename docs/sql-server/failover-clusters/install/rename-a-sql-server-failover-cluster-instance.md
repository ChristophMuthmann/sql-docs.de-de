---
title: Umbenennen einer SQL Server-Failoverclusterinstanz|Microsoft-Dokumente
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- clusters [SQL Server], virtual servers
- renaming virtual servers
- virtual servers [SQL Server], failover clustering
- failover clustering [SQL Server], virtual servers
ms.assetid: 2a49d417-25fb-4760-8ae5-5871bfb1e6f3
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c67ec4ead681235d0349ce1be00ea941cfa4f67b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="rename-a-sql-server-failover-cluster-instance"></a>Umbenennen einer SQL Server-Failoverclusterinstanz
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Wenn eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz Teil eines Failoverclusters ist, unterscheidet sich der Vorgang des Umbenennens des virtuellen Servers vom Umbenennen einer eigenständigen Instanz. Weitere Informationen finden Sie unter [Umbenennen eines Computers, der eine eigenständige Instanz von SQL Server hostet](../../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md).  
  
 Der Name des virtuellen Servers ist immer mit dem SQL-Netzwerknamen (dem Netzwerknamen des virtuellen Servers mit SQL Server) identisch. Sie können zwar den Namen des virtuellen Servers ändern, nicht jedoch den Instanznamen. Sie können z. B. einen virtuellen Server namens VS1\instance1 in einen anderen Namen ändern, z. B. in SQL35\instance1, der Instanzanteil des Namens, instance1, bleibt jedoch unverändert.  
  
 Bevor Sie den Umbenennungsvorgang beginnen, überprüfen Sie die nachfolgenden Elemente.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt nicht das Umbenennen von Servern, die an der Replikation beteiligt sind. Eine Ausnahme stellt die Verwendung von Protokollversand mit Replikation dar. Der sekundäre Server beim Protokollversand kann umbenannt werden, wenn der primäre Server dauerhaft verloren ist. Weitere Informationen finden Sie unter [Protokollversand und Replikation &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
-   Wenn Sie einen virtuellen Server umbenennen, der für die Verwendung von Datenbankspiegelung konfiguriert ist, müssen Sie die Datenbankspiegelung vor dem Umbenennungsvorgang deaktivieren und die Datenbankspiegelung mit dem neuen Namen des virtuellen Servers anschließend neu einrichten. Die Metadaten für die Datenbankspiegelung werden nicht automatisch aktualisiert, um den neuen Namen des virtuellen Servers widerzuspiegeln.  
  
### <a name="to-rename-a-virtual-server"></a>So benennen Sie einen virtuellen Server um:  
  
1.  Ändern Sie mithilfe der Clusterverwaltung den SQL-Netzwerknamen in den neuen Namen.  
  
2.  Schalten Sie die Netzwerknamenressource offline. Durch diesen Vorgang werden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource und andere abhängige Ressourcen ebenfalls offline geschaltet.  
  
3.  Schalten Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource erneut online.  
  
## <a name="verify-the-renaming-operation"></a>Überprüfen des Umbenennungsvorgangs  
 Nachdem ein virtueller Server umbenannt wurde, müssen alle Verbindungen, die den alten Namen verwendet haben, nun Verbindungen mithilfe des neuen Namens herstellen.  
  
 Um zu überprüfen, ob der Umbenennungsvorgang abgeschlossen wurde, wählen Sie Informationen aus **@@servername**oder **sys.servers** aus. Die **@@servername**-Funktion gibt den neuen Namen des virtuellen Servers zurück, und die **sys.servers**-Tabelle zeigt den neuen Namen des virtuellen Servers an. Um zu überprüfen, ob der Failoverprozess ordnungsgemäß mit dem neuen Namen arbeitet, sollte der Benutzer außerdem versuchen, ein Failover der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource auf die anderen Knoten auszuführen.  
  
 Für Verbindungen von einem beliebigen Knoten im Cluster kann der neue Name fast sofort verwendet werden. Für Verbindungen, die den neuen Namen von einem Clientcomputer aus verwenden, kann der neue Name jedoch erst zum Herstellen einer Verbindung zum Server verwendet werden, nachdem der neue Name für den betreffenden Clientcomputer sichtbar ist. Die Zeitspanne, die zum Weitergeben des neuen Namens über ein Netzwerk benötigt wird, kann abhängig von der Netzwerkkonfiguration zwischen einigen Sekunden bis hin zu 3 bis 5 Minuten betragen; zusätzliche Zeit ist möglicherweise erforderlich, bis der alte Name des virtuellen Servers nicht mehr im Netzwerk sichtbar ist.  
  
 Um die Verzögerung der Netzwerkweitergabe des Umbenennungsvorgangs eines virtuellen Servers zu minimieren, führen Sie die folgenden Schritte aus:  
  
#### <a name="to-minimize-network-propagation-delay"></a>So minimieren Sie die Verzögerung der Netzwerkweitergabe:  
  
1.  Geben Sie an einer Eingabeaufforderung auf dem Serverknoten die folgenden Befehle aus:  
  
    ```  
    ipconfig /flushdns  
    ipconfig /registerdns  
    nbtstat –RR  
    ```  
  
## <a name="additional-considerations-after-the-renaming-operation"></a>Weitere Überlegungen nach dem Umbenennungsvorgang  
 Nachdem der Netzwerkname des Failoverclusters geändert wurde, müssen die folgenden Anweisungen überprüft und ausgeführt werden, damit alle Szenarien in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent und [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]funktionieren.  
  
 **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Service:** Überprüfen Sie die unten genannten zusätzlichen Aktionen für den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Service, und führen Sie sie aus:  
  
-   Korrigieren Sie die Registrierungseinstellungen, wenn SQL Agent für die Ereignisweiterleitung konfiguriert ist. Weitere Informationen finden Sie unter [Bestimmen eines Ereignisweiterleitungsservers &#40;SQL Server Management Studio&#41;](http://msdn.microsoft.com/library/81dfcbe4-3000-4e77-99de-bf85fef63a12).  
  
-   Korrigieren Sie die Instanznamen von Masterserver (MSX) und Zielservern (TSX), wenn der Netzwerkname von Computern/Cluster umbenannt wird. Weitere Informationen finden Sie in folgenden Themen:  
  
    -   [Vollziehen des Austritts mehrerer Zielserver aus einem Masterserver](http://msdn.microsoft.com/library/61a3713b-403a-4806-bfc4-66db72ca1156)  
  
    -   [Erstellen einer Multiserverumgebung](http://msdn.microsoft.com/library/edc2b60d-15da-40a1-8ba3-f1d473366ee6)  
  
-   Konfigurieren Sie den Protokollversand neu, damit der aktualisierte Servername für die Sicherungs- und Wiederherstellungsprotokolle verwendet wird. Weitere Informationen finden Sie in folgenden Themen:  
  
    -   [Konfigurieren des Protokollversands &#40;SQL Server&#41;](../../../database-engine/log-shipping/configure-log-shipping-sql-server.md)  
  
    -   [Entfernen des Protokollversands &#40;SQL Server&#41;](../../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
-   Aktualisieren Sie die Auftragsschritte, die vom Servernamen abhängen. Weitere Informationen finden Sie unter [Manage Job Steps](http://msdn.microsoft.com/library/51352afc-a0a4-428b-8985-f9e58bb57c31).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Umbenennen eines Computers, der eine eigenständige Instanz von SQL Server hostet](../../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)  
  
  
