---
title: "Ausführen der Konsole SSMA (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
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
- Script file commands, Database connection commands
- Script file commands, Manageability commands
- Script file commands, Migration commands
- Script file commands, Migration preparation commands
- Script file commands, project commands
- Script file commands, Report commands
- Script file commands, Script generation commands
ms.assetid: e3e9f7e4-0619-4861-a202-3d5d39953b26
caps.latest.revision: 25
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d3524ac9d8aac255fdf87bedbe6cf3badad963bd
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="executing-the-ssma-console-mysqltosql"></a>Ausführen der Konsole SSMA (MySQLToSQL)
Microsoft stellt Ihnen Dateibefehle auszuführen und zu steuern SSMA Aktivitäten eine Reihe robuster Skript.  
  
Die Konsolenanwendung verwendet bestimmte Standardskripts Dateibefehle als aufgezählte in diesem Abschnitt.  
  
## <a name="project--script-file-commands"></a>Projekt Datei Skriptbefehle  
**Befehl**  
  
Neues-Projekt erstellen:   
                   Erstellt ein neues SSMA-Projekt.  
  
Das Handle des Projekt Befehle, die beim Erstellen von Projekten, öffnen, speichern und Beenden von Projekten.  
  
**Skript**  
  
1.  `project-folder`Gibt den Ordner, der das erste erstellte Projekt an.  
  
2.  `project-name`Gibt den Namen des Projekts an. {String}  
  
3.  `overwrite-if-exists`Optionales Attribut gibt an, ob ein vorhandenes Projekt überschrieben werden soll. {Boolean}  
  
4.  `project-type:`Optionales Attribut. Gibt an, das Projekttyp z. B. "Sql Server 2005" Project oder Project "Sql Server 2008" oder "Sql Server 2012" oder "Sql Server 2014" Projekt oder "Sql Azure". Standardwert ist "Sql Server 2008".  
  
**Syntaxbeispiel:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type==”<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>”   (optional)  
  
/>  
```  
Attribut "überschreiben-If-exists" ist **"false"** standardmäßig.  
  
Attribut "Projekttyp" ist **Sql Server 2008** standardmäßig.  
  
**Befehl**  
  
Open-Projekt:   
                  Öffnet ein vorhandenes Projekt.  
  
**Skript**  
  
1.  `project-folder`Gibt den Ordner, der das erste erstellte Projekt an. Der Befehl schlägt fehl, wenn der angegebene Ordner nicht vorhanden ist.  {String}  
  
2.  `project-name`Gibt den Namen des Projekts an. Der Befehl schlägt fehl, wenn das angegebene Projekt nicht vorhanden ist.  {String}  
  
**Syntaxbeispiel:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
> [!IMPORTANT]  
> SSMA für MySQL Konsolenanwendung unterstützt Abwärtskompatibilität. Sie werden können zum Öffnen von Projekten, die von der früheren Version von SSMA erstellt.  
  
**Befehl**  
  
Save-Projekt: Migrationsprojekts speichert.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<save-project/>  
```  
**Befehl**  
  
Close-Projekt  
                  : Das Migrationsprojekt schließt.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<save-project/>  
