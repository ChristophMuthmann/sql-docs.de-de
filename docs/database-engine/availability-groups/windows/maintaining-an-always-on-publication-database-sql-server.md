---
title: "Warten einer Always On-Veröffentlichungsdatenbank (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 55b345fe-2eb9-4b04-a900-63d858eec360
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52416e9d44e5c820bc584014d0d0902a069a616c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="maintaining-an-always-on-publication-database-sql-server"></a>Warten einer Always On-Veröffentlichungsdatenbank (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema werden besondere Überlegungen zum Verwalten einer Veröffentlichungsdatenbank bei Verwendung von Always On-Verfügbarkeitsgruppen erläutert.  
  
 **In diesem Thema:**  
  
-   [Verwalten einer veröffentlichten Datenbank in einer Verfügbarkeitsgruppe](#MaintainPublDb)  
  
-   [Entfernen einer veröffentlichten Datenbank aus einer Verfügbarkeitsgruppe](#RemovePublDb)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="MaintainPublDb"></a> Verwalten einer veröffentlichten Datenbank in einer Verfügbarkeitsgruppe  
 Die Wartung einer Always On-Veröffentlichungsdatenbank entspricht im Wesentlichen der Wartung einer standardmäßigen Veröffentlichungsdatenbank, wobei jedoch die folgenden Überlegungen zu berücksichtigen sind:  
  
-   Die Verwaltung muss beim primären Replikathost erfolgen. In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]werden Veröffentlichungen unter dem Ordner **Lokale Veröffentlichungen** für den primären Replikathost und auch für lesbare sekundäre Replikate angezeigt. Nach einem Failover müssen Sie unter Umständen [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] manuell aktualisieren, um die Änderung widerzuspiegeln, wenn das sekundäre Replikat, das zum primären Replikat höher gestuft wurde, nicht lesbar war.  
  
-   Der Replikationsmonitor zeigt immer Veröffentlichungsinformationen unter dem ursprünglichen Verleger an. Diese Informationen können jedoch von einem beliebigen Replikat aus im Replikationsmonitor angezeigt werden, indem der ursprüngliche Verleger als Server hinzugefügt wird.  
  
-   Bei Verwendung von gespeicherten Prozeduren oder Replikationsverwaltungsobjekten (RMO, Replication Management Objects) zum Verwalten der Replikation im primären Replikat müssen Sie in Fällen, in denen Sie den Verlegernamen angeben, den Namen der Instanz angeben, auf der die Datenbank für die Replikation aktiviert wurde. Den entsprechenden Namen ermitteln Sie mithilfe der **PUBLISHINGSERVERNAME** -Funktion. Wenn eine Veröffentlichungsdatenbank einer Verfügbarkeitsgruppe beitritt, sind die in den sekundären Datenbankreplikaten gespeicherten Replikationsmetadaten mit denen im primären Replikat identisch. Demzufolge entspricht für Veröffentlichungsdatenbanken, die in der primären Replikatdatenbank zur Replikation aktiviert wurden, der in den Systemtabellen des sekundären Replikats gespeicherte Verlegerinstanzname dem Namen der primären Replikatdatenbank und nicht dem Namen der sekundären Replikatdatenbank. Dies wirkt sich auf die Replikationskonfiguration und -wartung aus, wenn ein Failover der Veröffentlichungsdatenbank zur sekundären Replikatdatenbank erfolgt. Wenn Sie z.B. die Replikation mit gespeicherten Prozeduren bei einem sekundären Replikat nach einem Failover konfigurieren, und Sie ein Pullabonnement für eine Veröffentlichungsdatenbank möchten, die bei einem anderen Replikat aktiviert wurde, müssen Sie den Namen des ursprünglichen Verlegers statt des aktuellen Verlegers als *@publisher* -Parameter von **sp_addpullsubscription** oder **sp_addmergepulllsubscription**angeben. Wenn Sie jedoch eine Veröffentlichungsdatenbank nach einem Failover aktivieren, entspricht der in den Systemtabellen gespeicherte Verlegerinstanzname dem Namen des aktuellen primären Hosts. In diesem Fall würden Sie den Hostnamen des aktuellen primären Replikats für den *@publisher* -Parameter verwenden.  
  
    > [!NOTE]  
    >  Bei einigen Prozeduren, z.B. **sp_addpublication**, wird der *@publisher* -Parameter nur für Verleger unterstützt, die keine Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]sind. In diesen Fällen ist er für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Always On nicht relevant.  
  
-   Synchronisieren Sie die Pullabonnements vom Abonnenten und die Pushabonnements vom aktiven Verleger aus, um ein Abonnement in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] nach einem Failover zu synchronisieren.  
  
##  <a name="RemovePublDb"></a> Entfernen einer veröffentlichten Datenbank aus einer Verfügbarkeitsgruppe  
 Berücksichtigen Sie die folgenden Probleme, wenn eine veröffentlichte Datenbank aus einer Verfügbarkeitsgruppe entfernt wird, oder wenn eine Verfügbarkeitsgruppe, die eine veröffentlichte Elementdatenbank aufweist, gelöscht wird.  
  
