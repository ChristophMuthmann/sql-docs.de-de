---
title: "Hochladen einer Datei oder eines Berichts (Berichts-Manager) | Microsoft Docs"
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
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# Hochladen einer Datei oder eines Berichts (Berichts-Manager)
  Der Berichts-Manager umfasst eine Uploadfunktion, sodass Sie Berichte, Modelle und andere Dateien zu einem Berichtsserver hinzufügen können, ohne diese Elemente von einer Clientanwendung zu veröffentlichen. Dateien, die Sie über das Dateisystem hochladen, werden als Elemente auf dem Berichtsserver gespeichert. Die Speicherung erfolgt je nach Dateityp:  
  
-   RDL-Dateien werden als Berichte gespeichert.  
  
-   SMDL-Dateien werden als Berichtsmodelle gespeichert.  
  
-   Alle anderen Dateien, einschließlich freigegebener Datenquellendateien (RDS), werden als Ressourcen hochgeladen. Ressourcen werden nicht von einem Berichtsserver verarbeitet, können aber im Berichts-Manager angezeigt werden, wenn der Berichtsserver den MIME-Typ der Datei unterstützt.  
  
### So laden Sie eine Datei oder einen Bericht hoch  
  
1.  Starten Sie [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  Navigieren Sie im Berichts-Manager zur Seite **Inhalt** . Navigieren Sie zum Ordner, zu dem Sie ein Element hinzufügen möchten.  
  
3.  Klicken Sie auf **Datei hochladen**.  
  
4.  Klicken Sie auf **Durchsuchen** , um eine Datei zum Hochladen auszuwählen. Sie können eine Berichtsdefinitionsdatei, ein Bild, ein Dokument oder jede andere Datei hochladen, die Sie auf einem Berichtsserver zur Verfügung stellen möchten.  
  
5.  Geben Sie einen Namen für das neue Element ein. Ein Element darf Leerzeichen enthalten, jedoch nicht die folgenden reservierten Zeichen: ; ? : @ & = + , $ / * \< > |.  
  
6.  Wenn Sie ein vorhandenes Element durch ein neues ersetzen möchten, wählen Sie **Vorhandenes Element überschreiben**aus.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Erstellen, Löschen oder Ändern einer freigegebenen Datenquelle &#40;Berichts-Manager&#41;](../Topic/Create,%20Delete,%20or%20Modify%20a%20Shared%20Data%20Source%20\(Report%20Manager\).md)   
 [Inhalt &#40;Seite, Berichts-Manager&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [Datei hochladen &#40;Seite, Berichts-Manager&#41;](../Topic/Upload%20File%20Page%20\(Report%20Manager\).md)   
 [Hochladen von Dateien in einen Ordner](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  