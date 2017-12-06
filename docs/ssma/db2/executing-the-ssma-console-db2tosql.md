---
title: "Ausführen der Konsole SSMA (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ce63f633-067d-4f04-b8e9-e1abd7ec740b
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1346ccef45d9a8de619293da09a3d4a148bc9cf8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="executing-the-ssma-console-db2tosql"></a>Ausführen der Konsole SSMA (DB2ToSQL)
Microsoft stellt Ihnen Dateibefehle auszuführen und zu steuern SSMA Aktivitäten eine Reihe robuster Skript. In den folgenden Abschnitten ausführlich identisch. Die Konsolenanwendung verwendet bestimmte Standardskripts Dateibefehle als aufgezählte in diesem Abschnitt.  
  
## <a name="project-script-file-commands"></a>Projekt Datei Skriptbefehle  
Das Handle des Projekt Befehle, die beim Erstellen von Projekten, öffnen, speichern und Beenden von Projekten.  
  
**Befehl**  
  
erstellen – Neues Projekt  
  
Erstellt ein neues SSMA-Projekt.  
  
**Skript**  
  
-   `project-folder`Gibt den Ordner, der das erste erstellte Projekt an.  
  
-   `project-name`Gibt den Namen des Projekts an. {String}  
  
-   `overwrite-if-exists`Optionales Attribut gibt an, ob ein vorhandenes Projekt überschrieben werden soll. {Boolean}  
  
-   `project-type:`Optionales Attribut. Gibt den Projekttyp z. B. "Sql Server 2005" Projekt oder "Sql Server 2008" Project oder Project "Sql Server 2012" oder "Sql Server 2014" Projekt oder "Sql Azure". Der Standardwert ist "Sql Server 2014".  
  
**Beispiel:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
Attribut "überschreiben-If-exists" ist **"false"** standardmäßig.  
  
Attribut "Projekttyp" ist **Sql Server 2008** standardmäßig.  
  
**Befehl**  
  
Open-Projekt  
  
Öffnet ein vorhandenes Projekt.  
  
**Skript**  
  
-   `project-folder`Gibt den Ordner, der das erste erstellte Projekt an. Der Befehl schlägt fehl, wenn der angegebene Ordner nicht vorhanden ist.  {String}  
  
-   `project-name`Gibt den Namen des Projekts an. Der Befehl schlägt fehl, wenn das angegebene Projekt nicht vorhanden ist.  {String}  
  
**Syntaxbeispiel:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
SSMA für die DB2-Konsolenanwendung unterstützt Abwärtskompatibilität. Sie werden können zum Öffnen von Projekten, die von der früheren Version von SSMA erstellt.  
  
**Befehl**  
  
Save-Projekt  
  
Speichert das Migrationsprojekt.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<save-project/>  
```  
**Befehl**  
  
Close-Projekt  
  
Schließt das Migrationsprojekt an.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
  
## <a name="database-connection-script-file-commands"></a>Datenbank-Verbindung Datei Skriptbefehle  
Die Verbindung mit Datenbank-Befehle können mit der Datenbank herstellen.  
  
-   Die **Durchsuchen** Features der Benutzeroberfläche wird in der Konsole nicht unterstützt.  
  
-   Weitere Informationen zu "Skriptdateien erstellen", finden Sie unter [Skriptdateien erstellen &#40; OracleToSQL &#41;](../../ssma/oracle/creating-script-files-oracletosql.md).  
  
**Befehl**  
  
Verbinden-Quelldatenbank  
  
-   Führt die Verbindung mit der Quelldatenbank und lädt hohe Ebene Metadaten von der Quelldatenbank, aber nicht alle Metadaten.  
  
-   Wenn die Verbindung mit der Datenquelle hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter  
  
**Skript**  
  
Das Name-Attribut für jede Verbindung im Server-Abschnitt des Server-Verbindungsdatei oder die Skriptdatei definiert ist Serverdefinition entnommen.  
  
**Syntaxbeispiel:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Befehl**  
  
Force-Load-/ Ziel-Quelldatenbank  
  
-   Lädt die Quellmetadaten an.  
  
-   Für die Arbeit auf offline-Migrationsprojekts nützlich.  
  
-   Wenn die Verbindung mit den Quell-/Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter  
  
**Skript**  
  
Ist eine oder mehrere Metabase-Knoten als-Befehlszeilenparameter erforderlich.  
  
**Syntaxbeispiel:**  
  
```xml  
<force-load object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
oder  
  
