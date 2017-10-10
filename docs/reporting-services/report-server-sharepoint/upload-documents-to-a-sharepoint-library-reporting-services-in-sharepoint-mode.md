---
title: Hochladen von Dokumenten in einer SharePoint-Bibliothek (Reporting Services im SharePoint-Modus) | Microsoft Docs
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: d938f068ecf2d0c2a2b920fda9f7c414649f069d
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode"></a>Hochladen von Dokumenten in einer SharePoint-Bibliothek (Reporting Services im SharePoint-Modus)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Sie können Berichtsdefinitionen und Berichtsmodelle in eine SharePoint-Bibliothek hochladen. Beim Hochladen eines Berichtsserverelements müssen Sie eine Bibliothek oder einen Ordner innerhalb der Bibliothek auswählen. Sie können ein Berichtsserverelement nicht in eine Liste oder auf eine Seite hochladen.  

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

 Sie können keine Datenquellendatei (.rds) hochladen. Sie können RDS-Dateien jedoch aus einem Designtool wie dem Berichts-Designer in eine SharePoint-Bibliothek hochladen. Während der Veröffentlichung wird aus der ursprünglichen RDS-Datei im Projekt eine neue RSDS-Datei erstellt. Sie können auch eine neue RSDS-Datei in einer SharePoint-Bibliothek erstellen und Datenquellen-Verbindungseigenschaften in den hochgeladenen Berichten und Modellen festlegen, um die neue Verbindung zu verwenden.  
  
> [!NOTE]  
>  Der Berichtsserver muss für den SharePoint-Modus konfiguriert werden, und die Instanz des SharePoint-Produkts müssen das Reporting Services-Add-in, das Programmdateien zum Speichern und Zugreifen auf berichtsserverelemente aus einer SharePoint-Website bereitstellt.  
  
 Sie müssen auf der Websiteebene über die Berechtigung zum Hinzufügen von Elementen verfügen, um ein Dokument in eine Bibliothek hochzuladen. Wenn Sie Standardsicherheitseinstellungen verwenden, wird diese Berechtigung Mitgliedern der Gruppe **Besitzer** erteilt, die über Berechtigungen für den Vollzugriff verfügen, und der Gruppe **Mitglieder** , die über Berechtigungen vom Typ Teilnahme verfügen.  
  
## <a name="add-a-report-definition-or-report-model-to-a-library"></a>Eine Berichtsdefinition oder ein Berichtsmodell in einer Bibliothek hinzufügen
  
1.  Öffnen Sie die Bibliothek oder einen Ordner innerhalb einer Bibliothek. Wenn die Bibliothek nicht bereits geöffnet ist, klicken Sie auf ihren Namen auf der Schnellstartleiste. Wenn der Name der Bibliothek nicht angezeigt wird, klicken Sie auf **Alle Websiteinhalte einblenden**und anschließend auf den Namen der Bibliothek.  
  
2.  Klicken Sie im Menü **Upload** auf **Dokumentupload**.  
  
3.  Wählen Sie eine Berichtsdefinition (RDL-Datei) oder ein Berichtsmodell (SMDL-Datei) aus, und klicken Sie anschließend auf **OK**, um einen einzelnen Bericht oder eine einzelne Berichtsmodelldatei hochzuladen.  
  
     Wenn für die Berichtsdefinition eine freigegebene Datenquelldatei (RSDS-Datei) verwendet wird, um Verbindungsinformationen für eine externe Datenquelle zu speichern, können Sie die RDL- und die RSDS-Dateien gleichzeitig hochladen. Klicken Sie dazu auf **Mehrere Dokumente hochladen**, geben Sie beide Dateien an, und klicken Sie anschließend auf **OK**.  
  
 Wenn Sie einen Bericht hochladen, der Verweise auf freigegebene Datenquellen, Berichtsmodelle oder Unterberichte enthält, werden die Verweise im Bericht zerstört, wenn die Dateien hochgeladen werden. Weitere Informationen zum Zurücksetzen der Verweise finden Sie unter [erstellen und verwalten freigegebene Datenquellen &#40; Reporting Services in SharePoint integrierten Modus &#41; ](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 Wenn Sie einen Bericht hochladen, wird er bei Bedarf während des Öffnens ausgeführt. Gleichzeitig werden Livedaten aus der Datenquelle abgerufen. Sie können den Bericht so konfigurieren, dass Daten nach einem Zeitplan abgerufen werden oder dass zwischengespeicherte Daten verwendet werden. Weitere Informationen finden Sie unter [Verarbeitungsoptionen festgelegt &#40; Reporting Services in SharePoint integrierten Modus &#41; ](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
 Ein Bericht kann Parameter enthalten, sodass die Benutzer Daten filtern können. Sie können die Parameter so konfigurieren, dass bestimmte Werte verwendet werden. Zudem können Sie die Art der Darstellung der Parameter für die Benutzer ändern. Weitere Informationen finden Sie unter [legen Sie Parameter für einen publizierten Bericht &#40; Reporting Services in SharePoint integrierten Modus &#41; ](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Siehe auch

 [Veröffentlichen eines Berichts in einer SharePoint-Bibliothek](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Veröffentlichen Sie eine freigegebene Datenquelle in einer SharePoint-Bibliothek](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Granting Permissions on Report Server Items on a SharePoint Site (Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website)](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
