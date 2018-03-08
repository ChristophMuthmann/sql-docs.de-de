---
title: Hochladen von Dateien in einen Ordner | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
- files [Reporting Services]
- folders [Reporting Services], uploading files to
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
caps.latest.revision: "42"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4d095fa72856edf7d28f067620940fcafe824d6d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="upload-files-to-a-folder"></a>Hochladen von Dateien in einen Ordner
  Sie können Dateien vom Dateisystem hochladen und in einer Berichtsserver-Datenbank als verwaltete Elemente speichern. Vom Dateityp hängt es ab, was beim Hochladen einer Datei passiert.  
  
-   Das Hochladen einer RDL-Datei entspricht dem Veröffentlichen eines Berichts.  
  
-   Beim Hochladen anderer Dateien werden diese als einzelne binäre Objekte der Berichtsserver-Datenbank hinzugefügt. Diese Dateien werden auf einem Berichtsserver als Ressource veröffentlicht. Ressourcen können einen beliebigen Dateityp aufweisen. Falls die Dateierweiterung einem bekannten MIME-Typ entspricht, wird ein Symbol für diesen MIME-Typ zur Identifizierung des Ressourcentyps verwendet. Andernfalls wird ein allgemeines Dateisymbol zum Anzeigen einer Ressource verwendet.  
  
> [!NOTE]  
>  Sie können eine RDS-Datei (report data source, Berichtsdatenquelle) nicht hochladen, um eine freigegebene Datenquelle zu erstellen. Eine RDS-Datei wird nur im Berichts-Designer verwendet. Die Datei kann den Inhalt für ein freigegebenes Datenquellenelement, das Sie mithilfe des Berichts-Managers definieren und verwalten, nicht bereitstellen. Als Alternative zum Hochladen können Sie ein Skript schreiben, das eine freigegebene, auf einer RDS-Datei basierende Datenquelle erstellt.  
  
 Die maximale Dateigröße für hochgeladene Elemente wird von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]bestimmt. Standardmäßig beträgt die maximale Dateigröße 4 Megabyte (MB).  
  
 Dateien, die Sie in eine Berichtsserver-Datenbank hochladen, werden in der Ordnerhierarchie anhand der folgenden Symbole dargestellt.  
  
 ![Berichtsymbol](../../reporting-services/report-server/media/hlp-16doc.gif "Report icon")  
Berichtssymbol  
  
 ![Modellsymbol](../../reporting-services/report-server/media/model-icon.gif "Model icon")  
Berichtsmodellsymbol  
  
 ![Symbol allgemeine Ressource](../../reporting-services/report-server/media/hlp-16file.gif "generic resource icon")  
allgemeines Ressourcensymbol  
  
 Beim Hochladen einer Datei wird diese stets im aktuell ausgewählten Ordner gespeichert. Sie können zu dem Ordner navigieren, in dem das Element zuerst gespeichert werden soll. Oder Sie laden eine Datei hoch und verschieben diese dann später an den endgültigen Speicherort.  
  
 Laden Sie Dateien mit dem Berichts-Manager hoch. Ob Sie Dateien auf einen Berichtsserver hochladen können, hängt von den Tasks ab, die zu der Rollenzuweisung gehören. Falls Sie die Standardsicherheit verwenden, können lokale Administratoren Elemente zu einem Berichtsserver hinzufügen. Wenn Meine Berichte aktiviert ist, hat jeder Benutzer, der über einen Ordner Meine Berichte verfügt, die Berechtigung, Elemente in diesen Ordner hochzuladen. Wenn Sie benutzerdefinierte Rollenzuweisungen verwenden, muss die Rollenzuweisung Aufgaben für die Ordnerverwaltung enthalten.  
  
|Zweck|Einzubindende Aufgaben|  
|----------------|-------------------------|  
|Eine RDL-Datei in einen Ordner hochladen|Berichte verwalten|  
|Eine beliebige Datei als binäres Objekt hochladen|Ressourcen verwalten|  
|Die Inhalte eines Ordners anzeigen|Ressourcen anzeigen, Berichte anzeigen|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Aufgaben und Berechtigungen](../../reporting-services/security/tasks-and-permissions.md)   
 [Hochladen einer Datei oder eines Berichts (Berichts-Manager)](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)  
  
  
