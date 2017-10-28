---
title: "Regeln für das Eingeben von Suchwerten (Visual Database Tools) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time [SQL Server], searches
- date searches
- dates [SQL Server], searches
- embedding apostrophes [SQL Server]
- logical value searches [SQL Server]
- case-sensitive search matches
- search criteria [SQL Server], rules
- text value searches [SQL Server]
- numeric value searches [SQL Server]
ms.assetid: 3c8134b7-83f4-41b4-99c8-e3949a685ff5
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 96cd179445fcab211321ccf4e89f6fbce5792230
ms.contentlocale: de-de
ms.lasthandoff: 08/18/2017

---
# <a name="rules-for-entering-search-values-visual-database-tools"></a>Regeln für das Eingeben von Suchwerten (Visual Database Tools)
In diesem Thema werden die Konventionen erläutert, die beim Eingeben der folgenden Arten von Literalwerten für eine Suchbedingung beachtet werden müssen:  
  
-   Textwerte  
  
-   Numerische Werte  
  
-   Datumsangaben  
  
-   Logische Werte  
  
> [!NOTE]  
> Die Informationen in diesem Thema leiten sich aus den Regeln für Standard-SQL-92 ab. Datenbanken können SQL jedoch auf unterschiedliche Art implementieren. Die hier angezeigten Richtlinien sind daher nicht in jedem Fall gültig. Informationen zum Eingeben von Suchwerten in einer bestimmten Datenbank erhalten Sie in der Dokumentation zur verwendeten Datenbank.  
  
## <a name="searching-on-text-values"></a>Suchen von Textwerten  
Die folgenden Richtlinien gelten für die Eingabe von Textwerten in Suchbedingungen:  
  
-   **Anführungszeichen** Schließen Sie Textwerte in einfache Anführungszeichen ein, wie in diesem Beispiel für einen Nachnamen:  
  
    ```  
    'Smith'  
    ```  
  
    Wenn Sie eine Suchbedingung im [Kriterienbereich](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)eingeben, müssen Sie nur den Textwert eingeben, woraufhin der Abfrage- und Sicht-Designer diesen automatisch in einfache Anführungszeichen einschließt.  
  
    > [!NOTE]  
    > In einigen Datenbanken werden Begriffe in einfachen Anführungszeichen als Literalwerte interpretiert, wohingegen Begriffe in doppelten Anführungszeichen als Datenbankobjekte wie Spalten- oder Tabellenverweise interpretiert werden. Daher ist es möglich, dass der Abfrage- und Sicht-Designer die Begriffe in doppelten Anführungszeichen zwar akzeptiert, sie jedoch nicht wie erwartet interpretiert.  
  
-   **Einbetten von Apostrophen** Wenn die gesuchten Daten ein einzelnes Anführungszeichen (ein Apostroph) enthalten, können Sie mit zwei einzelnen Anführungszeichen kennzeichnen, dass dieses einzelne Anführungszeichen als Literalwert und nicht als Trennzeichen verwendet werden soll. Mit der folgenden Bedingung suchen Sie z. B. nach dem Wert "Swann's Way":  
  
    ```  
    ='Swann''s Way'  
    ```  
  
-   **Längenbegrenzung** Beachten Sie bei der Eingabe langer Zeichenfolgen die zulässige Höchstlänge für die SQL-Anweisung bei der verwendeten Datenbank.  
  
-   **Groß- und Kleinschreibung** Beachten Sie die Regeln für die Groß- und Kleinschreibung der verwendeten Datenbank. Die verwendete Datenbank bestimmt, ob bei Textsuchen die Groß- und Kleinschreibung beachtet werden muss. In einigen Datenbanken muss beim Operator "=" die Groß- und Kleinschreibung beachtet werden, während in anderen auch Kombinationen von groß und klein geschriebenen Zeichen zulässig sind.  
  
    Wenn Sie nicht wissen, ob in der verwendeten Datenbank die Groß- und Kleinschreibung beachtet wird, können Sie mit den UPPER- oder LOWER-Funktionen in der Suchbedingung, wie im folgenden Beispiel gezeigt, die Großschreibung der Suchdaten in Kleinschreibung konvertieren und umgekehrt:  
  
    ```  
    WHERE UPPER(lname) = 'SMITH'  
    ```  
  
## <a name="searching-on-numeric-values"></a>Suchen von numerischen Werten  
Die folgenden Richtlinien gelten für die Eingabe von numerischen Werten in Suchbedingungen:  
  
-   **Anführungszeichen** Zahlen dürfen nicht in Anführungszeichen eingeschlossen werden.  
  
