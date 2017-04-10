---
title: "Verbindungs-Manager-Editor f&#252;r Excel | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.excelconnection.f1"
helpviewer_keywords: 
  - "Verbindungs-Manager-Editor für Excel"
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# Verbindungs-Manager-Editor f&#252;r Excel
  Mithilfe des Dialogfelds **Verbindungs-Manager-Editor für Excel** können Sie einer vorhandenen oder neuen [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] -Arbeitsmappendatei eine Verbindung hinzufügen.  
  
 Weitere Informationen zum Excel-Verbindungs-Manager finden Sie unter [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
## enthalten  
 **Excel-Dateipfad**  
 Geben Sie den Pfad und den Dateinamen einer vorhandenen oder neuen Excel-Arbeitsmappendatei (XLS-Datei) ein.  
  
> [!NOTE]  
>  Es ist nicht möglich, eine Verbindung mit einer kennwortgeschützten Excel-Datei herzustellen.  
  
> [!WARNING]  
>  Der **Ziel-Editor für Excel** erstellt die Excel-Datei automatisch, wenn Sie eine **Excel-Verbindung** auswählen, die zu einer neuen oder nicht vorhandenen Datei zeigt, und dann auf **Neu** für **Name der Excel-Tabelle** klicken.  
  
 **Durchsuchen**  
 Verwenden Sie das Dialogfeld **Öffnen**, um zum Ordner zu navigieren, in dem die Excel-Datei enthalten ist bzw. in dem Sie die neue Datei erstellen möchten.  
  
 **Excel-Version**  
 Geben Sie die Version von Microsoft Excel an, die zum Erstellen der Datei verwendet wurde.  
  
 **Erste Zeile enthält Spaltennamen**  
 Geben Sie an, ob die erste Zeile der Daten in der ausgewählten Arbeitsmappe Spaltennamen enthält. Der Standardwert für diese Option ist **True**.  
  
## Anbieter und Treiber für Microsoft Excel- und Access-Dateien  
 Möglicherweise müssen Sie die OLE DB-Anbieter und -Treiber für Microsoft Office-Dateien herunterladen, sofern diese noch nicht installiert sind. Spätere Versionen des Anbieters dienen zum Öffnen von Dateien, die in früheren Versionen von Excel erstellt wurden.  
  
 Wenn der Computer über eine 32-Bit-Version von Office verfügt, müssen Sie die 32-Bit-Version der Treiber installieren. Sie müssen zudem sicherstellen, dass Sie den Assistenten oder das Integration Services-Paket ausführen, das den Treiber im 32-Bit-Modus erstellt.  
  
|Microsoft Office-Version|Herunterladen|  
|------------------------------|--------------|  
|2007|[2007 Office System-Treiber: Datenkonnektivitätskomponenten](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  