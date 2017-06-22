---
title: "Exportieren von Berichten über URL-Zugriff | Microsoft Docs"
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d9ee4dd3c00d9e250fd3c773a917ad3cf90f84c4
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="export-a-report-using-url-access"></a>Exportieren von Berichten über URL-Zugriff
  Sie können mit dem *rs:Format* -URL-Parameter optional das Format angeben, in dem ein Bericht gerendert werden soll.  Die Formate HTML4.0 und HTM5 (Renderingerweiterung) werden im Browser und für andere Formate gerendert, der Browser fordert zum Speichern der Berichtsausgabe in einer lokalen Datei auf.  
  
 Um beispielsweise von einem im einheitlichen Modus ausgeführten Berichtsserver direkt eine PDF-Kopie eines Berichts abzurufen, geben Sie Folgendes an:  
  
```  
http://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  
  
 Zum Abrufen von einem Berichtsserver im integrierten SharePoint-Modus geben Sie Folgendes an:  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
  
 Beispielsweise exportiert der folgende URL-Befehl in Ihrem Browser einen PPTX-Bericht von einer benannten Instanz des Berichtsservers:  
  
```  
http://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 Gültige Werte für diesen Parameter sind von den Berichtrenderingerweiterungen abhängig, die auf dem Berichtsserver installiert sind, auf den zugegriffen wird. Häufig verwendete Erweiterungen sind HTML4.0, MHTML, IMAGE, EXCELOPENXML (XLSX), WORDOPENXML (DOCX), CSV, PDF, XML und NULL. Wenn eine bestimmte Renderingerweiterung nicht auf dem Berichtsserver installiert ist, wird der Bericht nicht gerendert. Es wird ein Fehler generiert und im Browser angezeigt.  
  
 Wenn Sie den *Format* -Parameter nicht als Teil der URL aufnehmen, erkennt der Berichtsserver den Browser und rendert den Bericht im entsprechenden HTML-Format.  
  
## <a name="see-also"></a>Siehe auch  
 [URL-Zugriff &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL-Zugriffsparameterverweis](../reporting-services/url-access-parameter-reference.md)  
  
  
