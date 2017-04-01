---
title: "Berichte, Berichtsteile und Berichtsdefinitionen (Berichts-Generator und SSRS) | Microsoft Docs"
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
  - "Berichtsdefinitionen"
  - "Berichte"
ms.assetid: 2d746550-f8cc-4e97-8a06-d0f03cffc18d
caps.latest.revision: 26
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 26
---
# Berichte, Berichtsteile und Berichtsdefinitionen (Berichts-Generator und SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet eine Vielzahl von Begriffen, mit denen die verschiedenen Zustände eines paginierten Berichts beschrieben werden, darunter Anfangsdefinition, veröffentlichter Bericht und angezeigter Bericht, wie der Benutzer ihn sieht.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## RDL-Dateien (Berichtsdefinitionsdateien)  
 Bei einer Berichtsdefinition handelt es sich um eine Datei, die Sie in Berichts-Generator oder in Berichts-Designer erstellen. Sie enthält eine vollständige Beschreibung der Datenquellenverbindungen, Abfragen zum Abrufen von Daten, Ausdrücken, Parametern, Bildern, Textfeldern, Tabellen und der übrigen Entwurfszeitelemente, die in einem Bericht enthalten sein können. Obwohl eine Berichtsdefinition komplex sein kann, enthält sie mindestens eine Abfrage sowie andere Berichtsinhalte, Berichtseigenschaften und ein Berichtslayout.  
  
 Berichtsdefinitionen werden zur Laufzeit als verarbeiteter Bericht gerendert. Zur Laufzeit werden die Daten aus der Datenquelle abgerufen und entsprechend den Anweisungen in der Berichtsdefinition formatiert. Eine Berichtsdefinition kann direkt aus Ihrem Computer ausgeführt und lokal gespeichert werden. Sie kann auch auf einem Berichtsserver veröffentlicht werden, damit andere Benutzer sie ebenfalls ausführen können.  
  
 Berichtsdefinitionen werden in einem XML-Format geschrieben, das einer XML-Grammatik entspricht, der so genannten Berichtsdefinitionssprache (RDL, Report Definition Language). RDL beschreibt die XML-Elemente, die sämtliche möglichen Varianten eines Berichts umfassen.  
  
## Clientberichtsdefinitions-Dateien (RDLC)  
 Der Visual Studio-Berichts-Designer erzeugt Clientberichtsdefinitionsdateien (Dateierweiterung .rdlc) zur Verwendung mit dem ReportViewer-Steuerelement. Die RDLC-Dateien können zur Verwendung mit Reporting Services-Berichts-Designer in RDL-Dateien konvertiert werden.  
  
## Berichtsteildateien (.rsc)  
 Berichtsteile sind eigenständige Berichtselemente, die auf dem Berichtsserver gespeichert werden und in andere Berichte eingeschlossen werden können. Verwenden Sie den Berichts-Generator, um Teile im Berichtsteilkatalog zu durchsuchen und auszuwählen, die den Berichten hinzugefügt werden sollen. Speichern Sie Berichtsteile mithilfe des Berichts-Designers oder Berichts-Generators, damit sie im Berichtsteilkatalog verwendet werden können.  
  
 Eine Berichtsteildefinition ist ein XML-Fragment einer Berichtsdefinitionsdatei. Sie erstellen Berichtsteile, indem Sie eine Berichtsdefinition erstellen und dann Berichtselemente im Bericht auswählen, die als Berichtsteile getrennt veröffentlicht werden sollen. Berichtsteile umfassen Datenbereiche, Rechtecke und enthaltene Elemente sowie Bilder. Sie können einen Berichtsteil mit seinen abhängigen Datasets und freigegebenen Datenquellenverweisen speichern, damit er in anderen Berichten wiederverwendet werden kann.  
  
 Weitere Informationen finden Sie unter [Berichtsteile &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md) und [Berichtsteile im Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md).  
  
## Veröffentlichte Berichte  
 Nachdem Sie eine RDL-Datei erstellt haben, können Sie sie lokal oder in einem persönlichen Ordner (wie dem Ordner Meine Berichte) auf dem Berichtsserver speichern. Wenn der Bericht zur Anzeige durch andere Benutzer bereit ist, können Sie ihn veröffentlichen, indem Sie ihn aus dem Berichts-Generator in einem öffentlichen Ordner auf dem Berichtsserver speichern, über das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Webportal hochladen oder eine Berichtsprojektmappe aus Berichts-Designer bereitstellen. Ein veröffentlichter Bericht ist ein Element, das in einer Berichtsserver-Datenbank gespeichert und auf einem Berichtsserver oder einer SharePoint-Website verwaltet wird.  
  
 Ein veröffentlichter Bericht wird über Rollenzuweisungen gesichert, die das rollenbasierte Sicherheitsmodell von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwenden. Der Zugriff auf veröffentlichte Berichte erfolgt über URLs, SharePoint-Webparts oder das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Webportal. Sie können auch zu den Berichten navigieren und sie im Berichts-Generator öffnen.  
  
### Berichtsmomentaufnahmen  
 Ein Bericht kann auch als Momentaufnahme veröffentlicht werden, die sowohl Layoutinformationen als auch die Daten der ersten Berichtsausführung enthält. Berichtsmomentaufnahmen werden in keinem speziellen Renderingformat gespeichert. Stattdessen werden Berichtsmomentaufnahmen erst dann in einem endgültigen Anzeigeformat (wie HTML) gerendert, wenn sie von einem Benutzer oder einer Anwendung angefordert werden. Weitere Informationen finden Sie unter [Suchen und Anzeigen von Berichten in Berichts-Manager &#40;Berichts-Generator und SSRS&#41;](https://msdn.microsoft.com/library/dd255286.aspx).  
  
## Gerenderte Berichte  
 Ein gerenderter Bericht ist ein vollständig verarbeiteter Bericht, der sowohl Daten als auch Layoutinformationen in einem anzeigbaren Format (beispielsweise HTML) enthält. Ein Bericht kann erst dann angezeigt werden, nachdem er in ein Ausgabeformat gerendert wurde. Führen Sie zum Rendern von Berichten einen der folgenden Schritte durch:  
  
-   Erstellen oder öffnen Sie einen Bericht in Berichts-Generator oder Berichts-Designer, und führen Sie ihn aus.  
  
-   Suchen Sie einen Bericht im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Webportal, und führen Sie ihn aus.  
  
-   Suchen Sie auf einer in einen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver integrierten SharePoint-Website nach einem Bericht, und führen Sie ihn aus.  
  
-   Abonnieren Sie einen Bericht, der in einem von Ihnen angegebenen Ausgabeformat an einen E-Mail-Posteingang oder eine Dateifreigabe übermittelt wird.  
  
 Abonnieren Sie einen Bericht, der in einem von Ihnen angegebenen Ausgabeformat an einen E-Mail-Posteingang oder eine Dateifreigabe übermittelt wird. Das Standardrenderingformat für einen Bericht ist HTML 4.0. Außer in HTML können Berichte in einer Vielzahl von Dateiformaten gerendert werden, z. B. Excel, Word, XML, PDF, TIFF und CSV. Wie veröffentlichte Berichte können auch gerenderte Berichte nicht bearbeitet oder wieder auf einem Berichtsserver gespeichert werden. Weitere Informationen finden Sie unter [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
## Siehe auch  
 [Berichtserstellungskonzepte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Berichts-Generator in SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Suchen, Anzeigen und Verwalten von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  