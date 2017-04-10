---
title: "Ziel-Editor f&#252;r ODBC (Verbindungs-Manager-Seite) | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcdest.connection.f1"
ms.assetid: f6d9c6c2-e4c4-468b-9e0d-af7b9609614d
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Ziel-Editor f&#252;r ODBC (Verbindungs-Manager-Seite)
  Auf der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für ODBC** können Sie den ODBC-Verbindungs-Manager für das Ziel auswählen. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
 Weitere Informationen zum ODBC-Ziel finden Sie unter [ODBC Destination](../../integration-services/data-flow/odbc-destination.md).  
  
 **So öffnen Sie die Seite "Verbindungs-Manager" des Ziel-Editors für ODBC**  
  
## Aufgabenliste  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das das ODBC-Ziel enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ODBC-Ziel.  
  
-   Klicken Sie im **Ziel-Editor für ODBC**auf **Verbindungs-Manager**.  
  
## Optionen  
  
### Verbindungs-Manager  
 Wählen Sie in der Liste einen vorhandenen ODBC-Verbindungs-Manager aus, oder klicken Sie auf Neu, um eine neue Verbindung zu erstellen. Sie können eine Verbindung mit jeder von ODBC unterstützten Datenbank erstellen.  
  
### Neu  
 Klicken Sie auf **Neu**. Das Dialogfeld **ODBC-Verbindungs-Manager konfigurieren** , in dem Sie einen neuen Verbindungs-Manager erstellen können, wird geöffnet.  
  
### Datenzugriffsmodus  
 Wählen Sie die Methode zum Laden von Daten in das Ziel aus. Die Optionen sind in der folgenden Tabelle aufgeführt:  
  
|Option|Beschreibung|  
|------------|-----------------|  
|Tabellenname - Batch|Wählen Sie diese Option aus, um das ODBC-Ziel im Batchmodus zu konfigurieren. Bei Auswahl dieser Option sind die folgenden Optionen verfügbar:|  
||**Name der Tabelle oder Sicht**: Wählen Sie in der Liste eine verfügbare Tabelle oder Sicht aus.<br /><br /> Diese Liste enthält nur die ersten 1000 Tabellen. Wenn die Datenbank mehr als 1000 Tabellen enthält, können Sie den Anfang eines Tabellennamens eingeben oder das Platzhalterzeichen (\*) verwenden, um einen beliebigen Teil des Namens einzugeben und die gewünschten Tabellen anzuzeigen.<br /><br /> **Batchgröße**: Geben Sie die Größe des Batches für das Massenladen ein. Dies ist die Anzahl von Zeilen, die als Batch geladen werden.|  
|Tabellenname - Zeile für Zeile|Wählen Sie diese Option aus, um das ODBC-Ziel so zu konfigurieren, dass jede Zeile einzeln in die Zieltabelle eingefügt wird. Bei Auswahl dieser Option ist die folgende Option verfügbar:|  
||**Name der Tabelle oder Sicht**: Wählen Sie in der Liste eine verfügbare Tabelle oder Sicht in der Datenbank aus.<br /><br /> Diese Liste enthält nur die ersten 1000 Tabellen. Wenn die Datenbank mehr als 1000 Tabellen enthält, können Sie den Anfang eines Tabellennamens eingeben oder das Platzhalterzeichen (*) verwenden, um einen beliebigen Teil des Namens einzugeben und die gewünschten Tabellen anzuzeigen.|  
  
### Vorschau  
 Klicken Sie auf **Vorschau** , um die ersten 200 Zeilen (max.) für die ausgewählte Tabelle anzuzeigen.  
  
## Siehe auch  
 [Benutzerdefinierte Eigenschaften von ODBC-Zielen](../../integration-services/data-flow/odbc-destination-custom-properties.md)   
 [Ziel-Editor für ODBC &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)   
 [Ziel-Editor für ODBC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
  