```xml  
<force-load>  
  
   <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Befehl**  
  
Schließen Sie Quelldatenbank  
  
-   Verbindung mit der Quelldatenbank, aber keine Metadaten im Gegensatz zu den Befehl Connect Quelldatenbank wird nicht geladen.  
  
-   Herstellen der Verbindung mit der Datenquelle hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Befehl**  
  
Verbinden-Zieldatenbank  
  
-   Eine Verbindung mit SQL Server-Zieldatenbank her und lädt vollständig hohe Ebene Metadaten der Zieldatenbank, aber nicht die Metadaten.  
  
-   Wenn die Verbindung mit dem Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Skript**  
  
Das Name-Attribut für jede Verbindung im Server-Abschnitt des Server-Verbindungsdatei oder die Skriptdatei definiert ist Serverdefinition entnommen.  
  
**Syntaxbeispiel:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Befehl**  
  
Schließen Sie Zieldatenbank  
  
-   Erneut mit der Zieldatenbank, aber keine Metadaten, im Gegensatz zu den Befehl Connect der Zieldatenbank wird nicht geladen.  
  
-   Herstellen der Verbindung mit dem Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Berichtsbefehle Skript-Datei  
Die Berichtsserver-Befehle Generieren von Berichten auf die Leistung der verschiedenen SSMA-konsolenaktivitäten.  
  
**Befehl**  
  
Generieren von Bewertungsbericht  
  
-   Assessment-Berichte in der Quelldatenbank generiert.  
  
-   Wenn die Verbindung mit der Quelldatenbank nicht ausgeführt werden, bevor Sie diesen Befehl ausführen, wird ein Fehler generiert, und die Konsolenanwendung beendet.  
  
-   Während der Ausführung des Befehls eine Verbindung mit dem Datenbankserver auch führt dies in der Konsolenanwendung beendet.  
  
**Skript**  
  
-   `conversion-report-folder:`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
-   `object-name:`Gibt an, die Objekte, die zur Bewertung berichterstellung (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt besitzen) betrachtet.  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `conversion-report-overwrite:`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-summary-report-to:`Gibt den Pfad, in dem der zusammenfassende Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **AssessmentReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
**Syntaxbeispiel:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   assessment-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
oder  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Migration Datei Skriptbefehle  
Die Befehle für die Migration konvertieren das Schema der Zieldatenbank, die dem Quellschema und Migrieren von Daten auf dem Zielserver. Die Standard-Konsolenausgabe festlegen, für die Migration Befehle ist 'Full' Ausgabebericht mit keine ausführliche-Fehlerberichterstattung: nur Zusammenfassung am Stammknoten Quell-Objekt.  
  
**Befehl**  
  
Convert-schema  
  
-   Schemakonvertierung von der Quelle in das Zielschema durchgeführt.  
  
-   Wenn die Verbindung mit der Quelle oder Ziel wird nicht ausgeführt, bevor Sie diesen Befehl ausführen, oder die Verbindung mit dem Datenbankserver Quell- oder Zieltabelle, die während der Ausführung des Befehls Fehler auftreten, wird ein Fehler generiert, und die Konsolenanwendung beendet wird.  
  
**Skript**  
  
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
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
oder  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Befehl**  
  
Migrieren von Daten: migriert die Quelldaten zum Ziel.  
  
**Skript**  
  
