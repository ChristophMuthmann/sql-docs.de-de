---
title: "Ausführen der Konsole SSMA (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Database Connection Commands
- Sybase Console,Manageability Commands
- Sybase Console,Migration Commands
- Sybase Console,Migration Preparation Command
- Sybase Console,Project Commands
- Sybase Console,Report Commands
- Sybase Console,Script File Commands
- Sybase Console,Script Generation Commands
ms.assetid: ea8950b7-fabc-4aa4-89f8-9573a2617d70
caps.latest.revision: 22
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0df634087870db32ed0357c97b1211d4fc1ddcba
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="executing-the-ssma-console-sybasetosql"></a>Ausführen der Konsole SSMA (SybaseToSQL)
Microsoft stellt Ihnen Dateibefehle auszuführen und zu steuern SSMA Aktivitäten eine Reihe robuster Skript. In den folgenden Abschnitten ausführlich identisch.  
  
## <a name="script-file-commands"></a>Datei-Skriptbefehle  
Die Konsolenanwendung verwendet bestimmte Standardskripts Dateibefehle als aufgezählte in diesem Abschnitt.  
  
## <a name="project-commands"></a>Projekt-Befehle  
Das Handle des Projekt Befehle, die beim Erstellen von Projekten, öffnen, speichern und Beenden von Projekten.  
  
### <a name="create-new-project"></a>erstellen – Neues Projekt  
Erstellt ein neues SSMA-Projekt  
  
-   `project-folder`Gibt den Ordner, der das erste erstellte Projekt an.  
  
-   `project-name`Gibt den Namen des Projekts an. {String}  
  
-   `overwrite-if-exists`Optionales Attribut gibt an, ob ein vorhandenes Projekt überschrieben werden soll. {Boolean}  
  
-   `project-type:`Optionales Attribut. Gibt an, das Projekttyp z. B. "Sql Server 2005" Project oder Project "Sql Server 2008" oder "Sql Server 2012" Projekt oder "Sql Server 2014" Projekt oder "Sql Azure". Standardwert ist "Sql Server 2008".  
  
**Beispiel:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type=”<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>”  
/>  
```  
Attribut "überschreiben-If-exists" ist **"false"** standardmäßig.  
  
Attribut "Projekttyp" ist **Sql Server 2008** standardmäßig.  
  
### <a name="open-project"></a>Open-Projekt  
  
-   `project-folder`Gibt den Ordner, der das erste erstellte Projekt an. Der Befehl schlägt fehl, wenn der angegebene Ordner nicht vorhanden ist.  {String}  
  
-   `project-name`Gibt den Namen des Projekts an. Der Befehl schlägt fehl, wenn das angegebene Projekt nicht vorhanden ist.  {String}  
  
**Syntaxbeispiel:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA für Sybase-Konsolenanwendung unterstützt Abwärtskompatibilität. Sie werden können zum Öffnen von Projekten, die von der früheren Version von SSMA erstellt.  
  
### <a name="save-project"></a>Save-Projekt  
Speichert das Migrationsprojekt  
  
**Syntaxbeispiel:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>Close-Projekt  
Schließt das Migrationsprojekt  
  
**Syntaxbeispiel:**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
'If-modified'-Attribut ist optional, **ignorieren** standardmäßig.  
  
## <a name="database-connection-commands"></a>Datenbank-Verbindungsbefehle  
Die Verbindung mit Datenbank-Befehle können mit der Datenbank herstellen.  
  
> [!NOTE]  
> 1.  Die **Durchsuchen** Features der Benutzeroberfläche wird in der Konsole nicht unterstützt.  
> 2.  Weitere Informationen zu "Skriptdateien erstellen", finden Sie unter [Skriptdateien erstellen &#40; SybaseToSQL &#41; ](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
### <a name="connect-source-database"></a>Verbinden-Quelldatenbank  
  
-   Führt die Verbindung mit der Quelldatenbank und lädt hohe Ebene Metadaten von der Quelldatenbank, aber nicht alle Metadaten.  
  
-   Wenn die Verbindung mit der Datenquelle hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter  
  
Das Name-Attribut für jede Verbindung im Server-Abschnitt des Server-Verbindungsdatei oder die Skriptdatei definiert ist Serverdefinition entnommen.  
  
**Syntaxbeispiel:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>Force-Load-/ Ziel-Quelldatenbank  
  
-   Lädt die Quellmetadaten an.  
  
-   Für die Arbeit auf offline-Migrationsprojekts nützlich.  
  
-   Wenn die Verbindung mit den Quell-/Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter  
  
Ist eine oder mehrere Metabase-Knoten als-Befehlszeilenparameter erforderlich.  
  
**Syntaxbeispiel:**  
  
```xml  
<force-load metabase=”<source/target>” >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>Schließen Sie Quelldatenbank  
  