```  
**Befehl**  
  
Close-Projekt  
                  : Das Migrationsprojekt schließt.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
'If-modified'-Attribut ist optional, **ignorieren** standardmäßig.  
  
## <a name="database-connection-script-file-commands"></a>Datenbank-Verbindung Datei Skriptbefehle  
Die Verbindung mit Datenbank-Befehle können mit der Datenbank herstellen.  
  
1.  Die **Durchsuchen** Features der Benutzeroberfläche wird in der Konsole nicht unterstützt.  
  
2.  Die **Windows-Authentifizierung** und **Port** Parameter sind nicht anwendbar, wenn die Verbindung mit SQL Azure.  
  
3.  Weitere Informationen zu "Skriptdateien erstellen", finden Sie unter [Skriptdateien erstellen &#40; MySQLToSQL &#41; ](../../ssma/mysql/creating-script-files-mysqltosql.md).  
  
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
<force-load metabase="<source/target>"  
  
      <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Befehl**  
  
Schließen Sie Quelldatenbank  
  
1.  Verbindung mit der Quelldatenbank, aber keine Metadaten im Gegensatz zu den Befehl Connect Quelldatenbank wird nicht geladen.  
  
2.  Herstellen der Verbindung mit der Datenquelle hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Befehl**  
  
Verbinden-Zieldatenbank  
  
1.  Die Ziel-SQL Server- bzw. SQL Azure-Datenbank her, und hohe Ebene Metadaten der Zieldatenbank, aber nicht die Metadaten vollständig geladen.  
  
2.  Wenn die Verbindung mit dem Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Skript**  
  
Das Name-Attribut für jede Verbindung im Server-Abschnitt des Server-Verbindungsdatei oder die Skriptdatei definiert ist Serverdefinition entnommen.  
  
**Syntaxbeispiel:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Befehl**  
  
Schließen Sie Zieldatenbank  
  
1.  Erneut mit der Zieldatenbank, aber keine Metadaten, im Gegensatz zu den Befehl Connect der Zieldatenbank wird nicht geladen.  
  
2.  Herstellen der Verbindung mit dem Ziel hergestellt werden kann, wird ein Fehler generiert, und die Konsolenanwendung beendet die Ausführung weiter.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Berichtsbefehle Skript-Datei  
Die Berichtsserver-Befehle Generieren von Berichten auf die Leistung der verschiedenen SSMA-konsolenaktivitäten.  
  
**Befehl**  
  
Generieren von Bewertungsbericht  
  
1.  Assessment-Berichte in der Quelldatenbank generiert.  
  
2.  Wenn die Verbindung mit der Quelldatenbank nicht ausgeführt werden, bevor Sie diesen Befehl ausführen, wird ein Fehler generiert, und die Konsolenanwendung beendet.  
  
3.  Während der Ausführung des Befehls eine Verbindung mit dem Datenbankserver auch führt dies in der Konsolenanwendung beendet.  
  
**Skript**  
  
1.  `assessment-report-folder:`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
2.  `object-name:`Gibt an, die Objekte, die zur Bewertung berichterstellung (sie können einzelne Objektnamen oder einen Gruppennamen für das Objekt verfügen) betrachtet.  
  
3.  `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
4.  `assessment-report-overwrite:`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
5.  `write-summary-report-to:`Gibt den Pfad, in dem der zusammenfassende Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **AssessmentReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
**Syntaxbeispiel:**  
  
```xml  
<generate-assessment-report  
  
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
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration--script-file-commands"></a>Migration Datei Skriptbefehle  
Die Befehle für die Migration konvertieren das Schema der Zieldatenbank, die dem Quellschema und Migrieren von Daten auf dem Zielserver.  
  
Die Standard-Konsolenausgabe festlegen, für die Migration Befehle ist 'Full' Ausgabebericht mit keine ausführliche-Fehlerberichterstattung: nur Zusammenfassung am Stammknoten Quell-Objekt.  
  
**Befehl**  
  
Convert-schema  
  
1.  Schemakonvertierung von der Quelle in das Zielschema durchgeführt.  
  
2.  Wenn die Verbindung mit der Quelle oder Ziel wird nicht ausgeführt, bevor Sie diesen Befehl ausführen, oder die Verbindung mit dem Datenbankserver Quell- oder Zieltabelle, die während der Ausführung des Befehls Fehler auftreten, wird ein Fehler generiert, und die Konsolenanwendung beendet wird.  
  
**Skript**  
  
1.  `conversion-report-folder:`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
2.  `object-name:`Gibt an, die Objekte, die zum Konvertieren von Schemas (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt besitzen) betrachtet.  
  
3.  `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
4.  `conversion-report-overwrite:`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
5.  `write-summary-report-to:`Gibt den Pfad, in dem der zusammenfassende Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **SchemaConversionReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Zusammenfassungsbericht erstellen, weist zwei weitere Unterkategorien:  
  
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
  
      <metabase-object object-name="<object-names>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Befehl**  
  
Migrieren von Daten  
  
