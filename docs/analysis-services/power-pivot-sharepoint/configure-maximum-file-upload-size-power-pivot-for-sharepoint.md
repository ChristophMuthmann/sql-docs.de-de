---
title: Konfigurieren der maximalen Dateiuploadgröße (PowerPivot für SharePoint) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 44317542648286c36116c200e35534e536e331d1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-maximum-file-upload-size-power-pivot-for-sharepoint"></a>Konfigurieren der maximalen Dateiuploadgröße (PowerPivot für SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen enthalten oft große Datenmengen, was dazu führt, dass Dateien die maximal für SharePoint-Uploads zulässige Dateigröße überschreiten. Wenn Sie versuchen, eine Datei hochzuladen, die die Obergrenze überschreitet, wird die folgende Fehlermeldung in SharePoint angezeigt:  
  
-   „Die angegebene Datei ist größer als die maximal unterstützte Dateigröße.“  
  
 Um die Dateigröße zu erhöhen, legen Sie zunächst die Maximale Arbeitsmappengröße für Excel Services auf 50 MB fest. Dadurch werden die Grenzwerte für die maximale Dateigröße für Excel auf die der SharePoint-Webanwendungen festgelegt (standardmäßig 50 MB für SharePoint 2010 und 200 MB für SharePoint 2013). Wenn Dateien 50 MB überschreiten, erhöhen Sie die Dateigrößenbeschränkungen sowohl für Excel Services als auch für die Webanwendung.  
  
 Sie müssen SharePoint-Administrator sein, um die maximale Größe für Dateiuploads zu ändern.  
  
### <a name="configure-maximum-file-size-for-excel-services"></a>Konfigurieren der maximalen Dateigröße für Excel Services  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf den Namen der Excel Services-Anwendung.  
  
3.  Klicken Sie auf **Vertrauenswürdige Dateispeicherorte**.  
  
4.  Klicken Sie auf den Speicherort, um die Eigenschaften zu bearbeiten. Die Standardwebanwendung wird von Excel Services standardmäßig als vertrauenswürdige Website betrachtet. Wenn Sie die Standardwebanwendung verwenden, klicken Sie auf **http://** , um die Konfigurationsseite für diesen Speicherort zu öffnen.  
  
5.  Führen Sie einen Bildlauf zu **Arbeitsmappeneigenschaften**durch.  
  
6.  Erhöhen Sie die Dateigröße in Maximale Arbeitsmappengröße von 10 (Standardwert) auf 50 oder einen höheren Wert, der für Ihre Arbeitsdateien geeignet ist.  
  
     Die maximale Dateiuploadgröße für SharePoint-Webanwendungen beträgt standardmäßig 50 MB. Wenn Sie Maximale Arbeitsmappengröße auf einen Wert über 50 MB festlegen, führen Sie die Schritte im folgenden Verfahren aus, um Maximale Uploadgröße für die SharePoint-Webanwendung auf den gleichen Wert festzulegen.  
  
     Der maximale Wert, den Sie angeben können, beträgt 2 Gigabytes (bzw. 2.047 Megabytes wie in der Zentraladministration angegeben).  
  
7.  Klicken Sie auf **OK**.  
  
### <a name="configure-maximum-file-size-for-a-sharepoint-web-application"></a>Konfigurieren der maximalen Dateigröße für eine SharePoint-Webanwendung  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Webanwendungen verwalten**.  
  
    > [!NOTE]  
    >  Führen Sie die folgenden Schritte nur dann aus, wenn Sie die Maximale Arbeitsmappengröße in Excel Services hochgesetzt haben.  
  
2.  Wählen Sie die Anwendung (z.B. **SharePoint - 80**) aus.  
  
3.  Klicken Sie im Menüband Webanwendungen auf der Schaltfläche Allgemeine Einstellungen auf den Pfeil nach unten.  
  
4.  Klicken Sie auf **Allgemeine Einstellungen**.  
  
5.  Führen Sie einen Bildlauf zu **Maximale Uploadgröße**durch.  
  
6.  Legen Sie die Eigenschaft auf den unter Maximale Arbeitsmappengröße in Excel Services angegebenen oder einen höheren Wert fest.  
  
7.  Klicken Sie auf **OK**.  
  
  
