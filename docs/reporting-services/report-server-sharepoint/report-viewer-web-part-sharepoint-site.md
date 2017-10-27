---
title: Berichts-Viewer-Webpart auf einer SharePoint-Website | Microsoft Docs
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a37ed5efe7c365c601deb95d9fe761d227e7021e
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>Berichts-Viewer-Webpart auf einer SharePoint-Website

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Der Berichts-Viewer-Webpart ist ein benutzerdefiniertes Webpart an. Sie können das Webpart verwenden, um anzuzeigen, navigieren, Drucken und Exportieren von Berichten auf einem Berichtsserver innerhalb einer SharePoint-Website. Der Berichts-Viewer-Webpart ist Berichtsdefinitionsdateien (RDL), die von einem Microsoft SQL Server Reporting Services-Berichtsserver verarbeitet werden zugeordnet. 

Die aktuelle Berichts-Viewer-Webpart kann auch paginierte Berichte für Power BI-Berichtsserver bereitgestellt. Das Webpart kann nicht mit Power BI-Berichten verwendet werden.

## <a name="why-the-report-viewer-web-part-is-re-introduced"></a>Warum das Berichts-Viewer-Webpart wieder eingeführt wird.

Der Berichts-Viewer-Webpart gab es als Teil der Reporting Services-Add-in für SharePoint-Produkte. Das Webpart wurde speziell für Berichtsserver im integrierten SharePoint-Modus. Im integrierten SharePoint-Modus wurde nach dem SQL Server 2016 als veraltet markiert.

Beginnend mit SQL Server-2017, besteht nur ein Installationsmodus für Reporting Services: **im einheitlichen Modus**. Sie können alle Berichte-Typen, die mit einer Seiten-Viewer Web Teil mit Einbetten der *Rs: einbetten = "true"* URL-Parameter. Einbetten von Berichten in SharePoint-Seiten ist eine Integration Story angefordert von Kunden und das aktualisierte Berichts-Viewer-Webpart in diesem Szenario für paginierte Berichte kann.

Während das Seiten-Viewer-Webpart zum Einbetten eines paginierten Berichts in einer SharePoint-Seite Suffixe, bietet das aktualisierte Berichts-Viewer-Webpart Zusatzfunktionen.

* Bestimmte Symbolleistenschaltflächen ein-/ausblenden
* Überschreiben Sie Berichtsparameterwerte
* Filter-Webparts zu Berichtsparametern herstellen

## <a name="download-the-report-viewer-web-part-solution-package"></a>Herunterladen des Berichts-Viewer Web Teil-Lösungspakets

Der Berichts-Viewer-Webpart ist im Microsoft Download Center verfügbar.

[Herunterladen von Berichts-Viewer Web Teil-Lösungspaket](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="considerations-and-limitations"></a>Überlegungen und Einschränkungen

Die aufgelisteten Elemente sind spezifisch für das aktualisierte Berichts-Viewer-Webpart.

* Das Webpart kann nur verwendet werden, auf *klassischen* SharePoint-Seiten.
* Nur paginierte Berichte der (Berichtsdefinitionssprache RDL) werden unterstützt, im Berichts-Viewer-Webpart eingebettet. Wenn Sie zum Einbetten von Power BI-Berichten oder mobile-Berichte suchen, können Sie mithilfe der *Rs: einbetten = "true"* URL-Parameter.

## <a name="next-steps"></a>Nächste Schritte

Um mit dem aktualisierten Berichts-Viewer-Webpart beginnen, finden Sie unter [das Berichts-Viewer-Webpart auf einer SharePoint-Website bereitstellen](deploy-report-viewer-web-part.md).

