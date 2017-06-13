---
title: "Eine im einheitlichen Modus Bericht-Bereitstellung für dezentrales Skalieren konfigurieren | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], deployments
- deploying [Reporting Services], scale-out deployment model
- scale-out deployments [Reporting Services]
ms.assetid: b30d0308-4d9b-4f85-9f83-dece4dcb2775
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6a90a566e3e100fff3bb17e838a368a82ac3f4f5
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---

# <a name="configure-a-native-mode-report-server-scale-out-deployment"></a>Konfigurieren der Bereitstellung für horizontales Skalieren für Berichtsserver im einheitlichen Modus

  Der einheitliche Modus von Reporting Services unterstützt ein Bereitstellungsmodell für horizontales Skalieren, das die Ausführung mehrerer Berichtsserverinstanzen ermöglicht, die eine einzelne Berichtsserver-Datenbank gemeinsam nutzen. Die Bereitstellung für horizontales Skalieren wird verwendet, um die Skalierbarkeit von Berichtsservern zu erhöhen, sodass diese mehr gleichzeitige Benutzer und größere Berichtsausführungslasten unterstützen. Darüber hinaus können damit bestimmte Server für die Verarbeitung von interaktiven oder geplanten Berichten reserviert werden.  
  
 Berichtsserver im SharePoint-Modus verwenden die SharePoint-Produktinfrastruktur für horizontales Skalieren. Der SharePoint-Modus für horizontales Skalieren wird durch das Hinzufügen weiterer Berichtsserver im SharePoint-Modus zur SharePoint-Farm ausgeführt. Informationen zum horizontalen Skalieren im SharePoint-Modus finden Sie unter [Hinzufügen eines zusätzlichen Berichtsservers zu einer Farm &#40;Horizontales Skalieren für SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
 
  Eine *Bereitstellung für horizontales Skalieren* wird in den folgenden Szenarien verwendet:  
  
-   Als erforderliche Komponente für den Lastenausgleich mehrerer Berichtsserver in einem Servercluster. Bevor Sie einen Lastenausgleich für mehrere Berichtsserver ausführen können, müssen Sie sie zunächst für dieselbe Berichtsserver-Datenbank konfigurieren.  
  
-   Um Berichtsserver-Anwendungen auf verschiedenen Computern zu segmentieren, indem ein Server für die interaktive Berichtsverarbeitung und ein zweiter Server für die Planung der Berichtsverarbeitung verwendet wird. In diesem Szenario verarbeitet jede Serverinstanz verschiedene Anforderungen für denselben Berichtsserver-Inhalt, der in der freigegebenen Berichtsserver-Datenbank gespeichert ist.  
  
 **Bereitstellungen für horizontales Skalieren bestehen aus folgenden Komponenten:**  
  
-   Zwei oder mehr Berichtsserverinstanzen, die eine Berichtsserver-Datenbank gemeinsam nutzen  
  
-   Optional: Ein NLB-Cluster (Network Load Balancing, Netzwerklastenausgleich), um interaktive Benutzerlasten auf die Berichtsserverinstanzen zu verteilen  
  
 Wenn Sie Reporting Services auf einem NLB-Cluster bereitstellen, müssen Sie bei der Konfiguration von Berichtsserver-URLs den Namen des virtuellen NLB-Servers verwenden, und die Server müssen für die Verwendung desselben Anzeigestatus konfiguriert sein.  
  
 Reporting Services ist nicht Teil von MSCS-Clustern (Microsoft Clusterdienste). Sie können die Berichtsserver-Datenbank jedoch auf einer Datenbankmodul-Instanz erstellen, die Teil eines Failover-Clusters ist.  
  
 **Führen Sie folgende Schritte aus, um eine Bereitstellung für horizontales Skalieren zu planen, zu installieren und zu konfigurieren:**  
  
-   Anweisungen zum Installieren von Berichtsserverinstanzen finden Sie unter [Installieren von SQL Server 2016 vom Installations-Assistenten aus &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
-   Wenn Sie vorhaben, die Bereitstellung für horizontales Skalieren auf einem NLB-Cluster (Network Load Balancing, Netzwerklastenausgleich) zu hosten, müssen Sie den NLB-Cluster zuerst konfigurieren. Weitere Informationen finden Sie unter [Configure a Report Server on a Network Load Balancing Cluster](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md).  
  
-   Machen Sie sich mit den Verfahren in diesem Thema vertraut. Hier finden Sie Anweisungen zum Freigeben einer Berichtsserver-Datenbank und zum Verknüpfen von Berichtsservern für das horizontale Skalieren.  
  
     In den Verfahren wird erläutert, wie eine Bereitstellung für horizontales Skalieren mit Zwei-Knoten-Berichtsserver konfiguriert wird. Wiederholen Sie die Schritte in diesem Thema, um zusätzliche Berichtsserverknoten zur Skalierung hinzuzufügen.  
  
    -   Über das Setup können Sie jede Berichtsserverinstanz installieren, die mit der horizontalen Skalierung verbunden werden soll.  
  
         Damit Datenbank-Kompatibilitätsfehler vermieden werden, wenn Sie die Serverinstanzen mit der freigegebenen Datenbank verbinden, müssen Sie sicherstellen, dass alle Instanzen dieselbe Version aufweisen. Beispielsweise bei der Erstellung der Berichtsserver-Datenbank mit einer SQL Server 2016-Berichtsserverinstanz müssen alle anderen Instanzen in der gleichen Bereitstellung auch SQL Server 2016 sein.  
  
    -   Mit dem Konfigurations-Manager für Reporting Services stellen Sie eine Verbindung von den einzelnen Berichtsservern zu der gemeinsamen Datenbank her. Sie können nur jeweils eine Verbindung zu einem Berichtsserver herstellen und diesen Berichtsserver konfigurieren.  
  
    -   Mit dem Konfigurationstool für Reporting Services können Sie die horizontale Skalierung durchführen, indem Sie eine Verbindung von den neuen Berichtsserverinstanzen zur ersten Berichtsserverinstanz herstellen, die bereits an die Berichtsserverdatenbank angeschlossen ist.  
  
## <a name="to-install-a-sql-server-instance-to-host-the-report-server-databases"></a>So installieren Sie eine SQL Server-Instanz zum Hosten der Berichtsserver-Datenbanken  
  
1.  Installieren Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz auf einem Computer, der als Host für die Berichtsserver-Datenbanken fungiert. Sie müssen mindestens [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]installieren.  
  
2.  Falls notwendig, aktivieren Sie Remoteverbindungen auf dem Berichtsserver. In einigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind Remoteverbindungen für TCP/IP und Named Pipes standardmäßig nicht aktiviert. Verwenden Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager, und zeigen Sie die Einstellungen für die Netzwerkkonfiguration der Zielinstanz an, um festzustellen, ob Remoteverbindungen zugelassen werden. Wenn die Remoteinstanz zudem eine benannte Instanz ist, müssen Sie sicherstellen, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienst auf dem Zielserver aktiviert ist und ausgeführt wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser stellt die Portnummer bereit, mit der die Verbindung zur benannten Instanz hergestellt wird. 

## <a name="service-accounts"></a>Dienstkonten

Die für die Reporting Services-Instanz verwendeten Dienstkonten sind wichtig, beim Umgang mit einer Bereitstellung für horizontales Skalieren. Sie sollten einen der folgenden beim Bereitstellen von Reporting Services-Instanzen ausführen.

**Option 1:** alle Reporting Services-Instanzen müssen mit dem gleichen Domänenbenutzerkonto für das Dienstkonto konfiguriert werden.

**Option 2:** jedes einzelnen-Dienstkonto, Domänenkonto oder nicht, müssen Dbadmin-Berechtigungen in der SQL Server-Instanz erteilt werden, die den ReportServer-Katalogdatenbank gehostet wird.

Wenn Sie eine andere Konfiguration als eine der oben genannten Optionen konfiguriert haben, können ändern von Aufgaben im Zusammenhang mit SQL-Agent sind zwischenzeitliche Fehler auftreten. Dies wird angezeigt wie einen Fehler in der sowohl das Reporting Services zu protokollieren und auf das Webportal beim Bearbeiten eines Berichtsabonnements.

```
An error occurred within the report server database.  This may be due to a connection failure, timeout or low disk condition within the database.
``` 

Das Problem zeitweilig ist werden, die nur der Server, den SQL-Agent-Task erstellt, hat, Rechte zum Anzeigen besitzt, löschen oder Bearbeiten des Elements. Wenn Sie eine der oben aufgeführten Optionen nicht tun, werden die Vorgänge nur erfolgreich, wenn der Load Balancer alle Ihre Anforderungen für dieses Abonnement an den Server sendet, die der SQL-Agent-Task erstellt. 
  
## <a name="to-install-the-first-report-server-instance"></a>So installieren Sie die erste Berichtsserverinstanz  
  
1.  Installieren Sie die erste Berichtsserverinstanz, die Teil der Bereitstellung ist. Wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]installieren, wählen Sie auf der Seite Berichtsserver-Installationsoptionen die Option **Server installieren, jedoch nicht konfigurieren** .  
  
2.  Starten Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool.  
  
3.  Konfigurieren Sie die Berichtsserver-Webdienst-URL, Webportal-URL und der Berichtsserver-Datenbank. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers &#40;einheitlicher Reporting Services-Modus&#41;](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
4.  Überprüfen Sie, ob der Berichtsserver betriebsbereit ist. Weitere Informationen finden Sie unter [Überprüfen einer Installation von Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## <a name="to-install-and-configure-the-second-report-server-instance"></a>So installieren und konfigurieren Sie die zweite Berichtsserverinstanz  
  
1.  Führen Sie das Setup aus, um eine zweite Instanz von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf einem anderen Computer oder als benannte Instanz auf demselben Computer zu installieren. Wenn Sie Reporting Services installieren, wählen Sie auf der Seite Berichtsserver-Installationsoptionen die Option **Server installieren, jedoch nicht konfigurieren** .  
  
2.  Starten Sie das Konfigurationstool für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , und stellen Sie eine Verbindung mit der soeben installierten neuen Instanz her.  
  
3.  Stellen Sie eine Verbindung zwischen dem Berichtsserver und der Datenbank her, die Sie für die erste Berichtsserverinstanz verwendet haben:  
  
    1.  Wählen Sie **Datenbank** aus, um die Datenbankseite zu öffnen.  
  
    2.  Wählen Sie **Datenbank ändern**aus.  
  
    3.  Wählen Sie **Vorhandene Berichtsserver-Datenbank auswählen**aus.  
  
    4.  Geben Sie den Servernamen für die Instanz des SQL Server-Datenbankmoduls an, auf der die gewünschte Berichtsserver-Datenbank gehostet wird. Dies muss derselbe Server sein, zu dem Sie in den vorherigen Schritten eine Verbindung hergestellt haben.  
  
    5.  Wählen Sie **Verbindung testen**und dann **Weiter**aus.  
  
    6.  Wählen Sie unter **Berichtsserver-Datenbank**die Datenbank aus, die Sie für den ersten Berichtsserver erstellt haben, und wählen Sie dann **Weiter**aus. Der Standardname lautet "ReportServer". Wählen Sie nicht die Option ReportServerTempDB. Dieser Eintrag wird nur zum Speichern temporärer Daten während der Berichtsverarbeitung verwendet. Wiederholen Sie die letzten vier Schritte, um eine Verbindung zum Server herzustellen, wenn die Datenbank leer ist.  
  
    7.  Wählen Sie auf der Seite Anmeldeinformationen den Typ des Kontos und der Anmeldeinformationen aus, die der Berichtsserver für die Verbindung zur Berichtsserver-Datenbank verwendet. Sie können dieselben Anmeldeinformationen verwenden, die von der ersten Berichtsserverinstanz verwendet werden, oder andere. Wählen Sie **Weiter**aus.  
  
    8.  Wählen Sie **Zusammenfassung** und dann **Fertig stellen**aus.  
  
4.  Konfigurieren Sie die **Webdienst-URL**für den Berichtsserver. Testen Sie die URL noch nicht. Diese wird erst aufgelöst, wenn der Berichtsserver mit der horizontalen Skalierung verbunden wird.  
  
5.  Konfigurieren Sie die **Webportal-URL**. Testen Sie die URL noch nicht, und versuchen Sie noch nicht, die Anwendung zu überprüfen. Der Berichtsserver steht erst zur Verfügung, wenn er mit der horizontalen Skalierung verbunden ist.  
  
## <a name="to-join-the-second-report-server-instance-to-the-scale-out-deployment"></a>So verbinden Sie die zweite Berichtsserverinstanz mit der horizontalen Skalierung  
  
1.  Öffnen Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, und stellen Sie wieder eine Verbindung mit der ersten Berichtsserverinstanz her. Der erste Berichtsserver ist bereits für umkehrbare Verschlüsselungsvorgänge initialisiert. Daher kann er verwendet werden, um weitere Berichtsserverinstanzen mit der Bereitstellung für horizontales Skalieren zu verbinden.  
  
2.  Klicken Sie auf **Bereitstellung für horizontales Skalieren** , um die Seite „Bereitstellung für horizontales Skalieren“ zu öffnen. Hier sollten zwei Einträge angezeigt werden, einer für jede Berichtsserverinstanz, die mit der Berichtsserver-Datenbank verbunden ist. Für die erste Berichtsserverinstanz sollte bereits eine Verbindung bestehen. Der zweite Berichtsserver sollte auf den Join warten. Wenn Sie keine ähnlichen Einträge für die Skalieranwendung sehen, sollten Sie sich vergewissern, dass Sie mit dem ersten Berichtsserver verbunden sind, der bereits für die Verwendung der Berichtsserver-Datenbank konfiguriert und initialisiert wurde.  
  
     ![Bildschirmteilfoto der Seite "Bereitstellung für horizontales Skalieren"](../../reporting-services/install-windows/media/scaloutscreen.gif "bildschirmteilfoto der Seite "Bereitstellung für horizontales Skalieren"")  
  
3.  Wählen Sie auf der Seite „Bereitstellung für horizontales Skalieren“ die Berichtsserverinstanz aus, die auf den Join mit der Bereitstellung wartet, und wählen Sie **Server hinzufügen**aus.  
  
    > [!NOTE]  
    >  **Problem** : Wenn Sie versuchen, eine Reporting Services-Berichtsserverinstanz mit der Bereitstellung für horizontales Skalieren zu verknüpfen, wird möglicherweise eine Fehlermeldung vom Typ „Zugriff verweigert“ angezeigt.  
    >   
    >  **Problemumgehung:** Sichern Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Verschlüsselungsschlüssel von der ersten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz, und stellen Sie den Schlüssel auf dem zweiten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver wieder her. Versuchen Sie dann, den zweiten Server mit der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bereitstellung für horizontales Skalieren zu verknüpfen.  
  
4.  Sie sollten jetzt feststellen können, dass beide Berichtsserverinstanzen funktionstüchtig sind. Zur Überprüfung der zweiten Instanz können Sie über das Reporting Services-Konfigurationstool eine Verbindung mit dem Berichtsserver herstellen und auf die **Webdienst-URL** oder die **Webportal-URL**klicken.  
  
 Wenn Sie die Berichtsserver in einem Servercluster mit Lastenausgleich ausführen möchten, sind zusätzliche Konfigurationsschritte erforderlich. Weitere Informationen finden Sie unter [Configure a Report Server on a Network Load Balancing Cluster](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md).  

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren eines Dienstkontos](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0)   
[Konfigurieren einer URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Erstellen einer Berichtsserver-Datenbank im einheitlichen Modus](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
[Konfigurieren von Berichtsserver-URLs](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[Konfigurieren Sie eine Verbindung mit der Berichtsserver-Datenbank](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[Hinzufügen und Entfernen von Verschlüsselungsschlüsseln für die Bereitstellung für horizontales Skalieren](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
[Verwalten eines Berichtsservers von Reporting Services im einheitlichen Modus](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