-   Verbindung mit der Quelldatenbank, aber keine Metadaten im Gegensatz zu den Befehl Connect Quelldatenbank wird nicht geladen.  
  
-   Herstellen der Verbindung mit der Datenquelle hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Syntaxbeispiel:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>Verbinden-Zieldatenbank  
  
-   Eine Verbindung mit SQL Server-Zieldatenbank her und lädt vollständig hohe Ebene Metadaten der Zieldatenbank, aber nicht die Metadaten.  
  
-   Wenn die Verbindung mit dem Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
Das Name-Attribut für jede Verbindung im Server-Abschnitt des Server-Verbindungsdatei oder die Skriptdatei definiert ist Serverdefinition entnommen.  
  
**Syntaxbeispiel:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>Schließen Sie Zieldatenbank  
  
-   Erneut mit der Zieldatenbank, aber keine Metadaten, im Gegensatz zu den Befehl Connect der Zieldatenbank wird nicht geladen.  
  
-   Herstellen der Verbindung mit dem Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Syntaxbeispiel:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>Berichtsbefehle  
Die Berichtsserver-Befehle Generieren von Berichten auf die Leistung der verschiedenen SSMA-konsolenaktivitäten.  
  
### <a name="generate-assessment-report"></a>Generieren von Bewertungsbericht  
  
-   Assessment-Berichte in der Quelldatenbank generiert.  
  
-   Wenn die Verbindung mit der Quelldatenbank nicht ausgeführt werden, bevor Sie diesen Befehl ausführen, wird ein Fehler generiert, und die Konsolenanwendung beendet.  
  
-   Während der Ausführung des Befehls eine Verbindung mit dem Datenbankserver auch führt dies in der Konsolenanwendung beendet.  
  
-   `conversion-report-folder:`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
-   `object-name:`Gibt an, die Objekte, die zur Bewertung berichterstellung (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt besitzen) betrachtet.  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `conversion-report-overwrite:`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-summary-report-to:`Gibt den Pfad, in dem der Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **AssessmentReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
**Syntaxbeispiel:**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>”             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
oder  
  
```xml  
<generate-assessment-report  
  
  assessment-report-folder="<folder-name>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
<metabase-object object-name="<object-name>"  
  
        object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-commands"></a>Migration-Befehle  
Die Befehle für die Migration konvertieren das Schema der Zieldatenbank, die dem Quellschema und Migrieren von Daten auf dem Zielserver.  
  
### <a name="convert-schema"></a>Convert-schema  
  
-   Schemakonvertierung von der Quelle in das Zielschema durchgeführt.  
  
-   Wenn die Verbindung mit der Quelle oder Ziel wird nicht ausgeführt, bevor Sie diesen Befehl ausführen, oder die Verbindung mit dem Datenbankserver Quell- oder Zieltabelle, die während der Ausführung des Befehls Fehler auftreten, wird ein Fehler generiert, und die Konsolenanwendung beendet wird.  
  
-   `conversion-report-folder:`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
-   `object-name:`Gibt die Quelle-Objekte, die für das Konvertieren eines Schemas (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt haben) in Betracht gezogen.  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `conversion-report-overwrite:`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-summary-report-to:`Gibt den Pfad, in dem der zusammenfassende Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **SchemaConversionReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
**Syntaxbeispiel:**  
  
```xml  
<convert-schema  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  write-summary-report-to="<file-name/folder-name>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder-name>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
oder  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>Migrieren von Daten  
Migriert die Quelldaten zum Ziel.  
  
-   `object-name:`Gibt die Quelle-Objekte, die für die Migration in Betracht gezogen Daten (es kann haben Indivdual Objektnamen oder einen Gruppennamen-Objekt).  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `write-summary-report-to:`Gibt den Pfad, in dem der Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **DataMigrationReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
**Syntaxbeispiel:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>">  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
oder  
  
