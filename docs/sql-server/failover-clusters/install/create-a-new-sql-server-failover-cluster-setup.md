---
title: Erstellen eines neuen SQL Server-Failoverclusters (Setup)|Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
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
- adding nodes
- failover clustering [SQL Server], creating clusters
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- clusters [SQL Server], creating
- removing nodes
ms.assetid: 30e06a7d-75e9-44e2-bca3-b3b0c4a33f61
caps.latest.revision: 77
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: a1553c7584ec6d90bcefbbdabf7c44788830740d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-new-sql-server-failover-cluster-setup"></a>Erstellen eines neuen SQL Server-Failoverclusters (Setup)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Zum Installieren oder Aktualisieren eines [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusters müssen Sie das Setupprogramm für jeden einzelnen Knoten des Failoverclusters ausführen. Zum Hinzufügen eines Knotens zu einem vorhandenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster müssen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup für den Knoten ausführen, der der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz hinzugefügt werden soll. Führen Sie zum Verwalten der anderen Knoten Setup nicht für den aktiven Knoten aus.  
  
 Je nachdem, wie die Knoten gruppiert werden, wird der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster wie folgt konfiguriert:  
  
-   Knoten im gleichen Subnetz bzw. in der gleichen Gruppe von Subnetzen: Die IP-Adressabhängigkeit wird für diese Arten der Konfigurationen auf AND festgelegt.  
  
-   Knoten in anderen Subnetzen: Die IP-Adressabhängigkeit wird auf OR festgelegt, und die Konfiguration wird als [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Multisubnetz-Failoverclusterkonfiguration bezeichnet. Weitere Informationen finden Sie unter [SQL Server-Multisubnetzclustering &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md).  
  
 Die folgenden Optionen sind für die Installation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclustern verfügbar:  
  
 **Option 1: Integrierte Installation mithilfe von Knoten hinzufügen**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstallation besteht aus den folgenden Schritten:  
  
-   Erstellen und konfigurieren Sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz mit einem einzelnen Knoten. Wenn Sie den Knoten erfolgreich konfigurieren, verfügen Sie über eine voll funktionsfähige Failoverclusterinstanz. Zu diesem Zeitpunkt verfügt diese noch nicht über Hochverfügbarkeit, da nur ein Knoten im Failovercluster vorhanden ist.  
  
-   Führen Sie für jeden Knoten, der dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster hinzufügt werden soll, Setup mithilfe der Funktion Knoten hinzufügen aus.  
  
    -   Wenn der Knoten, den Sie hinzufügen, zusätzliche oder andere Subnetze enthält, ermöglicht Setup Ihnen, zusätzliche IP-Adressen anzugeben. Wenn der Knoten, den Sie hinzufügen, sich in einem anderen Subnetz befindet, müssen Sie auch die Änderung der IP-Adressabhängigkeit auf OR bestätigen. Weitere Informationen zu den verschiedenen möglichen Szenarien beim Hinzufügen von Knoten finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
 **Option 2: Erweiterte bzw. Enterprise-Installation**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] : die Installation des Advanced/Enterprise-Failoverclusters besteht aus den folgenden Schritten:  
  
