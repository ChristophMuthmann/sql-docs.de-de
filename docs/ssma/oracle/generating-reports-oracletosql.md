---
title: Generieren von Berichten (OracleToSQL) | Microsoft Docs
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
- Report Generation in Oracle Console, synchronize-target
- Report Generation in Oracle Console,refresh-from-database
- Report Generation in Oracle Console,write-summary-report-to
ms.assetid: ccad6262-01e1-447a-bd2b-c105154c80ce
caps.latest.revision: 17
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d82ebc3f1d6a3e88874430419d3a11baf5528695
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="generating-reports-oracletosql"></a>Generieren von Berichten (OracleToSQL)
Berichte über bestimmte Aktivitäten mit Befehlen durchgeführt werden in SSMA-Konsole auf Objektebene-Struktur generiert.  
  
Verwenden Sie das folgende Verfahren zum Generieren von Berichten:  
  
1.  Geben Sie die **schreiben Zusammenfassung-Bericht-in** Parameter. Der verknüpfte Bericht wird als Dateiname gespeichert (falls angegeben), oder geben Sie im Ordner "". Der Dateiname ist System vordefiniert, wie in der Tabelle unten WHERE-, erwähnt  **&lt; n &gt;**  ist die Anzahl von eindeutigen Dateinamen, die mit einer Ziffer bei jeder Ausführung desselben Befehls inkrementiert.  
  
    Die Berichte Vis gegenüber Befehle sind:  
  
    ||||  
    |-|-|-|  
    |**"SL". Nein.**|**Befehl**|**Berichtstitel**|  
    |1|Generieren von Bewertungsbericht|AssessmentReport&lt;n&gt;. XML|  
    |2|Convert-schema|SchemaConversionReport&lt;n&gt;. XML|  
    |3|Migrieren von Daten|DataMigrationReport&lt;n&gt;. XML|  
    |4|Convert-Sql-Anweisung|ConvertSQLReport&lt;n&gt;. XML|  
    |5|Synchronisieren von Ziel|TargetSynchronizationReport&lt;n&gt;. XML|  
    |6|Aktualisieren von Datenbank|SourceDBRefreshReport&lt;n&gt;. XML|  
  
    > [!IMPORTANT]  
    > Ein Ausgabebericht unterscheidet sich von Assessment-Bericht. Die erste ist ein Bericht auf die Leistung eines ausgeführten Befehls beim, die zweite Datei ist ein XML-Bericht für die programmgesteuerte Nutzung.  
  
    Für die Befehlsoptionen für das Ausgabeberichte (von "SL". Nein. 2 bis 4, oben), finden Sie in der [Ausführen der Konsole SSMA &#40; OracleToSQL &#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) Abschnitt.  
  
2.  Geben Sie den Umfang der Details, die Sie in den Ausgabebericht mithilfe der Einstellungen des Berichts Ausführlichkeit wünschen:  
  
    ||||  
    |-|-|-|  
    |**"SL". Nein.**|**Installationsbefehl und Parametersatz**|**Beschreibung der Ausgabe**|  
    |1|Ausführliche = "false"|Generiert einen zusammenfassenden Bericht der Aktivität.|  
    |2|Ausführliche = "true"|Generiert einen zusammengefassten und detaillierten Statusbericht für jede Aktivität an.|  
  
    > [!NOTE]  
    > Die oben angegebenen Einstellungen für die Ausführlichkeit gelten für generieren Bewertungsbericht, Convert-Schema, Migrieren von Daten, Convert-Sql-Anweisung Befehle zur Verfügung.  
  
3.  Geben Sie den Umfang der Details in die Fehlerberichte, die mit den Einstellungen für Fehlerberichterstattung entwurfsmöglichkeiten:  
  
    ||||  
    |-|-|-|  
    |**"SL". Nein.**|**Installationsbefehl und Parametersatz**|**Beschreibung der Ausgabe**|  
    |1|Melden von Fehlern = "false"|Keine Details zu Fehler / Warnung / Informationen Nachrichten.|  
    |2|Melden von Fehlern = "true"|Detaillierter Fehler / Warnung / Informationen Nachrichten.|  
  
    > [!NOTE]  
    > Die Einstellungen für Fehlerberichterstattung oben angegebenen gelten für generieren Bewertungsbericht, Convert-Schema, Migrieren von Daten, Convert-Sql-Anweisung Befehle zur Verfügung.  
  
**Beispiel:**  
  
```  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"/>  
```  
  
### <a name="synchronize-target"></a>Synchronisieren von Ziel:  
Der Befehl **synchronisieren Ziel** hat **Bericht Fehler zu** -Parameter, der den Speicherort der Fehlerbericht für den Synchronisierungsvorgang angibt. Klicken Sie dann eine Datei namens **TargetSynchronizationReport&lt;n&gt;. XML** wird am angegebenen Speicherort erstellt, in denen  **&lt; n &gt;**  ist die Anzahl von eindeutigen Dateinamen, die mit einer Ziffer bei jeder Ausführung desselben Befehls inkrementiert.  
  
**Hinweis:** , wenn der Ordnerpfad angegeben ist, und klicken Sie dann 'Bericht-Fehler-to'-Parameter ein optionales Attribut für den Befehl "Synchronisieren-Ziel ist".  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**Objektname:** gibt an, die Objekte, die für die Synchronisierung (sie können auch haben Indivdual Objektnamen oder einen Gruppennamen-Objekt) betrachtet.  
  
**Bei Fehler:** gibt an, ob die Synchronisierungsfehler als Warnungen oder Fehler angegeben. Verfügbare Optionen für auf Fehler:  
  
-   Bericht insgesamt als Warnung  
  
-   Bericht-each-als-Warnung  
  
-   Fail-Skript  
  
### <a name="refresh-from-database"></a>Aktualisierung aus Datenbank:  
Der Befehl **Aktualisierung aus Datenbank** hat **Bericht Fehler zu** -Parameter, der den Speicherort der Fehlerbericht für den Aktualisierungsvorgang angibt. Klicken Sie dann eine Datei namens **SourceDBRefreshReport&lt;n&gt;. XML** wird am angegebenen Speicherort erstellt, in denen  **&lt; n &gt;**  ist die Anzahl von eindeutigen Dateinamen, die mit einer Ziffer bei jeder Ausführung desselben Befehls inkrementiert.  
  
**Hinweis:** , wenn der Ordnerpfad angegeben ist, und klicken Sie dann 'Bericht-Fehler-to'-Parameter ein optionales Attribut für den Befehl "Synchronisieren-Ziel ist".  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**Objektname:** gibt an, die Objekte aktualisieren (es kann auch haben Indivdual Objektnamen oder einen Gruppennamen-Objekt) in Betracht gezogen.  
  
**Bei Fehler:** gibt an, ob die Aktualisierung Fehler als Warnungen oder Fehler anzugeben. Verfügbare Optionen für auf Fehler:  
  
-   Bericht insgesamt als Warnung  
  
-   Bericht-each-als-Warnung  
  
-   Fail-Skript  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen der Konsole SSMA (Oracle)](http://msdn.microsoft.com/en-us/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  

