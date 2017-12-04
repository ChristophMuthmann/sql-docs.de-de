---
title: "Bereitstellen von Abonnements und Warnungen für SSRS-Dienstanwendungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/03/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reporting Services Shared Service
- SharePoint Mode [Reporting Services]
- SharePoint Mode
- Reporting Services Service Application
- SSRS service application
ms.assetid: d0de3f1f-4887-47fb-bacf-46aaad74c4be
caps.latest.revision: "20"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a96245405f8f13de983215100cde3b189e2b0f17
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="provision-subscriptions-and-alerts-for-ssrs-service-applications"></a>Bereitstellen von Abonnements und Warnungen für SSRS-Dienstanwendungen
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnements und -Datenwarnungen setzt voraus, dass der SQL Server-Agent verwendet und SQL Server-Agentberechtigungen konfiguriert werden. Wenn Fehlermeldungen darauf hinweisen, dass der SQL Server-Agent erforderlich ist und Sie den SQL Server-Agent gestartet haben, können Sie die Berechtigungen aktualisieren oder überprüfen. Dieses Thema erstreckt sich auf [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus. Es werden drei Methoden beschrieben, wie Sie SQL Server-Agentberechtigungen bei Verwendung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnements aktualisieren können. Die Anmeldeinformationen, die Sie in den Schritten dieses Themas verwenden, müssen ausreichende Berechtigungen aufweisen, um RSExecRole-Ausführungsberechtigungen für Objekte in der Dienstanwendung sowie in der msdb- und Masterdatenbank zu gewähren.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2016 &#124; SharePoint 2013|  
  
 ![SQL Agent-Berechtigungen für Dienstanwendungs-Datenbanken](../../reporting-services/install-windows/media/rs-provisionsqlagent.gif "SQL Agent permissions to Service Application DBs")  
  
||Description|  
|------|-----------------|  
|**1**|Die Instanz des SQL Server-Datenbankmoduls, die die Reporting Services-Dienstanwendungsdatenbanken hostet.|  
|**2**|Die Instanz des SQL Server-Agents für die Instanz des SQL-Datenbankmoduls|  
|**3**|Die Reporting Services-Dienstanwendungsdatenbanken Die Namen basieren auf den Informationen, die zum Erstellen der Dienstanwendung verwendet wurden. Es werden beispielsweise folgende Datenbanknamen verwendet:<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0_Alerting<br /><br /> ReportingService_2fbae157295d49df86d0b85760c704b0TempDB|  
|**4**|Der Master und die MSDB-Datenbank der Instanz des SQL-Datenbankmoduls.|  
  
 Verwenden Sie einen der folgenden drei Methoden, um die Berechtigungen zu aktualisieren:  
  
1.  Geben Sie auf der Seite **Bereitstellungen und Abonnements und Warnungen** Anmeldeinformationen ein, und klicken Sie auf **OK**.  
  
2.  Klicken auf die Schaltfläche **Skript herunterladen** auf der Seite Bereitstellungen und Abonnements und Warnungen, um ein Transact-SQL-Skript für die Konfiguration von Berechtigungen herunterzuladen  
  
3.  Ausführen eines PowerShell-Cmdlet, um ein Transact-SQL-Skript für die Konfiguration von Berechtigungen zu erstellen  
  
### <a name="to-update-permissions-using-the-provision-page"></a>So aktualisieren Sie Berechtigungen mithilfe der Bereitstellungsseite  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Anwendungsverwaltung** auf **Dienstanwendungen verwalten**.  
  
2.  Suchen Sie die Dienstanwendung in der Liste, und klicken Sie auf den Namen der Anwendung. Sie können zum Auswählen der Dienstanwendung auch auf die Spalte **Typ** und anschließend im SharePoint-Menüband auf die Schaltfläche **Verwalten** klicken.  
  
3.  Klicken Sie auf der Seite **Reporting Services-Anwendung verwalten** auf **Abonnements und Warnungen bereitstellen**.  
  
4.  Wenn der SharePoint-Administrator über ausreichende Berechtigungen für die Masterdatenbank und die Dienstanwendungsdatenbanken verfügt, geben Sie diese Anmeldeinformationen ein.  
  
5.  Klicken Sie auf die Schaltfläche **OK** .  
  
##  <a name="bkmk_download"></a> So laden Sie das Transact-SQL-Skript herunter  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Anwendungsverwaltung** auf **Dienstanwendungen verwalten**.  
  
2.  Suchen Sie die Dienstanwendung in der Liste, und klicken Sie auf den Namen der Anwendung. Sie können zum Auswählen der Dienstanwendung auch auf die Spalte **Typ** und anschließend im SharePoint-Menüband auf die Schaltfläche **Verwalten** klicken.  
  
3.  Klicken Sie auf der Seite **Reporting Services-Anwendung verwalten** auf **Abonnements und Warnungen bereitstellen**.  
  
4.  Überprüfen Sie im Bereich **Status anzeigen** , ob der SQL Server-Agent ausgeführt wird.  
  
5.  Klicken Sie auf **Skript herunterladen** , um das Transact-SQL-Skript herunterzuladen, das Sie zum Erteilen von Berechtigungen in SQL Server Management Studio ausführen können. Der Name der erstellten Skriptdatei enthält den Namen der Reporting Services-Dienstanwendung, z.B. **[Name der Dienstanwendung]-GrantRights.sql**.  
  
### <a name="to-generate-the-transact-sql-statement-with-powershell"></a>So generieren Sie die Transact-SQL-Anweisung mit PowerShell  
  
1.  Sie können auch ein Windows PowerShell-Cmdlet in der Verwaltungsshell von SharePoint 2016 oder SharePoint 2013 verwenden, um das Transact-SQL-Skript zu erstellen.  
  
2.  Klicken Sie im Menü **Start** auf **Alle Programme**.  
  
3.  Erweitern Sie **Microsoft SharePoint 2016-Produkte** , und klicken Sie auf **SharePoint 2016-Verwaltungsshell**.
  
4.  Aktualisieren Sie das folgende PowerShell-Cmdlet, indem Sie den Namen der Berichtsserver-Datenbank, das Anwendungspoolkonto und den Pfad der Anweisung ersetzen.  
  
     **Syntax des Cmdlets:** `Get-SPRSDatabaseRightsScript –DatabaseName <ReportingServices database name> -UserName <app pool account> -IsWindowsUser | Out-File <path of statement>`  
  
     **Beispiel-Cmdlet:** `Get-SPRSDatabaseRightsScript –DatabaseName ReportingService_46fd00359f894b828907b254e3f6257c –UserName “NT AUTHORITY\NETWORK SERVICE” –IsWindowsUser | Out-File c:\SQLServerAgentrights.sql`  
  
## <a name="using-the-transact-sql-script"></a>Verwenden des Transact-SQL-Skripts  
 Die folgenden Verfahren können mit Skripts verwendet werden, die von der Bereitstellungsseite heruntergeladen oder mit PowerShell erstellt wurden.  
  
#### <a name="to-load-the-transact-sql-script-in-sql-server-management-studio"></a>So laden Sie das Transact-SQL-Skript in SQL Server Management Studio  
  
1.  Klicken Sie zum Öffnen von SQL Server Management Studio im Menü **Start** auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] und dann auf **SQL Server Management Studio**.  
  
