---
title: Reporting Services SharePoint Service and Service Applications | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 501aa9ee-8c13-458c-bf6f-24e00c82681b
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d34dfcd5c6c4ecb6ef91dc57cb7e98ee71512393
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Reporting Services-SharePoint-Dienst und -Dienstanwendungen
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint-Modus basiert auf der SharePoint-Dienstarchitektur und verwendet einen SharePoint-Dienst sowie mindestens eine dienstanwendung. Beim Erstellen einer Dienstanwendung wird der Dienst verfügbar gemacht und die Datenbank der Dienstanwendung generiert. Sie können mehrere Reporting Services-Dienstanwendungen erstellen, doch für die meisten Bereitstellungsszenarien ist eine Dienstanwendung ausreichend.  
  
 Dieses Thema enthält folgende Informationen:  
  
-   [Erstellen einer Reporting Services-Dienstanwendung](#bkmk_createapp)  
  
-   [Ändern der Zuordnungen der Dienstanwendung mit einer Proxygruppe](#bkmk_associations)  
  
-   [Bearbeiten von Eigenschaften für Dienstanwendungen](#bkmk_editserviceapplication)  
  
-   [So erstellen Sie eine Reporting Services-Dienstanwendung mit PowerShell](#bkmk_powershell_create_ssrs_serviceapp)  
  
-   [Verwandte Aufgaben](#bkmk_related)  
  
##  <a name="bkmk_createapp"></a> Erstellen einer Reporting Services-Dienstanwendung  
 Sie können die SharePoint-Zentraladministrations- oder PowerShell-Skripts verwenden, um die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungen zu erstellen. Weitere Informationen zum Verwenden der SharePoint-Zentraladministration finden Sie im Abschnitt "Erstellen einer Reporting Services-Dienstanwendung" in [Installieren des SharePoint-Modus von Reporting Services für SharePoint 2010](http://msdn.microsoft.com/en-us/47efa72e-1735-4387-8485-f8994fb08c8c). Lesen Sie den PowerShell-Abschnitt weiter unten in diesem Thema, um ein Beispiel zu einem PowerShell-Skript für die Erstellung von Dienstanwendungen zu erhalten.  
  
##  <a name="bkmk_associations"></a> Ändern der Zuordnungen der Dienstanwendung mit einer Proxygruppe  
 Die Seite Neu zum Erstellen einer Dienstanwendung enthält den Abschnitt **Zuordnung der Webanwendung**. Dieser Abschnitt ermöglicht es Ihnen, die Dienstanwendung im Rahmen der Erstellung zuzuordnen. Führen Sie die folgenden Schritte aus, um die Zuordnung zu ändern und der Dienstanwendung eine Kundenkonfiguration zuzuweisen. Sie können dasselbe allgemeine Verfahren auch verwenden, um den Proxy der Standardgruppe hinzuzufügen, anstatt die Zuordnung der Dienstanwendung in eine benutzerdefinierte Gruppe zu ändern.  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Anwendungsverwaltung auf **Zuordnungen von Dienstanwendungen konfigurieren**.  
  
2.  Ändern Sie auf der Seite Zuordnungen von Dienstanwendungen die Ansicht in **Dienstanwendungen**.  
  
3.  Suchen und klicken Sie auf den Namen der neuen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung. Sie können auch auf den Namen der Anwendungsproxygruppe **default** klicken, um den Proxy zur Standardgruppe hinzuzufügen, anstatt die folgenden Schritte auszuführen.  
  
4.  Wählen Sie im Auswahlfeld **Folgende Gruppe von Verbindungen bearbeiten** die Option **Benutzerdefiniert**.  
  
5.  Aktivieren Sie das Kontrollkästchen für den Proxy, und klicken Sie auf **OK**.  
  
##  <a name="bkmk_editserviceapplication"></a> Bearbeiten von Eigenschaften für Dienstanwendungen  
 Sie können die Eigenschaftenseite der Dienstanwendung erneut öffnen, um die Eigenschaften zu ändern.  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Wählen Sie die Dienstanwendung aus, indem Sie zum Auswählen der ganzen Zeile auf die Typspalte klicken. Wenn Sie auf den Namen der Anwendung klicken, wird die Seite mit Verwaltungsoptionen für den Dienst und nicht die Eigenschaftenseite der Dienstanwendung geöffnet.  
  
3.  Klicken Sie im Menüband Dienstanwendungen auf **Eigenschaften**.  
  
##  <a name="bkmk_powershell_create_ssrs_serviceapp"></a> So erstellen Sie eine Reporting Services-Dienstanwendung mit PowerShell  
 Sie können die Dienstanwendung und den Proxy mithilfe von PowerShell erstellen. Im Beispiel unten wird davon ausgegangen, dass Sie wissen, welchen Anwendungspool Sie für die Dienstanwendung konfigurieren möchten.  
  
1.  Fügen Sie das Anwendungspoolobjekt des Anwendungspoolnamens einer Variablen hinzu, die an die neue Aktion übergeben wird.  
  
    ```  
    $appPoolName = get-spserviceapplicationpool “<application pool name>”  
    ```  
  
2.  Erstellen Sie die Dienstanwendung mit einem von Ihnen angegebenen Namen und Anwendungspool.  
  
    ```  
    New-SPRSServiceApplication –Name ‘MyServiceApplication’ –ApplicationPool $appPoolName –DatabaseName ‘MyServiceApplicationDatabase’ –DatabaseServer ‘<Server Name>’  
    ```  
  
3.  Rufen Sie das neue Dienstanwendungsobjekt ab, und übergeben Sie das Objekt in die Pipe des neuen Proxy-Cmdlets.  
  
    ```  
    Get-SPRSServiceApplication –name MyServiceApplication | New-SPRSServiceApplicationProxy “MyServiceApplicationProxy”  
    ```  
  
##  <a name="bkmk_related"></a> Verwandte Aufgaben  
  
|Task|Link|  
|----------|----------|  
|Verwalten der Einstellungen der Dienstanwendung|[Verwalten einer Reporting Services SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|  
|Führen Sie für die Dienstanwendung (einschließlich zugehöriger Komponenten wie Verschlüsselungsschlüssel und Proxy) eine Sicherung und Wiederherstellung aus.|[Sichern und Wiederherstellen von Reporting Services SharePoint-Dienstanwendungen](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  
  
  
