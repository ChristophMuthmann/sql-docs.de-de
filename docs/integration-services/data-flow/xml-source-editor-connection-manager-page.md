---
title: "Quellen-Editor f&#252;r XML (Seite Verbindungs-Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.xmlsourceadapter.connectionmanager.f1"
helpviewer_keywords: 
  - "Quellen-Editor für XML"
ms.assetid: e6507403-a3ce-4b6f-91fc-a7de9f7b6283
caps.latest.revision: 20
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 20
---
# Quellen-Editor f&#252;r XML (Seite Verbindungs-Manager)
  Mithilfe der Seite **Verbindungs-Manager** in **Quellen-Editor für XML** können Sie eine XML-Datei und die XML-Schemadefinition (XSD) angeben, mit der die XML-Daten transformiert werden.  
  
 Weitere Informationen zur XML-Quelle finden Sie unter [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## Statische Optionen  
 **Datenzugriffsmodus**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Wert|Description|  
|-----------|-----------------|  
|XML-Dateispeicherort|Ruft Daten aus einer XML-Datei ab.|  
|XML-Datei aus Variable|Gibt den XML-Dateinamen in einer Variablen an.<br /><br /> **Verwandte Informationen:** [Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md)|  
|XML-Daten aus Variable|Ruft XML-Daten aus einer Variablen ab.|  
  
 **Inlineschema verwenden**  
 Gibt an, ob die XML-Quelldaten das XSD-Schema enthalten, mit dem die Struktur und die Daten definiert und überprüft werden.  
  
 **XSD-Speicherort**  
 Geben Sie den Pfad und den Dateinamen der XSD-Schemadatei ein, oder suchen Sie die Datei, indem Sie auf die Schaltfläche **Durchsuchen** klicken.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie die XSD-Schemadatei suchen.  
  
 **XSD-Code generieren**  
 Mithilfe des Dialogfelds **Speichern unter** können Sie einen Speicherort für die automatisch generierte XSD-Schemadatei auswählen. Der Editor leitet das Schema aus der Struktur der XML-Daten ab.  
  
## Dynamische Optionen (Datenzugriffsmodus)  
  
### Datenzugriffsmodus = Speicherort der XML-Datei  
 **XML-Speicherort**  
 Geben Sie den Pfad und den Dateinamen der XML-Datendatei ein, oder suchen Sie die Datei, indem Sie auf die Schaltfläche **Durchsuchen** klicken.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie die XML-Datendatei suchen.  
  
### Datenzugriffsmodus = XML-Datei aus Variable  
 **Variablenname**  
 Wählt die Variable aus, die den Pfad und den Dateinamen der XML-Datei enthält.  
  
### Datenzugriffsmodus = XML-Daten aus Variable  
 **Variablenname**  
 Wählt die Variable aus, die die XML-Daten enthält.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Quellen-Editor für XML &#40;Seite „Spalten“&#41;](../../integration-services/data-flow/xml-source-editor-columns-page.md)   
 [Quellen-Editor für XML &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/xml-source-editor-error-output-page.md)   
 [Extrahieren von Daten mithilfe der XML-Quelle](../../integration-services/data-flow/extract-data-by-using-the-xml-source.md)  
  
  