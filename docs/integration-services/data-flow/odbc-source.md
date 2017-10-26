---
title: ODBC-Quelle | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.odbcsource.f1
- sql13.ssis.designer.odbcsource.connection.f1
- sql13.ssis.designer.odbcsource.columns.f1
- sql13.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 1e26fe82d939dd58cbbfa850f041a7ae3d23b248
ms.contentlocale: de-de
ms.lasthandoff: 08/17/2017

---
# <a name="odbc-source"></a>ODBC-Quelle
  Die ODBC-Quelle extrahiert Daten mithilfe einer Datenbanktabelle, Sicht oder SQL-Anweisung aus einer Datenbank mit ODBC-Unterstützung.  
  
 Die ODBC-Quelle verfügt über die folgenden Datenzugriffsmodi zum Extrahieren von Daten:  
  
-   Eine Tabelle oder Sicht.  
  
-   Die Ergebnisse einer SQL-Anweisung.  
  
 Die Quelle verwendet einen ODBC-Verbindungs-Manager, der den zu verwendenden Anbieter angibt.  
  
 Eine ODBC-Quelle enthält die Ausgabespalten für Quelldaten. Wenn Ausgabespalten auf dem ODBC-Ziel den Zielspalten zugeordnet werden, treten möglicherweise Fehler auf, wenn den Zielspalten keine Ausgabespalten zugeordnet sind. Es können Spalten mit verschiedenen Typen zugeordnet werden. Wenn die Ausgabedaten mit dem Ziel jedoch nicht kompatibel sind, tritt zur Laufzeit ein Fehler auf. Je nach Einstellung des Fehlerverhaltens wird der Fehler ignoriert, ein Fehler verursacht oder die Zeile zurück an die Fehlerausgabe gesendet.  
  
 Die ODBC-Quelle weist eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Die ODBC-Quelle verfügt über eine Fehlerausgabe. Die Komponentenfehlerausgabe enthält die folgenden Ausgabespalten:  
  
-   **Fehlercode**: Ruft die Zahl ab, die dem aktuellen Fehler entspricht. Eine Liste der Fehler finden Sie in der Dokumentation zur Datenbank mit ODBC-Unterstützung. Eine Liste der SSIS-Fehlercodes finden Sie in der SSIS-Fehler- und Meldungsreferenz.  
  
-   **Fehlerspalte**: Die Quellspalte, die den Fehler verursacht (für Konvertierungsfehler).  
  
-   Die Spalten mit den Standardausgabedaten.  
  
 Je nach Einstellung des Fehlerverhaltens unterstützt die ODBC-Quelle das Zurückgeben von Fehlern (Datenkonvertierung, Abschneiden), die während des Extraktionsprozesses in der Fehlerausgabe auftreten. Weitere Informationen finden Sie unter [Ziel-Editor für ODBC &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md).  
  
## <a name="data-type-support"></a>Datentypunterstützung  
 Informationen zu den Datentypen, die von der ODBC-Quelle unterstützt werden, finden Sie unter Konnektor für Open Database Connectivity (ODBC) von Attunity.  
  
## <a name="extract-options"></a>Extrahierungsoptionen  
 Die ODBC-Quelle arbeitet entweder im Modus **Batch** oder **Zeile für Zeile** . Der verwendete Modus wird mithilfe der **FetchMethod** -Eigenschaft bestimmt. Die Modi werden in der folgenden Liste beschrieben:  
  
-   **Batch**: Die Komponente versucht, basierend auf den erkannten Funktionen des ODBC-Anbieters die effizienteste Abrufmethode zu verwenden. Für die meisten modernen ODBC-Anbieter ist dies SQLFetchScroll mit Arraybindung (wobei die Arraygröße von der **BatchSize** -Eigenschaft bestimmt wird). Wenn Sie **Batch** auswählen und der Anbieter diese Methode nicht unterstützt, wechselt das ODBC-Ziel automatisch zum Modus **Zeile für Zeile** .  
  
-   **Zeile für Zeile**: Die Komponente ruft die Zeilen mithilfe von SQLFetch einzeln ab.  
  
 Weitere Informationen zur **FetchMethod** -Eigenschaft finden Sie unter [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md).  
  
