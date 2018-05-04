---
title: Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster (Setup) | Microsoft-Dokumentation
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
- adding nodes
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- failover clustering [SQL Server], nodes
- deleting nodes
- cluster maintenance [SQL Server]
- removing nodes
ms.assetid: fe20dca9-a4c1-4d32-813d-42f1782dfdd3
caps.latest.revision: 49
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b92b192297633850fb96be13e6c35cb54628b899
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="add-or-remove-nodes-in-a-sql-server-failover-cluster-setup"></a>Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster (Setup)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Verwenden Sie diese Prozedur, um Knoten in einer vorhandenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz zu verwalten.  
  
 Um einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster zu aktualisieren oder zu entfernen, müssen Sie lokaler Administrator mit der Berechtigung sein, sich als Dienst auf allen Knoten des Failoverclusters anzumelden. Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.  
  
 Zum Hinzufügen eines Knotens zu einem vorhandenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster müssen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup für den Knoten ausführen, der der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz hinzugefügt werden soll. Führen Sie Setup nicht für den aktiven Knoten aus.  
  
 Zum Entfernen eines Knotens aus einem vorhandenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster müssen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup für den Knoten ausführen, der aus der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz entfernt werden soll.  
  
 Wählen Sie einen der folgenden Vorgänge aus, um Schritte zum Hinzufügen oder Entfernen von Knoten anzuzeigen:  
  
-   [Hinzufügen eines Knotens zu einem vorhandenen SQL Server-Failovercluster](#Add)  
  
-   [Entfernen eines Knotens aus einem vorhandenen SQL Server-Failovercluster](#Remove)  
  
> [!IMPORTANT]  
>  Der Laufwerkbuchstabe des Betriebssystems für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationsverzeichnisse muss auf allen Knoten übereinstimmen, die dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster hinzugefügt werden.  
  
##  <a name="Add"></a> Hinzufügen eines Knotens  
  
#### <a name="to-add-a-node-to-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>So fügen Sie einem vorhandenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster einen Knoten hinzu  
  
1.  Legen Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationsmedium ein, und doppelklicken Sie im Stammordner auf Setup.exe. Bei einer Installation über eine Netzwerkfreigabe navigieren Sie zum Stammordner der Freigabe, und doppelklicken Sie auf Setup.exe.  
  
2.  Das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationscenter wird vom Installations-Assistenten gestartet. Um einer vorhandenen Failoverclusterinstanz einen Knoten hinzuzufügen, klicken Sie im linken Bereich auf **Installation**. Wählen Sie dann **Knoten einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failovercluster** hinzufügen aus.  
  
3.  Die Systemkonfigurationsprüfung führt einen Ermittlungsvorgang auf dem Computer aus. [!INCLUDE[clickOK](../../../includes/clickok-md.md)], um den Vorgang fortzusetzen.  
  
4.  Auf der Seite für die Sprachauswahl können Sie die Sprache für die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] angeben, wenn Sie sie unter einem lokalisierten Betriebssystem installieren und die Installationsmedien Sprachpakete sowohl für Englisch als auch für die Sprache des Betriebssystems einschließen. Weitere Informationen zu sprachübergreifender Unterstützung und Überlegungen zur Installation finden Sie im [Thema zu lokalen Sprachversionen in SQL Server](../../../sql-server/install/local-language-versions-in-sql-server.md).  
  
     Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
5.  Geben Sie auf der Product Key-Seite den PID-Schlüssel für eine Produktionsversion des Produkts an. Der für diese Installation eingegebene Product Key muss für die Edition von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bestimmt sein, die für den aktiven Knoten installiert ist.  
  
6.  Lesen Sie auf der Seite mit den Lizenzbedingungen den Lizenzvertrag, und aktivieren Sie dann das Kontrollkästchen, um die Lizenzbestimmungen zu akzeptieren. Falls Sie zur Verbesserung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]beitragen möchten, können Sie auch die Option zur Funktionsverwendung aktivieren und Berichte an [!INCLUDE[msCoName](../../../includes/msconame-md.md)]senden. Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen. Klicken Sie auf **Abbrechen**, wenn Sie den Setupvorgang beenden möchten.  
  
7.  Die Systemkonfigurationsprüfung überprüft den Systemstatus des Computers, bevor Setup fortgesetzt wird. Nachdem die Prüfung abgeschlossen wurde, klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
8.  Verwenden Sie auf der Seite Clusterknotenkonfiguration das Dropdownfeld, um den Namen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz anzugeben, die bei diesem Setupvorgang geändert werden soll.  
  