-   `conversion-report-folder:`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
-   `object-name:`Gibt die Quelle-Objekte, die für die Migration in Betracht gezogen Daten (es kann haben Indivdual Objektnamen oder einen Gruppennamen-Objekt).  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `conversion-report-overwrite:`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-summary-report-to:`Gibt den Pfad, in dem der zusammenfassende Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **DataMigrationReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
**Syntaxbeispiel:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>">  
  
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
  
   report-errors="<true/false>"  
  
   verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Migration Vorbereitung Datei Skriptbefehle  
Die Vorbereitung der Migration-Befehl startet schemazuordnung zwischen den Quell- und Zieldatenbanken.  
  
**Befehl**  
  
Map-schema  
  
Schemazuordnung der Quelldatenbank mit dem Zielschema.  
  
**Skript**  
  
-   `source-schema`Gibt das Quellschema, das wir migrieren möchten.  
  
-   `sql-server-schema`Gibt das Zielschema, in dem wir migriert werden soll.  
  
**Syntaxbeispiel:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
**Befehl**  
  
Map-schema  
  
Schemazuordnung der Quelldatenbank mit dem Zielschema.  
  
**Skript**  
  
`source-schema`Gibt das Quellschema, das wir migrieren möchten.  
  
`sql-server-schema`Gibt das Zielschema, in dem wir migriert werden soll.  
  
**Syntaxbeispiel:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Verwaltbarkeit Datei Skriptbefehle  
Die Verwaltbarkeit Befehle können mit der Quelldatenbank Zielobjekte Datenbank zu synchronisieren.  
  
Die Standard-Konsolenausgabe festlegen, für die Migration Befehle ist 'Full' Ausgabebericht mit keine ausführliche-Fehlerberichterstattung: nur Zusammenfassung am Stammknoten Quell-Objekt.  
  
**Befehl**  
  
Synchronisieren von Ziel  
  
-   Synchronisiert die Zielobjekte mit der Zieldatenbank an.  
  
-   Wenn Sie diesen Befehl für die Quelldatenbank ausgeführt wird, ist ein Fehler aufgetreten.  
  
-   Wenn die Verbindung mit der Zieldatenbank wird nicht ausgeführt, bevor Sie diesen Befehl ausführen oder die Verbindung mit dem Zielserver für die Datenbank ein Fehler auftritt, während der Ausführung des Befehls, wird ein Fehler generiert, und die Konsolenanwendung beendet.  
  
**Skript**  
  
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
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
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
**Befehl**  
  
Aktualisieren von Datenbank  
  
-   Aktualisiert die Datenquelle Objekte aus der Datenbank.  
  
-   Wenn Sie diesen Befehl für die Zieldatenbank ausgeführt wird, wird ein Fehler generiert.  
  
**Skript**  
  
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
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
oder  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
oder  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Skriptbefehle für die Datei von Generation Skript  
Die Befehle Skriptgenerierung zwei Aufgaben ausführen: sie helfen bei der speichern die Konsolenausgabe in einer Skriptdatei; und zeichnen Sie die T-SQL-Ausgabe in der Konsole oder eine Datei basierend auf dem von Ihnen angegebenen Parameter.  
  
**Befehl**  
  
"Save-als-Script"  
  
Zum Speichern von den Skripts für die Objekte in einer Datei, wenn erwähnt Metabasis = Ziel, dies ist eine Alternative zum Synchronisationsbefehl, in denen in wir erhalten die Skripts und führen Sie die gleiche in der Zieldatenbank.  
  
**Skript**  
  
Ist eine oder mehrere Metabase-Knoten als-Befehlszeilenparameter erforderlich.  
  
-   `object-name:`Gibt an, die Objekte, deren Skripts sind gespeichert werden sollen. (sie können einzelne Objektnamen oder einen Gruppennamen für das Objekt verfügen)  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `metabase:`Gibt an, ob es die Quelle oder Ziel der Metabasis.  
  
-   `destination:`Gibt den Pfad oder den Ordner, in dem das Skript muss gespeichert werden, wenn der Dateiname nicht klicken Sie dann einen Dateinamen in das Format (Attributwert Object_name) .out angegeben ist  
  
-   `overwrite:`Bei "true" überschreibt es denselben Dateinamen vorhanden. Sie können die Werte (wahr/falsch) haben.  
  
**Syntaxbeispiel:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file/folder>"  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
oder  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file/folder>"  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Befehl**  
  
Convert-Sql-Anweisung  
  
-   `context`Gibt den Schemanamen an.  
  
-   `destination`Gibt an, ob die Ausgabe in einer Datei gespeichert werden sollen.  
  
    Wenn dieses Attribut nicht angegeben ist, wird die konvertierte T-SQL-Anweisung in der Konsole angezeigt. (optionales Attribut)  
  
-   `conversion-report-folder`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
-   `conversion-report-overwrite`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-converted-sql-to`Gibt die Datei Ordnerpfad, in dem die konvertierte T-SQL ist, gespeichert werden (oder). Wenn ein Pfad angegeben wird, zusammen mit der `sql-files` -Attribut, jeder Quelldatei klicken wird eine entsprechende Ziel T-SQL-Datei, die unter den angegebenen Ordner erstellt haben. Wenn ein Pfad angegeben wird, zusammen mit den `sql` -Attribut, das konvertierte T-SQL wird in eine Datei mit dem Namen geschrieben **Result.out** unter den angegebenen Ordner.  
  