1.  Migriert die Quelldaten zum Ziel.  
  
**Skript**  
  
1.  `object-name:`Gibt die Quelle-Objekte, die für die Migration in Betracht gezogen Daten (es kann haben Indivdual Objektnamen oder einen Gruppennamen-Objekt).  
  
2.  `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
3.  `write-summary-report-to:`Gibt den Pfad, in dem der zusammenfassende Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **DataMigrationReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
**Syntaxbeispiel:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>”  
  
   report-errors="true" verbose="true">  
  
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
  
   write-summary-report-to="<file-name/folder-name>”  
  
   report-errors="true" verbose="true"/>  
```  
  
## <a name="migration-preparation-script-file-command"></a>Migration Vorbereitung Datei Skriptbefehl  
Die Vorbereitung der Migration-Befehl startet schemazuordnung zwischen den Quell- und Zieldatenbanken.  
  
**Befehl**  
  
Map-schema  
  
Schemazuordnung der Quelldatenbank mit dem Zielschema.  
  
**Skript**  
  
1.  `source-schema`Gibt das Quellschema, das wir migrieren möchten.  
  
2.  `sql-server-schema`Gibt das Zielschema, in dem wir migriert werden soll.  
  
**Syntaxbeispiel:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Verwaltbarkeit Datei Skriptbefehle  
Die Verwaltbarkeit Befehle können mit der Quelldatenbank Zielobjekte Datenbank zu synchronisieren.  
  
> [!NOTE]  
> Die Standard-Konsolenausgabe festlegen, für die Migration Befehle ist 'Full' Ausgabebericht mit keine ausführliche-Fehlerberichterstattung: nur Zusammenfassung am Stammknoten Quell-Objekt.  
  
**Befehl**  
  
Synchronisieren von Ziel  
  
1.  Synchronisiert die Zielobjekte mit der Zieldatenbank an.  
  
2.  Wenn Sie diesen Befehl für die Quelldatenbank ausgeführt wird, ist ein Fehler aufgetreten.  
  
3.  Wenn die Verbindung mit der Zieldatenbank wird nicht ausgeführt, bevor Sie diesen Befehl ausführen oder die Verbindung mit dem Zielserver für die Datenbank ein Fehler auftritt, während der Ausführung des Befehls, wird ein Fehler generiert, und die Konsolenanwendung beendet.  
  
**Skript**  
  
1.  `object-name:`Gibt an, die Objekte, die für die Synchronisierung mit der Zieldatenbank (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt besitzen) betrachtet.  
  
2.  `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
3.  `on-error:`Gibt an, ob die Synchronisierungsfehler als Warnungen oder Fehler angegeben. Verfügbare Optionen für auf Fehler:  
  
    -   Bericht insgesamt als Warnung  
  
    -   Bericht-each-als-Warnung  
  
    -   Fail-Skript  
  
4.  `report-errors-to:`Speicherort der Fehlerbericht angibt, für der Synchronisierungsvorgang (optionales Attribut), wenn nur Ordnerpfad angegeben ist, dann Datei namentlich **TargetSynchronizationReport.XML** wird erstellt.  
  
**Syntaxbeispiel:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
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
  
1.  Aktualisiert die Datenquelle Objekte aus der Datenbank.  
  
2.  Wenn Sie diesen Befehl für die Zieldatenbank ausgeführt wird, wird ein Fehler generiert.  
  
**Skript**  
  
1.  `object-name:`Gibt die Quelle-Objekte, die beim Aktualisieren von der Quelldatenbank (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt haben) in Betracht gezogen.  
  
2.  `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
3.  `on-error:`Gibt an, ob die Synchronisierungsfehler als Warnungen oder Fehler angegeben. Verfügbare Optionen für auf Fehler:  
  
    -   Bericht insgesamt als Warnung  
  
    -   Bericht-each-als-Warnung  
  
    -   Fail-Skript  
  
4.  `report-errors-to:`Speicherort der Fehlerbericht angibt, für der Synchronisierungsvorgang (optionales Attribut), wenn nur Ordnerpfad angegeben ist, dann Datei namentlich **SourceDBRefreshReport.XML** wird erstellt.  
  
