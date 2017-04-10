---
title: "Verwenden von &quot;Meine Abonnements&quot; (Berichtsserver im einheitlichen Modus) | Microsoft Docs"
ms.custom: ""
ms.date: "07/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Abonnements [Reporting Services], Seite "Meine Abonnements""
  - "Meine Abonnements (Seite) [Reporting Services]"
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
caps.latest.revision: 40
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 38
---
# Verwenden von &quot;Meine Abonnements&quot; (Berichtsserver im einheitlichen Modus)
Das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Webportal enthält die Seite **Meine Abonnements**, auf der alle Ihre Abonnements zentral aufgelistet werden. Mithilfe von *Meine Abonnements* können Sie vorhandene Abonnements anzeigen, ändern und löschen. Abonnements können damit jedoch nicht erstellt werden.  Meine Abonnements zeigt nur die von Ihnen erstellten Abonnements. Abonnements anderer Benutzer werden nicht angezeigt, selbst wenn Sie als Abonnent zu diesen Abonnements hinzugefügt werden, und es werden auch keine datengesteuerten Abonnements angezeigt.
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus|  
  
Das Suchfeld filtert die Liste der Abonnements dynamisch. Sie können nicht basierend auf Besitzernamen, Triggerinformationen, Statusinformationen usw. nach Abonnements suchen. Weitere Informationen finden Sie unter [Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).
  
## So öffnen Sie die Seite 'Meine Abonnements'  
1. Öffnen Sie das [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]-Webportal.
2. Klicken Sie auf „Einstellungen“. ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) auf der Symbolleiste.
3. Klicken Sie auf **Meine Abonnements**.

Weitere Informationen finden Sie unter [Reporting Services-Webportal](../../reporting-services/web-portal-ssrs-native-mode.md).

## Verwenden von Windows PowerShell zum Auflisten von MySubscriptions  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.png "PowerShell-Inhalt")  
  
 Mit dem folgenden PowerShell-Skript wird die Liste der Abonnements und Abonnementeigenschaften für den aktuellen Benutzer zurückgegeben. Weitere Informationen finden Sie unter [ReportingService2010.ListMySubscriptions-Methode](http://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx).  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions

```  
  
## Siehe auch  
 [Datengesteuerte Abonnements](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Abonnements und Übermittlung &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Alt_Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus](http://msdn.microsoft.com/de-de/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)  
  
  