-   Wenn die Veröffentlichungsdatenbank beim ursprünglichen Verleger aus einem primären Replikat der Verfügbarkeitsgruppe entfernt wird, müssen Sie **sp_redirect_publisher** ausführen, ohne einen Wert für den *@redirected_publisher* -Parameter anzugeben, um die Umleitung für das Verleger-/Datenbankpaar zu entfernen.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB';  
    ```  
  
     Die Datenbank wird auf dem primären Replikat im Wiederherstellungsstatus belassen und muss wiederhergestellt werden. Sobald Sie dies tun, sollte die Replikation unverändert mit dem ursprünglichen Verleger funktionieren.  
  
-   Wenn für die Veröffentlichungsdatenbank ein Failover vom ursprünglichen Verleger zu einem Replikat ausgeführt und die Datenbank aus dem primären Replikat der Verfügbarkeitsgruppe entfernt wird, führen Sie die gespeicherte Prozedur **sp_redirect_publisher** aus, um den ursprünglichen Verleger zum neuen Verleger umzuleiten. Die Datenbank wird im Wiederherstellungsstatus belassen und muss wiederhergestellt werden. Sobald Sie dies tun, sollte die Replikation weiterhin so funktionieren wie zuvor in der Verfügbarkeitsgruppe.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB',  
        @redirected_publisher = 'MyNewPublisher';  
    ```  
  
     Entfernen Sie den Remoteserver für den ursprünglichen Verleger selbst dann nicht aus dem Verteiler, wenn nicht mehr auf den Server zugegriffen werden kann. Die Servermetadaten für den ursprünglichen Verleger werden beim Verteiler benötigt, um Abfragen von Veröffentlichungsmetadaten beantworten zu können  
  
-   Wenn eine vollständige Verfügbarkeitsgruppe entfernt wird, wirkt sich dies auf eine replizierte Mitgliedsdatenbank auf die gleiche Weise aus, wie das Entfernen einer veröffentlichten Datenbank aus einer Verfügbarkeitsgruppe. Die Replikation kann vom letzten primären Replikat fortgesetzt werden, sobald die Datenbank wiederhergestellt und die Umleitung geändert wurde. Wenn die Datenbank auf ihrem ursprünglichen Verleger wiederhergestellt wird, sollte die Umleitung entfernt werden. Wenn die Datenbank bei einem anderen Host wiederhergestellt wird, sollte Umleitung explizit an den neuen Host umgeleitet werden.  
  
    > [!NOTE]  
    >  Wenn eine Verfügbarkeitsgruppe entfernt wird, die über veröffentlichte Mitgliedsdatenbanken verfügt, oder wenn eine veröffentlichte Datenbank aus einer Verfügbarkeitsgruppe entfernt wird, werden alle Kopien der veröffentlichten Datenbanken im Wiederherstellungsstatus belassen. Nach der Wiederherstellung wird jede Datenbank als veröffentlichte Datenbank angezeigt. Nur eine Kopie sollte mit Veröffentlichungsmetadaten beibehalten werden. Um die Replikation für eine veröffentlichte Datenbankkopie zu deaktivieren, entfernen Sie zuerst alle Abonnements und Veröffentlichungen aus der Datenbank.  
  
     Führen Sie **sp_dropsubscription** aus, um die Veröffentlichungsabonnements zu entfernen. Vergessen Sie nicht, den Parameter *@ignore_distributributor* auf 1 festzulegen, um die Metadaten beim Verteiler für die aktive Veröffentlichungsdatenbank beizubehalten.  
  
    ```  
    USE MyDBName;  
    GO  
  
    EXEC sys.sp_dropsubscription   
        @subscriber = 'MySubscriber',  
        @publication = 'MyPublication',  
        @article = 'all',  
        @ignore_distributor = 1;  
    ```  
  
     Führen Sie **sp_droppublication** aus, um alle Veröffentlichungen zu entfernen. Auch hier dürfen Sie nicht vergessen, den Parameter *@ignore_distributor* auf 1 festzulegen, um die Metadaten beim Verteiler für die aktive Veröffentlichungsdatenbank beizubehalten.  
  
    ```  
    EXEC sys.sp_droppublication   
        @publication = 'MyPublication',  
        @ignore_distributor = 1;  
    ```  
  
     Führen Sie **sp_replicationdboption** aus, um die Replikation für die Datenbank zu deaktivieren.  
  
    ```  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'false';  
    ```  
  
     An diesem Punkt kann die Kopie der veröffentlichten Datenbank beibehalten oder gelöscht werden.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Konfigurieren der Replikation für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)  
  
-   [Replikation, Änderungsnachverfolgung, Change Data Capture und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)  
  
-   [Verwaltung &#40;Replikation&#41;](../../../relational-databases/replication/administration/administration-replication.md)  
  
-   [Replikationsabonnenten und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On-Verfügbarkeitsgruppen: Interoperabilität (SQL Server)](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [SQL Server-Replikation](../../../relational-databases/replication/sql-server-replication.md)  
  
  
