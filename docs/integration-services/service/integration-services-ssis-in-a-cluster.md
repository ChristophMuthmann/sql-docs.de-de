---
title: Integration Services (SSIS) in einem Cluster | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: service
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e05af2e5e01c9a0d7970a03af1c5fc0e121ded0f
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-ssis-in-a-cluster"></a>Integration Services (SSIS) in einem Cluster
  Für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ist Clustering nicht zu empfehlen, da es sich beim [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst nicht um einen Cluster- oder clusterfähigen Dienst handelt, der auch keine Failoverunterstützung zwischen Clusterknoten bietet. In einer Clusterumgebung sollte [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deshalb auf jedem Knoten im Cluster als eigenständiger Dienst installiert und gestartet werden.  
  
 Auch wenn der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst kein Clusterdienst ist, können Sie den Dienst manuell so konfigurieren, dass er das Clusterressource ausgeführt wird, wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] separat auf den einzelnen Clusterknoten installiert haben.  
  
 Wenn jedoch mit der Erstellung einer gruppierten Hardwareumgebung eine hohe Verfügbarkeit erzielt werden soll, dann müssen Sie dazu den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst nicht als Clusterressource konfigurieren.  Zum Verwalten der Pakete auf einem beliebigen Knoten im Cluster von einem beliebigen anderen Knoten des Clusters aus ändern Sie die Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst auf jedem Knoten im Cluster. Sie müssen diese Konfigurationsdatei ändern, um auf alle verfügbaren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verweisen zu können, auf denen Pakete gespeichert sind. Mit dieser Lösung kann die hohe Verfügbarkeit bereitgestellt werden, die die meisten Kunden benötigen, ohne dass die Probleme auftreten, zu denen es kommen kann, wenn der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst als Clusterressource konfiguriert wird. Weitere Informationen zum Ändern der Konfigurationsdatei finden Sie unter [Integration Services-Dienst &#40; SSIS-Dienst &#41; ](../../integration-services/service/integration-services-service-ssis-service.md).  
  
 Um fundierte Entscheidungen in Bezug auf das Konfigurieren des Diensts in einer Clusterumgebung treffen zu können, müssen Sie die Rolle des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts verstehen. Weitere Informationen finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
## <a name="disadvantages"></a>Nachteile
 Zu den möglichen Nachteilen der Konfiguration des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts als Clusterressource zählen die folgenden:  
  
-   **Wenn ein Failover auftritt, wird die Paketausführung nicht neu gestartet.**
    
    Zur Wiederherstellung nach Paketfehlern können Pakete an Prüfpunkten neu gestartet werden. Dazu muss der Dienst nicht als Clusterressource konfiguriert sein. Weitere Informationen finden Sie unter [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
-   Wenn Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst in einer anderen Ressourcengruppe als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konfigurieren, können Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] auf Clientcomputern nicht zum Verwalten von Paketen verwenden, die in der msdb-Datenbank gespeichert sind. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst kann in diesem Doppelhopszenario keine Anmeldeinformationen delegieren.  
  
-   Bei mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressourcengruppen, die den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst in einem Cluster aufweisen, kann ein Failover zu unerwarteten Ergebnissen führen. Nehmen Sie das folgende Szenario als Beispiel. Gruppe 1, die den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst und den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst aufweist, wird auf Knoten A ausgeführt. Gruppe 2, die ebenfalls den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst und den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst aufweist, wird auf Knoten B ausgeführt. Gruppe 2 führt ein Failover zu Knoten A aus. Beim Versuch, eine andere Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts auf Knoten A zu starten, tritt ein Fehler auf, weil der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ein Dienst mit einer Instanz ist. Ob bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst, der versucht, ein Failover zu Knoten A auszuführen, auch ein Fehler auftritt, hängt von der Konfiguration des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts in Gruppe 2 ab. Wenn der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst so konfiguriert wurde, dass er Auswirkungen auf die anderen Dienste in der Ressourcengruppe hat, dann tritt bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst, der das Failover ausführt, ein Fehler auf, da bei dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ein Fehler aufgetreten ist. Wenn der Dienst so konfiguriert wurde, dass er keinerlei Auswirkungen auf die anderen Dienste in der Ressourcengruppe hat, kann der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ein Failover zu Knoten A ausführen. Sofern nicht der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst in Gruppe 2 so konfiguriert wurde, dass er keine Auswirkungen auf die anderen Dienste in der Ressourcengruppe hat, kann der Fehler bei dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, der das Failover ausführt, dazu führen, dass bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst, der das Failover ausführt, auch ein Fehler auftritt.  

## <a name="configure-the-service-as-a-cluster-resource"></a>Konfigurieren Sie den Dienst als Clusterressource
Kunden, für die die Vorteile der Konfiguration des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts als Clusterressource die Nachteile überwiegen, finden in diesem Abschnitt alle erforderlichen Konfigurationsanweisungen. [!INCLUDE[msCoName](../../includes/msconame-md.md)] rät dennoch von einer Konfiguration des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts als Clusterressource ab.  
  
 Sie müssen Sie die folgenden Tasks ausführen, um den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst als Clusterressource zu konfigurieren.  
  
-   Installieren Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf einem Cluster.  
  
     Wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf einem Cluster installieren möchten, müssen Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf jedem Knoten im Cluster installieren.  
  
-   Konfigurieren Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] als Clusterressource.  
  
     Wenn Integration Services auf jedem Knoten im Cluster installiert ist, müssen Sie Integration Services als Clusterressource konfigurieren. Wenn Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst als Clusterressource konfigurieren, können Sie den Dienst der gleichen Ressourcengruppe wie [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]oder einer anderen Gruppe hinzufügen. In der folgenden Tabelle werden die möglichen Vor- und Nachteile des Auswählens einer Ressourcengruppe beschrieben.  
  
    |Wenn Integration Services und SQL Server sich in der gleichen Ressourcengruppe befinden|Wenn Integration Services und SQL Server sich in verschiedenen Ressourcengruppen befinden|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |Clientcomputer können mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Pakete verwalten, die in der msdb-Datenbank gespeichert sind, da sowohl der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Dienst als auch der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst auf dem gleichen virtuellen Server ausgeführt werden. Mit dieser Konfiguration können die Delegierungsprobleme des Doppelhopszenarios vermieden werden.|Clientcomputer können in der msdb-Datenbank gespeicherte Pakete nicht mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwalten. Der Client kann eine Verbindung mit dem virtuellen Server herstellen, auf dem der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ausgeführt wird. Allerdings kann dieser Computer die Anmeldeinformationen des Benutzers nicht an den virtuellen Server delegieren, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Dies wird als Doppelhopszenario bezeichnet.|  
    |Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst teilt sich die CPU- und andere Computerressourcen mit anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Diensten.|Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst teilt sich die CPU- und andere Computerressourcen nicht mit anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Diensten, da die verschiedenen Ressourcengruppen auf verschiedenen Knoten konfiguriert sind.|  
    |Pakete können schneller in die msdb-Datenbank geladen und dort gespeichert werden, und dabei wird weniger Netzwerkverkehr generiert, weil beide Dienste auf dem gleichen Computer ausgeführt werden.|Das Laden und Speichern von Paketen in der msdb-Datenbank dauert möglicherweise länger und generiert mehr Netzwerkverkehr.|  
    |Beide Dienste sind gleichzeitig online oder offline.|Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst kann online sein, während [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] offline ist. Das bedeutet, dass die in der msdb-Datenbank von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gespeicherten Pakete nicht verfügbar sind.|  
    |Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst kann bei Bedarf nicht schnell zu einem anderen Knoten verschoben werden.|Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst kann bei Bedarf schneller zu einem anderen Knoten verschoben werden.|  
  
     Wenn Sie entschieden haben, welcher Ressourcengruppe [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]hinzugefügt werden soll, müssen Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] als Clusterressource in dieser Gruppe konfigurieren.  
  
