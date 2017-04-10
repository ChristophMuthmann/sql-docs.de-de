---
title: "Integration Services (SSIS) in einem Cluster | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Integration Services (SSIS) in einem Cluster
  Für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ist Clustering nicht zu empfehlen, da es sich beim [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst nicht um einen Cluster- oder clusterfähigen Dienst handelt, der auch keine Failoverunterstützung zwischen Clusterknoten bietet. In einer Clusterumgebung sollte [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deshalb auf jedem Knoten im Cluster als eigenständiger Dienst installiert und gestartet werden.  
  
 Auch wenn der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst kein Clusterdienst ist, können Sie den Dienst manuell so konfigurieren, dass er das Clusterressource ausgeführt wird, wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] separat auf den einzelnen Clusterknoten installiert haben.  
  
 Wenn jedoch mit der Erstellung einer gruppierten Hardwareumgebung eine hohe Verfügbarkeit erzielt werden soll, dann müssen Sie dazu den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst nicht als Clusterressource konfigurieren.  Zum Verwalten der Pakete auf einem beliebigen Knoten im Cluster von einem beliebigen anderen Knoten des Clusters aus ändern Sie die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst auf jedem Knoten im Cluster. Sie müssen diese Konfigurationsdatei ändern, um auf alle verfügbaren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verweisen zu können, auf denen Pakete gespeichert sind. Mit dieser Lösung kann die hohe Verfügbarkeit bereitgestellt werden, die die meisten Kunden benötigen, ohne dass die Probleme auftreten, zu denen es kommen kann, wenn der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst als Clusterressource konfiguriert wird. Weitere Informationen zum Ändern der Konfigurationsdatei finden Sie unter [Konfigurieren des Integration Services-Diensts &#40;SSIS Service&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md)  
  
 Um fundierte Entscheidungen in Bezug auf das Konfigurieren des Diensts in einer Clusterumgebung treffen zu können, müssen Sie die Rolle des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts verstehen. Weitere Informationen finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
## <a name="understanding-the-disadvantages-of-configuring-integration-services-as-a-cluster-resource"></a>Grundlegendes zu den Nachteilen der Konfiguration von Integration Services als Clusterressource  
 Zu den möglichen Nachteilen der Konfiguration des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts als Clusterressource zählen die folgenden:  
  
-   **Wenn ein Failover auftritt, wird die Paketausführung nicht neu gestartet.**
    
    Zur Wiederherstellung nach Paketfehlern können Pakete an Prüfpunkten neu gestartet werden. Dazu muss der Dienst nicht als Clusterressource konfiguriert sein. Weitere Informationen finden Sie unter [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
-   Wenn Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst in einer anderen Ressourcengruppe als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konfigurieren, können Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] auf Clientcomputern nicht zum Verwalten von Paketen verwenden, die in der msdb-Datenbank gespeichert sind. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst kann in diesem Doppelhopszenario keine Anmeldeinformationen delegieren.  
  
-   Bei mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressourcengruppen, die den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst in einem Cluster aufweisen, kann ein Failover zu unerwarteten Ergebnissen führen. Nehmen Sie das folgende Szenario als Beispiel. Gruppe 1, die den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst und den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst aufweist, wird auf Knoten A ausgeführt. Gruppe 2, die ebenfalls den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst und den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst aufweist, wird auf Knoten B ausgeführt. Gruppe 2 führt ein Failover zu Knoten A aus. Beim Versuch, eine andere Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts auf Knoten A zu starten, tritt ein Fehler auf, weil der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ein Dienst mit einer Instanz ist. Ob bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst, der versucht, ein Failover zu Knoten A auszuführen, auch ein Fehler auftritt, hängt von der Konfiguration des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts in Gruppe 2 ab. Wenn der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst so konfiguriert wurde, dass er Auswirkungen auf die anderen Dienste in der Ressourcengruppe hat, dann tritt bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst, der das Failover ausführt, ein Fehler auf, da bei dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ein Fehler aufgetreten ist. Wenn der Dienst so konfiguriert wurde, dass er keinerlei Auswirkungen auf die anderen Dienste in der Ressourcengruppe hat, kann der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ein Failover zu Knoten A ausführen. Sofern nicht der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst in Gruppe 2 so konfiguriert wurde, dass er keine Auswirkungen auf die anderen Dienste in der Ressourcengruppe hat, kann der Fehler bei dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, der das Failover ausführt, dazu führen, dass bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst, der das Failover ausführt, auch ein Fehler auftritt.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Eine Schritt-für-Schritt-Anleitung zum Konfigurieren des Integration Services-Diensts in einem Cluster finden Sie unter [Konfigurieren des Integration Services-Diensts als Clusterressource](../../integration-services/service/configure-the-integration-services-service-as-a-cluster-resource.md).  
  
  