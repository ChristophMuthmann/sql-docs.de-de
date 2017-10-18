---
title: Aktualisieren einer SQL Server-Failoverclusterinstanz (Setup) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/22/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
caps.latest.revision: 63
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 50db49a567f4247b1014fba9114aa168b90709f5
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>Aktualisieren einer SQL Server-Failoverclusterinstanz (Setup)
  Sie können einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster mithilfe der Setupbenutzeroberfläche für [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] oder mithilfe einer Eingabeaufforderung auf einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster aktualisieren.  
  
 Bei lokalen Installationen müssen Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie auf der Remotefreigabe ein Domänenkonto mit Leseberechtigungen verwenden.  
  
 Lesen Sie zur Vorbereitung auf das Aktualisieren [Aktualisieren einer SQL Server-Failoverclusterinstanz (Setup)](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md).  
  
##  <a name="UpgradeSteps"></a> So aktualisieren Sie einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>So aktualisieren Sie einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster  
  
1.  Doppelklicken Sie in den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationsmedien für die Edition, die der Edition entspricht, die Sie aktualisieren, im Stammordner auf „setup.exe“. Möglicherweise werden Sie aufgefordert, die erforderlichen Komponenten zu installieren, falls sie nicht bereits installiert wurden.  
  
2.  Nachdem die erforderlichen Komponenten installiert wurden, startet der Installations-Assistent das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationscenter. Wählen Sie zum Aktualisieren einer vorhandenen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Ihre Instanz aus.  
  
3.  Wenn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup-Unterstützungsdateien erforderlich sind, werden diese durch das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup installiert. Wenn Sie zum Neustarten des Computers aufgefordert werden, führen Sie einen Neustart durch, bevor Sie den Vorgang fortsetzen.  
  
4.  Die Systemkonfigurationsprüfung führt einen Ermittlungsvorgang auf dem Computer aus. [!INCLUDE[clickOK](../../../includes/clickok-md.md)], um den Vorgang fortzusetzen.  
  
5.  Geben Sie auf der Seite Product Key den PID-Schlüssel für die neue Versionsedition ein, die der Edition der alten Produktversion entspricht. Wenn Sie z. B. einen Enterprise-Failovercluster aktualisieren möchten, müssen Sie einen PID-Schlüssel für [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]angeben. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen. Der für ein Failoverclusterupgrade verwendete PID-Schlüssel muss für alle Failoverclusterknoten einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz einheitlich sein.  
  
6.  Lesen Sie auf der Seite mit den Lizenzbedingungen den Lizenzvertrag, und aktivieren Sie dann das Kontrollkästchen, um den Lizenzbestimmungen zuzustimmen. Falls Sie zur Verbesserung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]beitragen möchten, können Sie auch die Option zur Funktionsverwendung aktivieren und Berichte an [!INCLUDE[msCoName](../../../includes/msconame-md.md)]senden. **Klicken Sie auf „Weiter“, um den Vorgang fortzusetzen**. Klicken Sie auf **Abbrechen**, wenn Sie den Setupvorgang beenden möchten.  
  
7.  Geben Sie auf der Seite Instanz auswählen die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] an, die auf [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]aktualisiert werden soll. **Klicken Sie auf „Weiter“, um den Vorgang fortzusetzen**.  
  