Ist eine oder mehrere Metabase-Knoten als-Befehlszeilenparameter erforderlich.  
  
**Syntaxbeispiel:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
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
  
1.  `object-name:`Gibt an, die Objekte, deren Skripts sind gespeichert werden sollen. (Es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt besitzen)  
  
2.  `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
3.  `metabase:`Gibt an, ob es die Quelle oder Ziel der Metabasis.  
  
4.  `destination:`Gibt den Pfad oder den Ordner, in dem das Skript muss gespeichert werden, wenn der Dateiname nicht klicken Sie dann einen Dateinamen in das Format (Attributwert Object_name) .out angegeben ist  
  
5.  `overwrite:`Bei "true" überschreibt es denselben Dateinamen vorhanden. Sie können die Werte (wahr/falsch) haben.  
  
**Syntaxbeispiel:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file-name/folder-name>”  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
oder  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file-name/folder-name>”  
  
      <metabase-object object-name="<object-name>"  
  
            object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Befehl**  
  
Convert-Sql-Anweisung  
  
1.  `context`Gibt den Schemanamen an.  
  
2.  `destination`Gibt an, ob die Ausgabe in einer Datei gespeichert werden sollen.  
  
    Wenn dieses Attribut nicht angegeben ist, wird die konvertierte T-SQL-Anweisung in der Konsole angezeigt. (optionales Attribut)  
  
3.  `conversion-report-folder`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
4.  `conversion-report-overwrite`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
5.  `write-converted-sql-to`Gibt die Datei Ordnerpfad, in dem die konvertierte T-SQL ist, gespeichert werden (oder). Wenn ein Pfad angegeben wird, zusammen mit der `sql-files` -Attribut, jeder Quelldatei klicken wird eine entsprechende Ziel T-SQL-Datei, die unter den angegebenen Ordner erstellt haben. Wenn ein Pfad angegeben wird, zusammen mit der `sql` -Attribut, das konvertierte T-SQL wird in eine Datei mit dem Namen Result.out unter den angegebenen Ordner geschrieben.  
  
6.  `sql`Gibt an, die MySQL-Sql-Anweisungen konvertiert werden, wird eine oder mehrere Anweisungen kann getrennt werden mithilfe einer ";"  
  
7.  `sql-files`Gibt den Pfad der Sql-Dateien mit T-SQL-Code konvertiert werden.  
  
8.  `write-summary-report-to`Gibt den Pfad, in dem der zusammenfassende Bericht generiert wird. Falls nur der Ordnerpfad angegeben wird, namentlich Datei **ConvertSQLReport.XML** wird erstellt. (optionales Attribut)  
  
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
  
   destination="stdout/file"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
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
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
oder  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-step"></a>Nächster Schritt  
Informationen zu Befehlszeilenoptionen finden Sie unter [Command Line Options SSMA-Konsole &#40; MySQLToSQL &#41; ](../../ssma/mysql/command-line-options-in-ssma-console-mysqltosql.md) .  
  
Weitere Informationen zu Beispiel Konsole-Skriptdateien, finden Sie unter [arbeiten mit der Konsole Skript-Beispieldateien &#40; MySQLToSQL &#41;](../../ssma/mysql/working-with-the-sample-console-script-files-mysqltosql.md)  
  
Der nächste Schritt hängt davon ab, auf die Anforderungen Ihres Projekts:  
  
1.  Zur Angabe eines Kennworts oder einer Exportieren / Importieren von Kennwörtern, finden Sie unter [Verwalten von Kennwörtern &#40; MySQLToSQL &#41; ](../../ssma/mysql/managing-passwords-mysqltosql.md).  
  
2.  Generieren von Berichten, finden Sie unter [Generieren von Berichten &#40; MySQLToSQL &#41; ](../../ssma/mysql/generating-reports-mysqltosql.md).  
  
3.  Behandlung von Problemen in der Konsole, finden Sie unter [Problembehandlung &#40; MySQLToSQL &#41; ](../../ssma/mysql/troubleshooting-mysqltosql.md).  
  

