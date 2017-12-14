---
title: ODBC-Ziel | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.odbcdest.f1
- sql13.ssis.designer.odbcdest.connection.f1
- sql13.ssis.designer.odbcdest.columns.f1
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0c3df5b8f8ef946021fcc72bb12cb164e99fdb5b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-destination"></a>ODBC-Ziel
  Das ODBC-Ziel führt für die Daten einen Massenladevorgang in Datenbanktabellen mit ODBC-Unterstützung durch. Das ODBC-Ziel verwendet einen ODBC-Verbindungs-Manager, um eine Verbindung mit der Datenquelle herzustellen.  
  
 Ein ODBC-Ziel enthält Zuordnungen zwischen Eingabespalten und Spalten in der Zieldatenquelle. Sie müssen nicht allen Zielspalten Eingabespalten zuordnen. In Abhängigkeit von den Eigenschaften der Zielspalten können jedoch Fehler auftreten, falls den Zielspalten keine Eingabespalten zugeordnet sind. Wenn eine Zielspalte z. B. keine NULL-Werte zulässt, muss dieser Spalte eine Eingabespalte zugeordnet werden. Außerdem können Spalten mit verschiedenen Typen zugeordnet werden. Wenn die Eingabedaten mit dem Typ der Zielspalte jedoch nicht kompatibel sind, tritt zur Laufzeit ein Fehler auf. Je nach Einstellung des Fehlerverhaltens wird der Fehler ignoriert, ein Fehler verursacht oder die Zeile zurück an die Fehlerausgabe gesendet.  
  
 Das ODBC-Ziel weist eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> Ladeoptionen  
 Das ODBC-Ziel kann eines von zwei Zugriffslademodulen verwenden. Sie legen den Modus im [Quellen-Editor für ODBC &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md) fest. Die beiden Modi sind:  
  
-   **Batch**: In diesem Modus versucht das ODBC-Ziel, basierend auf den erkannten Funktionen des ODBC-Anbieters die effizienteste Einfügemethode zu verwenden. Für die meisten modernen ODBC-Anbieter umfasst dies das Vorbereiten einer INSERT-Anweisung mit Parametern und das anschließende Verwenden einer Arrayparameterbindung pro Zeile (wobei die Arraygröße über die **BatchSize** -Eigenschaft gesteuert wird). Wenn Sie **Batch** auswählen und der Anbieter diese Methode nicht unterstützt, wechselt das ODBC-Ziel automatisch zum Modus **Zeile für Zeile** .  
  
-   **Zeile für Zeile**: In diesem Modus bereitet das ODBC-Ziel eine INSERT-Anweisung mit Parametern vor und verwendet **SQL Execute** , um Zeilen einzeln einzufügen.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Das ODBC-Ziel verfügt über eine Fehlerausgabe. Die Komponentenfehlerausgabe enthält die folgenden Ausgabespalten:  
  
-   **Fehlercode**: Ruft die Zahl ab, die dem aktuellen Fehler entspricht. Eine Liste der Fehler finden Sie in der Dokumentation zur Quelldatenbank. Eine Liste der SSIS-Fehlercodes finden Sie in der SSIS-Fehler- und Meldungsreferenz.  
  
-   **Fehlerspalte**: Die Quellspalte, die den Fehler verursacht (für Konvertierungsfehler).  
  
-   Die Spalten mit den Standardausgabedaten.  
  
 Je nach Einstellung des Fehlerverhaltens unterstützt das ODBC-Ziel das Zurückgeben von Fehlern (Datenkonvertierung, Abschneiden), die während des Extraktionsprozesses in der Fehlerausgabe auftreten. Weitere Informationen finden Sie unter [Quellen-Editor für ODBC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md).  
  
## <a name="parallelism"></a>Parallelität  
 Es gilt keine Einschränkung in Bezug auf die Anzahl von ODBC-Zielkomponenten, die parallel für dieselbe Tabelle oder verschiedene Tabellen, auf demselben Computer oder auf unterschiedlichen Computern ausgeführt werden können (mit Ausnahme normaler Einschränkungen für globale Sitzungen).  
  
 Aufgrund von Einschränkungen in Verbindung mit dem verwendeten ODBC-Anbieter kann die Anzahl gleichzeitiger Verbindungen über den Anbieter möglicherweise trotzdem eingeschränkt sein. Diese Einschränkungen begrenzen die Anzahl der unterstützten parallelen Instanzen, die für das ODBC-Ziel möglich sind. Der SSIS-Entwickler muss sich über die Einschränkungen im Klaren sein, die für verwendete ODBC-Anbieter gelten, und diese beim Erstellen von SSIS-Paketen beachten.  
  
 Sie müssen auch beachten, dass das gleichzeitige Laden in dieselbe Tabelle aufgrund der standardmäßigen Datensatzsperrung zu einer Verschlechterung der Leistung führen kann. Dies hängt von den Daten ab, die geladen werden, sowie von der Tabellenorganisation.  
  