2.  Legen Sie im Dialogfeld **Verbindung mit Server herstellen** die folgenden Optionen fest:  
  
    -   Wählen Sie in der Liste **Servertyp** die Option **Datenbankmodul**aus.  
  
    -   Geben Sie unter **Servernamen**den Namen der SQL Server-Instanz ein, auf der Sie den SQL Server-Agent konfigurieren möchten.  
  
    -   Wählen Sie einen Authentifizierungsmodus aus.  
  
    -   Wenn Sie eine Verbindung mit SQL Server-Authentifizierung herstellen, geben Sie einen Anmeldenamen und ein Kennwort an.  
  
3.  Klicken Sie auf **Verbinden**.  
  
#### <a name="to-run-the-transact-sql-statement"></a>So führen Sie die Transact-SQL-Anweisung aus  
  
1.  Klicken Sie auf der Symbolleiste von SQL Server Management Studio auf **Neue Abfrage**.  
  
2.  Klicken Sie im Menü **Datei** auf **Öffnen**und dann auf **Datei**.  
  
3.  Navigieren Sie zu dem Ordner, in dem Sie die Transact-SQL-Anweisung gespeichert haben, die Sie in der Verwaltungsshell von SharePoint 2016 oder SharePoint 2013 generiert haben.  
  
4.  Klicken Sie auf die Datei, und klicken Sie dann auf **Öffnen**.  
  
     Die Anweisung wird dem Abfragefenster hinzugefügt.  
  
5.  Klicken Sie auf **Ausführen**.  
  
  
