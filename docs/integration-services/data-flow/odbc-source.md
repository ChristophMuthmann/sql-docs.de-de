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
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fa8fcf2545618602bcf9f574a52ba51d0074a850
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

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
  
 Weitere Informationen finden Sie in einem der folgenden Themen:  
  
-   [Quellen-Editor für ODBC &#40; Seite Verbindungs-Manager &#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)  
  
-   [Quellen-Editor für ODBC &#40; Seite "Spalten" &#41;](../../integration-services/data-flow/odbc-source-editor-columns-page.md)  
  
-   [Quellen-Editor für ODBC &#40; Seite "Fehlerausgabe" Fehler &#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können.  
  
 So öffnen Sie das Dialogfeld **Erweiterter Editor** :  
  
-   Klicken Sie auf dem Bildschirm **Datenfluss** des [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Projekts mit der rechten Maustaste auf die ODBC-Quelle, und wählen Sie **Erweiterten Editor anzeigen**.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld Erweiterter Editor festlegen können, finden Sie unter [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Quellen-Editor für ODBC &#40; Seite "Fehlerausgabe" Fehler &#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
-   [Quellen-Editor für ODBC &#40; Seite "Spalten" &#41;](../../integration-services/data-flow/odbc-source-editor-columns-page.md)  
  
-   [Quellen-Editor für ODBC &#40; Seite Verbindungs-Manager &#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)  
  
-   [Extrahieren von Daten mithilfe der ODBC-Quelle](../../integration-services/data-flow/extract-data-by-using-the-odbc-source.md)  
  
-   [Benutzerdefinierte Eigenschaften der ODBC-Quelle](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
  