9. Geben Sie auf der Seite Serverkonfiguration – Dienstkonten Anmeldekonten für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste an. Welche Dienste tatsächlich auf dieser Seite konfiguriert werden, hängt von den Funktionen ab, die Sie für die Installation ausgewählt haben. Bei Failoverclusterinstallationen wurden der Kontoname und der Starttyp anhand der Einstellungen für den aktiven Knoten bereits auf dieser Seite eingetragen. Sie müssen Kennwörter für jedes Konto bereitstellen. Weitere Informationen finden Sie unter [Serverkonfiguration – Dienstkonten](http://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) und [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     **Sicherheitshinweis** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     Wenn Sie die Angabe der Anmeldeinformationen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienste abgeschlossen haben, klicken Sie auf **Weiter**.  
  
10. Geben Sie auf der Seite Fehlerberichterstellung [!INCLUDE[msCoName](../../../includes/msconame-md.md)] die Informationen an, die Sie an [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]senden möchten, um zur Verbesserung von  beizutragen. Die Option für Fehlerberichte ist standardmäßig aktiviert.  
  
11. Die Systemkonfigurationsprüfung führt einen weiteren Regelsatz aus, um die Konfiguration des Computers anhand der von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Funktionen zu überprüfen.  
  
12. Auf der Seite Der Knoten kann nun hinzugefügt werden wird eine Strukturansicht der Installationsoptionen angezeigt, die während des Setups angegeben wurden.  
  
13. Auf der Seite Status des Vorgangs des Hinzufügens eines Knotens wird der Status angegeben, sodass Sie während des Setupvorgangs den Fortschritt der Installation überwachen können.  
  
14. Nach der Installation bietet die Seite Abgeschlossen einen Link zur zusammenfassenden Protokolldatei für die Installation und andere wichtige Hinweise. Klicken Sie auf Schließen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um die Installation von **abzuschließen**.  
  
15. Starten Sie den Computer neu, falls Sie dazu aufgefordert werden. Nachdem das Setup abgeschlossen ist, sollten Sie unbedingt die vom Installations-Assistenten ausgegebene Meldung lesen. Weitere Informationen zu Setupprotokolldateien finden Sie unter [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
##  <a name="Remove"></a> Entfernen eines Knotens  
  
#### <a name="to-remove-a-node-from-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>So entfernen Sie einen Knoten aus einem vorhandenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster  
  
1.  Legen Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationsmedium ein. Doppelklicken Sie im Stammordner auf setup.exe. Bei einer Installation über eine Netzwerkfreigabe navigieren Sie zum Stammordner der Freigabe, und doppelklicken Sie auf Setup.exe.  
  
2.  Das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Installationscenter wird vom Installations-Assistenten gestartet. Um einen Knoten aus einer vorhandenen Failoverclusterinstanz zu entfernen, klicken Sie im linken Bereich auf **Wartung** und wählen dann **Knoten aus einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failovercluster entfernen** aus.  
  
3.  Die Systemkonfigurationsprüfung führt einen Ermittlungsvorgang auf dem Computer aus. [!INCLUDE[clickOK](../../../includes/clickok-md.md)], um den Vorgang fortzusetzen.  
  
4.  Nachdem Sie auf der Seite Setupunterstützungsdateien auf Installieren geklickt haben, wird der Systemstatus des Computers von der Systemkonfigurationsprüfung überprüft, bevor Setup fortgesetzt wird. Nachdem die Prüfung abgeschlossen wurde, klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.  
  
5.  Verwenden Sie auf der Seite Clusterknotenkonfiguration das Dropdownfeld, um den Namen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz anzugeben, die bei diesem Setupvorgang geändert werden soll. Der zu entfernende Knoten wird im Feld **Name dieses Knotens** aufgeführt.  
  
6.  Auf der Seite Der Knoten kann nun entfernt werden wird eine Strukturansicht der Optionen angezeigt, die während des Setups angegeben wurden. Klicken Sie zum Fortsetzen des Vorgangs auf **Entfernen**.  
  
7.  Während des Entfernungsvorgangs wird auf der Seite Status des Vorgangs des Entfernens des Knotens der Status angezeigt.  
  
8.  Auf der Seite Abgeschlossen finden Sie einen Link zur zusammenfassenden Protokolldatei für das Entfernen des Knotens und andere wichtige Hinweise. Klicken Sie auf **Schließen** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um das Entfernen des Knotens in abzuschließen. Weitere Informationen zu Setupprotokolldateien finden Sie unter [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
