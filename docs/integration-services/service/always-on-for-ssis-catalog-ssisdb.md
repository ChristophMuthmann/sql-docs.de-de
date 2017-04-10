---
title: "Always On for SSIS Catalog (SSISDB) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.alwayson.f1"
ms.assetid: 7f089455-35ee-4c13-884e-9254b685d07d
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Always On for SSIS Catalog (SSISDB)
  Das Feature der Always On-Verfügbarkeitsgruppen ist eine Lösung für hohe Verfügbarkeit und Notfallwiederherstellung, die eine Alternative zur Datenbankspiegelung auf Unternehmensebene bietet. Eine Verfügbarkeitsgruppe unterstützt eine Failoverumgebung für einen diskreten Satz von Benutzerdatenbanken. Diese werden auch als Verfügbarkeitsdatenbanken bezeichnet, die zusammen ein Failover ausführen. Weitere Informationen finden Sie unter [Always On-Verfügbarkeitsgruppen](https://msdn.microsoft.com/library/hh510230.aspx).  
  
 Um eine hohe Verfügbarkeit für den SSIS-Katalog (SSISDB) und dessen Inhalt (Projekte, Pakete, Ausführungsprotokolle usw.) zu gewährleisten, können Sie die SSISDB-Datenbank wie jede andere Benutzerdatenbank zu einer Always On-Verfügbarkeitsgruppe hinzufügen. Wenn ein Failover auftritt, übernimmt einer der sekundären Knoten automatisch die Rolle eines primären Knoten.  
 
 > [!IMPORTANT]  Wenn ein Failover auftritt, werden Pakete, die ausgeführt wurden, nicht neu gestartet oder fortgesetzt. 
 
 **In diesem Thema:**  
  
1.  [Voraussetzungen](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#prereq)  
  
2.  [Konfigurieren der SSIS-Unterstützung für Always On](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Firsttime)  
  
3.  [Upgraden von SSISDB in einer Verfügbarkeitsgruppe](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade)  
  
##  <a name="a-nameprereqa-prerequisites"></a><a name="prereq"></a>Voraussetzungen  
 Bevor Sie die Always On-Unterstützung für die SSISDB-Datenbank aktivieren, müssen Sie folgende Schritte ausführen.  
  
1.  Erstellen Sie einen Windows-Failovercluster. Weitere Anweisungen finden Sie im Blogbeitrag [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Failoverclusterfunktion und Tools für Windows Server 2012 installieren). Sie sollten die Funktion und die Tools auf allen Clusterknoten installieren.  
  
2.  Installieren Sie SQL Server 2016 mit der Funktion Integration Services (SSIS) auf jedem Clusterknoten.  
  
3.  Aktivieren Sie die Always On-Funktion für jede SQL Server-Instanz. Weitere Informationen finden Sie unter [Aktivieren von Always On-Verfügbarkeitsgruppen](https://msdn.microsoft.com/library/ff878259.aspx) .  
  
##  <a name="a-namefirsttimea-configure-ssis-support-for-always-on"></a><a name="Firsttime"></a> Konfigurieren der SSIS-Unterstützung für Always On  
  
-   [Schritt 1: Erstellen des Integration Services-Katalogs](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step1)  
  
-   [Schritt 2: Hinzufügen von SSISDB zu einer Always On-Verfügbarkeitsgruppe](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2)  
  
-   [Schritt 3: Aktivieren der SSIS-Unterstützung für Always On](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3)  
  
> [!IMPORTANT]  
>  -   Sie müssen diese Schritte auf dem **Primärknoten** der Verfügbarkeitsgruppe ausführen.  
> -   Sie müssen die **SSIS-Unterstützung für Always On** nach dem Hinzufügen von SSISDB zu einer Always On-Gruppe aktivieren.  
  
###  <a name="a-namestep1a-step-1-create-integration-services-catalog"></a><a name="Step1"></a> Schritt 1: Erstellen des Integration Services-Katalogs  
  
1.  Starten Sie **SQL Server Management Studio** , und stellen Sie eine Verbindung mit einer SQL Server-Instanz in dem Cluster her, den Sie als **primären Knoten** der Always On-Gruppe mit hoher Verfügbarkeit für SSISDB festlegen möchten.  
  
2.  Erweitern Sie im Objekt-Explorer den Serverknoten, klicken Sie mit der rechten Maustaste auf den Knoten **Integration Services-Kataloge** , und klicken Sie dann auf **Katalog erstellen**.  
  
3.  Klicken Sie auf **CLR-Integration aktivieren**. Für den Katalog werden gespeicherte CLR-Prozeduren verwendet.  
  
4.  Klicken Sie auf **Automatische Ausführung gespeicherter Integration Services-Prozeduren beim Starten von SQL Server aktivieren** , um die gespeicherte [catalog.startup](https://msdn.microsoft.com/library/hh230984.aspx) -Prozedur jedes Mal ausführen zu lassen, wenn die SSIS-Serverinstanz neu gestartet wird. Durch die gespeicherte Prozedur wird der Status von Vorgängen für den SSISDB-Katalog verwaltet. Dabei wird der Status aller Pakete korrigiert, die während des Ausfalls der SSIS-Serverinstanz (falls zutreffend) ausgeführt wurden.  
  
5.  Geben Sie ein **Kennwort**ein, und klicken Sie dann auf **OK**. Das Kennwort schützt den Datenbank-Hauptschlüssel, der zum Verschlüsseln der Katalogdaten verwendet wird. Bewahren Sie das Kennwort sicher auf. Es wird empfohlen, auch den Datenbank-Hauptschlüssel zu sichern. Weitere Informationen finden Sie unter [Sichern eines Datenbank-Hauptschlüssels](https://msdn.microsoft.com/library/aa337546.aspx).  
  
###  <a name="a-namestep2a-step-2-add-ssisdb-to-an-always-on-availability-group"></a><a name="Step2"></a> Schritt 2: Hinzufügen von SSISDB zu einer Always On-Verfügbarkeitsgruppe  
 Das Hinzufügen der SSISDB-Datenbank zu einer Always On-Verfügbarkeitsgruppe ist fast identisch mit dem Hinzufügen einer anderen Benutzerdatenbank zu einer Verfügbarkeitsgruppe. Weitere Informationen finden Sie unter [Verwenden des Assistenten für Verfügbarkeitsgruppen (SQL Server Management Studio)](https://msdn.microsoft.com/library/hh403415.aspx).  
  
 Sie müssen das Kennwort angeben, das Sie beim Erstellen des SSIS-Katalogs auf der Seite **Datenbanken auswählen** im Assistenten für die **Neue Verfügbarkeitsgruppe** angegeben haben.  
  
 ![New Availability Group](../../integration-services/service/media/ssis-newavailabilitygroup.png "New Availability Group")  
  
###  <a name="a-namestep3a-step-3-enable-ssis-support-for-always-on"></a><a name="Step3"></a> Schritt 3: Aktivieren der SSIS-Unterstützung für Always On  
 Nach dem Erstellen des Integration Service-Katalogs klicken Sie mit der rechten Maustaste auf den Knoten **Integration Service-Kataloge** , und klicken Sie auf **Always On-Unterstützung aktivieren...**. Daraufhin sollte das Dialogfeld **Unterstützung für Always On aktivieren** angezeigt werden. Wenn dieses Menüelement deaktiviert ist, vergewissern Sie sich, dass Sie alle erforderlichen Komponenten installiert haben, und klicken Sie auf **Aktualisieren**.  
  
 ![Enable Support for AlwaysOn](../../integration-services/service/media/ssis-enablesupportforalwayson.png "Enable Support for AlwaysOn")  
  
> [!WARNING]  
>  Das automatische Failover für die SSISDB-Datenbank wird nur unterstützt, wenn Sie die SSIS-Unterstützung für Always On aktiviert haben.  
  
 Die neu hinzugefügten sekundären Replikate aus der AlwaysOn-Verfügbarkeitsgruppe werden in der Tabelle angezeigt. Klicken Sie auf **Verbinden…** , und geben Sie Anmeldeinformationen für die Authentifizierung ein, um eine Verbindung mit dem Replikat herzustellen. Das Benutzerkonto muss auf jedem Replikat Mitglied der Gruppe „sysadmin“ sein, um die SSIS-Unterstützung für Always On zu aktivieren. Klicken Sie nach der erfolgreichen Herstellung einer Verbindung mit jedem Replikat auf **OK** , um die SSIS-Unterstützung für Always On zu aktivieren.  
  
##  <a name="a-nameupgradea-upgrading-ssisdb-in-an-availability-group"></a><a name="Upgrade"></a> Upgraden von SSISDB in einer Verfügbarkeitsgruppe  
 Wenn Sie SQL Server von einer früheren Version aktualisieren und sich SSISDB in einer Always On-Verfügbarkeitsgruppe befindet, wird Ihr Upgrade möglicherweise durch die Regel „Überprüfung ,SSISDB in Always On-Verfügbarkeitsgruppe‘“ blockiert. Diese Blockierung tritt auf, da die Aktualisierung im Einzelbenutzermodus ausgeführt wird, während eine Verfügbarkeitsdatenbank eine Mehrbenutzerdatenbank sein muss. Daher werden während des Upgradens oder Patchens alle Verfügbarkeitsdatenbanken, einschließlich SSISDB, offline geschaltet und werden daher nicht upgegradet oder gepatcht. Um das Upgrade fortzusetzen, müssen Sie zuerst SSISDB aus der Verfügbarkeitsgruppe entfernen, dann jeden Knoten upgraden oder patchen und SSISDB dann wieder der Verfügbarkeitsgruppe hinzufügen.  
  
 Wenn Sie durch die Regel „Überprüfung ,SSISDB in Always On-Verfügbarkeitsgruppe‘“ blockiert werden, müssen Sie diese Schritte ausführen, um SQL Server zu aktualisieren.  
  
1.  Entfernen Sie die SSISDB-Datenbank aus der Verfügbarkeitsgruppe. Weitere Informationen finden Sie unter [Entfernen einer sekundären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md) und [Entfernen einer primären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
2.  Klicken Sie im Upgrade-Assistenten auf **Erneut ausführen**. Die Regel „Überprüfung ,SSISDB in Always On-Verfügbarkeitsgruppe‘“ wird nun erfolgreich ausgeführt.  
  
3.  Klicken Sie auf **Weiter** , um das Upgrade fortzusetzen.  
  
4.  Nachdem Sie alle Knoten aktualisiert haben, fügen Sie die SSISDB-Datenbank wieder zur Always On-Verfügbarkeitsgruppe hinzu. Weitere Informationen finden Sie unter [Hinzufügen einer Datenbank zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/add-a-database-to-an-availability-group-sql-server.md).  
  
 Wenn Sie beim Upgrade von SQL Server nicht blockiert werden und SSISDB sich in einer Always On-Verfügbarkeitsgruppe befindet, müssen Sie SSISDB nach dem Upgrade des SQL Server-Datenbankmoduls gesondert aktualisieren. Verwenden Sie den SSIS-Upgrade-Assistenten, um die SSISDB upzugraden, wie im folgenden Verfahren beschrieben.  
  
1.  Verschieben Sie die SSISDB-Datenbank aus der Verfügbarkeitsgruppe, oder löschen Sie die Verfügbarkeitsgruppe, falls SSISDB die einzige Datenbank in der Verfügbarkeitsgruppe ist. Sie müssen **SQL Server Management Studio** auf dem **Primärknoten** der Verfügbarkeitsgruppe starten, um diese Aufgabe auszuführen.  
  
2.  Entfernen Sie die SSISDB-Datenbank von allen **Replikatknoten**.  
  
3.  Upgraden Sie die SSISDB-Datenbank auf dem **Primärknoten**. Erweitern Sie im**Objekt-Explorer** in SQL Server Management Studio die **Integration Services-Kataloge**, klicken Sie mit der rechten Maustaste auf **SSISDB**, und wählen Sie dann **Datenbankupgrade**aus. Führen Sie die Anweisungen im **SSISDB-Upgrade-Assistenten** aus, um die Datenbank upzugraden. Sie müssen den **SSIDB-Upgrade-Assistenten** lokal auf dem **Primärknoten**starten.  
  
4.  Befolgen Sie die Anweisungen in [Schritt 2: Hinzufügen von SSISDB zu einer Always On-Verfügbarkeitsgruppe](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2) , um die SSISDB wieder zu einer Verfügbarkeitsgruppe hinzuzufügen.  
  
5.  Befolgen Sie die Anweisungen in [Schritt 3: Aktivieren der SSIS-Unterstützung für Always On](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3).  
  
  