-   `sql`Gibt an, DB2 Sql-Anweisungen konvertiert werden, eine oder mehrere Anweisungen können getrennt werden, mithilfe einer ";"  
  
-   `sql-files`Gibt den Pfad der Sql-Dateien mit T-SQL-Code konvertiert werden.  
  
-   `write-summary-report-to`Gibt den Pfad, in dem der Bericht generiert wird. Falls nur der Ordnerpfad angegeben wird, namentlich Datei **ConvertSQLReport.XML** wird erstellt. (optionales Attribut)  
  
    Bericht Erstellung hat 2 Unterkategorien, begrenzt weiter..,:  
  
    -   Fehlerberichte (= "wahr/falsch", Standardwert "false" (optionale Attribute)).  
  
    -   Verbose (= "wahr/falsch", Standardwert "false" (optionale Attribute)).  
  
**Skript**  
  
Ist eine oder mehrere Metabase-Knoten als-Befehlszeilenparameter erforderlich.  
  
**Syntaxbeispiel:**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   file-name="<file-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
   <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
oder  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>" (optional)  
  
   verbose="<true/false>" (optional)  
  
   report-errors="<true/false>"  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
oder  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
  
## <a name="next-step"></a>Nächster Schritt  
Informationen zu Befehlszeilenoptionen finden Sie unter [Command Line Options SSMA-Konsole &#40; DB2ToSQL &#41;](../../ssma/db2/command-line-options-in-ssma-console-db2tosql.md) .  
  
Informationen zum Beispiel Konsole-Skriptdateien, finden Sie unter [arbeiten mit der Konsole Skript-Beispieldateien &#40; DB2ToSQL &#41;](../../ssma/db2/working-with-the-sample-console-script-files-db2tosql.md)  
  
Der nächste Schritt hängt davon ab, auf die Anforderungen Ihres Projekts:  
  
-   Zur Angabe eines Kennworts oder einer Exportieren / Importieren von Kennwörtern, finden Sie unter [Verwalten von Kennwörtern &#40; DB2ToSQL &#41;](../../ssma/db2/managing-passwords-db2tosql.md).  
  
-   Generieren von Berichten, finden Sie unter [Generieren von Berichten &#40; DB2ToSQL &#41;](../../ssma/db2/generating-reports-db2tosql.md).  
  
-   Behandlung von Problemen in der Konsole, finden Sie unter [Problembehandlung &#40; DB2ToSQL &#41;](../../ssma/db2/troubleshooting-db2tosql.md).  
  
