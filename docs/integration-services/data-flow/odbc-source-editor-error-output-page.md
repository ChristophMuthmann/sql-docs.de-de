---
title: "Quellen-Editor f&#252;r ODBC (Seite Fehlerausgabe) | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcsource.errorhandling.f1"
ms.assetid: b2f6866c-db07-4cb3-9f38-889f8d2b03e6
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Quellen-Editor f&#252;r ODBC (Seite Fehlerausgabe)
  Auf der Seite **Fehlerausgabe** des Dialogfelds **Quellen-Editor für ODBC** können Sie Optionen für die Fehlerbehandlung auswählen.  
  
 Weitere Informationen zur ODBC-Quelle finden Sie unter [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## Aufgabenliste  
 **So öffnen Sie die Seite "Fehlerausgabe" des Quellen-Editors für ODBC**  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die ODBC-Quelle enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die ODBC-Quelle.  
  
-   Klicken Sie im **Quellen-Editor für ODBC**auf **Fehlerausgabe**.  
  
## enthalten  
  
### Eingabe/Ausgabe  
 Zeigt den Namen der Datenquelle an.  
  
### Column  
 Wird nicht verwendet.  
  
### Fehler  
 Wählen Sie aus, wie die ODBC-Quelle Fehler in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### Abschneiden  
 Wählen Sie aus, wie die ODBC-Quelle Kürzungen in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### Description  
 Wird nicht verwendet.  
  
### Diesen Wert für ausgewählte Zellen festlegen  
 Wählen Sie aus, wie die ODBC-Quelle im Fall eines Fehlers oder einer Kürzung mit den ausgewählten Zellen verfahren soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
### Anwenden  
 Wendet die Fehlerbehandlungsoptionen auf die ausgewählten Zellen an.  
  
## Fehlerbehandlungsoptionen  
 Mit den folgenden Optionen konfigurieren Sie, wie die ODBC-Quelle Fehler und Kürzungen behandelt.  
  
### Fehler bei Komponente  
 Bei einem Fehler oder beim Abschneiden von Daten wird der Datenflusstask nicht ausgeführt. Dies ist das Standardverhalten.  
  
### Fehler ignorieren  
 Der Fehler oder die Kürzung wird ignoriert.  
  
### Zeile umleiten  
 Die Zeile, die den Fehler oder die Kürzung verursacht, wird an die Fehlerausgabe der ODBC-Quelle umgeleitet. Weitere Informationen finden Sie unter [ODBC Source](../../integration-services/data-flow/odbc-source.md).  
  
## Siehe auch  
 [Quellen-Editor für ODBC &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [Quellen-Editor für ODBC &#40;Seite „Spalten“&#41;](../../integration-services/data-flow/odbc-source-editor-columns-page.md)  
  
  