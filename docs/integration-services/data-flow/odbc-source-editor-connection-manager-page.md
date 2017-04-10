---
title: "Quellen-Editor f&#252;r ODBC (Seite Verbindungs-Manager) | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcsource.connection.f1"
ms.assetid: e2c8dc83-6394-4d6c-9232-97e94be72431
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Quellen-Editor f&#252;r ODBC (Seite Verbindungs-Manager)
  Auf der Seite **Verbindungs-Manager** des Dialogfelds **Quellen-Editor für ODBC** können Sie den ODBC-Verbindungs-Manager für die Quelle auswählen. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
 Weitere Informationen zur ODBC-Quelle finden Sie unter [ODBC Source](../../integration-services/data-flow/odbc-source.md).  
  
## Aufgabenliste  
 **So öffnen Sie die Seite "Verbindungs-Manager" des Quellen-Editors für ODBC**  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die ODBC-Quelle enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die ODBC-Quelle.  
  
## enthalten  
  
### Verbindungs-Manager  
 Wählen Sie in der Liste einen vorhandenen ODBC-Verbindungs-Manager aus, oder klicken Sie auf **Neu** , um eine neue Verbindung zu erstellen. Sie können eine Verbindung mit jeder von ODBC unterstützten Datenbank erstellen.  
  
### Neu  
 Klicken Sie auf **Neu**. Das Dialogfeld **ODBC-Verbindungs-Manager konfigurieren** , in dem Sie einen neuen ODBC-Verbindungs-Manager erstellen können, wird geöffnet.  
  
### Datenzugriffsmodus  
 Wählen Sie die Methode für die Auswahl von Daten aus der Quelle aus. Die Optionen sind in der folgenden Tabelle aufgeführt:  
  
|Option|Description|  
|------------|-----------------|  
|Tabellenname|Ruft Daten aus einer Tabelle oder Sicht in der ODBC-Datenquelle ab. Bei Auswahl dieser Option wählen Sie einen der folgenden Werte in der Liste aus:|  
||**Name der Tabelle oder Sicht**: Wählen Sie in der Liste eine verfügbare Tabelle oder Sicht aus, oder geben Sie einen regulären Ausdruck ein, um die Tabelle zu identifizieren.|  
||Diese Liste enthält nur die ersten 1000 Tabellen. Wenn die Datenbank mehr als 1000 Tabellen enthält, können Sie den Anfang eines Tabellennamens eingeben oder das Platzhalterzeichen (*) verwenden, um einen beliebigen Teil des Namens einzugeben und die gewünschten Tabellen anzuzeigen.|  
|SQL-Befehl|Ruft mit einer SQL-Abfrage Daten aus der ODBC-Datenquelle ab. Die Abfrage sollte in der Syntax der verwendeten Quelldatenbank geschrieben werden. Bei Auswahl dieser Option geben Sie anhand einer der folgenden Methoden eine Abfrage ein:|  
||Geben Sie den Text der SQL-Abfrage im Feld **SQL-Befehlstext** ein.|  
||Klicken Sie auf **Durchsuchen** , um die SQL-Abfrage aus einer Textdatei zu laden.|  
||Klicken Sie auf **Abfrage analysieren** , um die Syntax des Abfragetextes zu überprüfen.|  
  
### Vorschau  
 Klicken Sie auf **Vorschau** , um die ersten 200 Zeilen (max.) der Daten anzuzeigen, die aus der ausgewählten Tabelle bzw. Sicht extrahiert wurden.  
  
## Siehe auch  
 [Benutzerdefinierte Eigenschaften der ODBC-Quelle](../../integration-services/data-flow/odbc-source-custom-properties.md)   
 [Quellen-Editor für ODBC &#40;Seite „Spalten“&#41;](../../integration-services/data-flow/odbc-source-editor-columns-page.md)   
 [Quellen-Editor für ODBC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  