---
title: "Hochladen von Dateien in einen Ordner | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Veröffentlichen von Berichten [Reporting Services], Hochladen von Dateien"
  - "Berichte [Reporting Services], veröffentlichen"
  - "Hochladen von Berichten [Reporting Services]"
  - "Hochladen von Dateien [Reporting Services]"
  - "Dateien [Reporting Services], hochladen"
  - "Dateien [Reporting Services]"
  - "Ordner [Reporting Services], Hochladen von Dateien in"
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# Hochladen von Dateien in einen Ordner
  Sie können Dateien vom Dateisystem hochladen und in einer Berichtsserver-Datenbank als verwaltete Elemente speichern. Vom Dateityp hängt es ab, was beim Hochladen einer Datei passiert.  
  
-   Das Hochladen einer RDL-Datei entspricht dem Veröffentlichen eines Berichts.  
  
-   Beim Hochladen anderer Dateien werden diese als einzelne binäre Objekte der Berichtsserver-Datenbank hinzugefügt. Diese Dateien werden auf einem Berichtsserver als Ressource veröffentlicht. Ressourcen können einen beliebigen Dateityp aufweisen. Falls die Dateierweiterung einem bekannten MIME-Typ entspricht, wird ein Symbol für diesen MIME-Typ zur Identifizierung des Ressourcentyps verwendet. Andernfalls wird ein allgemeines Dateisymbol zum Anzeigen einer Ressource verwendet.  
  
> [!NOTE]  
>  Sie können eine RDS-Datei (report data source, Berichtsdatenquelle) nicht hochladen, um eine freigegebene Datenquelle zu erstellen. Eine RDS-Datei wird nur im Berichts-Designer verwendet. Die Datei kann den Inhalt für ein freigegebenes Datenquellenelement, das Sie mithilfe des Berichts-Managers definieren und verwalten, nicht bereitstellen. Als Alternative zum Hochladen können Sie ein Skript schreiben, das eine freigegebene, auf einer RDS-Datei basierende Datenquelle erstellt.  
  
 Die maximale Dateigröße für hochgeladene Elemente wird von [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]bestimmt. Standardmäßig beträgt die maximale Dateigröße 4 Megabyte (MB).  
  
 Dateien, die Sie in eine Berichtsserver-Datenbank hochladen, werden in der Ordnerhierarchie anhand der folgenden Symbole dargestellt.  
  
 ![Bericht (Symbol)](../../reporting-services/report-server/media/hlp-16doc.png "Bericht (Symbol)")  
Berichtssymbol  
  
 ![Modell (Symbol)](../../reporting-services/report-server/media/model-icon.png "Modell (Symbol)")  
Berichtsmodellsymbol  
  
 ![allgemeines Ressourcensymbol](../../reporting-services/report-server/media/hlp-16file.png "allgemeines Ressourcensymbol")  
allgemeines Ressourcensymbol  
  
 Beim Hochladen einer Datei wird diese stets im aktuell ausgewählten Ordner gespeichert. Sie können zu dem Ordner navigieren, in dem das Element zuerst gespeichert werden soll. Oder Sie laden eine Datei hoch und verschieben diese dann später an den endgültigen Speicherort.  
  
 Laden Sie Dateien mit dem Berichts-Manager hoch. Ob Sie Dateien auf einen Berichtsserver hochladen können, hängt von den Tasks ab, die zu der Rollenzuweisung gehören. Falls Sie die Standardsicherheit verwenden, können lokale Administratoren Elemente zu einem Berichtsserver hinzufügen. Wenn Meine Berichte aktiviert ist, hat jeder Benutzer, der über einen Ordner Meine Berichte verfügt, die Berechtigung, Elemente in diesen Ordner hochzuladen. Wenn Sie benutzerdefinierte Rollenzuweisungen verwenden, muss die Rollenzuweisung Aufgaben für die Ordnerverwaltung enthalten.  
  
|Zweck|Einzubindende Aufgaben|  
|----------------|-------------------------|  
|Eine RDL-Datei in einen Ordner hochladen|Berichte verwalten|  
|Eine beliebige Datei als binäres Objekt hochladen|Ressourcen verwalten|  
|Die Inhalte eines Ordners anzeigen|Ressourcen anzeigen, Berichte anzeigen|  
  
## Siehe auch  
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Aufgaben und Berechtigungen](../../reporting-services/security/tasks-and-permissions.md)   
 [Hochladen einer Datei oder eines Berichts &#40;Berichts-Manager&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)  
  
  