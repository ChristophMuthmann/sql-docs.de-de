---
title: "Hochladen von Dokumenten in eine SharePoint-Bibliothek (Reporting Services im SharePoint-Modus) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SharePoint-Integration [Reporting Services], Anzeigen von Berichten"
  - "SharePoint-Integration [Reporting Services], Content Management"
  - "Hochladen von Berichten [Reporting Services]"
ms.assetid: 93bd1b19-061b-409f-8dc2-ec416b2f4b39
caps.latest.revision: 11
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 11
---
# Hochladen von Dokumenten in eine SharePoint-Bibliothek (Reporting Services im SharePoint-Modus)
  Sie können Berichtsdefinitionen und Berichtsmodelle in eine SharePoint-Bibliothek hochladen. Beim Hochladen eines Berichtsserverelements müssen Sie eine Bibliothek oder einen Ordner innerhalb der Bibliothek auswählen. Sie können ein Berichtsserverelement nicht in eine Liste oder auf eine Seite hochladen.  
  
 Sie können keine Datenquellendatei (.rds) hochladen. Sie können RDS-Dateien jedoch aus einem Designtool wie dem Berichts-Designer in eine SharePoint-Bibliothek hochladen. Während der Veröffentlichung wird aus der ursprünglichen RDS-Datei im Projekt eine neue RSDS-Datei erstellt. Sie können auch eine neue RSDS-Datei in einer SharePoint-Bibliothek erstellen und Datenquellen-Verbindungseigenschaften in den hochgeladenen Berichten und Modellen festlegen, um die neue Verbindung zu verwenden.  
  
> [!NOTE]  
>  Der Berichtsserver muss für den SharePoint-Modus konfiguriert sein, und die Instanz des SharePoint-Produkts muss über das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-In verfügen, das Programmdateien zum Speichern und Aufrufen von Berichtsserverelementen über eine SharePoint-Website bereitstellt.  
  
 Sie müssen auf der Websiteebene über die Berechtigung zum Hinzufügen von Elementen verfügen, um ein Dokument in eine Bibliothek hochzuladen. Wenn Sie Standardsicherheitseinstellungen verwenden, wird diese Berechtigung Mitgliedern der Gruppe **Besitzer** erteilt, die über Berechtigungen für den Vollzugriff verfügen, und der Gruppe **Mitglieder** , die über Berechtigungen vom Typ Teilnahme verfügen.  
  
### So fügen Sie einer Bibliothek eine Berichtsdefinition oder ein Berichtsmodell hinzu  
  
1.  Öffnen Sie die Bibliothek oder einen Ordner innerhalb einer Bibliothek. Wenn die Bibliothek nicht bereits geöffnet ist, klicken Sie auf ihren Namen auf der Schnellstartleiste. Wenn der Name der Bibliothek nicht angezeigt wird, klicken Sie auf **Alle Websiteinhalte einblenden**und anschließend auf den Namen der Bibliothek.  
  
2.  Klicken Sie im Menü **Upload** auf **Dokumentupload**.  
  
3.  Wählen Sie eine Berichtsdefinition (RDL-Datei) oder ein Berichtsmodell (SMDL-Datei) aus, und klicken Sie anschließend auf **OK**, um einen einzelnen Bericht oder eine einzelne Berichtsmodelldatei hochzuladen.  
  
     Wenn für die Berichtsdefinition eine freigegebene Datenquelldatei (RSDS-Datei) verwendet wird, um Verbindungsinformationen für eine externe Datenquelle zu speichern, können Sie die RDL- und die RSDS-Dateien gleichzeitig hochladen. Klicken Sie dazu auf **Mehrere Dokumente hochladen**, geben Sie beide Dateien an, und klicken Sie anschließend auf **OK**.  
  
 Wenn Sie einen Bericht hochladen, der Verweise auf freigegebene Datenquellen, Berichtsmodelle oder Unterberichte enthält, werden die Verweise im Bericht zerstört, wenn die Dateien hochgeladen werden. Weitere Informationen zum Zurücksetzen der Verweise finden Sie unter [Erstellen und Verwalten von freigegebenen Datenquellen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md).  
  
 Wenn Sie einen Bericht hochladen, wird er bei Bedarf während des Öffnens ausgeführt. Gleichzeitig werden Livedaten aus der Datenquelle abgerufen. Sie können den Bericht so konfigurieren, dass Daten nach einem Zeitplan abgerufen werden oder dass zwischengespeicherte Daten verwendet werden. Weitere Informationen finden Sie unter [Festlegen von Verarbeitungsoptionen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
 Ein Bericht kann Parameter enthalten, sodass die Benutzer Daten filtern können. Sie können die Parameter so konfigurieren, dass bestimmte Werte verwendet werden. Zudem können Sie die Art der Darstellung der Parameter für die Benutzer ändern. Weitere Informationen finden Sie unter [Festlegen von Parametern für einen veröffentlichten Bericht &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-design/set parameters on a published report - sharepoint integrated mode.md).  
  
## Siehe auch  
 [Veröffentlichen eines Berichts in einer SharePoint-Bibliothek](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Veröffentlichen einer freigegebenen Datenquelle in einer SharePoint-Bibliothek](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  