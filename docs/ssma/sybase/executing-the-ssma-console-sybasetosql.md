---
title: Ausführen der Konsole SSMA (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 87b2db2a9a6265ebb792fc9178c6a9b66a7e858a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="executing-the-ssma-console-sybasetosql"></a>Ausführen der Konsole SSMA (SybaseToSQL)
Microsoft stellt Ihnen Dateibefehle auszuführen und zu steuern SSMA Aktivitäten eine Reihe robuster Skript. In den folgenden Abschnitten ausführlich identisch.  
  
## <a name="script-file-commands"></a>Datei-Skriptbefehle  
Die Konsolenanwendung verwendet bestimmte Standardskripts Dateibefehle als aufgezählte in diesem Abschnitt.  
  
## <a name="project-commands"></a>Projekt-Befehle  
Das Handle des Projekt Befehle, die beim Erstellen von Projekten, öffnen, speichern und Beenden von Projekten.  
  
### <a name="create-new-project"></a>erstellen – Neues Projekt  
Dieser Befehl erstellt ein neues SSMA-Projekt.  
  
-   `project-folder` Gibt den Ordner, der das erste erstellte Projekt an.  
  
-   `project-name` Gibt den Namen des Projekts an. {string}  
  
-   `overwrite-if-exists`Optionales Attribut gibt an, ob ein vorhandenes Projekt überschrieben werden soll. {Boolean}  
  
-   `project-type:`Optionales Attribut. Gibt an, der "Sql Server 2005" Projekt "Sql Server 2008"-Projekt oder Projekt "Sql Server 2012" oder "Sql Server 2014" Projekt oder "Sql Azure" Projekt ist Projekttyp. Standardwert ist "Sql-Server-2008".  
  
**Syntaxbeispiel:**  
  
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
Mit diesem Befehl wird das Projekt geöffnet.

-   `project-folder` Gibt den Ordner, der das erste erstellte Projekt an. Der Befehl schlägt fehl, wenn der angegebene Ordner nicht vorhanden ist.  {string}  
  
-   `project-name` Gibt den Namen des Projekts an. Der Befehl schlägt fehl, wenn das angegebene Projekt nicht vorhanden ist.  {string}  
  
**Syntaxbeispiel:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA für SAP ASE Konsolenanwendung unterstützt Abwärtskompatibilität. Sie können Sie die um Vorgängerversion von SSMA erstellte Projekte zu öffnen.  
  
### <a name="save-project"></a>Save-Projekt  
Dieser Befehl speichert das Migrationsprojekt.  
  
**Syntaxbeispiel:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>Close-Projekt  
Mit diesem Befehl wird das Migrationsprojekt geschlossen.  
  
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
> - Die **Durchsuchen** Features der Benutzeroberfläche wird in der Konsole nicht unterstützt.  
> - Weitere Informationen zu "Skriptdateien erstellen", finden Sie unter [Skriptdateien erstellen &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
### <a name="connect-source-database"></a>Verbinden-Quelldatenbank  
Dieser Befehl führt die Verbindung mit der Quelldatenbank und lädt auf hoher Ebene Metadaten von der Quelldatenbank, aber nicht alle Metadaten.
  
Wenn die Verbindung mit der Datenquelle hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.
  
Definition des Servers wird aus dem Namensattribut für jede Verbindung im Server-Abschnitt des Server-Verbindungsdatei oder die Skriptdatei definiert abgerufen.  
  
**Syntaxbeispiel:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>Force-Load-/ Ziel-Quelldatenbank  
Dieser Befehl lädt die Quellmetadaten und eignet sich zum Migrationsprojekt offline arbeiten.  
  
Wenn die Verbindung mit den Quell-/Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
Dieser Befehl erfordert einen oder mehrere Metabase-Knoten als Befehlszeilenparameter an.  
  
**Syntaxbeispiel:**  
  
```xml  
<force-load metabase=”<source/target>” >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>Schließen Sie Quelldatenbank  
Dieser Befehl erneut mit der Quelldatenbank, aber keine Metadaten im Gegensatz zu den Befehl Connect Quelldatenbank wird nicht geladen.  
  
Herstellen der Verbindung mit der Datenquelle hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Syntaxbeispiel:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>Verbinden-Zieldatenbank  
Dieser Befehl eine Verbindung mit SQL Server-Zieldatenbank her und lädt vollständig auf hoher Ebene Metadaten der Zieldatenbank, aber nicht die Metadaten.  
  
Wenn die Verbindung mit dem Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
Definition des Servers wird aus dem Namensattribut für jede Verbindung im Server-Abschnitt des Server-Verbindungsdatei oder die Skriptdatei definiert abgerufen.  
  
**Syntaxbeispiel:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>Schließen Sie Zieldatenbank  
  
Dieser Befehl erneut mit der Zieldatenbank, aber keine Metadaten, im Gegensatz zu den Befehl Connect der Zieldatenbank wird nicht geladen.  
  
Herstellen der Verbindung mit dem Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Syntaxbeispiel:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>Berichtsbefehle  
Die Berichtsserver-Befehle Generieren von Berichten auf die Leistung der verschiedenen SSMA-konsolenaktivitäten.  
  
### <a name="generate-assessment-report"></a>Generieren von Bewertungsbericht  
  
Dieser Befehl generiert Bewertungsberichte für die Quelldatenbank.  
  
Wenn die Verbindung mit der Quelldatenbank nicht ausgeführt werden, bevor Sie diesen Befehl ausführen, wird ein Fehler generiert, und die Konsolenanwendung beendet.  
  
Während der Ausführung des Befehls eine Verbindung mit dem Datenbankserver auch führt dies in der Konsolenanwendung beendet.  
  
-   `conversion-report-folder:` Gibt den Ordner, in dem der Assessment-Bericht gespeichert werden kann. (optionales Attribut)  
  
-   `object-name:` Gibt an, die Objekte, die für die Bewertung berichtgenerierung (unterstützt einzelne Objektnamen oder einen Gruppennamen-Objekt) in Betracht gezogen.  
  
-   `object-type:` Gibt den Typ des Objekts als Legende im Objekt-Name-Attribut (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `conversion-report-overwrite:` Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-summary-report-to:` Gibt den Pfad zu dem der Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **AssessmentReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors` (= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose` (= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
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
Die Befehle für die Migration das Schema der Zieldatenbank, die dem Quellschema zu konvertieren und Migrieren von Daten auf dem Zielserver.  
  
### <a name="convert-schema"></a>Convert-schema  
Mit diesem Befehl wird die schemakonvertierung aus der Quelle mit dem Zielschema.  
  
Wenn die Verbindung mit der Quelle oder Ziel wird nicht ausgeführt, bevor Sie diesen Befehl ausführen, oder die Verbindung mit dem Datenbankserver Quell- oder Zieltabelle, die während der Ausführung des Befehls Fehler auftreten, wird ein Fehler generiert, und die Konsolenanwendung beendet wird.  
  
-   `conversion-report-folder:` Gibt an, Ordner, in dem der Assessment-Bericht gespeichert werden kann. (optionales Attribut)  
  
-   `object-name:` Gibt die Quelle-Objekte, die für das Konvertieren eines Schemas (unterstützt einzelne Objektnamen oder einen Gruppennamen-Objekt) in Betracht gezogen.  
  
-   `object-type:` Gibt den Typ des Objekts als Legende im Objekt-Name-Attribut (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `conversion-report-overwrite:` Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-summary-report-to:` Gibt den Pfad zu dem der zusammenfassende Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **SchemaConversionReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors` (= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose` (= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
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
Mit diesem Befehl werden die Quelldaten zum Ziel migriert.  
  
-   `object-name:` Gibt die Quelle-Objekte, die für die Migration in Betracht gezogen Daten (unterstützt einzelne Objektnamen oder einen Gruppennamen-Objekt).  
  
-   `object-type:` Gibt den Typ des Objekts als Legende im Objekt-Name-Attribut (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `write-summary-report-to:` Gibt den Pfad zu dem der Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **DataMigrationReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors` (= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose` (= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
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
Dieser Befehl stellt die schemazuordnung von der Quelldatenbank mit dem Zielschema.  
  
-   `source-schema` Gibt das Quellschema zum Migrieren.  
  
-   `sql-server-schema` Gibt das Zielschema auf das Quellschema migriert werden.  
  
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
Mit diesem Befehl wird der Zielobjekte mit der Zieldatenbank synchronisiert.  
 
Wenn Sie diesen Befehl für die Quelldatenbank ausgeführt wird, ist ein Fehler aufgetreten.  
  
Wenn die Verbindung mit der Zieldatenbank wird nicht ausgeführt, bevor Sie diesen Befehl ausführen oder die Verbindung mit dem Zielserver für die Datenbank ein Fehler auftritt, während der Ausführung des Befehls, wird ein Fehler generiert, und die Konsolenanwendung beendet.  
  
-   `object-name:` Gibt an, die Ziel-Objekte, die für die Synchronisierung mit der Zieldatenbank (unterstützt einzelne Objektnamen oder einen Gruppennamen-Objekt) betrachtet.  
  
-   `object-type:` Gibt den Typ des Objekts als Legende im Objekt-Name-Attribut (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `on-error:` Gibt an, ob die Synchronisierungsfehler als Warnungen oder Fehler angegeben. Verfügbare Optionen für auf Fehler:  
  
    -   Bericht insgesamt als Warnung  
  
    -   Bericht-each-als-Warnung  
  
    -   Fail-Skript  
  
-   `report-errors-to:` Gibt Speicherort der Fehlerbericht für den Synchronisierungsvorgang (optionales Attribut). Wenn nur Ordnerpfad angegeben wird, namentlich Datei **TargetSynchronizationReport.XML** wird erstellt.  
  
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
Mit diesem Befehl werden die Objekte aus der Datenbank aktualisiert.  
  
Wenn Sie diesen Befehl für die Zieldatenbank ausgeführt wird, wird ein Fehler generiert.  
  
Dieser Befehl erfordert einen oder mehrere Metabase-Knoten als Befehlszeilenparameter an.  
  
-   `object-name:` Gibt die Quelle-Objekte, die beim Aktualisieren von der Quelldatenbank (unterstützt einzelne Objektnamen oder einen Gruppennamen-Objekt) in Betracht gezogen.  
  
-   `object-type:` Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `on-error:` Gibt an, ob Aktualisierung Fehler als Warnungen oder Fehler aufzurufen. Verfügbare Optionen für auf Fehler:  
  
    -   Bericht insgesamt als Warnung  
  
    -   Bericht-each-als-Warnung  
  
    -   Fail-Skript  
  
-   `report-errors-to:` Gibt Speicherort der Fehlerbericht für den Aktualisierungsvorgang (optionales Attribut). Wenn nur Ordnerpfad angegeben wird, namentlich Datei **SourceDBRefreshReport.XML** wird erstellt.  
  
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
Die Befehle Skriptgenerierung zwei Aufgaben ausführen: sie helfen bei der speichern die Konsolenausgabe in einer Skriptdatei, und zeichnen Sie die T-SQL-Ausgabe in der Konsole oder eine Datei basierend auf dem Parameter, die Sie angeben.  
  
### <a name="save-as-script"></a>"Save-als-Script"  
Mit diesem Befehl wird zum Speichern der Skripts für die Objekte in einer Datei erwähnt Wenn Metabasis = Ziel. Dies ist eine Alternative zum Synchronisationsbefehl insofern, dass wir erhalten die Skripts, und führen die gleiche in der Zieldatenbank.  
  
Dieser Befehl erfordert einen oder mehrere Metabase-Knoten als Befehlszeilenparameter an.  
  
-   `object-name:` Gibt an, die Objekte, deren Skripts sind (unterstützt einzelne Objektnamen oder einen Gruppennamen-Objekt) gespeichert werden sollen.  
  
-   `object-type:` Gibt den Typ des Objekts als Legende im Objekt-Name-Attribut (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `metabase:` Gibt an, ob es die Quelle oder Ziel der Metabasis.  
  
-   `destination:` Gibt den Pfad oder den Ordner, in dem das Skript gespeichert werden muss. Wenn der Dateiname nicht angegeben ist, wird ein Dateiname in das Format (Attributwert Object_name) .out bereitgestellt werden.
  
-   `overwrite:` Bei "true", überschreibt es denselben Dateinamen, falls es vorhanden ist. Sie können die Werte (wahr/falsch) haben.  
  
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
Mit diesem Befehl konvertiert die SQL-Anweisung.  
  
-   `context` Gibt den Schemanamen an.  
  
-   `destination` Gibt an, ob die Ausgabe in einer Datei gespeichert werden sollen.  
  
    Wenn dieses Attribut nicht angegeben ist, wird die konvertierte T-SQL-Anweisung in der Konsole angezeigt. (optionales Attribut)  
  
-   `conversion-report-folder` Gibt den Ordner, in dem der Assessment-Bericht gespeichert werden kann. (optionales Attribut)  
  
-   `conversion-report-overwrite` Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-converted-sql-to` Gibt die Datei Ordnerpfad (oder) auf die das konvertierte T-SQL gespeichert werden sollen. Wenn ein Pfad angegeben wird, zusammen mit der `sql-files` -Attribut, jeder Quelldatei verfügt über eine entsprechende Ziel T-SQL-Datei, die unter den angegebenen Ordner erstellt. Wenn ein Pfad angegeben wird, zusammen mit der `sql` -Attribut, das konvertierte T-SQL wird in eine Datei mit dem Namen Result.out unter den angegebenen Ordner geschrieben.  
  
-   `sql` Gibt an, die Sybase-Sql-Anweisungen konvertiert werden, eine oder mehrere Anweisungen können getrennt werden, mithilfe einer ";"  
  
-   `sql-files` Gibt den Pfad der Sql-Dateien, die in T-SQL-Code konvertiert werden.  
  
-   `write-summary-report-to` Gibt den Pfad, in dem der zusammenfassende Bericht generiert wird. Falls nur der Ordnerpfad angegeben wird, namentlich Datei **ConvertSQLReport.XML** wird erstellt. (optionales Attribut)  
  
    Zusammenfassungsbericht erstellen, weist zwei weitere Unterkategorien, nämlich:  
  
    -   Fehlerberichte (= "wahr/falsch", Standardwert "false" (optionale Attribute)).  
  
    -   Verbose (= "wahr/falsch", Standardwert "false" (optionale Attribute)).  
  
Dieser Befehl erfordert einen oder mehrere Metabase-Knoten als Befehlszeilenparameter an.  
  
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
  
## <a name="next-steps"></a>Nächste Schritte  
Informationen zu Befehlszeilenoptionen finden Sie unter [Befehlszeilenoptionen in der Konsole SSMA (AccessToSQL)](../access/command-line-options-in-ssma-console-accesstosql.md).  
  
Informationen auf eine Konsole Beispielskriptdatei finden Sie unter [arbeiten mit der Konsole Skript-Beispieldateien &#40;SybaseToSQL&#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
Der nächste Schritt hängt davon ab, auf die Anforderungen Ihres Projekts:  
  
-   Zur Angabe eines Kennworts oder einer Exportieren / Importieren von Kennwörtern, finden Sie unter [Verwalten von Kennwörtern &#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   Generieren von Berichten, finden Sie unter [Generieren von Berichten &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   Behandlung von Problemen in der Konsole, finden Sie unter [Problembehandlung &#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  
