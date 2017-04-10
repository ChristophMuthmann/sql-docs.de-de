---
title: "Konfigurieren des Integration Services-Diensts als Clusterressource | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 367835aa-9855-4791-a989-b3d08402ad4c
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Konfigurieren des Integration Services-Diensts als Clusterressource
  Kunden, für die die Vorteile der Konfiguration des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Diensts als Clusterressource die Nachteile überwiegen, finden in diesem Abschnitt alle erforderlichen Konfigurationsanweisungen. [!INCLUDE[msCoName](../../includes/msconame-md.md)] rät dennoch von einer Konfiguration des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Diensts als Clusterressource ab.  
  
 Sie müssen Sie die folgenden Tasks ausführen, um den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst als Clusterressource zu konfigurieren.  
  
-   Installieren Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf einem Cluster.  
  
     Wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf einem Cluster installieren möchten, müssen Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf jedem Knoten im Cluster installieren.  
  
-   Konfigurieren Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] als Clusterressource.  
  
     Wenn Integration Services auf jedem Knoten im Cluster installiert ist, müssen Sie Integration Services als Clusterressource konfigurieren. Wenn Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst als Clusterressource konfigurieren, können Sie den Dienst der gleichen Ressourcengruppe wie [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] oder einer anderen Gruppe hinzufügen. In der folgenden Tabelle werden die möglichen Vor- und Nachteile des Auswählens einer Ressourcengruppe beschrieben.  
  
    |Wenn Integration Services und SQL Server sich in der gleichen Ressourcengruppe befinden|Wenn Integration Services und SQL Server sich in verschiedenen Ressourcengruppen befinden|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |Clientcomputer können mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Pakete verwalten, die in der msdb-Datenbank gespeichert sind, da sowohl der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Dienst als auch der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst auf dem gleichen virtuellen Server ausgeführt werden. Mit dieser Konfiguration können die Delegierungsprobleme des Doppelhopszenarios vermieden werden.|Clientcomputer können in der msdb-Datenbank gespeicherte Pakete nicht mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwalten. Der Client kann eine Verbindung mit dem virtuellen Server herstellen, auf dem der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst ausgeführt wird. Allerdings kann dieser Computer die Anmeldeinformationen des Benutzers nicht an den virtuellen Server delegieren, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Dies wird als Doppelhopszenario bezeichnet.|  
    |Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst teilt sich die CPU- und andere Computerressourcen mit anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Diensten.|Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst teilt sich die CPU- und andere Computerressourcen nicht mit anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Diensten, da die verschiedenen Ressourcengruppen auf verschiedenen Knoten konfiguriert sind.|  
    |Pakete können schneller in die msdb-Datenbank geladen und dort gespeichert werden, und dabei wird weniger Netzwerkverkehr generiert, weil beide Dienste auf dem gleichen Computer ausgeführt werden.|Das Laden und Speichern von Paketen in der msdb-Datenbank dauert möglicherweise länger und generiert mehr Netzwerkverkehr.|  
    |Beide Dienste sind gleichzeitig online oder offline.|Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst kann online sein, während [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] offline ist. Das bedeutet, dass die in der msdb-Datenbank von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gespeicherten Pakete nicht verfügbar sind.|  
    |Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst kann bei Bedarf nicht schnell zu einem anderen Knoten verschoben werden.|Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst kann bei Bedarf schneller zu einem anderen Knoten verschoben werden.|  
  
     Wenn Sie entschieden haben, welcher Ressourcengruppe [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] hinzugefügt werden soll, müssen Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] als Clusterressource in dieser Gruppe konfigurieren.  
  
-   Konfigurieren Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst und den Paketspeicher.  
  
     Nachdem Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] als Clusterressource konfiguriert haben, müssen Sie den Speicherort und den Inhalt der Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst auf jedem Knoten im Cluster ändern. Durch diese Änderungen sind bei einem Failover die Konfigurationsdatei und der Paketspeicher für alle Knoten verfügbar. Nachdem Sie den Speicherort und den Inhalt der Konfigurationsdatei geändert haben, müssen Sie den Dienst online schalten.  
  
-   Schalten Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst als Clusterressource online.  
  
 Nach dem Konfigurieren des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Diensts auf einem Cluster oder auf einem beliebigen Server müssen Sie möglicherweise DCOM-Berechtigungen konfigurieren, bevor Sie von einem Clientcomputer aus eine Verbindung mit dem Dienst herstellen können. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einem Integration Services-Remoteserver &#40;SSIS-Dienst&#41;](../../integration-services/service/connect-to-a-remote-integration-services-server-ssis-service.md).  
  
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst kann keine Anmeldeinformationen delegieren. Daher können Sie in der msdb-Datenbank gespeicherte Pakete nicht mithilfe von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] verwalten, wenn die folgenden Bedingungen zutreffen:  
  
-   Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden auf separaten Servern oder virtuellen Servern ausgeführt.  
  