## <a name="troubleshooting-the-odbc-destination"></a>Problembehandlung des ODBC-Ziels  
 Sie können die von der ODBC-Quelle an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme beim Speichern von Daten in externen Datenquellen durch das ODBC-Ziel behandeln. Aktivieren Sie die Ablaufverfolgung für den ODBC-Treiber-Manager, um die Aufrufe zu protokollieren, die vom ODBC-Ziel an externe Datenanbieter gesendet werden. Weitere Informationen finden Sie in der Microsoft-Dokumentation unter *Generieren einer ODBC-Ablaufverfolgung mit dem ODBC-Datenquellen-Administrator*.  
  
## <a name="configuring-the-odbc-destination"></a>Konfigurieren des ODBC-Ziels  
 Sie können das ODBC-Ziel programmgesteuert oder mit dem SSIS-Designer konfigurieren.  
  
 Weitere Informationen finden Sie in einem der folgenden Themen:  
  
-   [Ziel-Editor für ODBC &#40;Verbindungs-Manager-Seite&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [Ziel-Editor für ODBC &#40;Seite Zuordnungen&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [Ziel-Editor für ODBC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können.  
  
 So öffnen Sie das Dialogfeld **Erweiterter Editor** :  
  
-   Klicken Sie auf dem Bildschirm **Datenfluss** des [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Projekts mit der rechten Maustaste auf das ODBC-Ziel, und wählen Sie **Erweiterten Editor anzeigen**.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld Erweiterter Editor festlegen können, finden Sie unter [ODBC Destination Custom Properties](../../integration-services/data-flow/odbc-destination-custom-properties.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Laden von Daten mithilfe des ODBC-Ziels](../../integration-services/data-flow/load-data-by-using-the-odbc-destination.md)  
  
-   [Benutzerdefinierte Eigenschaften von ODBC-Zielen](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
## <a name="odbc-destination-editor-connection-manager-page"></a>Ziel-Editor für ODBC (Verbindungs-Manager-Seite)
  Auf der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für ODBC** können Sie den ODBC-Verbindungs-Manager für das Ziel auswählen. Außerdem können Sie auf dieser Seite eine Tabelle oder Sicht aus der Datenbank auswählen.  
  
 **So öffnen Sie die Seite "Verbindungs-Manager" des Ziel-Editors für ODBC**  
  
### <a name="task-list"></a>Aufgabenliste  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das das ODBC-Ziel enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ODBC-Ziel.  
  
-   Klicken Sie im **Ziel-Editor für ODBC**auf **Verbindungs-Manager**.  
  
### <a name="options"></a>Optionen  
  
#### <a name="connection-manager"></a>Verbindungs-Manager  
 Wählen Sie in der Liste einen vorhandenen ODBC-Verbindungs-Manager aus, oder klicken Sie auf Neu, um eine neue Verbindung zu erstellen. Sie können eine Verbindung mit jeder von ODBC unterstützten Datenbank erstellen.  
  
#### <a name="new"></a>Neu  
 Klicken Sie auf **Neu**. Das Dialogfeld **ODBC-Verbindungs-Manager konfigurieren** , in dem Sie einen neuen Verbindungs-Manager erstellen können, wird geöffnet.  
  
#### <a name="data-access-mode"></a>Datenzugriffsmodus  
 Wählen Sie die Methode zum Laden von Daten in das Ziel aus. Die Optionen sind in der folgenden Tabelle aufgeführt:  
  
|Option|Beschreibung|  
|------------|-----------------|  
|Tabellenname - Batch|Wählen Sie diese Option aus, um das ODBC-Ziel im Batchmodus zu konfigurieren. Bei Auswahl dieser Option sind die folgenden Optionen verfügbar:|  
||**Name der Tabelle oder Sicht**: Wählen Sie in der Liste eine verfügbare Tabelle oder Sicht aus.<br /><br /> Diese Liste enthält nur die ersten 1000 Tabellen. Wenn die Datenbank mehr als 1000 Tabellen enthält, können Sie den Anfang eines Tabellennamens eingeben oder das Platzhalterzeichen (\*) verwenden, um einen beliebigen Teil des Namens einzugeben und die gewünschten Tabellen anzuzeigen.<br /><br /> **Batchgröße**: Geben Sie die Größe des Batches für das Massenladen ein. Dies ist die Anzahl von Zeilen, die als Batch geladen werden.|  
|Tabellenname - Zeile für Zeile|Wählen Sie diese Option aus, um das ODBC-Ziel so zu konfigurieren, dass jede Zeile einzeln in die Zieltabelle eingefügt wird. Bei Auswahl dieser Option ist die folgende Option verfügbar:|  
||**Name der Tabelle oder Sicht**: Wählen Sie in der Liste eine verfügbare Tabelle oder Sicht in der Datenbank aus.<br /><br /> Diese Liste enthält nur die ersten 1000 Tabellen. Wenn die Datenbank mehr als 1000 Tabellen enthält, können Sie den Anfang eines Tabellennamens eingeben oder das Platzhalterzeichen (*) verwenden, um einen beliebigen Teil des Namens einzugeben und die gewünschten Tabellen anzuzeigen.|  
  
#### <a name="preview"></a>Vorschau  
 Klicken Sie auf **Vorschau** , um die ersten 200 Zeilen (max.) für die ausgewählte Tabelle anzuzeigen.  
  
## <a name="odbc-destination-editor-mappings-page"></a>Ziel-Editor für ODBC (Seite Zuordnungen)
  Auf der Seite **Zuordnungen** des Dialogfelds **Ziel-Editor für ODBC** können Sie eine Zuordnung von Eingabe- zu Zielspalten vornehmen.  
  
### <a name="options"></a>enthalten  
  
#### <a name="available-input-columns"></a>Verfügbare Eingabespalten  
 Die Liste der verfügbaren Eingabespalten. Ordnen Sie die Eingabespalten per Drag & Drop den verfügbaren Zielspalten zu.  
  
#### <a name="available-destination-columns"></a>Verfügbare Zielspalten  
 Die Liste der verfügbaren Zielspalten. Ordnen Sie die Zielspalten per Drag & Drop den verfügbaren Eingabespalten zu.  
  
#### <a name="input-column"></a>Eingabespalte  
 Zeigt die von Ihnen ausgewählten Eingabespalten an. Sie können Zuordnungen entfernen, indem Sie **\<ignore>** auswählen, um Spalten aus der Ausgabe auszuschließen.  
  
#### <a name="destination-column"></a>Zielspalte  
 Zeigt alle verfügbaren Zielspalten an, sowohl die zugeordneten als auch die nicht zugeordneten.  
  
## <a name="odbc-destination-editor-error-output-page"></a>Ziel-Editor für ODBC (Seite "Fehlerausgabe")
  Auf der Seite **Fehlerausgabe** des Dialogfelds **Ziel-Editor für ODBC** können Sie Optionen für die Fehlerbehandlung auswählen.  
  
 **So öffnen Sie die Seite "Fehlerausgabe" des Ziel-Editors für ODBC**  
  
### <a name="task-list"></a>Aufgabenliste  
  
-   Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das das ODBC-Ziel enthält.  
  
-   Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das ODBC-Ziel.  
  
-   Klicken Sie im **Ziel-Editor für ODBC**auf **Fehlerausgabe**.  
  
### <a name="options"></a>enthalten  
  
#### <a name="inputoutput"></a>Eingabe/Ausgabe  
 Zeigt den Namen der Datenquelle an.  
  
#### <a name="column"></a>Column  
 Wird nicht verwendet.  
  
#### <a name="error"></a>Fehler  
 Wählen Sie aus, wie das ODBC-Ziel Fehler in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
#### <a name="truncation"></a>Abschneiden  
 Wählen Sie aus, wie das ODBC-Ziel Kürzungen in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
#### <a name="description"></a>Description  
 Zeigt eine Beschreibung des Fehlers an.  
  
#### <a name="set-this-value-to-selected-cells"></a>Diesen Wert für ausgewählte Zellen festlegen  
 Wählen Sie aus, wie das ODBC-Ziel im Fall eines Fehlers oder einer Kürzung mit den ausgewählten Zellen verfahren soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
#### <a name="apply"></a>Anwenden  
 Wendet die Fehlerbehandlungsoptionen auf die ausgewählten Zellen an.  
  
### <a name="error-handling-options"></a>Fehlerbehandlungsoptionen  
 Mit den folgenden Optionen konfigurieren Sie, wie das ODBC-Ziel Fehler und Kürzungen behandelt.  
  
#### <a name="fail-component"></a>Fehler bei Komponente  
 Bei einem Fehler oder beim Abschneiden von Daten wird der Datenflusstask nicht ausgeführt. Dies ist das Standardverhalten.  
  
#### <a name="ignore-failure"></a>Fehler ignorieren  
 Der Fehler oder die Kürzung wird ignoriert.  
  
#### <a name="redirect-flow"></a>Zeile umleiten  
 Die Zeile, die den Fehler oder die Kürzung verursacht, wird an die Fehlerausgabe des ODBC-Ziels umgeleitet. Weitere Informationen finden Sie unter "ODBC-Ziel".  
  
