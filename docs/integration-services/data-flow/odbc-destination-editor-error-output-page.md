---
title: "Ziel-Editor f&#252;r ODBC (Seite &quot;Fehlerausgabe&quot;) | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcdest.errorhandling.f1"
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Ziel-Editor f&#252;r ODBC (Seite &quot;Fehlerausgabe&quot;)
  Auf der Seite **Fehlerausgabe** des Dialogfelds **Ziel-Editor für ODBC** können Sie Optionen für die Fehlerbehandlung auswählen.  
  
 Weitere Informationen zum ODBC-Ziel finden Sie unter [ODBC Destination](../../integration-services/data-flow/odbc-destination.md).  
  
 **So öffnen Sie die Seite "Fehlerausgabe" des Ziel-Editors für ODBC**  
  
## Aufgabenliste  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das das ODBC-Ziel enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ODBC-Ziel.  
  
-   Klicken Sie im **Ziel-Editor für ODBC**auf **Fehlerausgabe**.  
  
## enthalten  
  
### Eingabe/Ausgabe  
 Zeigt den Namen der Datenquelle an.  
  
### Column  
 Wird nicht verwendet.  
  
### Fehler  
 Wählen Sie aus, wie das ODBC-Ziel Fehler in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### Abschneiden  
 Wählen Sie aus, wie das ODBC-Ziel Kürzungen in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### Description  
 Zeigt eine Beschreibung des Fehlers an.  
  
### Diesen Wert für ausgewählte Zellen festlegen  
 Wählen Sie aus, wie das ODBC-Ziel im Fall eines Fehlers oder einer Kürzung mit den ausgewählten Zellen verfahren soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### Anwenden  
 Wendet die Fehlerbehandlungsoptionen auf die ausgewählten Zellen an.  
  
## Fehlerbehandlungsoptionen  
 Mit den folgenden Optionen konfigurieren Sie, wie das ODBC-Ziel Fehler und Kürzungen behandelt.  
  
### Fehler bei Komponente  
 Bei einem Fehler oder beim Abschneiden von Daten wird der Datenflusstask nicht ausgeführt. Dies ist das Standardverhalten.  
  
### Fehler ignorieren  
 Der Fehler oder die Kürzung wird ignoriert.  
  
### Zeile umleiten  
 Die Zeile, die den Fehler oder die Kürzung verursacht, wird an die Fehlerausgabe des ODBC-Ziels umgeleitet. Weitere Informationen finden Sie unter "ODBC-Ziel".  
  
## Siehe auch  
 [Ziel-Editor für ODBC &#40;Verbindungs-Manager-Seite&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [Ziel-Editor für ODBC &#40;Seite Zuordnungen&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
  