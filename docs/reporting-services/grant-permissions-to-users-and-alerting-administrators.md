---
title: "Erteilen von Berechtigungen für Benutzer und Warnungsadministratoren | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
caps.latest.revision: "11"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9a4aa4f2ce4b9b69035fe45642a8247794f1e395
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>Gewähren von Berechtigungen an Benutzer und Warnungsadministratoren

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Bevor Benutzer und Warnungsadministratoren Datenwarnungen erstellen, bearbeiten, löschen und anzeigen können, muss ihnen SharePoint-Berechtigungen gewährt werden. Es gibt keine speziellen Berechtigungen für die Verwendung mit der [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Datenwarnungsfunktion. Verwenden Sie die integrierten SharePoint-Berechtigungen.

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

**Information Worker**– Berechtigungen müssen die SharePoint-Berechtigungen "Warnung erstellen" und "Elemente anzeigen" beinhalten. Die integrierten SharePoint-Berechtigungensebenen namens Entwerfen, Mitwirken, Lesen und Nur anzeigen enthalten die SharePoint-Berechtigungen "Warnung erstellen" und "Elemente anzeigen". Sie können auch eine benutzerdefinierte Berechtigungsebene mit den erforderlichen Berechtigungen erstellen, um Benutzer zu unterstützen, die Datenwarnungen erstellen, bearbeiten, ausführen und anzeigen.

**Warnungsadministratoren**– Berechtigungen müssen die SharePoint-Berechtigung "Warnung verwalten" einschließen. Standardmäßig schließt nur die Berechtigungsstufe "Vollzugriff" diese Berechtigung für mit der Websitevorlage der Teamwebsite erstellte Websites ein. Wenn Sie andere Websitevorlagen verwenden, sehen Sie andere Listen mit Standard-SharePoint-Gruppen. Sie können einer der integrierten Berechtigungsebenen die Berechtigung "Warnung verwalten" hinzufügen oder eine benutzerdefinierte Berechtigungsebene mit der erforderlichen Berechtigung erstellen, um Warnungsadministratoren zu unterstützen, die Datenwarnungen anzeigen und löschen.

Weitere Informationen zu SharePoint-Berechtigungen finden Sie im Thema zu [Benutzerberechtigungen und Berechtigungsstufen (SharePoint Server 2010)](http://technet.microsoft.com/library/cc721640.aspx).

## <a name="grant-permissions"></a>Berechtigungen erteilen
  
1.  Wechseln Sie zu der SharePoint-Website, der Sie Berechtigungen erteilen möchten.  
  
2.  Klicken Sie auf der Symbolleiste auf **Websiteaktionen** und dann auf **Websiteberechtigungen**.  
  
     Wenn diese Option nicht angezeigt wird, haben Sie keine ausreichende Berechtigung, um anderen Berechtigungen zu erteilen.  
  
3.  Klicken Sie auf **Berechtigungen erteilen**.  
  
4.  Geben Sie unter **Benutzer/Gruppen**die Benutzernamen, Gruppennamen oder E-Mail-Adressen ein, denen Sie Berechtigungen erteilen möchten.  
  
5.  Aktivieren Sie die Option **Benutzer einer SharePoint-Gruppe hinzufügen** oder **Benutzern eine Berechtigung direkt erteilen** . Abhängig davon, ob Sie **Benutzer einer SharePoint-Gruppe hinzufügen** oder **Benutzern eine Berechtigung direkt erteilen** ausgewählt haben, gehen Sie wie folgt vor:  
  
    -   Wenn Sie **Benutzer einer SharePoint-Gruppe hinzufügen**ausgewählt haben, wählen Sie in der Dropdownliste eine Berechtigungsebene aus.  
  
    -   Wenn Sie **Benutzern eine Berechtigung direkt erteilen**ausgewählt haben, wählen Sie eine Berechtigungsebene aus.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

## <a name="see-also"></a>Weitere Informationen finden Sie unter

[Festlegen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
[Reporting Services-Datenwarnungen](../reporting-services/reporting-services-data-alerts.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