```xml  
<migrate-data  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>Migration Vorbereitung-Befehl  
Die Vorbereitung der Migration-Befehl startet schemazuordnung zwischen den Quell- und Zieldatenbanken.  
  
> [!NOTE]  
> Die Standard-Konsolenausgabe festlegen, für die Migration Befehle ist 'Full' Ausgabebericht mit keine ausführliche-Fehlerberichterstattung: nur Zusammenfassung am Stammknoten Quell-Objekt.  
  
### <a name="map-schema"></a>Map-schema  
Schemazuordnung der Quelldatenbank mit dem Zielschema.  
  
-   `source-schema`Gibt das Quellschema, das wir migrieren möchten.  
  
-   `sql-server-schema`Gibt das Zielschema, in dem wir migriert werden soll.  
  
**Syntaxbeispiel:**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>Verwaltbarkeit Befehle  
Die Verwaltbarkeit Befehle können mit der Quelldatenbank Zielobjekte Datenbank zu synchronisieren.  
  
> [!NOTE]  
> Die Standard-Konsolenausgabe festlegen, für die Migration Befehle ist 'Full' Ausgabebericht mit keine ausführliche-Fehlerberichterstattung: nur Zusammenfassung am Stammknoten Quell-Objekt.  
  
### <a name="synchronize-target"></a>Synchronisieren von Ziel  
  
-   Synchronisiert die Zielobjekte mit der Zieldatenbank an.  
  
-   Wenn Sie diesen Befehl für die Quelldatenbank ausgeführt wird, ist ein Fehler aufgetreten.  
  
-   Wenn die Verbindung mit der Zieldatenbank wird nicht ausgeführt, bevor Sie diesen Befehl ausführen oder die Verbindung mit dem Zielserver für die Datenbank ein Fehler auftritt, während der Ausführung des Befehls, wird ein Fehler generiert, und die Konsolenanwendung beendet.  
  
-   `object-name:`Gibt an, die Ziel-Objekte, die für die Synchronisierung mit der Zieldatenbank (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt besitzen) betrachtet.  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `on-error:`Gibt an, ob die Synchronisierungsfehler als Warnungen oder Fehler angegeben. Verfügbare Optionen für auf Fehler:  
  
    -   Bericht insgesamt als Warnung  
  
    -   Bericht-each-als-Warnung  
  
    -   Fail-Skript  
  
-   `report-errors-to:`Speicherort der Fehlerbericht angibt, für der Synchronisierungsvorgang (optionales Attribut), wenn nur Ordnerpfad angegeben ist, dann Datei namentlich **TargetSynchronizationReport.XML** wird erstellt.  
  
**Syntaxbeispiel:**  
  
```xml  
<synchronize-target  
  
object-name="<object-name>"  
  
on-error="<report-total-as-warning/  
  
report-each-as-warning/  
  
fail-script>" (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
oder  
  
```xml  
<synchronize-target  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
oder  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
  
### <a name="refresh-from-database"></a>Aktualisieren von Datenbank  
  
-   Aktualisiert die Datenquelle Objekte aus der Datenbank.  
  
-   Wenn Sie diesen Befehl für die Zieldatenbank ausgeführt wird, wird ein Fehler generiert.  
  
Ist eine oder mehrere Metabase-Knoten als-Befehlszeilenparameter erforderlich.  
  
-   `object-name:`Gibt die Quelle-Objekte, die beim Aktualisieren von der Quelldatenbank (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt haben) in Betracht gezogen.  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `on-error:`Gibt an, ob die Aktualisierung Fehler als Warnungen oder Fehler angegeben. Verfügbare Optionen für auf Fehler:  
  
    -   Bericht insgesamt als Warnung  
  
    -   Bericht-each-als-Warnung  
  
    -   Fail-Skript  
  
-   `report-errors-to:`Speicherort der Fehlerbericht angibt, für der Aktualisierungsvorgang (optionales Attribut) Wenn nur Ordnerpfad angegeben ist, klicken Sie dann Datei namentlich **SourceDBRefreshReport.XML** wird erstellt.  
  
**Syntaxbeispiel:**  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  on-error="<report-total-as-warning/  
  
             report-each-as-warning/  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
oder  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
oder  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>Befehle des Skripts generieren  
Die Befehle Skriptgenerierung zwei Aufgaben ausführen: sie helfen bei der speichern die Konsolenausgabe in einer Skriptdatei; und zeichnen Sie die T-SQL-Ausgabe in der Konsole oder eine Datei basierend auf dem von Ihnen angegebenen Parameter.  
  
### <a name="save-as-script"></a>"Save-als-Script"  
Zum Speichern von den Skripts für die Objekte in einer Datei, wenn erwähnt Metabasis = Ziel, dies ist eine Alternative zum Synchronisationsbefehl, in denen in wir erhalten die Skripts und führen Sie die gleiche in der Zieldatenbank.  
  
Ist eine oder mehrere Metabase-Knoten als-Befehlszeilenparameter erforderlich.  
  
-   `object-name:`Gibt an, die Objekte, deren Skripts sind gespeichert werden sollen. (Es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt besitzen)  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `metabase:`Gibt an, ob es IDer Quelle oder Ziel der Metabasis.  
  
-   `destination:`Gibt den Pfad oder den Ordner, in dem das Skript muss gespeichert werden, wenn der Dateiname nicht klicken Sie dann einen Dateinamen in das Format (Attributwert Object_name) .out angegeben ist  
  
-   `overwrite:`Bei "true" überschreibt es denselben Dateinamen vorhanden. Sie können die Werte (wahr/falsch) haben.  
  
**Syntaxbeispiel:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  destination="<file-name/folder-name>"  
  
  overwrite="<true/false>"   (optional)  
  
/>  
```  
oder  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>Convert-Sql-Anweisung  
  
