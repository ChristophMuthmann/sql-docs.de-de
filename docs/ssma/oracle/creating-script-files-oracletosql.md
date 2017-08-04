---
title: Erstellen von Skriptdateien (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Script File Creation, Configuring Oracle Console Settings
- Script File Creation, Non-Configurable option
- Script File Creation, Script File Validation
ms.assetid: 55e5bc68-3040-4f07-bb00-0408a17c9821
caps.latest.revision: 37
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7fb3f2390d27d89877ed57b50da5e40da95e2c3b
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="creating-script-files-oracletosql"></a>Erstellen von Skriptdateien (OracleToSQL)
Der erste Schritt vor dem Starten SSMA-Konsolenanwendung auf die Skriptdatei erstellt wird und bei Bedarf den Wert der Variablen-Datei und die Server-Verbindung erstellen.  
  
Die Skriptdatei kann begrenzt in drei Abschnitte unterteilt werden..,:  
  
1.  **Config:** ermöglicht es dem Benutzer die Konfigurationsparameter für die Konsolenanwendung festlegen.  
  
2.  **Server:** ermöglicht es dem Benutzer, das Quell-/Ziel Serverdefinitionen festzulegen. Dies kann auch in einem separaten Server-Verbindungsdatei sein.  
  
3.  **Befehle des Skripts:** ermöglicht es dem Benutzer SSMA Workflowbefehle ausführen.  
  
Jeder Abschnitt ist im folgenden ausführlich beschrieben:  
  
## <a name="configuring-oracle-console-settings"></a>Konfigurieren von Einstellungen der Oracle-Konsole  
Die Konfigurationen eines Skripts werden in der Skriptdatei für die Konsole angezeigt.  
  
Wenn eines der Elemente im Knoten "Konfiguration" angegeben werden, sind sie festgelegt als globale Einstellung d. h. sie gelten für alle Befehle des Skripts. Zu diesen Konfigurationselementen können auch festgelegt werden innerhalb jeder Befehl in der Skriptbefehl Abschnitt, wenn der Benutzer möchte die globale Einstellung außer Kraft setzen.  
  
BenutzerKonfigurierbar-Optionen:  
  
1.  **Anbieter der Ausgabe-Fenster:** Wenn unterdrücken Nachrichten Attribut festgelegt ist, auf "true", die befehlsspezifische Nachrichten werden nicht in der Konsole angezeigt abrufen. Attribute werden im folgenden beschrieben:  
  
    -   Ziel: Gibt an, ob die Ausgabe in einer Datei oder "stdout" gedruckt abrufen muss. Dies ist standardmäßig "false".  
  
    -   Dateiname: der Pfad der Datei (Optional).  
  
    -   Unterdrücken Sie Nachrichten: Nachrichten in der Konsole unterdrückt. Dies ist standardmäßig "false".  
  
    **Beispiel:**  
  
    ```xml  
    <output-providers>  
  
      <output-window  
  
        suppress-messages="<true/false>"   (optional)  
  
        destination="<file/stdout>"        (optional)  
  
        file-name="<file-name>"            (optional)  
  
       />  
  
    </output-providers>  
    ```  
    *oder*  
  
    ```xml  
    <…All commands…>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </…All commands…>  
    ```  
  
2.  **Verbindungsanbieter des Daten-Migration:** Dies gibt an, welche Quell-/Zielelement-Server ist bei der Migration Daten berücksichtigt werden.  Source-Verwendung – zuletzt verwendete gibt an, dass die letzte verwendete Quellserver für die Datenmigration verwendet wird. Ziel-Verwendung – zuletzt verwendete gibt ebenso an, dass der zuletzt verwendeten Zielserver für die Datenmigration verwendet wird. Der Benutzer kann auch die Möglichkeit, den Server (Quelle oder Ziel) angeben, mit der Attribute-Quellserver oder Zielserver.  
  
    D. h. kann nur ein oder anderen angegebenen Attributs verwendet werden:  
  
    -   Source-Verwendung – zuletzt verwendete = "Wahr" (Standard) oder die Quellserver = "Source_servername"  
  
    -   Ziel-Verwendung – zuletzt verwendete = "Wahr" (Standard) oder Ziel-Server = "Target_servername"  
  
    **Beispiel:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection source-use-last-used="true"  
  
                                 target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *oder*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **Benutzer Eingabe Popup:** dadurch Behandlung von Fehlern, die Objekte aus der Datenbank geladen werden. Der Benutzer die Eingabe Modi, und im Falle eines Fehlers die Konsole wird fortgesetzt, wie Benutzer angibt.  
  
    Die Modi sind:  
  
    -   **Bitten Sie Benutzer –** fordert den Benutzer auf continue('yes') oder Fehler ausgegeben ("No").  
  
    -   **Fehler –** die Konsole zeigt einen Fehler an und hält die Ausführung an.  
  
    -   **weiterhin-** die Konsole mit der Ausführung wird fortgesetzt.  
  
    Der Standardmodus ist **Fehler**.  
  
    **Beispiel:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *oder*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **Verbinden Sie die Anbieter:** Dies ermöglicht es dem Benutzer festzulegende Einstellungen zuzulassen, falls die erneute Verbindung der Verbindungsfehler. Dies kann für die Quell-und Zielserver festgelegt werden.  
  
    Die erneute Verbindung Modi sind:  
  
    -   Verbinden und letzten-verwendet-Server: Wenn die Verbindung nicht aktiv ist, versucht wird, bis zum letzten darf höchstens 5-Mal verwendeten Server zu verbinden.  
  
    -   generiert einen Fehler: Wenn die Verbindung nicht aktiv ist, wird ein Fehler generiert.  
  
    Der Standardmodus ist **generieren einen Fehler**.  
  
    **Beispiel:**  
  
    ```xml  
    <output-providers>  
  
      <reconnect-manager on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                         on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *oder*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *oder*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="<target-server-unique-name>">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **Konverter überschreiben Anbieter:** Dadurch kann der Benutzer Objekte zu behandeln, die bereits auf dem Zielgerät vorhanden sind Metabase. Die möglichen Aktionen zählen:  
  
    -   Fehler: die Konsole zeigt einen Fehler an und hält die Ausführung an.  
  
    -   Überschreiben: überschreibt vorhandene Werte des Objekts. Standardmäßig ist diese Aktion erfolgt.  
  
    -   Überspringen: die Konsole überspringt die Objekte, die bereits vorhanden für die Datenbank  
  
    -   Bitten Sie Benutzer: fordert den Benutzer zur Eingabe ("yes" / "Nein")  
  
    **Beispiel:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *oder*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **Fehlerhafte Voraussetzungen-Anbieter:** Dadurch kann der Benutzer, alle erforderlichen Komponenten zu behandeln, die für die Verarbeitung eines Befehls erforderlich sind. Standardmäßig ist der strict-Modus 'false'. Wenn sie festgelegt ist, auf "true", eine Ausnahme generiert für die Voraussetzungen erfüllt.  
  
    **Beispiel:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **Der Beendigungsvorgang:** während des Mid-Vorgangs, ob der Benutzer möchte, klicken Sie dann den Vorgang Abbrechen **"STRG + C"** Hotkey verwendet werden kann. SSMA für die Oracle-Konsole zum Abschließen des Vorgangs wartet, und beendet die Ausführung der Konsole.  
  
    Wenn der Benutzer die Ausführung dann sofort beenden möchte **"STRG + C"** Hotkey für abrupten Beendigung der Anwendung SSMA-Konsole erneut gedrückt werden kann.  
  
8.  **Status-Anbieter:** den Status der einzelnen Datenbankkonsistenzprüfer informiert. Dies ist standardmäßig deaktiviert. Die Attribute statuserfassung umfassen:  
  
    -   off  
  
    -   Alle %1  
  
    -   alle %2%  
  
    -   EVERY - 5 %  
  
    -   alle %10  
  
    -   EVERY - 20 %  
  
    **Beispiel:**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"            (optional)  
  
                          report-messages="<true/false>"   (optional)  
  
                          report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off" (optional)/>  
  
    </output-providers>  
    ```  
    *oder*  
  
    ```xml  
    <…All commands…>  
  
      <progress-reporting  
  
        enable="<true/false>"            (optional)  
  
        report-messages="<true/false>"   (optional)  
  
        report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off"     (optional)/>  
  
    </…All commands…>  
    ```  
  
9. **Ausführlichkeit der Protokollierung:** legt Ausführlichkeit Protokollebene. Dies entspricht der Option alle Kategorien in der Benutzeroberfläche. Standardmäßig ist die Protokollebene für die Ausführlichkeit "Error".  
  
    Die Protokollierung auf den Optionen gehören:  
  
    -   Schwerwiegender Fehler: Nachrichten, die nur schwerwiegende Fehler protokolliert werden.  
  
    -   Fehler: nur Fehler und schwerwiegende Fehlermeldungen werden protokolliert.  
  
    -   Warnung: alle Ebenen außer Debug- und Info Meldungen werden protokolliert.  
  
    -   Info: alle Ebenen außer der Debugmeldungen protokolliert werden.  
  
    -   Debuggen: alle Ebenen der Nachrichten protokolliert.  
  
    > [!NOTE]  
    > Obligatorische Nachrichten werden auf jeder Ebene protokolliert.  
  
    **Beispiel:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *oder*  
  
    ```xml  
    <…All commands…>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </…All commands…>  
    ```  
  
10. **Außerkraftsetzung verschlüsselte Kennwort:** 'true', das Klartextkennwort angegebene im Abschnitt Definition Server, der die Server-Verbindungsdatei oder in der Skriptdatei überschreibt das verschlüsselte Kennwort gespeichert, die im Speicher geschützt, wenn vorhanden ist. Falls kein Kennwort in Klartext angegeben ist, wird der Benutzer aufgefordert, das Kennwort eingeben.  
  
    Hier entstehen zwei Fällen:  
  
    1.  Wenn Option überschreiben ist **"false"**, die Reihenfolge der Suche werden geschützte Speicher -&gt;Skript-Datei -&gt;Server Verbindung Datei -&gt; Benutzer auffordern.  
  
    2.  Wenn Option überschreiben ist **"true"**, die Reihenfolge der Suche werden Skript-Datei -&gt;Server Verbindung Datei -&gt;Benutzer auffordern.  
  
    **Beispiel:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
Nicht konfigurierbare Option ist:  
  
-   **Maximale Verbindungswiederherstellungsversuchen:** bei eine bereits eingerichteten Verbindung ein Timeout oder aufgrund von Netzwerkfehlern unterbricht, der Server ist erforderlich, um die Verbindung hergestellt werden. Der erneuten Herstellen einer Verbindung versucht dürfen maximal **5** Wiederholungen nach, die die Konsole wird automatisch beim erneuten Verbindungsversuch ausgeführt. Die Einrichtung der automatischen erneuten Herstellen einer Verbindung wird der Aufwand bei der erneuten Ausführen des Skripts reduziert.  
  
## <a name="server-connection-parameters"></a>Server-Verbindungsparameter  
Server-Verbindungsparameter können in der Skriptdatei oder in der Datei der Server-Verbindung definiert werden. Finden Sie in der [erstellen, die Server-Connection-Dateien &#40; OracleToSQL &#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) Abschnitt, um weitere Details.  
  
## <a name="script-commands"></a>Skriptbefehle  
Die Skriptdatei enthält eine Sequenz von Migration Workflowbefehle in das XML-Format. Die SSMA-Konsolenanwendung verarbeitet die Migration in der Reihenfolge der Befehle, die angezeigt werden, in der Skriptdatei an.  
  
Eine typische Datenmigration, der eine bestimmte Tabelle in einer Oracle-Datenbank folgt z. B. die Hierarchie der: Schema -&gt; Tabelle.  
  
Wenn alle Befehle in der Skriptdatei erfolgreich ausgeführt werden, wird die SSMA-Konsolenanwendung beendet und das Steuerelement an den Benutzer zurückgegeben. Den Inhalt einer Skriptdatei sind mehr oder weniger statisch mit Variableninformationen enthalten entweder in einem [Variable-Wert-Dateien erstellen &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md) oder in einem separaten Abschnitt innerhalb der Skriptdatei für Variablenwerte.  
  
**Beispiel:**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="<project-folder>"  
  
                        project-name="<project-name>"  
  
                        overwrite-if-exists="<true/false>"/>  
  
    <connect-source-database server="<source-server-unique-name>"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
Vorlagen 3 Skriptdateien (zum Ausführen von verschiedenen Szenarios), bestehend aus Variablenwert-Datei und einer Server-Verbindung werden in der Konsole Beispielskripts-Ordner des Verzeichnisses Produkt bereitgestellt:  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
Sie können Vorlagen (Dateien) ausgeführt wird, nachdem eine Änderung der Parameter für Relevanz darin angezeigt.  
  
Vollständige Liste der Befehle des Skripts befinden sich im [Ausführen der Konsole SSMA &#40; OracleToSQL &#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="script-file-validation"></a>Skript-Dateiüberprüfung  
Benutzer kann problemlos überprüfen Benutzervoreinstellung Skriptdatei anhand der Schemadefinitionsdatei **"O2SSConsoleScriptSchema.xsd"** in den Ordner "Schemas" verfügbar.  
  
## <a name="next-step"></a>Nächster Schritt  
Im nächsten Schritt in der Konsole Betrieb [erstellen Variable Wertdateien &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen Variablenwert Dateien &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  