## <a name="parallelism"></a>Parallelität  
 Es gilt keine Einschränkung in Bezug auf die Anzahl von ODBC-Quellkomponenten, die parallel für dieselbe Tabelle oder verschiedene Tabellen, auf demselben Computer oder auf unterschiedlichen Computern ausgeführt werden können (mit Ausnahme normaler Einschränkungen für globale Sitzungen).  
  
 Aufgrund von Einschränkungen in Verbindung mit dem verwendeten ODBC-Anbieter kann die Anzahl gleichzeitiger Verbindungen über den Anbieter möglicherweise trotzdem eingeschränkt sein. Diese Einschränkungen begrenzen die Anzahl der unterstützten parallelen Instanzen, die für die ODBC-Quelle möglich sind. Der SSIS-Entwickler muss sich über die Einschränkungen im Klaren sein, die für verwendete ODBC-Anbieter gelten, und diese beim Erstellen von SSIS-Paketen beachten.  
  
## <a name="troubleshooting-the-odbc-source"></a>Problembehandlung der ODBC-Quelle  
 Sie können die von der ODBC-Quelle an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Laden von Daten aus externen Datenquellen durch die ODBC-Quelle behandeln. Aktivieren Sie die Ablaufverfolgung für den ODBC-Treiber-Manager, um die Aufrufe zu protokollieren, die von der ODBC-Quelle an externe Datenanbieter gesendet werden. Weitere Informationen finden Sie in der Microsoft-Dokumentation unter *Generieren einer ODBC-Ablaufverfolgung mit dem ODBC-Datenquellen-Administrator*.  
  
## <a name="configuring-the-odbc-source"></a>Konfigurieren der ODBC-Quelle  
 Sie können die ODBC-Quelle programmgesteuert oder mit dem SSIS-Designer konfigurieren.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können.  
  
 So öffnen Sie das Dialogfeld **Erweiterter Editor** :  
  
