---
title: "ODBC-Ziel | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcdest.f1"
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# ODBC-Ziel
  Das ODBC-Ziel führt für die Daten einen Massenladevorgang in Datenbanktabellen mit ODBC-Unterstützung durch. Das ODBC-Ziel verwendet einen ODBC-Verbindungs-Manager, um eine Verbindung mit der Datenquelle herzustellen.  
  
 Ein ODBC-Ziel enthält Zuordnungen zwischen Eingabespalten und Spalten in der Zieldatenquelle. Sie müssen nicht allen Zielspalten Eingabespalten zuordnen. In Abhängigkeit von den Eigenschaften der Zielspalten können jedoch Fehler auftreten, falls den Zielspalten keine Eingabespalten zugeordnet sind. Wenn eine Zielspalte z. B. keine NULL-Werte zulässt, muss dieser Spalte eine Eingabespalte zugeordnet werden. Außerdem können Spalten mit verschiedenen Typen zugeordnet werden. Wenn die Eingabedaten mit dem Typ der Zielspalte jedoch nicht kompatibel sind, tritt zur Laufzeit ein Fehler auf. Je nach Einstellung des Fehlerverhaltens wird der Fehler ignoriert, ein Fehler verursacht oder die Zeile zurück an die Fehlerausgabe gesendet.  
  
 Das ODBC-Ziel weist eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> Ladeoptionen  
 Das ODBC-Ziel kann eines von zwei Zugriffslademodulen verwenden. Sie legen den Modus im [Quellen-Editor für ODBC &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md) fest. Die beiden Modi sind:  
  
-   **Batch**: In diesem Modus versucht das ODBC-Ziel, basierend auf den erkannten Funktionen des ODBC-Anbieters die effizienteste Einfügemethode zu verwenden. Für die meisten modernen ODBC-Anbieter umfasst dies das Vorbereiten einer INSERT-Anweisung mit Parametern und das anschließende Verwenden einer Arrayparameterbindung pro Zeile (wobei die Arraygröße über die **BatchSize**-Eigenschaft gesteuert wird). Wenn Sie **Batch** auswählen und der Anbieter diese Methode nicht unterstützt, wechselt das ODBC-Ziel automatisch zum Modus **Zeile für Zeile**.  
  
-   **Zeile für Zeile**: In diesem Modus bereitet das ODBC-Ziel eine INSERT-Anweisung mit Parametern vor und verwendet **SQL Execute**, um Zeilen einzeln einzufügen.  
  
## Fehlerbehandlung  
 Das ODBC-Ziel verfügt über eine Fehlerausgabe. Die Komponentenfehlerausgabe enthält die folgenden Ausgabespalten:  
  
-   **Fehlercode**: Ruft die Zahl ab, die dem aktuellen Fehler entspricht. Eine Liste der Fehler finden Sie in der Dokumentation zur Quelldatenbank. Eine Liste der SSIS-Fehlercodes finden Sie in der SSIS-Fehler- und Meldungsreferenz.  
  
-   **Fehlerspalte**: Die Quellspalte, die den Fehler verursacht (für Konvertierungsfehler).  
  
-   Die Spalten mit den Standardausgabedaten.  
  
 Je nach Einstellung des Fehlerverhaltens unterstützt das ODBC-Ziel das Zurückgeben von Fehlern (Datenkonvertierung, Abschneiden), die während des Extraktionsprozesses in der Fehlerausgabe auftreten. Weitere Informationen finden Sie unter [Quellen-Editor für ODBC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md).  
  
## Parallelität  
 Es gilt keine Einschränkung in Bezug auf die Anzahl von ODBC-Zielkomponenten, die parallel für dieselbe Tabelle oder verschiedene Tabellen, auf demselben Computer oder auf unterschiedlichen Computern ausgeführt werden können (mit Ausnahme normaler Einschränkungen für globale Sitzungen).  
  
 Aufgrund von Einschränkungen in Verbindung mit dem verwendeten ODBC-Anbieter kann die Anzahl gleichzeitiger Verbindungen über den Anbieter möglicherweise trotzdem eingeschränkt sein. Diese Einschränkungen begrenzen die Anzahl der unterstützten parallelen Instanzen, die für das ODBC-Ziel möglich sind. Der SSIS-Entwickler muss sich über die Einschränkungen im Klaren sein, die für verwendete ODBC-Anbieter gelten, und diese beim Erstellen von SSIS-Paketen beachten.  
  
 Sie müssen auch beachten, dass das gleichzeitige Laden in dieselbe Tabelle aufgrund der standardmäßigen Datensatzsperrung zu einer Verschlechterung der Leistung führen kann. Dies hängt von den Daten ab, die geladen werden, sowie von der Tabellenorganisation.  
  
## Problembehandlung des ODBC-Ziels  
 Sie können die von der ODBC-Quelle an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Speichern von Daten in externen Datenquellen durch das ODBC-Ziel behandeln. Aktivieren Sie die Ablaufverfolgung für den ODBC-Treiber-Manager, um die Aufrufe zu protokollieren, die vom ODBC-Ziel an externe Datenanbieter gesendet werden. Weitere Informationen finden Sie in der Microsoft-Dokumentation unter *Generieren einer ODBC-Ablaufverfolgung mit dem ODBC-Datenquellen-Administrator*.  
  
## Konfigurieren des ODBC-Ziels  
 Sie können das ODBC-Ziel programmgesteuert oder mit dem SSIS-Designer konfigurieren.  
  
 Weitere Informationen finden Sie in einem der folgenden Themen:  
  
-   [Ziel-Editor für ODBC &#40;Verbindungs-Manager-Seite&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [Ziel-Editor für ODBC &#40;Seite Zuordnungen&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [Ziel-Editor für ODBC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können.  
  
 So öffnen Sie das Dialogfeld **Erweiterter Editor** :  
  
-   Klicken Sie auf dem Bildschirm **Datenfluss** des [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Projekts mit der rechten Maustaste auf das ODBC-Ziel, und wählen Sie **Erweiterten Editor anzeigen**.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld Erweiterter Editor festlegen können, finden Sie unter [ODBC Destination Custom Properties](../../integration-services/data-flow/odbc-destination-custom-properties.md).  
  
## In diesem Abschnitt  
  
-   [Ziel-Editor für ODBC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
-   [Ziel-Editor für ODBC &#40;Seite Zuordnungen&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [Ziel-Editor für ODBC &#40;Verbindungs-Manager-Seite&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [Laden von Daten mithilfe des ODBC-Ziels](../../integration-services/data-flow/load-data-by-using-the-odbc-destination.md)  
  
-   [Benutzerdefinierte Eigenschaften von ODBC-Zielen](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
  