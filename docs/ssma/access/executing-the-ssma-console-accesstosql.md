---
title: "Ausführen der Konsole SSMA (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
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
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
caps.latest.revision: "25"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 29f9c2bbce707aa08ce5cff918965e65f66d8370
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="executing-the-ssma-console-accesstosql"></a>Ausführen der Konsole SSMA (AccessToSQL)
Microsoft stellt Ihnen eine Reihe robuster Skriptbefehle für die Datei und Befehlszeilenoptionen zum Ausführen und Steuern von SSMA-Aktivitäten. In den folgenden Abschnitten ausführlich identisch.  
  
## <a name="project--script-file-commands"></a>Projekt Datei Skriptbefehle  
Das Handle des Projekt Befehle, die beim Erstellen von Projekten, öffnen, speichern und Beenden von Projekten.  
  
**Befehl**  
  
Erstellen neuer-Projekt: erstellt ein neues SSMA-Projekt.  
  
**Skript**  
  
-   `project-folder`Gibt den Ordner, der das erste erstellte Projekt an.  
  
-   `project-name`Gibt den Namen des Projekts an. {String}  
  
-   `overwrite-if-exists`Optionales Attribut gibt an, ob ein vorhandenes Projekt überschrieben werden soll. {Boolean}  
  
-   `project-type`ist ein optionales Attribut.  Die folgenden Optionen sind für Projekttyp verfügbar:  
  
    -   SQL Server 2005  
  
    -   SQL Server 2008  
  
    -   SQL-Server-2012  
  
    -   SQL-Server-2014  
  
    -   SQL Server 2016  
  
    -   SQL azure  
  
    Standardwert ist "Sql Server 2008".  
  
**Beispiel:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type=”<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>”  
  
/>  
```  
Attribut "überschreiben-If-exists" ist **"false"** standardmäßig.  
  
Attribut "Projekttyp" ist **Sql Server 2008** standardmäßig.  
  
**Befehl**  
  
Open-Projekt: Öffnet ein vorhandenes Projekt.  
  
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
**Hinweis:** SSMA für Access-Konsole Anwendung unterstützt Abwärtskompatibilität. Sie werden können zum Öffnen von Projekten, die von der früheren Version von SSMA erstellt.  
  
**Befehl**  
  
Save-Projekt: Migrationsprojekts speichert.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<save-project/>  
```  
**Befehl**  
  
Close-Projekt: Migrationsprojekts schließt.  
  
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
  
Die **Durchsuchen** Features der Benutzeroberfläche wird in der Konsole nicht unterstützt.  
  
Die **Windows-Authentifizierung** und **Port** Parameter sind nicht anwendbar, wenn die Verbindung mit SQL Azure.  
  