-   **Nicht numerische Zeichen** Fügen Sie keine nicht numerischen Zeichen außer dem dezimalen Trennzeichen (wie in der Windows-Systemsteuerung im Dialogfeld **Ländereinstellungen** definiert) und dem negativen Vorzeichen (-) ein. Fügen Sie keine Zeichen für das Gruppieren von Ziffern (z. B. einen Punkt zwischen Tausendergruppen) oder Währungssymbole ein.  
  
-   **Dezimalzeichen** Wenn Sie ganze Zahlen eingeben, können Sie ein Dezimalzeichen einfügen, um zu kennzeichnen, ob es sich bei diesem Wert um eine ganze oder um eine reelle Zahl handelt.  
  
-   **Wissenschaftliche Schreibweise** Sie können sehr große oder kleine Zahlen wie im folgenden Beispiel mit der wissenschaftlichen Schreibweise eingeben:  
  
    ```  
    > 1.23456e-9  
    ```  
  
## <a name="searching-on-dates"></a>Suchen von Datumsangaben  
Das für die Eingabe von Daten zu verwendende Format hängt von der Datenbank und dem Bereich des Abfrage- und Sicht-Designers ab, in dem Sie diese eingeben.  
  
> [!NOTE]  
> Falls Sie nicht wissen, welches Format Ihre Datenquelle verwendet, geben Sie in der Filterzeile des Kriterienbereichs ein Datum in einem Ihnen vertrauten Format ein. Der Designer solche Einträge in den meisten Fällen in das geeignete Format konvertieren.  
  
Im Abfrage- und Sicht-Designer können die folgenden Datumsformate verwendet werden:  
  
-   **Gebietsschemaspezifisch** Das für Datumsangaben in den Einstellungen im Windows-Dialogfeld **Region** festgelegte Format.  
  
-   **Datenbankspezifisch** Jedes von der Datenbank akzeptierte Format.  
  
-   **ANSI-Standarddatum** Ein Format, bei dem wie im folgenden Beispiel geschweifte Klammern, die Markierung „d“ zum Kennzeichnen des Datums und eine Datumszeichenfolge verwendet werden:  
  
    ```  
    { d '1990-12-31' }  
    ```  
  
-   **ANSI-Standarddatum/-uhrzeit** Dies entspricht dem ANSI-Standarddatum, wobei aber „ts“ anstelle von „d“ verwendet wird und Stunden, Minuten und Sekunden zum Datum hinzugefügt werden (im 24-Stundenformat), wie im folgenden Beispiel für den 31. Dezember 1990 gezeigt:  
  
    ```  
    { ts '1990-12-31 00:00:00' }  
    ```  
  
    Im Allgemeinen wird das ANSI-Standarddatenformat bei Datenbanken verwendet, in denen Daten mit einem True-Date-Datentyp dargestellt werden. Im Gegensatz dazu wird das Datetime-Format bei Datenbanken verwendet, die den Datetime-Datentyp unterstützen.  
  
In der folgenden Tabelle werden die Datumsformate aufgeführt, die Sie in den verschiedenen Bereichen des Abfrage- und Sicht-Designers verwenden können.  
  
|**Bereich**|**Datumsformat**|  
|------------|-------------------|  
|Kriterien|Gebietsschemaspezifisch? Datenbankspezifisch? ANSI-Standard<br /><br />Die im [Kriterienbereich](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) eingegebenen Datumsangaben werden im SQL-Bereich in ein datenbankkompatibles Format konvertiert.|  
|SQL|Datenbankspezifisch? ANSI-Standard|  
|Ergebnisse|Gebietsschemaspezifisch|  
  
## <a name="searching-on-logical-values"></a>Suchen von logischen Werten  
Das Format logischer Daten ist in den einzelnen Datenbanken unterschiedlich. In vielen Fällen wird der Wert False als Null (0) gespeichert. Der Wert True wird häufig als 1 und in bestimmten Fällen auch als -1 gespeichert Die folgenden Richtlinien gelten für die Eingabe von logischen Werten in Suchbedingungen:  
  
-   Verwenden Sie zum Suchen des Werts False wie im folgenden Beispiel dargestellt eine 0:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 0  
    ```  
  
-   Wenn Sie nicht genau wissen, welches Format Sie für die Suche eines Werts True verwenden sollen, versuchen Sie es wie im folgenden Beispiel mit dem Wert 1:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 1  
    ```  
  
-   Sie können den Gültigkeitsbereich der Suche erweitern, indem Sie nach allen Werten suchen, die nicht 0 sind, wie im folgenden Beispiel dargestellt:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract <> 0  
    ```  
  
## <a name="see-also"></a>Siehe auch  
[Angeben von Suchkriterien &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