-   Konfigurieren Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst und den Paketspeicher.  
  
     Nachdem Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] als Clusterressource konfiguriert haben, müssen Sie den Speicherort und den Inhalt der Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst auf jedem Knoten im Cluster ändern. Durch diese Änderungen sind bei einem Failover die Konfigurationsdatei und der Paketspeicher für alle Knoten verfügbar. Nachdem Sie den Speicherort und den Inhalt der Konfigurationsdatei geändert haben, müssen Sie den Dienst online schalten.  
  
-   Schalten Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst als Clusterressource online.  
  
 Nach dem Konfigurieren des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts auf einem Cluster oder auf einem beliebigen Server müssen Sie möglicherweise DCOM-Berechtigungen konfigurieren, bevor Sie von einem Clientcomputer aus eine Verbindung mit dem Dienst herstellen können. Weitere Informationen finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst kann keine Anmeldeinformationen delegieren. Daher können Sie in der msdb-Datenbank gespeicherte Pakete nicht mithilfe von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] verwalten, wenn die folgenden Bedingungen zutreffen:  
  
-   Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden auf separaten Servern oder virtuellen Servern ausgeführt.  
  
-   Der Client, auf dem [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ausgeführt wird, ist ein dritter Computer.  
  
 Der Client kann eine Verbindung mit dem virtuellen Server herstellen, auf dem der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ausgeführt wird. Allerdings kann dieser Computer die Anmeldeinformationen des Benutzers nicht an den virtuellen Server delegieren, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Dies wird als Doppelhopszenario bezeichnet.  
  
### <a name="to-install-integration-services-on-a-cluster"></a>So installieren Sie Integration Services auf einem Cluster  
  
1.  Installieren und konfigurieren Sie einen Cluster mit einem oder mehreren Knoten.  
  
2.  (Optional) Installieren Sie Clusterdienste, wie z.B. das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
3.  Installieren Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf jedem Knoten des Clusters.  
  
### <a name="to-configure-integration-services-as-a-cluster-resource"></a>So konfigurieren Sie Integration Services als Clusterressource  
  
1.  Öffnen Sie die **Clusterverwaltung**.  
  
2.  Wählen Sie in der Konsolenstruktur den Gruppenordner aus.  
  
3.  Wählen Sie im Ergebnisbereich die Gruppe aus, der Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]hinzufügen möchten:  
  
    -   Wählen Sie die Gruppe aus, zu der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gehört, um Integration Services als Clusterressource der gleichen Ressourcengruppe wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hinzuzufügen.  
  
    -   Um Integration Services als Clusterressource einer anderen Ressourcengruppe als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hinzuzufügen, wählen Sie eine Gruppe aus, zu der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht gehört.  
  