-   `context`Gibt den Schemanamen an.  
  
-   `destination`Gibt an, ob die Ausgabe in einer Datei gespeichert werden sollen.  
  
    Wenn dieses Attribut nicht angegeben ist, wird die konvertierte T-SQL-Anweisung in der Konsole angezeigt. (optionales Attribut)  
  
-   `conversion-report-folder`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
-   `conversion-report-overwrite`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-converted-sql-to`Gibt die Datei Ordnerpfad, in dem die konvertierte T-SQL ist, gespeichert werden (oder). Wenn ein Pfad angegeben wird, zusammen mit der `sql-files` -Attribut, jeder Quelldatei klicken wird eine entsprechende Ziel T-SQL-Datei, die unter den angegebenen Ordner erstellt haben. Wenn ein Pfad angegeben wird, zusammen mit der `sql` -Attribut, das konvertierte T-SQL wird in eine Datei mit dem Namen Result.out unter den angegebenen Ordner geschrieben.  
  
-   `sql`Gibt an, die Sybase-Sql-Anweisungen konvertiert werden, wird eine oder mehrere Anweisungen kann getrennt werden mithilfe einer ";"  
  
-   `sql-files`Gibt den Pfad der Sql-Dateien mit T-SQL-Code konvertiert werden.  
  
-   `write-summary-report-to`Gibt den Pfad, in dem der zusammenfassende Bericht generiert wird. Falls nur der Ordnerpfad angegeben wird, namentlich Datei **ConvertSQLReport.XML** wird erstellt. (optionales Attribut)  
  
    Zusammenfassungsbericht Erstellung hat 2 Unterkategorien, begrenzt weiter..,:  
  
    -   Fehlerberichte (= "wahr/falsch", Standardwert "false" (optionale Attribute)).  
  
    -   Verbose (= "wahr/falsch", Standardwert "false" (optionale Attribute)).  
  
Ist eine oder mehrere Metabase-Knoten als-Befehlszeilenparameter erforderlich.  
  
**Syntaxbeispiel:**  
  
```  
<convert-sql-statement  
  
       context="<database-name>.<schema-name>"  
  
        conversion-report-folder="<folder-name>"  
  
        conversion-report-overwrite="<true/false>"  
  
        write-summary-report-to="<file-name/folder-name>"   (optional)  
  
        verbose="<true/false>"   (optional)  
  
        report-errors="<true/false>"   (optional)  
  
        destination="<stdout/file>"   (optional)  
  
        write-converted-sql-to ="<file-name/folder-name>"  
  
        sql="SELECT 1 FROM DUAL;">  
  
    <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
oder  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         write-summary-report-to="<file-name/folder-name>"   (optional)  
  
         verbose="<true/false>"   (optional)  
  
         report-errors="<true/false>"   (optional)  
  
         destination="<stdout/file>"   (optional)  
  
         write-converted-sql-to ="<file-name/folder-name>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
oder  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-step"></a>Nächster Schritt  
Informationen zu Befehlszeilenoptionen finden Sie unter [Command Line Options SSMA-Konsole &#40; SybaseToSQL &#41; ](../../ssma/sybase/command-line-options-in-ssma-console-sybasetosql.md) .  
  
Informationen auf Beispielskriptdatei für die Konsole finden Sie unter [arbeiten mit der Konsole Skript-Beispieldateien &#40; SybaseToSQL &#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
Der nächste Schritt hängt davon ab, auf die Anforderungen Ihres Projekts:  
  
-   Zur Angabe eines Kennworts oder einer Exportieren / Importieren von Kennwörtern, finden Sie unter [Verwalten von Kennwörtern &#40; SybaseToSQL &#41; ](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   Generieren von Berichten, finden Sie unter [Generieren von Berichten &#40; SybaseToSQL &#41; ](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   Behandlung von Problemen in der Konsole, finden Sie unter [Problembehandlung &#40; SybaseToSQL &#41; ](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  