-   Klicken Sie auf dem Bildschirm **Datenfluss** des [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Projekts mit der rechten Maustaste auf die ODBC-Quelle, und wählen Sie **Erweiterten Editor anzeigen**.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld Erweiterter Editor festlegen können, finden Sie unter [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Extrahieren von Daten mithilfe der ODBC-Quelle](../../integration-services/data-flow/extract-data-by-using-the-odbc-source.md)  
  
-   [Benutzerdefinierte Eigenschaften der ODBC-Quelle](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
## <a name="odbc-source-editor-connection-manager-page"></a>Quellen-Editor für ODBC (Seite Verbindungs-Manager)
  Auf der Seite **Verbindungs-Manager** des Dialogfelds **Quellen-Editor für ODBC** können Sie den ODBC-Verbindungs-Manager für die Quelle auswählen. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
### <a name="task-list"></a>Aufgabenliste  
 **So öffnen Sie die Seite "Verbindungs-Manager" des Quellen-Editors für ODBC**  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die ODBC-Quelle enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die ODBC-Quelle.  
  
### <a name="options"></a>enthalten  
  
#### <a name="connection-manager"></a>Verbindungs-Manager  
 Wählen Sie in der Liste einen vorhandenen ODBC-Verbindungs-Manager aus, oder klicken Sie auf **Neu** , um eine neue Verbindung zu erstellen. Sie können eine Verbindung mit jeder von ODBC unterstützten Datenbank erstellen.  
  
#### <a name="new"></a>Neu  
 Klicken Sie auf **Neu**. Das Dialogfeld **ODBC-Verbindungs-Manager konfigurieren** , in dem Sie einen neuen ODBC-Verbindungs-Manager erstellen können, wird geöffnet.  
  
#### <a name="data-access-mode"></a>Datenzugriffsmodus  
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
  
#### <a name="preview"></a>Vorschau  
 Klicken Sie auf **Vorschau** , um die ersten 200 Zeilen (max.) der Daten anzuzeigen, die aus der ausgewählten Tabelle bzw. Sicht extrahiert wurden.  
  
## <a name="odbc-source-editor-columns-page"></a>Quellen-Editor für ODBC (Seite Spalten)
  Auf der Seite **Spalten** des Dialogfelds **Quellen-Editor für ODBC** können Sie jeder externen Spalte (Quellspalte) eine Ausgabespalte zuordnen.  
  
### <a name="task-list"></a>Aufgabenliste  
 **So öffnen Sie die Seite "Spalten" des Quellen-Editors für ODBC**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die ODBC-Quelle enthält.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die ODBC-Quelle.  
  
3.  Klicken Sie im **Quellen-Editor für ODBC**auf **Spalten**.  
  
### <a name="options"></a>enthalten  
  
#### <a name="available-external-columns"></a>Verfügbare externe Spalten  
 Eine Liste der in der Datenquelle verfügbaren externen Spalten. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden. Wählen Sie die zu verwendenden Spalten aus der Datenquelle aus. Die ausgewählten Spalten werden der Liste **Externe Spalte** in der Reihenfolge hinzugefügt, in der Sie sie auswählen.  
  
 Aktivieren Sie das Kontrollkästchen **Alle auswählen** , um alle Spalten auszuwählen.  
  
#### <a name="external-column"></a>Externe Spalte  
 Eine Ansicht der externen Spalten (Quellspalten) in der Reihenfolge, in der sie angezeigt werden, wenn Sie Komponenten konfigurieren, die Daten aus dieser Quelle verwenden.  
  
#### <a name="output-column"></a>Ausgabespalte  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen ein. Standardmäßig wird der Name der ausgewählten externen (Quell-)Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der eingegebene Name wird im SSIS-Designer angezeigt.  
  
## <a name="odbc-source-editor-error-output-page"></a>Quellen-Editor für ODBC (Seite Fehlerausgabe)
  Auf der Seite **Fehlerausgabe** des Dialogfelds **Quellen-Editor für ODBC** können Sie Optionen für die Fehlerbehandlung auswählen.  
  
### <a name="task-list"></a>Aufgabenliste  
 **So öffnen Sie die Seite "Fehlerausgabe" des Quellen-Editors für ODBC**  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die ODBC-Quelle enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die ODBC-Quelle.  
  
-   Klicken Sie im **Quellen-Editor für ODBC**auf **Fehlerausgabe**.  
  
### <a name="options"></a>enthalten  
  
#### <a name="inputoutput"></a>Eingabe/Ausgabe  
 Zeigt den Namen der Datenquelle an.  
  
#### <a name="column"></a>Column  
 Wird nicht verwendet.  
  
#### <a name="error"></a>Fehler  
 Wählen Sie aus, wie die ODBC-Quelle Fehler in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
#### <a name="truncation"></a>Abschneiden  
 Wählen Sie aus, wie die ODBC-Quelle Kürzungen in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
#### <a name="description"></a>Description  
 Wird nicht verwendet.  
  
#### <a name="set-this-value-to-selected-cells"></a>Diesen Wert für ausgewählte Zellen festlegen  
 Wählen Sie aus, wie die ODBC-Quelle im Fall eines Fehlers oder einer Kürzung mit den ausgewählten Zellen verfahren soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
#### <a name="apply"></a>Anwenden  
 Wendet die Fehlerbehandlungsoptionen auf die ausgewählten Zellen an.  
  
### <a name="error-handling-options"></a>Fehlerbehandlungsoptionen  
 Mit den folgenden Optionen konfigurieren Sie, wie die ODBC-Quelle Fehler und Kürzungen behandelt.  
  
#### <a name="fail-component"></a>Fehler bei Komponente  
 Bei einem Fehler oder beim Abschneiden von Daten wird der Datenflusstask nicht ausgeführt. Dies ist das Standardverhalten.  
  
#### <a name="ignore-failure"></a>Fehler ignorieren  
 Der Fehler oder die Kürzung wird ignoriert.  
  
#### <a name="redirect-flow"></a>Zeile umleiten  
 Die Zeile, die den Fehler oder die Kürzung verursacht, wird an die Fehlerausgabe der ODBC-Quelle umgeleitet.  
  
  