4.  Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie anschließend auf **Ressource**.  
  
5.  Geben Sie auf der Seite **Neue Ressource** des Assistenten für Ressourcen einen Namen ein, und wählen Sie **Allgemeiner Dienst** als **Diensttyp**aus. Ändern Sie den Wert für **Gruppe**nicht. Klicken Sie auf **Weiter**.  
  
6.  Fügen Sie auf der Seite **Mögliche Besitzer** die Knoten des Clusters als mögliche Besitzer der Ressource hinzu, oder entfernen Sie sie. Klicken Sie auf **Weiter**.  
  
7.  Wählen Sie unter **Verfügbare Ressourcen** eine Ressource aus, und klicken Sie anschließend auf **Hinzufügen**, um Abhängigkeiten auf der Seite **Abhängigkeiten**hinzuzufügen. Im Falle eines Failovers sollten sowohl [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als auch der freigegebene Datenträger mit den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen wieder online geschaltet werden, bevor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] online geschaltet wird. Nachdem Sie die Abhängigkeiten ausgewählt haben, klicken Sie auf **Weiter**.  
  
     Weitere Informationen finden Sie unter [Hinzufügen von Abhängigkeiten zu einer Ressource von SQL Server](../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md).  
  
8.  Geben Sie auf der Seite **Allgemeine Dienstparameter** **MsDtsServer** als Namen des Diensts ein. Klicken Sie auf **Weiter**.  
  
9. Klicken Sie auf der Seite **Registrierungsreplikation** auf **Hinzufügen** , um den Registrierungsschlüssel hinzuzufügen, der den Speicherort der Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst identifiziert. Diese Datei muss sich auf einem freigegebenen Datenträger befinden, der sich in der gleichen Ressourcengruppe wie der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst befindet.  
  
10. Geben Sie im Dialogfeld **Registrierungsschlüssel** **SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile**ein. Klicken Sie auf **OK**und anschließend auf **Fertig stellen**.  
  
     Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst wurde nun als Clusterressource hinzugefügt.  
  
### <a name="to-configure-the-integration-services-service-and-package-store"></a>So konfigurieren Sie den Integration Services-Dienst und den Paketspeicher  
  
1.  Suchen Sie die Konfigurationsdatei unter %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml. Kopieren Sie sie auf den freigegebenen Datenträger für die Gruppe, der Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst hinzugefügt haben.  
  
2.  Erstellen Sie auf dem freigegebenen Datenträger einen neuen Ordner mit dem Namen **Packages** . Dieser soll als Paketspeicher dienen. Erteilen Sie den entsprechenden Benutzern und Gruppen Ordnerauflist- und Schreibberechtigungen für den neuen Ordner.  
  
3.  Öffnen Sie die Konfigurationsdatei auf dem freigegebenen Datenträger in einem Text- oder XML-Editor. Ändern Sie den Wert des **ServerName** -Elements in den Namen des virtuellen Servers [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , der sich in der gleichen Ressourcengruppe befindet.  
  
4.  Ändern Sie den Wert des **StorePath** -Elements in den vollqualifizierten Pfad des Ordners **Packages** , der in einem vorangehenden Schritt auf dem freigegebenen Datenträger erstellt wurde.  
  
5.  Ersetzen Sie den Wert der Datei **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** in der Registrierung durch den vollqualifizierten Pfad und Namen der Dienstkonfigurationsdatei auf dem freigegebenen Datenträger.  
  
### <a name="to-bring-the-integration-services-service-online"></a>So schalten Sie den Integration Services-Dienst online  
  
-   Wählen Sie in der **Clusterverwaltung**den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst aus, klicken Sie mit der rechten Maustaste, und wählen Sie im Popupmenü **Online schalten** aus. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ist nun als Clusterressource online.  
  
  