Weitere Informationen zu "Skriptdateien erstellen", finden Sie unter [Skriptdateien erstellen &#40; AccessToSQL &#41; ](../../ssma/access/creating-script-files-accesstosql.md).  
  
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
  
Load-Access-Datenbank: zum Laden von Access-Datenbankdateien verwendet  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
oder  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
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
<force-load  
  
  object-name="<object-name>"  
  
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
  
-   Die Ziel-SQL Server- bzw. SQL Azure-Datenbank her, und hohe Ebene Metadaten der Zieldatenbank, aber nicht die Metadaten vollständig geladen.  
  
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
  
-   `assessment-report-folder:`Gibt an, Ordner, in dem Bericht die Beurteilung kann gespeichert werden soll. (optionales Attribut)  
  
-   `object-name:`Gibt an, die Objekte, die zur Bewertung berichterstellung (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt besitzen) betrachtet.  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `assessment-report-overwrite:`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-summary-report-to:`Gibt den Pfad, in dem der Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **AssessmentReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
**Syntaxbeispiel:**  
  
```xml  
<generate-assessment-report  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  
  write-summary-report-to="<file>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  conversion-report-folder="<folder>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
oder  
  
```xml  
<generate-assessment-report  
  
  conversion-report-folder="<folder>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
    <metabase-object object-name="ssma.Procedures"  
  
        object-type="category"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Migration Datei Skriptbefehle  
Die Befehle für die Migration konvertieren das Schema der Zieldatenbank, die dem Quellschema und Migrieren von Daten auf dem Zielserver.  
  
Die Standard-Konsolenausgabe festlegen, für die Migration Befehle ist 'Full' Ausgabebericht mit keine ausführliche-Fehlerberichterstattung: nur Zusammenfassung am Stammknoten Quell-Objekt.  
  
**Befehl**  
  
Convert-schema  
  
-   Schemakonvertierung von der Quelle in das Zielschema durchgeführt.  
  
-   Wenn die Verbindung mit der Quelle oder Ziel wird nicht ausgeführt, bevor Sie diesen Befehl ausführen, oder die Verbindung mit dem Datenbankserver Quell- oder Zieltabelle, die während der Ausführung des Befehls Fehler auftreten, wird ein Fehler generiert, und die Konsolenanwendung beendet wird.  
  
**Skript**  
  
-   `conversion-report-folder:`Gibt an, Ordner, in dem der Assessment-Bericht gespeichert werden kann. (optionales Attribut)  
  
-   `object-name:`Gibt die Quelle-Objekte, die für das Konvertieren eines Schemas (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt haben) in Betracht gezogen.  
  
-   `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
-   `conversion-report-overwrite:`Gibt an, ob die Berichtsordner Assessment zu überschreiben, wenn sie bereits vorhanden ist.  
  
    **Standardwert:** "false". (optionales Attribut)  
  
-   `write-summary-report-to:`Gibt den Pfad, in dem der Bericht generiert wird.  
  
    Falls nur der Ordnerpfad angegeben wird, namentlich Datei **SchemaConversionReport&lt;n&gt;. XML** wird erstellt. (optionales Attribut)  
  
    Erstellen des Berichts verfügt über zwei weitere Unterkategorien:  
  
    -   `report-errors`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
    -   `verbose`(= "wahr/falsch", Standardwert "false" (optionale Attribute))  
  
**Syntaxbeispiel:**  
  
```xml  
<convert-schema  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  write-summary-report-to="<filepath/folder>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
oder  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder>"         (optional)  
  
  conversion-report-overwrite="<true/false>"  (optional)  
  
  <metabase-object object-name="ssma.Procedures"  
  
    object-type="category"/>  
  
</convert-schema>  
```  
**Befehl**  
  
Migrieren von Daten  
  
1.  Migriert die Quelldaten zum Ziel.  
  
**Skript**  
  
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
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true">  
  
    <metabase-object object-name="ssma.TT1"/>  
  
    <metabase-object object-name="ssma.TT2"/>  
  
    <metabase-object object-name="ssma.TT3"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
oder  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```  
**Befehl**  
  
Tabellen verknüpfen: mit diesem Befehl verknüpft die Quelltabelle (Access) mit der Zieltabelle.  
  
**Skript**  
  
**Syntaxbeispiel:**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```  
oder  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```  
**Befehl**  
  
Aufheben der Verknüpfung Tabellen: mit diesem Befehl hebt die Verknüpfung mit der Quelltabelle (Access) in der Zieltabelle.  
  
**Skript**  
  
**Beispiele für die Abfrageausdruckssyntax:**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```  
oder  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Migration Vorbereitung Datei Skriptbefehle  
Die Vorbereitung der Migration-Befehl startet schemazuordnung zwischen den Quell- und Zieldatenbanken.  
  
**Befehl**  
  
Map-Schema: Schema-Zuordnung der Quelldatenbank mit dem Zielschema.  
  
**Skript**  
  
-   `source-schema`Gibt das Quellschema, das wir migrieren möchten.  
  
-   `sql-server-schema`Gibt das Zielschema, in dem wir migriert werden soll.  
  
**Syntaxbeispiel:**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>Verwaltbarkeit Befehle  
Die Verwaltbarkeit Befehle können mit der Quelldatenbank Zielobjekte Datenbank zu synchronisieren.  
  
Die Standard-Konsolenausgabe festlegen, für die Migration Befehle ist 'Full' Ausgabebericht mit keine ausführliche-Fehlerberichterstattung: nur Zusammenfassung am Stammknoten Quell-Objekt.  
  
**Befehl**  
  
Synchronisieren von Ziel  
  
1.  Synchronisiert die Zielobjekte mit der Zieldatenbank an.  
  
2.  Wenn Sie diesen Befehl für die Quelldatenbank ausgeführt wird, ist ein Fehler aufgetreten.  
  
3.  Wenn die Verbindung mit der Zieldatenbank wird nicht ausgeführt, bevor Sie diesen Befehl ausführen oder die Verbindung mit dem Zielserver für die Datenbank ein Fehler auftritt, während der Ausführung des Befehls, wird ein Fehler generiert, und die Konsolenanwendung beendet.  
  
**Skript**  
  
1.  `object-name:`Gibt an, die Ziel-Objekte, die für die Synchronisierung mit der Zieldatenbank (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt besitzen) betrachtet.  
  
2.  `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
3.  `on-error:`Gibt an, ob die Synchronisierungsfehler als Warnungen oder Fehler angegeben. Verfügbare Optionen für auf Fehler:  
  
    -   Bericht insgesamt als Warnung  
  
    -   Bericht-each-als-Warnung  
  
    -   Fail-Skript  
  
4.  `report-errors-to:`Speicherort der Fehlerbericht angibt, für der Synchronisierungsvorgang (optionales Attribut), wenn nur Ordnerpfad angegeben ist, dann Datei namentlich **TargetSynchronizationReport.XML** wird erstellt.  
  
**Syntaxbeispiel:**  
  
```xml  
<synchronize-target  
  
  object-name="ots_triggers.dbo"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
oder  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```  
oder  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```  
**Befehl**  
  
Aktualisieren von Datenbank  
  
-   Aktualisiert die Datenquelle Objekte aus der Datenbank.  
  
-   Wenn Sie diesen Befehl für die Zieldatenbank ausgeführt wird, wird ein Fehler generiert.  
  
**Skript**  
  
Ist eine oder mehrere Metabase-Knoten als-Befehlszeilenparameter erforderlich.  
  
1.  `object-name:`Gibt die Quelle-Objekte, die beim Aktualisieren von der Quelldatenbank (es kann Indivdual Objektnamen oder einen Gruppennamen für das Objekt haben) in Betracht gezogen.  
  
2.  `object-type:`Gibt den Typ des Objekts im Objekt-Name-Attribut angegeben ist (wenn Objektkategorie angegeben wird, dann Objekttyp "Category").  
  
3.  `on-error:`Gibt an, ob die Aktualisierung Fehler als Warnungen oder Fehler angegeben. Verfügbare Optionen für auf Fehler:  
  
    -   Bericht insgesamt als Warnung  
  
    -   Bericht-each-als-Warnung  
  
    -   Fail-Skript  
  
4.  `report-errors-to:`Speicherort der Fehlerbericht angibt, für der Aktualisierungsvorgang (optionales Attribut) Wenn nur Ordnerpfad angegeben ist, klicken Sie dann Datei namentlich **SourceDBRefreshReport.XML** wird erstellt.  
  
**Syntaxbeispiel:**  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.TT1"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
oder  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```  
oder  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Skriptbefehle für die Datei von Generation Skript  
Skriptgenerierung Befehle helfen zu die Konsolenausgabe in einer Skriptdatei speichern.  
  
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
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"  
  
  destination="<file/folder>"  
  
  overwrite="<true/false>"             (optional)  
  
/>  
```  
oder  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-step"></a>Nächster Schritt  
Informationen zu Befehlszeilenoptionen finden Sie unter [Command Line Options SSMA-Konsole &#40; AccessToSQL &#41; ](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) .  
  
Informationen zum Beispiel Konsole-Skriptdateien, finden Sie unter [arbeiten mit der Beispiel-Konsole Skript FilesExecuting SSMA-Konsole &#40; AccessToSQL &#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
Der nächste Schritt hängt davon ab, auf die Anforderungen Ihres Projekts:  
  
-   Zur Angabe eines Kennworts oder einer Exportieren / Importieren von Kennwörtern, finden Sie unter [Verwalten von Kennwörtern &#40; AccessToSQL &#41; ](../../ssma/access/managing-passwords-accesstosql.md).  
  
-   Generieren von Berichten, finden Sie unter [Generieren von Berichten &#40; AccessToSQL &#41; ](../../ssma/access/generating-reports-accesstosql.md).  
  
-   Behandlung von Problemen in der Konsole, finden Sie unter [Problembehandlung &#40; AccessToSQL &#41; ](../../ssma/access/troubleshooting-accesstosql.md).  
  
