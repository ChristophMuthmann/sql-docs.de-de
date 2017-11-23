---
title: Generieren von Berichten (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: abb4264a-622e-4215-af5b-14e309b8a399
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84298ed11ae25bf533b5916711d3634bddec1b98
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="generating-reports-accesstosql"></a>Generieren von Berichten (AccessToSQL)
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
    |4|Synchronisieren von Ziel|TargetSynchronizationReport&lt;n&gt;. XML|  
    |5|Aktualisieren von Datenbank|SourceDBRefreshReport&lt;n&gt;. XML|  
  
    > [!IMPORTANT]  
    > Ein Ausgabebericht unterscheidet sich von Assessment-Bericht. Die erste ist ein Bericht auf die Leistung eines ausgeführten Befehls beim, die zweite Datei ist ein XML-Bericht für die programmgesteuerte Nutzung.  
  
    Für die Befehlsoptionen für das Ausgabeberichte (von "SL". Nein. 2 bis 4, oben), finden Sie in der [Ausführen der Konsole SSMA &#40; AccessToSQL &#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md) Abschnitt.  
  
2.  Geben Sie den Umfang der Details, die Sie in den Ausgabebericht mithilfe der Einstellungen des Berichts Ausführlichkeit wünschen:  
  
    ||||  
    |-|-|-|  
    |**"SL". Nein.**|**Installationsbefehl und Parametersatz**|**Beschreibung der Ausgabe**|  
    |1|Ausführliche = "false"|Generiert einen zusammenfassenden Bericht der Aktivität.|  
    |2|Ausführliche = "true"|Generiert einen zusammengefassten und detaillierten Statusbericht für jede Aktivität an.|  
  
    > [!NOTE]  
    > Die oben angegebenen Einstellungen für die Ausführlichkeit gelten für generieren Bewertungsbericht, Convert-Schema, migrieren Sie Datenbefehle.  
  
3.  Geben Sie den Umfang der Details in die Fehlerberichte, die mit den Einstellungen für Fehlerberichterstattung entwurfsmöglichkeiten:  
  
    ||||  
    |-|-|-|  
    |**"SL". Nein.**|**Installationsbefehl und Parametersatz**|**Beschreibung der Ausgabe**|  
    |1|Melden von Fehlern = "false"|Keine Details zu Fehler / Warnung / Informationen Nachrichten.|  
    |2|Melden von Fehlern = "true"|Detaillierter Fehler / Warnung / Informationen Nachrichten.|  
  
    > [!NOTE]  
    > Die Einstellungen für Fehlerberichterstattung oben angegebenen gelten für generieren Bewertungsbericht, Convert-Schema, migrieren Sie Datenbefehle.  
  
**Beispiel:**  
  
```xml  
<generate-assessment-report  
  
    object-name="testschema"  
  
    object-type="Schemas"  
  
    verbose="yes"  
  
    report-erors="yes"  
  
    write-summary-report-to="$AssessmentFolder$\Report1.xml"  
  
    assessment-report-folder="$AssessmentFolder$\assesment_report"  
  
    assessment-report-overwrite="true"  
  
/>  
```  
  
### <a name="synchronize-target"></a>Synchronisieren von Ziel:  
Der Befehl **synchronisieren Ziel** hat **Bericht Fehler zu** -Parameter, der den Speicherort der Fehlerbericht für den Synchronisierungsvorgang angibt. Klicken Sie dann eine Datei namens **TargetSynchronizationReport&lt;n&gt;. XML** wird am angegebenen Speicherort erstellt, in denen  **&lt; n &gt;**  ist die Anzahl von eindeutigen Dateinamen, die mit einer Ziffer bei jeder Ausführung desselben Befehls inkrementiert.  
  
**Hinweis:** , wenn der Ordnerpfad angegeben ist, und klicken Sie dann 'Bericht-Fehler-to'-Parameter ein optionales Attribut für den Befehl "Synchronisieren-Ziel ist".  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="$TargetDB$.dbo"  
  
    on-error="fail-script"  
  
    report-errors-to="$SynchronizationReports$"  
  
/>  
```  
**Objektname:** gibt an, die Objekte, die für die Synchronisierung (sie können auch haben Indivdual Objektnamen oder einen Gruppennamen-Objekt) betrachtet.  
  
**Bei Fehler:** gibt an, ob die Synchronisierungsfehler als Warnungen oder Fehler angegeben. Verfügbare Optionen für auf Fehler:  
  
-   Bericht insgesamt als Warnung  
  
-   Bericht-each-als-Warnung  
  
-   Fail-Skript  
  
### <a name="refresh-from-database"></a>Aktualisierung aus Datenbank:  
Der Befehl **Aktualisierung aus Datenbank** hat **Bericht Fehler zu** -Parameter, der den Speicherort der Fehlerbericht für den Aktualisierungsvorgang angibt. Klicken Sie dann eine Datei namens **SourceDBRefreshReport&lt;n&gt;. XML** wird am angegebenen Speicherort erstellt, in denen  **&lt; n &gt;**  ist die Anzahl von eindeutigen Dateinamen, die mit einer Ziffer bei jeder Ausführung desselben Befehls inkrementiert.  
  
**Hinweis:** , wenn der Ordnerpfad angegeben ist, und klicken Sie dann 'Bericht-Fehler-to'-Parameter ein optionales Attribut für den Befehl "Synchronisieren-Ziel ist".  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="$SourceDatabaseStandard$"  
  
    object-type ="Databases"  
  
    on-error="fail-script"  
  
    report-errors-to="$RefreshDBFolder$\RefreshReport.xml"  
  
/>  
```  
**Objektname:** gibt an, die Objekte aktualisieren (es kann auch haben Indivdual Objektnamen oder einen Gruppennamen-Objekt) in Betracht gezogen.  
  
**Bei Fehler:** gibt an, ob die Aktualisierung Fehler als Warnungen oder Fehler anzugeben. Verfügbare Optionen für auf Fehler:  
  
-   Bericht insgesamt als Warnung  
  
-   Bericht-each-als-Warnung  
  
-   Fail-Skript  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen der Konsole SSMA (Access)](http://msdn.microsoft.com/en-us/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
