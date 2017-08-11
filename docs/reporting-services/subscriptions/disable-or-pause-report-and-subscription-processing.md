---
title: Deaktivieren oder Anhalten der Berichts- und Abonnementverarbeitung | Microsoft Docs
ms.custom: 
ms.date: 09/29/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9fa43a5766fc82bfb716f275600b50eaab6c1ed0
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="disable-or-pause-report-and-subscription-processing"></a>Deaktivieren oder Anhalten der Berichts- und Abonnementverarbeitung
  Es gibt verschiedene Methoden zum Deaktivieren oder Anhalten der Berichts- und Abonnementverarbeitung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Die in diesem Thema beschriebenen Ansätze reichen vom Deaktivieren eines Abonnements bis hin zum Unterbrechen der Datenquellenverbindung. Nicht alle Ansätze sind in beiden [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Servermodi möglich. In den folgenden Tabellen werden die Methoden und unterstützten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Servermodi zusammengefasst:  
  
##  <a name="bkmk_top"></a> In diesem Thema  
  
||Unterstützter Servermodus|  
|-|---------------------------|  
|[Aktivieren und Deaktivieren von Abonnements](#bkmk_disable_subscription)|Einheitlicher Modus|  
|[Anhalten eines freigegebenen Zeitplans](#bkmk_pause_schedule)|Einheitlicher und SharePoint-Modus|  
|[Deaktivieren einer freigegebenen Datenquelle](#bkmk_disable_shared_datasource)|Einheitlicher und SharePoint-Modus|  
|[Ändern von Rollenzuweisungen zum Verhindern des Zugriffs auf einen Bericht (einheitlicher Modus)](#bkmk_modify_role_assignment)|Einheitlicher Modus|  
|[Entfernen von Berechtigungen zur Abonnementverwaltung aus Rolle (einheitlicher Modus)](#bkmk_remove_manage_subscriptions_permission)|Einheitlicher Modus|  
|[Deaktivieren von Übermittlungserweiterungen](#bkmk_disable_extensions)|Einheitlicher und SharePoint-Modus|  
  
##  <a name="bkmk_disable_subscription"></a> Aktivieren und Deaktivieren von Abonnements  
  
> [!TIP]  
>  Neu in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]! **Aktivieren und Deaktivieren von Abonnements**. Neue Optionen der Benutzeroberfläche ermöglichen Ihnen ein schnelles Deaktivieren und Aktivieren von Abonnements. Die deaktivierten Abonnements behalten ihre anderen Konfigurationseigenschaften, z. B. den Zeitplan, bei und können leicht aktiviert werden. Sie können Abonnements auch programmgesteuert aktivieren und deaktivieren oder überwachen, welche Abonnements deaktiviert werden.  
  
 ![Reporting services-Abonnement Menüband](../../reporting-services/subscriptions/media/ssrs-subscription-ribbon.png "reporting services-Abonnement-Menüband")  
  
 Wechseln Sie im Berichts-Manager im einheitlichen Modus zum Abonnement. Verwenden Sie dafür entweder die Seite **Meine Abonnements** oder die Seite **Verwalten** eines einzelnen Abonnements. Wählen Sie ein oder mehrere Abonnements aus, und klicken Sie dann auf deaktivieren ![Deaktivieren eines Abonnements für reporting Services](../../reporting-services/subscriptions/media/ssrs-disable-subscription.png "Deaktivieren eines Abonnements für reporting Services") Schaltfläche oder aktivieren Sie die Schaltfläche ![Aktivieren von reporting Services-Abonnement](../../reporting-services/subscriptions/media/ssrs-enable-subscription.png "Aktivieren von reporting Services-Abonnement") auf dem Menüband. Deaktivierte Abonnements werden mit einem Warnsymbol gekennzeichnet ![Warnung bei Status eines reporting services-Subscriptio](../../reporting-services/subscriptions/media/ssrs-subscription-warning.png "Warnung bei Status eines reporting services-Subscriptio") und der Status wird als **deaktiviert**.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] schreibt eine Zeile in das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Protokoll, wenn ein Abonnement deaktiviert wird, und einen weiteren Eintrag, wenn das Abonnement aktiviert wird. In der Berichtsserver-Protokolldatei:  
  
 `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__10_16_2014_00_02_18.log`  
  
 werden in etwa folgende Zeilen angezeigt:  
  
 `library!ReportServer_0-1!b08!10/16/2014-16:21:14:: i INFO: Call to DisableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934)`  
  
 `library!ReportServer_0-1!2eec!10/16/2014-16:44:18:: i INFO: Call to EnableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934).`  
  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt") **Verwenden von PowerShell zum Deaktivieren eines einzelnen Abonnements:** verwenden Sie das folgende PowerShell-Skript, um ein bestimmtes Abonnement zu deaktivieren. Aktualisieren Sie den Servernamen und die Abonnement-ID.  
  
```  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid”;  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 Mit dem folgenden Skript können Sie alle Abonnements mit ihren IDs auflisten. Aktualisieren Sie den Servernamen.  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt") **Verwenden von PowerShell zum Auflisten aller deaktivierten Abonnements:** verwenden Sie das folgende PowerShell-Skript zum Auflisten aller deaktivierten Abonnements auf dem aktuellen Berichtsserver im einheitlichen Modus. Aktualisieren Sie den Servernamen.  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt") **Verwenden von PowerShell zum Aktivieren aller deaktivierten Abonnements:** das folgende PowerShell-Skript verwenden, um alle Abonnements zu ermöglichen, die derzeit deaktiviert sind. Aktualisieren Sie den Servernamen.  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt") **Verwenden von Windows PowerShell zum Deaktivieren aller Abonnements:** verwenden Sie das folgende PowerShell-Skript zu deaktivieren **alle** Abonnements.  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="bkmk_pause_schedule"></a> Anhalten eines freigegebenen Zeitplans  
 Wenn ein Bericht oder ein Abonnement mit einem freigegebenen Zeitplan ausgeführt wird, können Sie den Zeitplan anhalten, um die Verarbeitung zu verhindern. Alle Berichts- und Abonnementverarbeitungen, die durch den Zeitplan gesteuert werden, werden zurückgestellt, bis der Zeitplan fortgesetzt wird.  
  
-   **SharePoint-Modus:** ![SharePoint Einstellungen](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Einstellungen") In **Siteeinstellungen**Option **freigegebene Zeitpläne verwalten**. Wählen Sie den Zeitplan aus, und klicken Sie auf **Ausgewählte Zeitpläne anhalten**.  
  
-   **Einheitlicher Modus:** Klicken Sie im Berichts-Manager auf **Standorteinstellungen**. Wählen Sie den Zeitplan aus, und klicken Sie auf **Anhalten**.  
  
##  <a name="bkmk_disable_shared_datasource"></a> Deaktivieren einer freigegebenen Datenquelle  
 Ein Vorteil des Verwendens freigegebener Datenquellen ist, dass Sie diese deaktivieren können, um die Ausführung eines Berichts oder eines datengesteuerten Abonnements zu verhindern. Durch das Deaktivieren einer freigegebenen Datenquelle wird die Verbindung des Berichts mit der externen Quelle getrennt. Die deaktivierte Datenquelle steht für keine Berichte und Abonnements zur Verfügung.  
  
 Beachten Sie, dass der Bericht weiterhin geladen wird, selbst wenn die Datenquelle nicht verfügbar ist. Der Bericht enthält keine Daten, aber Benutzer mit entsprechenden Berechtigungen haben Zugriff auf die Eigenschaftenseiten, Sicherheitseinstellungen, den Berichtsverlauf und die Abonnementinformationen für den Bericht.  
  
-   **SharePoint-Modus:** Um eine freigegebene Datenquelle in einem Berichtsserver im SharePoint-Modus zu deaktivieren, wechseln Sie zu der Dokumentbibliothek, die die Datenquelle enthält. ![Symbol für freigegebene Datenquelle](../../reporting-services/report-data/media/hlp-16datasource.png "Symbol für freigegebene Datenquelle") klicken Sie auf die Datenquelle, und deaktivieren Sie dann die **diese Datenquelle aktivieren** Kontrollkästchen.  
  
-   **Einheitlicher Modus:** Um eine freigegebene Datenquelle auf einem Berichtsserver im einheitlichen Modus zu deaktivieren, öffnen Sie die Datenquelle im Berichts-Manager, und deaktivieren Sie das Kontrollkästchen **Diese Datenquelle aktivieren** .  
  
##  <a name="bkmk_modify_role_assignment"></a> Ändern von Rollenzuweisungen zum Verhindern des Zugriffs auf einen Bericht (einheitlicher Modus)  
 Eine Möglichkeit, um einen Bericht nicht verfügbar zu machen, ist das vorübergehende Entfernen der Rollenzuweisung, die den Zugriff auf den Bericht bereitstellt. Diese Vorgehensweise kann für alle Berichte unabhängig von der Art der Datenquellenverbindung verwendet werden. Dabei ist nur der Bericht betroffen. Die Ausführung anderer Berichte oder Elemente ist davon nicht betroffen.  
  
 Öffnen Sie die Eigenschaftenseite Sicherheit des Berichts im Berichts-Manager, um die Rollenzuweisung zu entfernen. Falls der Bericht die Sicherheit von einem übergeordneten Bericht erbt, können Sie auf **Elementsicherheit bearbeiten** klicken, um eine restriktive Sicherheitsrichtlinie zu erstellen, die Rollenzuweisungen für den Zugriff auf breiter Basis ausklammert (entfernen Sie z.B. eine Rollenzuweisung, die jedem Benutzer den Zugriff ermöglicht, und behalten Sie die Rollenzuweisung, die einer kleinen Benutzergruppe den Zugriff ermöglicht, wie z.B. Administratoren).  
  
##  <a name="bkmk_remove_manage_subscriptions_permission"></a> Entfernen von Berechtigungen zur Abonnementverwaltung aus Rolle (einheitlicher Modus)  
 Entfernen Sie den Task **Einzelne Abonnements verwalten** aus der Rolle, um zu verhindern, dass Benutzer Abonnements erstellen. Wenn Sie diesen Task entfernen, sind die Abonnementseiten nicht verfügbar. Im Berichts-Manager scheint die Seite Meine Abonnements leer zu sein (kann nicht gelöscht werden), selbst wenn zuvor Abonnements enthalten waren. Das Entfernen von Tasks im Zusammenhang mit Abonnements verhindert, dass Benutzer Abonnements erstellen und ändern. Vorhandene Abonnements werden dadurch jedoch nicht gelöscht. Vorhandene Abonnements werden so lange weiter ausgeführt, bis Sie sie löschen. So entfernen Sie die Berechtigung:  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
2.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver her.  
  
3.  Erweitern Sie den Knoten **Sicherheit** .  
  
4.  Wählen Sie die Rolle aus, und deaktivieren Sie den Task **Einzelne Abonnements verwalten** .  
  
##  <a name="bkmk_disable_extensions"></a> Deaktivieren von Übermittlungserweiterungen  
 Alle auf einem Berichtsserver installierten Übermittlungserweiterungen sind für jeden Benutzer verfügbar, der Berechtigungen zum Erstellen eines Abonnements für einen vorhandenen Bericht hat. Die folgenden Übermittlungserweiterungen sind verfügbar und werden automatisch konfiguriert:  
  
-   Windows-Dateifreigabe  
  
-   SharePoint-Bibliothek (nur über eine SharePoint-Website verfügbar, die in einen Berichtsserver mit integriertem SharePoint-Modus integriert ist)  
  
 Die E-Mail-Übermittlung muss konfiguriert werden, bevor sie verwendet werden kann. Wenn Sie sie nicht konfigurieren, ist sie nicht verfügbar. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83).  
  
 Wenn Sie bestimmte Erweiterungen deaktivieren möchten, können Sie die Erweiterungseinträge in der Datei **RSReportServer.config** entfernen. Weitere Informationen finden Sie unter [Reporting Services-Konfigurationsdateien](../../reporting-services/report-server/reporting-services-configuration-files.md) und [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83).  
  
 Eine entfernte Übermittlungserweiterung ist im Berichts-Manager oder auf einer SharePoint-Website nicht mehr verfügbar. Das Entfernen einer Übermittlungserweiterung kann inaktive Abonnements zur Folge haben. Stellen Sie vor dem Entfernen einer Erweiterung sicher, dass Sie die Abonnements löschen oder sie so konfigurieren, dass sie eine andere Übermittlungserweiterung verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Abonnements und Übermittlung &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services-Konfigurationsdateien](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Konfigurieren des Berichts-Manager &#40; Im einheitlichen Modus &#41;](../../reporting-services/report-server/configure-report-manager-native-mode.md)   
 [Reporting Services-Berichtsserver &#40; Im einheitlichen Modus &#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Berichts-Manager &#40; SSRS im einheitlichen Modus &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Sicherheit-Eigenschaftenseite, Elemente &#40; Berichts-Manager &#41;](http://msdn.microsoft.com/library/351b8503-354f-4b1b-a7ac-f1245d978da0)  
  
  