8.  Auf der Seite Funktionsauswahl sind die zu aktualisierenden Funktionen bereits markiert. Nach Auswahl des Funktionsnamens wird im rechten Bereich eine Beschreibung für die einzelnen Komponentengruppen angezeigt. Sie können die zu aktualisierenden Funktionen nicht ändern und während des Aktualisierungsvorgangs keine Funktionen hinzufügen. Wenn Sie einer aktualisierten Instanz von [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Funktionen hinzufügen möchten, nachdem der Upgradevorgang abgeschlossen wurde, finden Sie entsprechende Informationen unter [Hinzufügen von Funktionen zu einer Instanz von SQL Server 2016 &#40;Setup&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
  
     Die erforderlichen Komponenten für die ausgewählten Funktionen werden im rechten Bereich angezeigt. SQL Server-Setup installiert die erforderlichen Komponenten, die nicht bereits während des im weiteren Verlauf dieser Prozedur beschriebenen Installationsschritts installiert werden. Um Zeit zu sparen, sollten Sie die erforderlichen Komponenten im Voraus auf jedem Knoten installieren.  
  
9. Auf der Seite Instanzkonfiguration werden die Felder automatisch aus der alten Instanz aufgefüllt. Sie können optional auch den neuen InstanceID-Wert angeben.  
  
     **Instanz-ID** : Standardmäßig wird der Instanzname als Instanz-ID verwendet. Das Ziel ist dabei, Installationsverzeichnisse und Registrierungsschlüssel für die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zu identifizieren. Dies ist der Fall für Standardinstanzen und benannte Instanzen. Bei einer Standardinstanz lauten Instanzname und Instanz-ID MSSQLSERVER. Wenn Sie nicht die Standardinstanz-ID verwenden möchten, aktivieren Sie das Kontrollkästchen **Instanz-ID** , und geben Sie einen Wert ein. Wenn Sie den Standardwert überschreiben, müssen Sie die gleiche Instanz-ID für die Instanz angeben, die in allen Failoverclusterknoten aktualisiert wird. Die Instanz-ID für die aktualisierte Instanz muss in allen Knoten übereinstimmen.  
  
     **Ermittelte Instanzen und Funktionen** : Das Raster zeigt Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , die sich auf dem Computer befinden, auf dem das Setup ausgeführt wird. **Klicken Sie auf „Weiter“, um den Vorgang fortzusetzen**.  
  
10. Auf der Seite Erforderlicher Speicherplatz wird der für die angegebenen Funktionen erforderliche Speicherplatz berechnet, und die Anforderungen werden mit dem Speicherplatz verglichen, der auf dem Computer verfügbar ist, auf dem Setup ausgeführt wird.  
  
11. Geben Sie auf der Seite Aktualisieren der Volltextsuche die Aktualisierungsoptionen für die Datenbanken an, die aktualisiert werden sollen. Weitere Informationen finden Sie unter [Upgradeoptionen für die Volltextsuche](http://msdn.microsoft.com/library/16c9376b-5fbb-4495-a429-06a2493849c9).  
  
12. Geben Sie auf der Seite **Fehlerberichterstellung** die Informationen an, die Sie an [!INCLUDE[msCoName](../../../includes/msconame-md.md)] senden möchten, um zur Verbesserung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]beizutragen. Die Option für Fehlerberichte ist standardmäßig aktiviert.  
  
13. Bei der Systemkonfigurationsprüfung wird eine weitere Reihe von Regeln ausgeführt, um die Konfiguration des Computers anhand der von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Funktionen zu überprüfen, bevor der Aktualisierungsvorgang beginnt.  
  
14. Auf der Seite Clusteraktualisierungsbericht werden die Liste mit den Knoten in der Failoverclusterinstanz und die Instanzversionsinformationen für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Komponenten in jedem Knoten angezeigt. Der Datenbankskriptstatus und der Replikationsskriptstatus werden angezeigt. Außerdem werden Informationsmeldungen zu den Vorgängen angezeigt, die ausgeführt werden, wenn Sie auf **Weiter**klicken. Abhängig von der Anzahl bereits aktualisierter Failoverclusterknoten und der Gesamtzahl an Knoten zeigt Setup das Failoververhalten an, das ausgeführt wird, wenn Sie auf **Weiter**klicken. Es werden auch Warnungen bei möglicher unnötiger Ausfallzeit angezeigt, wenn die erforderlichen Komponenten noch nicht installiert sind.  
  
15. Auf der Seite Das Upgrade kann jetzt ausgeführt werden wird eine Strukturansicht der Installationsoptionen angezeigt, die während des Setups angegeben wurden. Klicken Sie zum Fortsetzen des Vorgangs auf **Aktualisieren**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Setup installiert zuerst die erforderlichen Komponenten für die ausgewählten Funktionen und dann die Funktionen.  
  
16. Während des Upgrades wird auf der Seite Status der Status angezeigt, sodass Sie während des Setupvorgangs den Upgradefortschritt überwachen können.  
  
17. Nach der Aktualisierung des aktuellen Knotens werden auf der Seite Clusteraktualisierungsbericht Statusinformationen zur Aktualisierung der einzelnen Failoverclusterknoten sowie die Funktionen in jedem Failoverclusterknoten und ihre Versionsinformationen angezeigt. Bestätigen Sie die angezeigten Versionsinformationen, und fahren Sie mit der Aktualisierung der verbleibenden Knoten fort. Wenn das Failover zu aktualisierten Knoten aufgetreten ist, wird dies ebenfalls auf der Statusseite angezeigt. Sie können diese Informationen zur Bestätigung außerdem im Windows-Clusterverwaltungstool überprüfen.  
  
18. Nach der Aktualisierung werden auf der Seite Abgeschlossen ein Link zur zusammenfassenden Protokolldatei für die Installation sowie weitere wichtige Hinweise bereitgestellt. Klicken Sie auf Schließen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , um die Installation von **abzuschließen**.  
  
19. Starten Sie den Computer neu, falls Sie dazu aufgefordert werden. Wenn Sie den Setupvorgang abgeschlossen haben, sollten Sie unbedingt die vom Installations-Assistenten angezeigte Meldung lesen. Weitere Informationen zu Setupprotokolldateien finden Sie unter [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
20. Wiederholen Sie diese Schritte in allen anderen Knoten des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusters, um den Upgradevorgang abzuschließen.  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>So aktualisieren Sie auf einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Multisubnetz-Failovercluster  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>Aktualisieren auf einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Multisubnetz-Failovercluster (vorhandener [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Cluster ist kein Multisubnetzcluster)  
  
1.  Führen Sie die oben beschriebenen Schritte zum Aktualisieren des Clusters auf [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]durch.  
  
2.  Fügen Sie mit der Setupaktion AddNode einen Knoten in einem anderen Subnetz hinzu, und bestätigen Sie auf der Seite **Netzwerkkonfiguration für Cluster** die Änderung der IP-Adressabhängigkeit in OR. Weitere Informationen finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>So aktualisieren Sie einen Multisubnetzcluster mit Stretch-V-Lan  
  
1.  Führen Sie die oben beschriebenen Schritte zum Aktualisieren des Clusters auf [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]durch.  
  
2.  Ändern Sie die Netzwerkeinstellungen, um den Remoteknoten in ein anderes Subnetz zu verschieben.  
  
3.  Fügen Sie mit dem Failovercluster-Manager von Windows eine neue IP-Adresse für das neue Subnetz hinzu, und legen Sie die IP-Adressabhängigkeit auf OR fest.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Führen Sie nach dem Aktualisieren auf [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]die folgenden Tasks aus:  
  
-   [Abschließen des Datenbankmodul-Upgrades](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [Ändern des Datenbank-Kompatibilitätsmodus und Verwenden des Abfragespeichers](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [Nutzen Sie die Vorteile der neuen Features von SQL Server 2016](http://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)  
  
## <a name="see-also"></a>Siehe auch  
 [Aktualisieren einer SQL Server-Failoverclusterinstanz (Setup)](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)   
 [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Hinzufügen von Funktionen zu einer Instanz von SQL Server 2016 &#40;Setup&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)  
  
  

