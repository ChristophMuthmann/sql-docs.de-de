---
title: Einrichten von FILESTREAM auf einem Failovercluster | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], setting up on a failover cluster
ms.assetid: 6721f780-20b7-4109-8ddb-ac327310699e
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8c5bcc49ace68aaf9d35fd3365e693ddd953a0ce
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="set-up-filestream-on-a-failover-cluster"></a>Einrichten von FILESTREAM auf einem Failovercluster
  In diesem Thema erfahren Sie, wie Sie FILESTREAM auf einem Failovercluster aktivieren. Zur Durchführung dieser Prozedur müssen Sie mit [Failoverclustering](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) vertraut sein, und FILESTREAM muss aktiviert sein. Informationen zum Aktivieren von FILESTREAM finden Sie unter [Aktivieren und Konfigurieren von FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md).  
  
### <a name="to-set-up-filestream-on-a-failover-cluster"></a>So richten Sie FILESTREAM auf einem Failovercluster ein  
  
1.  Richten Sie den primären Knoten für den Failovercluster ein.  
  
     Aktivieren Sie anschließend mit dem **SQL Server-Konfigurations-Manager**FILESTREAM auf dem primären Knoten. Hierdurch werden die Einstellungen aktiviert, die Windows-Administratorrechte erfordern. Wenn Remotezugriff erforderlich ist, wählen Sie **Streamingzugriff von Remoteclients auf FILESTREAM-Daten zulassen**. Hierdurch wird eine geclusterte Dateifreigaberessource erstellt.  
  
2.  Richten Sie einen passiven Knoten ein.  
  
     Aktivieren Sie anschließend mit dem **SQL Server-Konfigurations-Manager**FILESTREAM auf dem passiven Knoten. Der unter **Windows-Freigabename** angegebene Name muss auf allen Knoten im Cluster einheitlich sein.  
  
3.  Wiederholen Sie Schritt 2, um weitere passive Knoten hinzuzufügen.  
  
4.  Nachdem Sie alle Knoten hinzugefügt haben, schließen Sie den Prozess ab, indem Sie die gespeicherte Prozedur sp_configure auf jeder Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausführen.  
  
5.  Wiederholen Sie die Schritte 2, 3 und 4, um dem Cluster weitere Knoten hinzuzufügen und diese zu aktivieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Erstellen eines neuen SQL Server-Failoverclusters &#40;Setup&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [Entfernen einer SQL Server-Failoverclusterinstanz &#40;Setup&#41;](../../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)   
 [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
  