-   Der Client, auf dem [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ausgeführt wird, ist ein dritter Computer.  
  
 Der Client kann eine Verbindung mit dem virtuellen Server herstellen, auf dem der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst ausgeführt wird. Allerdings kann dieser Computer die Anmeldeinformationen des Benutzers nicht an den virtuellen Server delegieren, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Dies wird als Doppelhopszenario bezeichnet.  
  
### So installieren Sie Integration Services auf einem Cluster  
  
1.  Installieren und konfigurieren Sie einen Cluster mit einem oder mehreren Knoten.  
  
2.  (Optional) Installieren Sie Clusterdienste, wie z.B. das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
3.  Installieren Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf jedem Knoten des Clusters.  
  
### So konfigurieren Sie Integration Services als Clusterressource  
  
1.  Öffnen Sie die **Clusterverwaltung**.  
  
2.  Wählen Sie in der Konsolenstruktur den Gruppenordner aus.  
  
3.  Wählen Sie im Ergebnisbereich die Gruppe aus, der Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] hinzufügen möchten:  
  
    -   Wählen Sie die Gruppe aus, zu der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gehört, um Integration Services als Clusterressource der gleichen Ressourcengruppe wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hinzuzufügen.  
  
    -   Um Integration Services als Clusterressource einer anderen Ressourcengruppe als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hinzuzufügen, wählen Sie eine Gruppe aus, zu der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht gehört.  
  
4.  Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie anschließend auf **Ressource**.  
  
5.  Geben Sie auf der Seite **Neue Ressource** des Assistenten für Ressourcen einen Namen ein, und wählen Sie **Allgemeiner Dienst** als **Diensttyp** aus. Ändern Sie den Wert für **Gruppe** nicht. Klicken Sie auf **Weiter**.  
  
6.  Fügen Sie auf der Seite **Mögliche Besitzer** die Knoten des Clusters als mögliche Besitzer der Ressource hinzu, oder entfernen Sie sie. Klicken Sie auf **Weiter**.  
  
7.  Wählen Sie unter **Verfügbare Ressourcen** eine Ressource aus, und klicken Sie anschließend auf **Hinzufügen**, um Abhängigkeiten auf der Seite **Abhängigkeiten** hinzuzufügen. Im Falle eines Failovers sollten sowohl [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als auch der freigegebene Datenträger mit den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen wieder online geschaltet werden, bevor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] online geschaltet wird. Nachdem Sie die Abhängigkeiten ausgewählt haben, klicken Sie auf **Weiter**.  
  
     Weitere Informationen finden Sie unter [Hinzufügen von Abhängigkeiten zu einer Ressource von SQL Server](../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md).  
  
8.  Geben Sie auf der Seite **Allgemeine Dienstparameter** **MsDtsServer** als Namen des Diensts ein. Klicken Sie auf **Weiter**.  
  
9. Klicken Sie auf der Seite **Registrierungsreplikation** auf **Hinzufügen**, um den Registrierungsschlüssel hinzuzufügen, der den Speicherort der Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst identifiziert. Diese Datei muss sich auf einem freigegebenen Datenträger befinden, der sich in der gleichen Ressourcengruppe wie der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst befindet.  
  
10. Geben Sie im Dialogfeld **Registrierungsschlüssel** **SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** ein. Klicken Sie auf **OK** und anschließend auf **Fertig stellen**.  
  
     Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst wurde nun als Clusterressource hinzugefügt.  
  
### So konfigurieren Sie den Integration Services-Dienst und den Paketspeicher  
  
1.  Suchen Sie die Konfigurationsdatei unter %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml. Kopieren Sie sie auf den freigegebenen Datenträger für die Gruppe, der Sie den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst hinzugefügt haben.  
  
2.  Erstellen Sie auf dem freigegebenen Datenträger einen neuen Ordner mit dem Namen **Packages**. Dieser soll als Paketspeicher dienen. Erteilen Sie den entsprechenden Benutzern und Gruppen Ordnerauflist- und Schreibberechtigungen für den neuen Ordner.  
  
3.  Öffnen Sie die Konfigurationsdatei auf dem freigegebenen Datenträger in einem Text- oder XML-Editor. Ändern Sie den Wert des **ServerName**-Elements in den Namen des virtuellen Servers [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], der sich in der gleichen Ressourcengruppe befindet.  
  
4.  Ändern Sie den Wert des **StorePath**-Elements in den vollqualifizierten Pfad des Ordners **Packages**, der in einem vorangehenden Schritt auf dem freigegebenen Datenträger erstellt wurde.  
  
5.  Ersetzen Sie den Wert der Datei **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** in der Registrierung durch den vollqualifizierten Pfad und Namen der Dienstkonfigurationsdatei auf dem freigegebenen Datenträger.  
  
### So schalten Sie den Integration Services-Dienst online  
  
-   Wählen Sie in der **Clusterverwaltung** den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst aus, klicken Sie mit der rechten Maustaste, und wählen Sie im Popupmenü **Online schalten** aus. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst ist nun als Clusterressource online.  
  
  