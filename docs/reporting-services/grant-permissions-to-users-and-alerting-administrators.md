---
title: "Erteilen von Berechtigungen für Benutzer und Warnungsadministratoren | Microsoft Docs"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 91700c92ed7f96e00ba05d7ee9ca96590d0a4837
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>Gewähren von Berechtigungen an Benutzer und Warnungsadministratoren

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Bevor Benutzer und Warnungsadministratoren Datenwarnungen erstellen, bearbeiten, löschen und anzeigen können, muss ihnen SharePoint-Berechtigungen gewährt werden. Es gibt keine speziellen Berechtigungen für die Verwendung mit der [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Datenwarnungsfunktion. Verwenden Sie die integrierten SharePoint-Berechtigungen.

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

**Information Worker**– Berechtigungen müssen die SharePoint-Berechtigungen "Warnung erstellen" und "Elemente anzeigen" beinhalten. Die integrierten SharePoint-Berechtigungensebenen namens Entwerfen, Mitwirken, Lesen und Nur anzeigen enthalten die SharePoint-Berechtigungen "Warnung erstellen" und "Elemente anzeigen". Sie können auch eine benutzerdefinierte Berechtigungsebene mit den erforderlichen Berechtigungen erstellen, um Benutzer zu unterstützen, die Datenwarnungen erstellen, bearbeiten, ausführen und anzeigen.

**Warnungsadministratoren**– Berechtigungen müssen die SharePoint-Berechtigung "Warnung verwalten" einschließen. Standardmäßig schließt nur die Berechtigungsstufe "Vollzugriff" diese Berechtigung für mit der Websitevorlage der Teamwebsite erstellte Websites ein. Wenn Sie andere Websitevorlagen verwenden, sehen Sie andere Listen mit Standard-SharePoint-Gruppen. Sie können einer der integrierten Berechtigungsebenen die Berechtigung "Warnung verwalten" hinzufügen oder eine benutzerdefinierte Berechtigungsebene mit der erforderlichen Berechtigung erstellen, um Warnungsadministratoren zu unterstützen, die Datenwarnungen anzeigen und löschen.

Weitere Informationen zu SharePoint-Berechtigungen finden Sie im Thema zu [Benutzerberechtigungen und Berechtigungsstufen (SharePoint Server 2010)](http://technet.microsoft.com/library/cc721640.aspx).

## <a name="grant-permissions"></a>Erteilen von Berechtigungen
  
1.  Wechseln Sie zu der SharePoint-Website, der Sie Berechtigungen erteilen möchten.  
  
2.  Klicken Sie auf der Symbolleiste auf **Websiteaktionen** und dann auf **Websiteberechtigungen**.  
  
     Wenn diese Option nicht angezeigt wird, haben Sie keine ausreichende Berechtigung, um anderen Berechtigungen zu erteilen.  
  
3.  Klicken Sie auf **Berechtigungen erteilen**.  
  
4.  Geben Sie unter **Benutzer/Gruppen**die Benutzernamen, Gruppennamen oder E-Mail-Adressen ein, denen Sie Berechtigungen erteilen möchten.  
  
5.  Aktivieren Sie die Option **Benutzer einer SharePoint-Gruppe hinzufügen** oder **Benutzern eine Berechtigung direkt erteilen** . Abhängig davon, ob Sie **Benutzer einer SharePoint-Gruppe hinzufügen** oder **Benutzern eine Berechtigung direkt erteilen** ausgewählt haben, gehen Sie wie folgt vor:  
  
    -   Wenn Sie **Benutzer einer SharePoint-Gruppe hinzufügen**ausgewählt haben, wählen Sie in der Dropdownliste eine Berechtigungsebene aus.  
  
    -   Wenn Sie **Benutzern eine Berechtigung direkt erteilen**ausgewählt haben, wählen Sie eine Berechtigungsebene aus.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

## <a name="see-also"></a>Siehe auch

[Festlegen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
[Reporting Services-Datenwarnungen](../reporting-services/reporting-services-data-alerts.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
