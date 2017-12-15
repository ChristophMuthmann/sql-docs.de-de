---
title: "Einstellungen der SharePoint-Website für den Berichts-Viewer-Webpart | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: jt000
ms.author: jasontre
ms.workload: Inactive
ms.openlocfilehash: 0be12b3f74dd2cf4e6d07d3ccc70208d5bd099b8
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="sharepoint-site-settings-for-the-report-viewer-web-part"></a>Einstellungen der SharePoint-Website für den Berichts-Viewer-Webpart

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Der Berichts-Viewer-Webpart weist einige Einstellungen auf, die konfiguriert werden können. Diese Einstellungen können auf der SharePoint-Websiteeinstellungenseite durch einen Websiteadministrator aktiviert und deaktiviert werden. Beachten Sie, dass jede Website eigene Einstellungen aufweist. Darüber hinaus werden diese Einstellungen nach der Neuinstallation des Berichts-Viewer-Webparts nicht zurückgesetzt.

## <a name="accessing-the-site-settings-page"></a>Zugreifen auf die Websiteeinstellungenseite

So können Sie auf die Websiteeinstellungen zugreifen:

1. Wählen Sie auf Ihrer SharePoint-Website das **Zahnradsymbol** in der oberen linken Ecke und anschließend **Websiteeinstellungen** aus.

    ![Websiteeinstellungen über das Zahnradsymbol.](media/sharepoint-site-settings.png)

2. Klicken auf **Einstellungen für Berichts-Viewer-Webpart** in der Websiteeinstellungengruppe **Reporting Services**.

    > [!NOTE]
    > Die Websiteeinstellungen können Sie auch durch direktes Navigieren zu `<site>/_layouts/15/ReportViewerWebPart/ReportViewerWebPartSettings.aspx` erreichen.

## <a name="report-viewer-web-part-settings"></a>Berichts-Viewer-Webparteinstellungen

|Einstellung|Kommentare|  
|-------------|--------------|  
|Nutzungsdaten sammeln|Ermöglicht das Senden von Fehler- und Nutzungsinformationen an Microsoft, um eine Verbesserung der Produkte zu ermöglichen. Die Microsoft-Richtlinie für die Fehlerbericht-Datensammlung finden Sie in den [Microsoft SQL Server-Datenschutzbestimmungen](https://go.microsoft.com/fwlink/?linkid=860782&clcid=0x409).|  
|Barrierefreiheit-Metadaten für Berichte aktivieren|Legt die [`AccessibleTablix`-Geräteinfo](../html-device-information-settings.md) für gerenderte Berichte fest.| 