-   Führen Sie für jeden Knoten, bei dem es sich um einen möglichen Besitzer des neu zu erstellenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusters handelt, die im [Abschnitt "Vorbereitung"](#prepare)aufgeführten Setupschritte zum Vorbereiten des Failoverclusters aus. Nachdem Sie die Schritte zum Vorbereiten des Failoverclusters für einen Knoten ausgeführt haben, erstellt Setup die Datei Configuration.ini, in der alle Einstellungen aufgeführt werden, die Sie angegeben haben. Für die zusätzlichen vorzubereitenden Knoten können Sie die automatisch generierte Datei Configuration.ini von dem ersten Knoten als Eingabe in der Setup-Befehlszeile bereitstellen, statt diese Schritte auszuführen. Weitere Informationen finden Sie unter [Installieren von SQL Server 2016 mithilfe einer Konfigurationsdatei](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md). Mit diesem Schritt werden die Knoten für die Gruppierung vorbereitet. Nach diesem Schritt ist jedoch keine funktionstüchtige [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz vorhanden.  
  
-   Nachdem die Knoten für das Clustering bereit sind, führen Sie Setup auf einem der vorbereiteten Knoten aus. Durch diesen Schritt wird die Failoverclusterinstanz konfiguriert und abgeschlossen. Am Ende dieses Schritts verfügen Sie über eine funktionsfähige [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz, und alle zuvor für diese Instanz vorbereiteten Knoten sind die potenziellen Besitzer des neu erstellten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusters.  
  
     Wenn Sie Knoten in mehreren Subnetzen gruppieren, erkennt Setup die Union aller Subnetze in allen Knoten, für die eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz vorbereitet wurde. Sie können mehrere IP-Adressen für die Subnetze angeben. Jeder vorbereitete Knoten muss möglicher Besitzer mindestens einer IP-Adresse sein.  
  
     Wenn alle IP-Adressen, die für die Subnetze angegeben wurden, in allen vorbereiteten Knoten unterstützt werden, wird die Abhängigkeit auf AND festgelegt.  
  
     Wenn alle IP-Adressen, die für die Subnetze angegeben wurden, in allen vorbereiteten Knoten nicht unterstützt werden, wird die Abhängigkeit auf OR festgelegt. Weitere Informationen finden Sie unter [SQL Server-Multisubnetzclustering &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md).  
  
    > [!NOTE]  
    >  Zum Abschließen des Failoverclusters muss der zugrunde liegende Windows-Failovercluster vorhanden sein. Wenn der Windows-Failovercluster nicht vorhanden ist, wird Setup mit einem Fehler beendet.  
  
 Weitere Informationen zum Hinzufügen oder zum Entfernen von Knoten zu bzw. aus einer vorhandenen Failoverclusterinstanz finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
 Weitere Informationen zur Remoteinstallation finden Sie unter [Unterstützte Versions- und Editionsupgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
 Weitere Informationen zur Installation von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in einem Windows-Failovercluster finden Sie unter [Verwenden von SQL Server Analysis Services in einem Cluster](http://go.microsoft.com/fwlink/p/?LinkId=396548).  
  
## <a name="prerequisites"></a>Voraussetzungen  
 Konsultieren Sie vor der Installation die folgenden Themen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Onlinedokumentation:  
  
-   [Planen einer SQL Server-Installation](../../../sql-server/install/planning-a-sql-server-installation.md)  
  
-   [Vor dem Installieren des Failoverclusterings](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
-   [Überlegungen zur Sicherheit bei SQL Server-Installationen](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [SQL Server-Multisubnetzclustering &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)  
  
> [!NOTE]  
>  Notieren Sie sich die Adresse des freigegebenen Laufwerks in der Clusterverwaltung, bevor Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup ausführen. Sie benötigen diese Informationen, um einen neuen Failovercluster zu erstellen.  
  
### <a name="to-install-a-new-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-integrated-install-with-add-node"></a>So installieren Sie einen neuen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster mithilfe der integrierten Installation mit "Knoten hinzufügen"  
  
1.  Legen Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationsmedium ein, und doppelklicken Sie im Stammordner auf Setup.exe. Wenn Sie eine Installation über eine Netzwerkfreigabe ausführen möchten, navigieren Sie in der Freigabe zum Stammordner, und doppelklicken Sie dann auf Setup.exe. Weitere Informationen zum Installieren der erforderlichen Komponenten finden Sie unter [Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md).  
  
2.  Das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Installationscenter wird vom Installations-Assistenten ausgeführt. Klicken Sie zum Erstellen einer neuen Clusterinstallation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf der Installationsseite auf **Neue [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failoverclusterinstallation**.  
  
3.  Die Systemkonfigurationsprüfung führt einen Ermittlungsvorgang auf dem Computer aus. [!INCLUDE[clickOK](../../../includes/clickok-md.md)], um den Vorgang fortzusetzen. Sie können die Details auf dem Bildschirm anzeigen, indem Sie auf **Details anzeigen**klicken, oder als HTML-Bericht, indem Sie auf **Detaillierten Bericht anzeigen**klicken.  
  
4.  Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
5.  Klicken Sie auf der Seite **Setup-Unterstützungsdateien** auf Installieren, um die Setup-Unterstützungsdateien zu installieren.  
  
6.  Die Systemkonfigurationsprüfung überprüft den Systemstatus des Computers, bevor Setup fortgesetzt wird. Nachdem die Prüfung abgeschlossen wurde, klicken Sie auf **Weiter** , um den Vorgang fortzusetzen. Sie können die Details auf dem Bildschirm anzeigen, indem Sie auf **Details anzeigen**klicken, oder als HTML-Bericht, indem Sie auf **Detaillierten Bericht anzeigen**klicken.  
  
7.  Geben Sie auf der Seite Product Key an, ob Sie eine kostenlose Edition von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]installieren oder über einen PID-Schlüssel für eine Produktionsversion des Produkts verfügen. Weitere Informationen finden Sie unter [Editionen und Komponenten von SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
8.  Lesen Sie auf der Seite mit den Lizenzbedingungen den Lizenzvertrag, und aktivieren Sie dann das Kontrollkästchen, um den Lizenzbestimmungen zuzustimmen. Falls Sie zur Verbesserung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]beitragen möchten, können Sie auch die Option zur Funktionsverwendung aktivieren und Berichte an [!INCLUDE[msCoName](../../../includes/msconame-md.md)]senden. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen. Klicken Sie auf **Abbrechen**, wenn Sie den Setupvorgang beenden möchten.  
  
9. Wählen Sie auf der Seite Funktionsauswahl die Komponenten für die Installation aus. Nach Auswahl des Funktionsnamens wird im rechten Bereich eine Beschreibung für die einzelnen Komponentengruppen angezeigt. Sie können eine beliebige Kombination von Kontrollkästchen aktivieren, das Failoverclustering wird jedoch nur von [!INCLUDE[ssDE](../../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] im tabellarischen Modus und [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] im mehrdimensionalen Modus unterstützt. Andere ausgewählte Komponenten werden als eigenständige Funktion ohne Failoverfunktionen für den aktuellen Knoten ausgeführt, für den das Setup erfolgt. Weitere Informationen zu [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Bereitstellungsmodi finden Sie unter [Bestimmen des Servermodus einer Analysis Services-Instanz](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
     Die erforderlichen Komponenten für die ausgewählten Funktionen werden im rechten Bereich angezeigt. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup installiert die erforderlichen Komponenten, die nicht bereits während des Installationsschritts installiert werden, der im weiteren Verlauf dieser Prozedur beschrieben wird.  
  
     Sie können ein benutzerdefiniertes Verzeichnis für freigegebene Komponenten angeben. Verwenden Sie dazu das Feld unten auf dieser Seite. Um den Installationspfad für freigegebene Komponenten zu ändern, aktualisieren Sie den Pfad im Feld unten im Dialogfeld, oder klicken Sie auf die Schaltfläche mit den drei Punkten, um zu einem Installationsverzeichnis zu navigieren. Der Standardinstallationspfad lautet „C:\Programme\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] \\“.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt auch das Installieren von Systemdatenbanken (Master, Modell, MSDB und TempDB) und [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Benutzerdatenbanken auf einer Server Message Block-Dateifreigabe (SMB). Weitere Informationen zum Installieren von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mithilfe einer SMB-Dateifreigabe als Speicher finden Sie unter [Installieren von SQL Server mit SMB-Dateifreigabe als Speicheroption](../../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
     Der Pfad für die freigegebenen Komponenten muss ein absoluter Pfad sein. Der Ordner darf nicht komprimiert oder verschlüsselt werden. Zugeordnete Laufwerke werden nicht unterstützt. Wenn Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unter einem 64-Bit-Betriebssystem installieren, sehen Sie die folgenden Optionen:  
  
    1.  Freigegebenes Funktionsverzeichnis  
  
    2.  Freigegebenes Funktionsverzeichnis (x86)  
  
     Für jeden der oben erwähnten Optionen muss ein anderer Pfad angegeben werden.  
  
    > [!NOTE]  
    >  Wenn Sie die Funktion [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Dienste auswählen, werden Replikation und Volltextsuche automatisch ausgewählt. Data Quality Services (DQS) wird ebenfalls ausgewählt, wenn Sie die Funktion „ [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Dienste“ auswählen. Durch Aufheben der Auswahl eines dieser Subfunktionen wird auch die Auswahl der Funktion [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Dienste aufgehoben.  
  
10. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup wird eine weitere Reihe von Regeln ausgeführt, die auf den für die Überprüfung der Konfiguration ausgewählten Funktionen basieren.  
  
11. Geben Sie auf der Seite Instanzkonfiguration an, ob Sie eine Standardinstanz oder eine benannte Instanz installieren möchten. Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).  
  
     **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Netzwerkname** - Geben Sie den Netzwerknamen für die neue Instanz des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusters an. Anhand dieses Namens wird der Failovercluster im Netzwerk erkannt.  
  
    > [!NOTE]  
    >  Dieser wird in früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclustern als virtueller [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Name bezeichnet.  
  
     **Instanz-ID** – In der Standardeinstellung wird der Instanzname als Instanz-ID verwendet. So werden Installationsverzeichnisse und Registrierungsschlüssel für die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]identifiziert. Dies ist der Fall für Standardinstanzen und benannte Instanzen. Bei einer Standardinstanz lauten Instanzname und Instanz-ID MSSQLSERVER. Wenn Sie nicht die Standard-Instanz-ID verwenden möchten, markieren Sie das Feld **Instanz-ID** , und geben Sie einen Wert an.  
  
    > [!NOTE]  
    >  Typische eigenständige [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen – sowohl Standardinstanzen als auch benannte Instanzen – verwenden keine Nicht-Standardwerte für das Feld **Instanz-ID** .  
  
     **Instanzstammverzeichnis** – Standardmäßig lautet das Instanzstammverzeichnis „C:\Programme\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\\“. Wenn Sie ein nicht standardmäßiges Stammverzeichnis angeben möchten, verwenden Sie das dafür vorgesehene Feld. Sie können auch auf die Schaltfläche mit den drei Punkten klicken, um einen Installationsordner zu suchen.  
  
     **Erkannte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen und -Funktionen auf diesem Computer** – Im Raster werden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen angezeigt, die sich auf dem Computer befinden, auf dem Setup ausgeführt wird. Wenn bereits eine Standardinstanz auf dem Computer installiert ist, muss eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] installiert werden. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
12. Auf der Seite Clusterressourcengruppe [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können Sie den Namen der Clusterressourcengruppe angeben, in der sich die Ressourcen des virtuellen Servers für  befinden. Sie verfügen über zwei Optionen, um den Namen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Clusterressourcengruppe anzugeben:  
  
    -   Geben Sie die vorhandene Gruppe, die Sie verwenden möchten, mithilfe des Dropdownfelds an.  
  
    -   Geben Sie den Namen der neuen Gruppe ein, die Sie erstellen möchten. Beachten Sie, dass der Name "Verfügbarer Speicherplatz" kein gültiger Gruppenname ist.  
  
13. Wählen Sie auf der Seite Datenträgerauswahl für Cluster [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die freigegebene Cluster-Datenträgerressource für den -Failovercluster aus. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Daten werden auf dem Clusterdatenträger abgelegt. Es können mehrere Datenträger angegeben werden. Im Raster Verfügbare freigegebene Datenträger werden verfügbare Datenträger sowie Informationen zur Qualifikation der Datenträger als freigegebene Datenträger und eine Beschreibung der einzelnen Datenträgerressourcen angezeigt. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
    > [!NOTE]  
    >  Das erste Laufwerk wird als Standardlaufwerk für alle Datenbanken verwendet. Es kann jedoch auf der Konfigurationsseite von [!INCLUDE[ssDE](../../../includes/ssde-md.md)] oder [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] geändert werden.  
    >   
    >  Auf der Seite Datenträgerauswahl für Cluster können Sie die Auswahl eines freigegebenen Datenträgers optional überspringen, wenn Sie die SMB-Dateifreigabe als Datenordner verwenden möchten.  
  
14. Geben Sie auf der Seite Netzwerkkonfiguration für Cluster die Netzwerkressourcen für die Failoverclusterinstanz an:  
  
    -   **Netzwerkeinstellungen** – Geben Sie den IP-Typ und die IP-Adresse für die Failoverclusterinstanz an.  
  
     Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
15. Auf dieser Seite können Sie die Sicherheitsrichtlinie für Cluster angeben.  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] und höher – Die Verwendung von Dienst-SIDs (Server-Sicherheits-IDs) wird empfohlen. Dies ist die Standardeinstellung. Es ist keine Option zum Ändern in Sicherheitsgruppen verfügbar. Weitere Informationen über die Funktionen „Dienst-SID“ in [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). Dies wurde im eigenständigen Modus und für das [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]-Cluster-Setup getestet.  
  
    -   Geben Sie unter [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)]Domänengruppen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste an. Alle Ressourcenberechtigungen werden durch Gruppen auf Domänenebene gesteuert, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonten als Mitglieder enthalten.  
  
     Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
16. Der Ablauf für die weiteren Vorgänge dieses Themas ist von den Funktionen abhängig, die Sie für die Installation angegeben haben. Je nach Auswahl ([!INCLUDE[ssDE](../../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]) werden möglicherweise nicht alle Seiten angezeigt.  
  
17. Geben Sie auf der Seite Serverkonfiguration – Dienstkonten Anmeldekonten für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste an. Welche Dienste tatsächlich auf dieser Seite konfiguriert werden, ist von den Funktionen abhängig, die Sie für die Installation ausgewählt haben.  
  
     Sie können allen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Diensten dasselbe Anmeldekonto zuweisen, oder Sie können jedes Dienstkonto einzeln konfigurieren. Der Starttyp ist für alle clusterabhängigen Dienste, einschließlich Volltextsuche und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent, auf Manuell festgelegt und kann während der Installation nicht geändert werden. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] , die Dienstkonten einzeln zu konfigurieren, um möglichst geringe Rechte für jeden Dienst bereitzustellen. Dabei erhalten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste die Berechtigungen, die mindestens erforderlich ist, um ihre Tasks auszuführen. Weitere Informationen finden Sie unter [Serverkonfiguration – Dienstkonten](http://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) und [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Um für alle Dienstkonten in dieser Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]dasselbe Anmeldekonto anzugeben, geben Sie in den Feldern unten auf dieser Seite die entsprechenden Anmeldeinformationen ein.  
  
     **Sicherheitshinweis** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     Wenn Sie die Angabe der Anmeldeinformationen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste abgeschlossen haben, klicken Sie auf **Weiter**.  
  
18. Mithilfe der Registerkarte **Serverkonfiguration – Sortierung** können Sie für [!INCLUDE[ssDE](../../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]Sortierungen angeben, die von der Standardeinstellung abweichen.  
  
19. Geben Sie auf der Seite Konfiguration des [!INCLUDE[ssDE](../../../includes/ssde-md.md)] s – Kontenbereitstellung folgende Informationen an:  
  
    -   Sicherheitsmodus: Wählen Sie die Windows-Authentifizierung oder die Authentifizierung im gemischten Modus für die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]aus. Bei Auswahl des gemischten Authentifizierungsmodus müssen Sie ein sicheres Kennwort für das integrierte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Systemadministratorkonto angeben.  
  
         Nachdem ein Gerät erfolgreich eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]hergestellt hat, wird für die Windows-Authentifizierung und den gemischten Modus derselbe Sicherheitsmechanismus verwendet.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Administratoren – Sie müssen mindestens einen Systemadministrator für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz angeben. Um das Konto hinzuzufügen, unter dem das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup ausgeführt werden soll, klicken Sie auf **Aktuellen Benutzer hinzufügen**. Um Konten zur Liste der Systemadministratoren hinzuzufügen bzw. daraus zu entfernen, klicken Sie auf **Hinzufügen** bzw. **Entfernen**, und bearbeiten Sie anschließend die Liste der Benutzer, Gruppen bzw. Computer, die Administratorrechte für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz haben sollen.  
  
     Wenn Sie die Bearbeitung der Liste abgeschlossen haben, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Überprüfen Sie die Liste der Administratoren im Konfigurationsdialogfeld. Sobald die Liste vollständig ist, klicken Sie auf **Weiter**.  
  
20. Geben Sie ggf. auf der Seite [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Konfiguration – Datenverzeichnisse andere Installationsverzeichnisse als das Standardinstallationsverzeichnis an. Wenn die Installation in Standardverzeichnissen erfolgen soll, klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie andere Installationsverzeichnisse als die Standardverzeichnisse angeben, stellen Sie sicher, dass die Installationsordner für diese Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]eindeutig sind. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen von anderen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen genutzt werden. Die Datenverzeichnisse sollten sich auf dem freigegebenen Clusterdatenträger für den Failovercluster befinden.  
  
    > [!NOTE]  
    >  Legen Sie zum Angeben eines Server Message Block-Dateiservers (SMB) als Datenverzeichnis das **Standard-Datenstammverzeichnis** auf die Dateifreigabe mit dem Format „ \\\Servername\Name der Freigabe\\...“ fest.  
   
21. Aktivieren Sie auf der Seite „ [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Konfiguration – FILESTREAM“ den FILESTREAM für Ihre Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
22. Geben Sie auf der Seite [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Konfiguration – Kontobereitstellung-Konfiguration – Kontobereitstellung die Benutzer oder Konten an, die über Administratorberechtigungen für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]verfügen sollen. Sie müssen wenigstens einen Systemadministrator für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]angeben. Um das Konto hinzuzufügen, unter dem das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup ausgeführt werden soll, klicken Sie auf **Aktuellen Benutzer hinzufügen**. Um Konten zur Liste der Systemadministratoren hinzuzufügen bzw. daraus zu entfernen, klicken Sie auf **Hinzufügen** bzw. **Entfernen**, und bearbeiten Sie anschließend die Liste der Benutzer, Gruppen bzw. Computer, die Administratorrechte für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]haben sollen.
  
     Wenn Sie die Bearbeitung der Liste abgeschlossen haben, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Überprüfen Sie die Liste der Administratoren im Konfigurationsdialogfeld. Sobald die Liste vollständig ist, klicken Sie auf **Weiter**.  
  
23. Geben Sie auf der Seite [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Konfiguration – Datenverzeichnisse andere Installationsverzeichnisse als das Standardinstallationsverzeichnis an. Wenn die Installation in Standardverzeichnissen erfolgen soll, klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie andere Installationsverzeichnisse als die Standardverzeichnisse angeben, stellen Sie sicher, dass die Installationsordner für diese Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]eindeutig sind. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen von anderen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen genutzt werden. Die Datenverzeichnisse sollten sich auf dem freigegebenen Clusterdatenträger für den Failovercluster befinden.  
   
24. Auf der Seite für die Konfiguration von [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] können Sie die Art der zu erstellenden [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -Installation angeben. Für die Failoverclusterinstallation ist die Option auf Nicht konfigurierte -Installation [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] festgelegt. Nach dem Abschluss der Installation müssen Sie [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -Dienste konfigurieren.  
  
 
25. Die Systemkonfigurationsprüfung führt einen weiteren Regelsatz aus, um die Konfiguration anhand der von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Funktionen zu überprüfen.  
  
26. Auf der Seite Installationsbereit wird eine Strukturansicht der Installationsoptionen angezeigt, die während des Setups angegeben wurden. Klicken Sie zum Fortsetzen des Vorgangs auf **Installieren**. Setup installiert zuerst die erforderlichen Komponenten für die ausgewählten Funktionen und dann die Funktionen.  
  
27. Während der Installation wird auf der Seite Installationsstatus der Status angezeigt, sodass Sie während der Installation den Installationsstatus überwachen können.  
  
28. Nach der Installation bietet die Seite **Abgeschlossen** einen Link zur zusammenfassenden Protokolldatei für die Installation und andere wichtige Hinweise. Klicken Sie auf **Schließen** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , um die Installation von abzuschließen.  
  
29. Starten Sie den Computer neu, falls Sie dazu aufgefordert werden. Wenn Sie den Setupvorgang abgeschlossen haben, sollten Sie unbedingt die vom Installations-Assistenten angezeigte Meldung lesen. Weitere Informationen über Setupprotokolldateien finden Sie unter [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
30. Um dem gerade erstellten Failovercluster mit einem einzelnen Knoten weitere Knoten hinzuzufügen, führen Sie Setup für jeden zusätzlichen Knoten aus, und befolgen Sie die Schritte für AddNode-Vorgänge. Weitere Informationen finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
    > [!NOTE]  
    >  Wenn Sie mehrere Knoten hinzufügen, können Sie die Installationen mithilfe der Konfigurationsdatei bereitstellen. Weitere Informationen finden Sie unter [Installieren von SQL Server 2016 mithilfe einer Konfigurationsdatei](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
    >   
    >  Die zu installierende [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Edition muss für alle Knoten in einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster übereinstimmen. Wenn Sie einem vorhandenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster einen neuen Knoten hinzufügen, müssen Sie angeben, dass die Edition mit der Edition des vorhandenen Failoverclusters übereinstimmt.  
  
##  <a name="prepare"></a> Vorbereiten  
  
#### <a name="advancedenterprise-failover-cluster-install-step-1-prepare"></a>Schritt 1 für die erweiterte bzw. Enterprise-Failoverclusterinstallation: Vorbereiten  
  
1.  Legen Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationsmedium ein, und doppelklicken Sie im Stammordner auf Setup.exe. Wenn Sie eine Installation über eine Netzwerkfreigabe ausführen möchten, navigieren Sie in der Freigabe zum Stammordner, und doppelklicken Sie dann auf Setup.exe. Weitere Informationen zum Installieren der erforderlichen Komponenten finden Sie unter [Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md). Möglicherweise werden Sie aufgefordert, die erforderlichen Komponenten zu installieren, falls sie nicht bereits installiert wurden.  
  
2.  Windows Installer 4.5 ist erforderlich und wird ggf. vom Installations-Assistenten installiert. Wenn Sie aufgefordert werden, den Computer neu zu starten, führen Sie einen Neustart durch, und führen Sie Setup für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dann erneut aus.  
  
3.  Nachdem die erforderlichen Komponenten installiert wurden, startet der Installations-Assistent das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationscenter. Um den Knoten für Clustering vorzubereiten, wechseln Sie zur Seite **Erweitert** , und klicken Sie dann auf **Erweiterte Clustervorbereitung**.  
  
4.  Die Systemkonfigurationsprüfung führt einen Ermittlungsvorgang auf dem Computer aus. [!INCLUDE[clickOK](../../../includes/clickok-md.md)], um den Vorgang fortzusetzen. Sie können die Details auf dem Bildschirm anzeigen, indem Sie auf **Details anzeigen**klicken, oder als HTML-Bericht, indem Sie auf **Detaillierten Bericht anzeigen**klicken.  
  
5.  Klicken Sie auf der Seite **Setup-Unterstützungsdateien** auf Installieren, um die Setup-Unterstützungsdateien zu installieren.  
  
6.  Die Systemkonfigurationsprüfung überprüft den Systemstatus des Computers, bevor Setup fortgesetzt wird. Nachdem die Prüfung abgeschlossen wurde, klicken Sie auf **Weiter** , um den Vorgang fortzusetzen. Sie können die Details auf dem Bildschirm anzeigen, indem Sie auf **Details anzeigen**klicken, oder als HTML-Bericht, indem Sie auf **Detaillierten Bericht anzeigen**klicken.  
  
7.  Auf der Seite für die Sprachauswahl können Sie die Sprache für die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] angeben, wenn Sie sie unter einem lokalisierten Betriebssystem installieren und die Installationsmedien Sprachpakete sowohl für Englisch als auch für die Sprache des Betriebssystems einschließen. Weitere Informationen zu sprachübergreifender Unterstützung und Überlegungen zur Installation finden Sie im [Thema zu lokalen Sprachversionen in SQL Server](../../../sql-server/install/local-language-versions-in-sql-server.md).  
  
     Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
8.  Klicken Sie auf der Seite Product Key auf die entsprechende Option, um anzugeben, ob Sie eine kostenlose Edition von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]installieren oder über einen PID-Schlüssel für eine Produktionsversion des Produkts verfügen. Weitere Informationen finden Sie unter [Editionen und Komponenten von SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
    > [!NOTE]  
    >  Sie müssen für alle Knoten, die Sie für denselben Failovercluster vorbereiten, denselben Produktschlüssel angeben.  
  
9. Lesen Sie auf der Seite mit den Lizenzbedingungen den Lizenzvertrag, und aktivieren Sie dann das Kontrollkästchen, um den Lizenzbestimmungen zuzustimmen. Falls Sie zur Verbesserung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]beitragen möchten, können Sie auch die Option zur Funktionsverwendung aktivieren und Berichte an [!INCLUDE[msCoName](../../../includes/msconame-md.md)]senden. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen. Klicken Sie auf **Abbrechen**, wenn Sie den Setupvorgang beenden möchten.  
  
10. Wählen Sie auf der Seite Funktionsauswahl die Komponenten für die Installation aus. Nach Auswahl des Funktionsnamens wird im rechten Bereich eine Beschreibung für die einzelnen Komponentengruppen angezeigt. Sie können eine beliebige Kombination von Kontrollkästchen aktivieren, das Failoverclustering wird jedoch nur von [!INCLUDE[ssDE](../../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] im tabellarischen Modus und [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] im mehrdimensionalen Modus unterstützt. Andere ausgewählte Komponenten werden als eigenständige Funktion ohne Failoverfunktionen für den aktuellen Knoten ausgeführt, für den das Setup erfolgt. Weitere Informationen zu [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Bereitstellungsmodi finden Sie unter [Bestimmen des Servermodus einer Analysis Services-Instanz](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
     Die erforderlichen Komponenten für die ausgewählten Funktionen werden im rechten Bereich angezeigt. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup installiert die erforderlichen Komponenten, die nicht bereits während des Installationsschritts installiert werden, der im weiteren Verlauf dieser Prozedur beschrieben wird.  
  
     Sie können ein benutzerdefiniertes Verzeichnis für freigegebene Komponenten angeben. Verwenden Sie dazu das Feld unten auf dieser Seite. Um den Installationspfad für freigegebene Komponenten zu ändern, aktualisieren Sie den Pfad im Feld unten im Dialogfeld, oder klicken Sie auf die Schaltfläche mit den drei Punkten, um zu einem Installationsverzeichnis zu navigieren. Der Standardinstallationspfad lautet „C:\Programme\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\“.  
  
    > [!NOTE]  
    >  Wenn Sie die Funktion [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Dienste auswählen, werden Replikation und Volltextsuche automatisch ausgewählt. Durch Aufheben der Auswahl eines dieser Subfunktionen wird auch die Auswahl der Funktion [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Dienste aufgehoben.  
  
11. Geben Sie auf der Seite Instanzkonfiguration an, ob Sie eine Standardinstanz oder eine benannte Instanz installieren möchten.
  
     **Instanz-ID** – In der Standardeinstellung wird der Instanzname als Instanz-ID verwendet. So werden Installationsverzeichnisse und Registrierungsschlüssel für die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]identifiziert. Dies ist der Fall für Standardinstanzen und benannte Instanzen. Bei einer Standardinstanz lauten Instanzname und Instanz-ID MSSQLSERVER. Wenn Sie nicht die Standard-Instanz-ID verwenden möchten, markieren Sie das Textfeld **Instanz-ID** , und geben Sie einen Wert ein.  
  
    > [!NOTE]  
    >  Typische eigenständige [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen – sowohl Standardinstanzen als auch benannte Instanzen – verwenden keine Nicht-Standardwerte für das Textfeld **Instanz-ID** .  
  
    > [!IMPORTANT]  
    >  Verwenden Sie für alle Knoten, die für den Failovercluster vorbereitet werden, dieselbe Instanz-ID.  
  
     **Instanzstammverzeichnis** – Standardmäßig lautet das Instanzstammverzeichnis „C:\Programme\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\\“. Wenn Sie ein nicht standardmäßiges Stammverzeichnis angeben möchten, verwenden Sie das dafür vorgesehene Feld. Sie können auch auf die Schaltfläche mit den drei Punkten klicken, um einen Installationsordner zu suchen.  
  
     **Installierte Instanzen** – Im Raster werden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanzen angezeigt, die sich auf dem Computer befinden, auf dem Setup ausgeführt wird. Wenn bereits eine Standardinstanz auf dem Computer installiert ist, muss eine benannte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]installiert werden. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
12. Auf der Seite Erforderlicher Speicherplatz wird der für die angegebenen Funktionen erforderliche Speicherplatz berechnet, und die Anforderungen werden mit dem Speicherplatz verglichen, der auf dem Computer verfügbar ist, auf dem Setup ausgeführt wird.  
  
13. Auf dieser Seite können Sie die Sicherheitsrichtlinie für Cluster angeben.  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] und höher – Die Verwendung von Dienst-SIDs (Server-Sicherheits-IDs) wird empfohlen. Dies ist die Standardeinstellung. Es ist keine Option zum Ändern in Sicherheitsgruppen verfügbar. Weitere Informationen über die Funktionen „Dienst-SID“ in [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). Dies wurde im eigenständigen Modus und für das [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]-Cluster-Setup getestet.  
  
    -   Geben Sie unter [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)]Domänengruppen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste an. Alle Ressourcenberechtigungen werden durch Gruppen auf Domänenebene gesteuert, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonten als Mitglieder enthalten.  
  
     Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
14. Der Ablauf für die weiteren Vorgänge dieses Themas ist von den Funktionen abhängig, die Sie für die Installation angegeben haben. Je nach Auswahl werden möglicherweise nicht alle Seiten angezeigt.  
  
15. Geben Sie auf der Seite Serverkonfiguration – Dienstkonten Anmeldekonten für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste an. Welche Dienste tatsächlich auf dieser Seite konfiguriert werden, ist von den Funktionen abhängig, die Sie für die Installation ausgewählt haben.  
  
     Sie können allen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Diensten dasselbe Anmeldekonto zuweisen, oder Sie können jedes Dienstkonto einzeln konfigurieren. Der Starttyp ist für alle clusterabhängigen Dienste, einschließlich Volltextsuche und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent, auf Manuell festgelegt und kann während der Installation nicht geändert werden. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] , die Dienstkonten einzeln zu konfigurieren, um möglichst geringe Rechte für jeden Dienst bereitzustellen. Dabei erhalten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste die Berechtigungen, die mindestens erforderlich ist, um ihre Tasks auszuführen. Weitere Informationen finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Um für alle Dienstkonten in dieser Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]dasselbe Anmeldekonto anzugeben, geben Sie in den Feldern unten auf dieser Seite die entsprechenden Anmeldeinformationen ein.  
  
     **Sicherheitshinweis** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     Wenn Sie die Angabe der Anmeldeinformationen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste abgeschlossen haben, klicken Sie auf **Weiter**.  
  
16. Mithilfe der Registerkarte **Serverkonfiguration – Sortierung** können Sie für [!INCLUDE[ssDE](../../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]Sortierungen angeben, die von der Standardeinstellung abweichen.  
  
17. Verwenden Sie **Serverkonfiguration – FILESTREAM** , um FILESTREAM für Ihre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz zu aktivieren.  Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
18. Auf der Seite für die Konfiguration von [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] können Sie die Art der zu erstellenden [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -Installation angeben. Für die Failoverclusterinstallation ist die Option auf Nicht konfigurierte -Installation [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] festgelegt. Nach dem Abschluss der Installation müssen Sie [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -Dienste konfigurieren.  
   
19. Geben Sie auf der Seite Fehlerberichterstellung die Informationen an, die Sie an [!INCLUDE[msCoName](../../../includes/msconame-md.md)] senden möchten, um zur Verbesserung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]beizutragen. Die Option für Fehlerberichte ist standardmäßig aktiviert.  
  
20. Die Systemkonfigurationsprüfung führt einen weiteren Regelsatz aus, um die Konfiguration anhand der von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Funktionen zu überprüfen.  
  
21. Auf der Seite Installationsbereit wird eine Strukturansicht der Installationsoptionen angezeigt, die während des Setups angegeben wurden. Klicken Sie zum Fortsetzen des Vorgangs auf **Installieren**. Setup installiert zuerst die erforderlichen Komponenten für die ausgewählten Funktionen und dann die Funktionen.  
  
     Während der Installation wird auf der Seite Installationsstatus der Status angezeigt, sodass Sie während der Installation den Installationsstatus überwachen können. Nach der Installation bietet die Seite **Abgeschlossen** einen Link zur zusammenfassenden Protokolldatei für die Installation und andere wichtige Hinweise.  
  
22. Klicken Sie auf Schließen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um die Installation von **abzuschließen**.  
  
23. Starten Sie den Computer neu, falls Sie dazu aufgefordert werden. Wenn Sie den Setupvorgang abgeschlossen haben, sollten Sie unbedingt die vom Installations-Assistenten angezeigte Meldung lesen. Weitere Informationen über Setupprotokolldateien finden Sie unter [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
24. Wiederholen Sie die vorherigen Schritte, um die anderen Knoten für den Failovercluster vorzubereiten. Sie können die anderen Knoten auch mithilfe der automatisch generierten Konfigurationsdatei vorbereiten. Weitere Informationen finden Sie unter [Installieren von SQL Server 2016 mithilfe einer Konfigurationsdatei](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
## <a name="complete"></a>Abgeschlossen  
  
#### <a name="advancedenterprise-failover-cluster-install-step-2-complete"></a>Schritt 2 für die erweiterte bzw. Enterprise-Failoverclusterinstallation: Abschließen  
  
1.  Nachdem Sie alle Knoten wie im Schritt [Vorbereiten](#prepare)beschrieben vorbereitet haben, führen Sie Setup für einen der vorbereiteten Knoten aus, und zwar nach Möglichkeit für den Knoten, der Besitzer des freigegebenen Datenträgers ist. Klicken Sie im -Installationscenter auf der Registerkarte **Erweitert** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf **Erweiterter Clusterabschluss**.  
  
2.  Die Systemkonfigurationsprüfung führt einen Ermittlungsvorgang auf dem Computer aus. [!INCLUDE[clickOK](../../../includes/clickok-md.md)], um den Vorgang fortzusetzen. Sie können die Details auf dem Bildschirm anzeigen, indem Sie auf **Details anzeigen**klicken, oder als HTML-Bericht, indem Sie auf **Detaillierten Bericht anzeigen**klicken.  
  
3.  Klicken Sie auf der Seite **Setup-Unterstützungsdateien** auf Installieren, um die Setup-Unterstützungsdateien zu installieren.  
  
4.  Die Systemkonfigurationsprüfung überprüft den Systemstatus des Computers, bevor Setup fortgesetzt wird. Nachdem die Prüfung abgeschlossen wurde, klicken Sie auf **Weiter** , um den Vorgang fortzusetzen. Sie können die Details auf dem Bildschirm anzeigen, indem Sie auf **Details anzeigen**klicken, oder als HTML-Bericht, indem Sie auf **Detaillierten Bericht anzeigen**klicken.  
  
5.  Auf der Seite für die Sprachauswahl können Sie die Sprache für die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] angeben, wenn Sie sie unter einem lokalisierten Betriebssystem installieren und die Installationsmedien Sprachpakete sowohl für Englisch als auch für die Sprache des Betriebssystems einschließen. Weitere Informationen zu sprachübergreifender Unterstützung und Überlegungen zur Installation finden Sie im [Thema zu lokalen Sprachversionen in SQL Server](../../../sql-server/install/local-language-versions-in-sql-server.md).  
  
     Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
6.  Auf der Seite Clusterknotenkonfiguration [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können Sie den Namen der für Clustering vorbereiteten Instanz auswählen und den Netzwerknamen für den neuen -Failovercluster angeben. Anhand dieses Namens wird der Failovercluster im Netzwerk erkannt.  
  
    > [!NOTE]  
    >  Dieser wird in früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclustern als virtueller [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Name bezeichnet.  
  
7.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup wird eine weitere Reihe von Regeln ausgeführt, die auf den für die Überprüfung der Konfiguration ausgewählten Funktionen basieren.  
  
8.  Auf der Seite Clusterressourcengruppe [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können Sie den Namen der Clusterressourcengruppe angeben, in der sich die Ressourcen des virtuellen Servers für  befinden. Geben Sie den Namen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Clusterressourcengruppe an. Hierfür stehen zwei Möglichkeiten zur Verfügung:  
  
    -   Geben Sie die vorhandene Gruppe, die Sie verwenden möchten, mithilfe der Liste an.  
  
    -   Geben Sie den Namen der neuen Gruppe ein, die Sie erstellen möchten. Beachten Sie, dass der Name "Verfügbarer Speicherplatz" kein gültiger Gruppenname ist.  
  
9. Wählen Sie auf der Seite Datenträgerauswahl für Cluster [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die freigegebene Cluster-Datenträgerressource für den -Failovercluster aus. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Daten werden auf dem Clusterdatenträger abgelegt. Es können mehrere Datenträger angegeben werden. Im Raster Verfügbare freigegebene Datenträger werden verfügbare Datenträger sowie Informationen zur Qualifikation der Datenträger als freigegebene Datenträger und eine Beschreibung der einzelnen Datenträgerressourcen angezeigt. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
    > [!NOTE]  
    >  Das erste Laufwerk wird als Standardlaufwerk für alle Datenbanken verwendet. Es kann jedoch auf der Konfigurationsseite von [!INCLUDE[ssDE](../../../includes/ssde-md.md)] oder [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] geändert werden.  
  
10. Geben Sie auf der Seite Netzwerkkonfiguration für Cluster die Netzwerkressourcen für die Failoverclusterinstanz an:  
  
    -   **Netzwerkeinstellungen** – Geben Sie den IP-Typ und die IP-Adresse für alle Knoten und Subnetze der Failoverclusterinstanz an. Sie können für einen Multisubnetz-Failovercluster mehrere IP-Adressen angeben, jedoch wird nur eine IP-Adresse pro Subnetz unterstützt. Jeder vorbereitete Knoten sollte Besitzer von mindestens einer IP-Adresse sein. Wenn Sie der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster mehrere Subnetze aufweist, werden Sie aufgefordert, die IP-Adressabhängigkeit auf OR festzulegen.  
  
     Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
11. Der Ablauf für die weiteren Vorgänge dieses Themas ist von den Funktionen abhängig, die Sie für die Installation angegeben haben. Je nach Auswahl werden möglicherweise nicht alle Seiten angezeigt.  
  
12. Geben Sie auf der Seite Konfiguration des [!INCLUDE[ssDE](../../../includes/ssde-md.md)] s – Kontenbereitstellung folgende Informationen an:  
  
    -   Sicherheitsmodus: Wählen Sie die Windows-Authentifizierung oder die Authentifizierung im gemischten Modus für die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]aus. Bei Auswahl des gemischten Authentifizierungsmodus müssen Sie ein sicheres Kennwort für das integrierte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Systemadministratorkonto angeben.  
  
         Nachdem ein Gerät erfolgreich eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]hergestellt hat, wird für die Windows-Authentifizierung und den gemischten Modus derselbe Sicherheitsmechanismus verwendet.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Administratoren – Sie müssen mindestens einen Systemadministrator für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz angeben. Um das Konto hinzuzufügen, unter dem das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup ausgeführt werden soll, klicken Sie auf **Aktuellen Benutzer hinzufügen**. Um Konten zur Liste der Systemadministratoren hinzuzufügen bzw. daraus zu entfernen, klicken Sie auf **Hinzufügen** bzw. **Entfernen**, und bearbeiten Sie anschließend die Liste der Benutzer, Gruppen bzw. Computer, die Administratorrechte für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz haben sollen.  
  
     Wenn Sie die Bearbeitung der Liste abgeschlossen haben, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Überprüfen Sie die Liste der Administratoren im Konfigurationsdialogfeld. Sobald die Liste vollständig ist, klicken Sie auf **Weiter**.  
  
13. Geben Sie ggf. auf der Seite [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Konfiguration – Datenverzeichnisse andere Installationsverzeichnisse als das Standardinstallationsverzeichnis an. Wenn die Installation in Standardverzeichnissen erfolgen soll, klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie andere Installationsverzeichnisse als die Standardverzeichnisse angeben, stellen Sie sicher, dass die Installationsordner für diese Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]eindeutig sind. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen von anderen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen genutzt werden. Die Datenverzeichnisse sollten sich auf dem freigegebenen Clusterdatenträger für den Failovercluster befinden.  
  
  
14. Geben Sie auf der Seite [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Konfiguration – Kontobereitstellung-Konfiguration – Kontobereitstellung die Benutzer oder Konten an, die über Administratorberechtigungen für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]verfügen sollen. Sie müssen wenigstens einen Systemadministrator für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]angeben. Um das Konto hinzuzufügen, unter dem das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup ausgeführt werden soll, klicken Sie auf **Aktuellen Benutzer hinzufügen**. Um Konten zur Liste der Systemadministratoren hinzuzufügen bzw. daraus zu entfernen, klicken Sie auf **Hinzufügen** bzw. **Entfernen**, und bearbeiten Sie anschließend die Liste der Benutzer, Gruppen bzw. Computer, die Administratorrechte für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]haben sollen.  
  
     Wenn Sie die Bearbeitung der Liste abgeschlossen haben, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Überprüfen Sie die Liste der Administratoren im Konfigurationsdialogfeld. Sobald die Liste vollständig ist, klicken Sie auf **Weiter**.  
  
15. Geben Sie auf der Seite [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Konfiguration – Datenverzeichnisse andere Installationsverzeichnisse als das Standardinstallationsverzeichnis an. Wenn die Installation in Standardverzeichnissen erfolgen soll, klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie andere Installationsverzeichnisse als die Standardverzeichnisse angeben, stellen Sie sicher, dass die Installationsordner für diese Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]eindeutig sind. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen von anderen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzen genutzt werden. Die Datenverzeichnisse sollten sich auf dem freigegebenen Clusterdatenträger für den Failovercluster befinden.  
  
  
16. Die Systemkonfigurationsprüfung führt einen weiteren Regelsatz aus, um die Konfiguration anhand der von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Funktionen zu überprüfen.  
  
17. Auf der Seite Installationsbereit wird eine Strukturansicht der Installationsoptionen angezeigt, die während des Setups angegeben wurden. Klicken Sie zum Fortsetzen des Vorgangs auf **Installieren**. Setup installiert zuerst die erforderlichen Komponenten für die ausgewählten Funktionen und dann die Funktionen.  
  
18. Während der Installation wird auf der Seite Installationsstatus der Status angezeigt, sodass Sie während der Installation den Installationsstatus überwachen können.  
  
19. Nach der Installation bietet die Seite **Abgeschlossen** einen Link zur zusammenfassenden Protokolldatei für die Installation und andere wichtige Hinweise. Klicken Sie auf Schließen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um die Installation von **abzuschließen**. Nach diesem Schritt sind alle für denselben Failovercluster vorbereiteten Knoten Teil des abgeschlossenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusters.  
  
## <a name="next-steps"></a>Next Steps  
 **Konfigurieren Sie Ihre neue [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Installation:** Zentrale Dienste und Funktionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] werden selektiv installiert und aktiviert, um die Angriffsfläche eines Systems zu verringern. Weitere Informationen finden Sie unter [Surface Area Configuration](../../../relational-databases/security/surface-area-configuration.md).  
  
 Weitere Informationen zu Speicherorten von Protokolldateien finden Sie unter [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
