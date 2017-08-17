---
title: "Änderungsprotokoll für SQL Server Data Tools (SSDT) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b071f8b8-c8e5-44e0-bbb6-04804dd1863a
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 3f12671ace99d5fefc199c7b1c2db31e5b3cfade
ms.openlocfilehash: 51cfeaf15f9d7a01ce55968907e0074f7f2cb955
ms.contentlocale: de-de
ms.lasthandoff: 08/08/2017

---
# <a name="changelog-for-sql-server-data-tools-ssdt"></a>Änderungsprotokoll für SQL Server Data Tools (SSDT)
Dieses Änderungsprotokoll bezieht sich auf [SQL Server Data Tools (SSDT) für Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx).  
  
Ausführliche Beiträge zu den Neuigkeiten und Änderungen finden Sie auf [the SSDT Team blog (dem SSDT-Team-Blog)](https://blogs.msdn.microsoft.com/ssdt/)



## <a name="ssdt-172"></a>SSDT 17.2
Buildnummer: 14.0.61707.300

### <a name="whats-new"></a>Neues


**AS-Projekte:**
- Die Sicherheit auf Objektebene kann nun im Dialogfeld *Rollen* konfiguriert werden, um erweiterte Sicherheit in tabellarischen Modellen mit Kompatibilitätsgrad 1400 zu gewährleisten.
- Neue AAD-Rollenmemberauswahl für Benutzer ohne E-Mail-Adressen in AS Azure-Modellen in SSDT AS-Projekten für VS2017.
- Neue Projekteigenschaft „Immer auffordern“ für tabellarische SSDT AS-Projekte in AS Azure, um das Verhalten der Zwischenspeicherung von Anmeldeinformationen in der ADAL anzupassen.


### <a name="bug-fixes"></a>Fehlerbehebungen

**Allgemein**
- Aktualisierte Branding-Verweise für SQL Server 2017.

**AS-Projekte**
- Die Leistung wurde bedeutend verbessert, um die Benutzerfreundlichkeit bei der Weitergabe von Änderungen an DAX-Measures und anderen Modellbearbeitungen zu erhöhen.
- Es wurde eine Reihe von Problemen mit der Integration von Power Query in Analysis Services-Projekte, die tabellarische Modelle mit Kompatibilitätsgrad 1400 verwenden, behoben.
- Es wurde ein Problem mit mehrdimensionalen Projekten in VS2017 behoben, bei dem der Aggregation-Designer möglicherweise nicht lädt.
- Es wurde ein Problem beim Ziehen eines Elements in das mehrdimensionale DSV-Diagramm in Analysis Services behoben, das einen Absturz von VS2017 verursachen konnte.
- Es wurde ein Problem mit AS-Projekten behoben, bei dem das Dialogfeld für die Bereitstellung in Visual Studio nicht immer im Vordergrund angezeigt wurde.
- Der Analysis Services-Import wurde aus dem Data Marketplace als Datenquelle entfernt, da der Dienst außer Betrieb genommen wurde.
- Es wurde ein Problem behoben, bei dem der Tabellen-Designer deaktiviert blieb, nachdem eine neue Tabelle aus einer bestehenden Datenquelle mit dem Tabellenmodell-Explorer importiert wurde.
- Es wurde ein Problem behoben, bei dem die Elemente „Importieren aus Datenquelle“ und „Datenquelle hinzufügen“ im Menü „Modelle“ im falschen Kontext verborgen blieben.
- Die Benutzerfreundlichkeit bei der Erstellung eines Measure aus dem Tabellenmodell-Explorer wurde verbessert, indem der Fokus nicht mehr zurück zu der Spalte gewechselt werden muss, die für die Erstellung des Measure verwendet wurde.
- Die alten Datenbankdateien werden nun bereinigt, wenn vom in die tabellarischen AS-Projekte integrierten Arbeitsbereich zum expliziten Arbeitsbereichsserver gewechselt wird.
- Es wurde ein Problem mit tabellarischen AS-Projekten für 1400-Modelle behoben, bei dem der Zustand des Kontrollkästchens „Sicherheit auf Zeilenebene“ auf der Benutzeroberfläche zunächst als deaktiviert angezeigt wird, unabhängig vom tatsächlich zugrunde liegenden Objektstatus.
- Es wurden ein Absturz und eine nicht behandelte Ausnahme behoben, die auftreten konnten, wenn Text- oder Excel-Dateien mit Power Query in ein tabellarisches Modell mit Kompatibilitätsgrad 1400 importiert wurden.
- Es wurde ein Problem behoben, das bei der Bildlaufleiste des Steuerelements in der DAX-Formel im tabellarischen AS-Modell-Designer auftreten konnte.
- Es wurde ein Problem behoben, das beim Ändern einer Mashupdatenquelle in Power Query auftreten konnte, wenn diese eine Benutzernamen- oder Kennwortauthentifizierung beinhaltet.
- Es wurde ein Problem behoben, das eine Datenquelle am Verbinden hindern konnte, wenn zusätzliche Eigenschaften in der Verbindungszeichenfolge festgelegt sind.
- Es wurde ein Problem behoben, das einen Absturz von VS verursachen konnte, wenn mehrere tabellarische AS-Modellprojekte geladen und der zweite Modell-Designer geschlossen wurde, ohne vorher mit einem Element des Designers zu interagieren.
- Es wurde ein Problem behoben, bei denen Änderungen an der Formatierung von KPI in manchen Fällen nicht beibehalten wurden.
- Es wurde ein Problem mit der Benutzeroberfläche von Power Query behoben, bei dem im Menü der falsche Zustand des Kontrollkästchens für die Bearbeitungsleiste angezeigt wurde.
- Es wurde ein Problem mit tabellarischen AS-Projekten mit Kompatibilitätsgrad 1400 und Power Query-Datenquellen behoben, bei dem ein Absturz von VS auftreten konnte, wenn das Menü „Datenquelle ändern“ im Tabellenmodell-Explorer angeklickt wurde.
- Es wurde ein zeitweiliger Fehler behoben, bei dem das Laden eines tabellarischen 1400-Modells möglicherweise den Fehler *Datei oder Assembly ‚Microsoft.ProBI.MashupLibrary‘ konnte nicht geladen werden* angezeigt hat.

**RS-Projekte**
- Die Benutzereinstellungen für den Auswahlzustand der Textfelder für das RS-Lineal und die RS-Parameter wird sitzungsübergreifend korrekt gespeichert.

**IS-Projekte**
- Es wurde ein Problem behoben, bei dem der Container „ADO/ADO.NET ForEachLoop“ nicht ordnungsgemäß angezeigt wurde
- Es wurde ein Problem behoben, bei dem einige Aufgaben/Komponenten/Assistenten nicht lokalisiert wurden
- Die neueste *TargetServerVersion* wurde von „SQL Server vNext“ zu „SQL Server 2017“ geändert


## <a name="ssdt-171"></a>SSDT 17.1
Buildnummer: : 14.0.61705.170

### <a name="whats-new"></a>Neues
**AS-Projekte:**
- Benutzer können Codierungshinweise für Spalten in der Benutzeroberfläche von Modellen vom 1400-Typ angeben
- Das nicht auf Datenmodellen basierende IntelliSense ist nun im Offlinemodus verfügbar
- Der tabellarische Modell-Explorer enthält nun einen Knoten, der benannte M-Ausdrücke für das Modell (Tabellenmodelle mit Kompatibilitätsgrad 1400) verfügbar macht
- Die Personenauswahl in Azure Active Directory ist nun ähnlich wie das IAM im Microsoft Azure-Portal verfügbar, wenn Rollenmitglieder in tabellarischen Modellen eingerichtet werden

**Datenbankprojekte:**
- Aktualisiert auf DacFx 17.1

### <a name="bug-fixes"></a>Fehlerbehebungen
- Es wurde ein Problem behoben, bei dem der Gruppenname des Business Intelligence-Designers in den Visual Studio-Optionen in VS2017 nicht korrekt angezeigt wurde
- Es wurde ein Problem behoben, bei dem es zu einem Absturz kommen konnte, wenn eine Code Map für eine Projektmappe mit einem Berichtsprojekt oder einem AS-Projekt erstellt wurde
- Es wurden eine Reihe von Problemen behoben, die bei der Integration von Power Query in Tabellenmodelle mit Kompatibilitätsgrad 1400 von Analysis Services auftreten konnten
- Es wurde ein Problem im neuen Toolfenster des DAX-Editors behoben, bei dem der Zuweisungsoperator beim Definieren eines Measure nicht in einer eigenen Zeile stehen konnte
- Es wurde ein Problem, bei dem das Aktualisieren der tabellarischen Measureanzeige bei der Umbenennung von Measures in Perspektive verhindert wurde
- Aktualisierung des in Analysis Services integrierten Arbeitsbereichmodells und des tabellarischen Objektmodells, wodurch eine Regression repariert werden konnte, durch die tabellarische Modelle vom 1200-Typ, die Translationen enthalten, nicht auf einem Server von SQL Server 2016 Analysis Service bereitgestellt werden konnten
- Es wurde ein Leistungsproblem behoben, bei dem das Erstellen und Löschen von neuen tabellarischen Datenquellen vom 1400-Typ sehr langsam erfolgte
- Es wurde ein Problem behoben, bei dem das DSV-Diagramm bei mehrdimensionalen Modellen das Rendern beenden konnte, wenn die Ansicht schnell zwischen verschiedenen DSVs gewechselt wurde

## <a name="dacfx-171"></a>DacFx 17.1
- Es wurde ein Problem bei der Verschlüsselung einer Spalte mit einer speicheroptimierten Tabelle, die andere Identitätsspalten enthält, behoben
- SQLDOM-Unterstützung für die CATALOG_COLLATION-Option für CREATE DATABASE

## <a name="dacfx-1701"></a>DacFx 17.0.1 
- Behebung eines Problems mit Datenbanken mit asymmetrischem Schlüssel durch ein HSM mit einem [Connect item (Connect-Element)](https://connect.microsoft.com/SQLServer/feedback/details/3132749/sqlpackage-exe-fails-when-extracting-a-database-which-contains-an-asymmetric-key-using-an-ekm-provider) eines EKM-Anbieters

## <a name="ssdt-170-supports-up-to-sql-server-2017"></a>SSDT 17.0 (Unterstützung bis SQL Server 2017)
Buildnummer: : 14.0.61704.140

### <a name="whats-new"></a>Neues
**Datenbankprojekte:**
- Das Ändern eines gruppierten Index in einer Ansicht blockiert keine Bereitstellungen mehr
- Schemavergleichszeichenfolgen, die mit der Spaltenverschlüsselung in Zusammenhang stehen, verwenden den tatsächlichen Namen und nicht den Instanznamen.   
- Eine neue Befehlszeilenoption wurde zu SqlPackage hinzugefügt: ModelFilePath.  Dies bietet eine Option für fortgeschrittene Benutzer, um eine externe model.xml-Datei für Import-, Veröffentlichungs- und Skriptvorgänge anzugeben   
- Die DacFx-API wurde erweitert, um die universale Azure AD-Authentifizierung und die mehrstufige Authentifizierung (MFA) zu unterstützen

**IS-Projekte:**
- Die OData-Quelle und der OData-Verbindungs-Manager von SSIS unterstützen jetzt Verbindungen mit den OData-Feeds von Microsoft Dynamics AX Online und Microsoft Dynamics CRM Online.
- SSIS-Projekte unterstützen jetzt die Zielserverversion von „SQL Server 2017“ 
- Unterstützung für CDC Control Task, CDC Splitter und CDC Source beim Adressieren von SQL Server 2017. 

**AS-Projekte:**
- Integration der Analysis Services-Power Query (tabellarisches Modell mit Kompatibilitätsgrad 1400):
    - DirectQuery ist für SQL Oracle und Teradata verfügbar, wenn der Benutzer Treiber von Drittanbietern installiert hat
    - Hinzufügen von Spalten anhand eines Beispiels in PowerQuery
    - Datenzugriffsoptionen in Modellen vom 1400-Typ (vom M-Modul verwendete Eigenschaften auf Modellebene)
        - Aktivieren von schnellem Kombinieren (der Standardwert ist „FALSE“, wenn er auf „TRUE“ gesetzt wird, ignoriert das Mashup-Modul die Datenschutzebenen der Datenquellen beim Kombinieren von Daten)
        - Aktivieren von Legacy-Umleitungen (der Standardwert ist „FALSE“, wenn er auf „TRUE“ gesetzt wird, folgt das Mashup-Modul HTTP-Umleitungen, die potenziell unsicher sind.  Beispielsweise eine Umleitung von einer HTTPS- zu einer HTTP-URI)  
        - Zurückgeben von Fehlerwerten als NULL (der Standardwert ist „FALSE“, wenn er auf „TRUE“ gesetzt wird, werden Fehler auf Zellebene als NULL zurückgegeben. Wenn der Wert „FALSE“ ist, wird eine Ausnahme ausgelöst, falls die Zelle einen Fehler enthält)  
    - Zusätzliche Datenquellen (Dateidatenquellen) mithilfe von PowerQuery
        - Excel 
        - Text/CSV 
        - Xml 
        - JSON 
        - Ordner 
        - Access-Datenbank 
        - Azure BLOB-Speicher 
    - Lokalisierte PowerQuery-Benutzeroberfläche
- DAX-Editor-Toolfenster
    - Verbesserte DAX-Bearbeitungsoptionen für Measures, berechnete Spalten und Ausdrücken für Detailzeilen. Diese sind über das Menü „Andere Fenster anzeigen“ in SSDT verfügbar
    - Verbesserungen an DAX-Parser/IntelliSense


**RS-Projekte:**
- Ein integrierbares RVC-Steuerelement, das SSRS 2016 unterstützt, ist jetzt verfügbar

### <a name="bug-fixes"></a>Behebung von Programmfehlern
**AS-Projekte:**
- Der Fehler bei der Vorlagenpriorität für BI-Projekte wurde behoben, damit sie nicht oben in den Kategorien „New Projects“ (Neue Projekte) in Visual Studio angezeigt werden
- Ein VS-Absturz wurde behoben, der in seltenen Fällen auftreten kann, wenn eine SSIS-, SSAS- oder SSRS-Projektmappe geöffnet ist
- Tabellarisch: unterschiedlichste Erweiterungen und Leistungsproblembehebungen für die DAX-Analyse und die Bearbeitungsleiste.
- Tabellarisch: Der tabellarische Modellexplorer wird nicht mehr angezeigt, wenn keine SSAS-Tabellenprojekte geöffnet sind.
- Multidimensional: Das Problem wurde behoben, dass das Verarbeitungsdialogfeld auf hochauflösenden Computern nicht mehr verwendet werden konnte.
- Tabellarisch: Das Problem wurde behoben, dass bei SSDT ein Fehler auftritt, wenn ein beliebiges BI-Projekt geöffnet wird, wenn SSMS bereits geöffnet ist. [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3100900/ssdt-faults-when-opening-any-bi-project-when-ssms-is-already-open)
- Tabellarisch: Das Problem wurde behoben, dass Hierarchien nicht ordnungsgemäß in die BIM-Datei in einem 1103-Modell gespeichert werden konnten. [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3105222/vs-2015-ssdt)
- Tabellarisch: Das Problem wurde behoben, dass der Modus „Integrierte Arbeitsbereiche“ auf 32-Bit-Computern erlaubt war, obwohl er dort nicht unterstützt wird.
- Tabellarisch: Das Problem wurde behoben, dass beim Klicken auf eine beliebige Stelle im Halbauswahlmodus (z.B. das Klicken auf eine Maßnahme bei der Eingabe eines DAX-Ausdrucks) Abstürze ausgelöst werden konnten.
- Tabellarisch: Das Problem wurde behoben, dass der Bereitstellungsassistent die Name-Eigenschaft des Modells auf „Model“ zurücksetzt. [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3107018/ssas-deployment-wizard-resets-modelname-to-model)
- Tabellarisch: Das Problem wurde behoben, dass durch das Auswählen einer Hierarchie in TME Eigenschaften angezeigt werden sollten, wenn Diagrammsicht nicht ausgewählt ist.
- Tabellarisch: Das Problem wurde behoben, dass beim Einfügen aus bestimmten Anwendungen in die DAX-Bearbeitungsleiste Bilder und andere Inhalte statt des Texts eingefügt wurden.
- Tabellarisch: Das Problem wurde behoben, dass einige alte Modelle in 1103 nicht geöffnet werden konnten, da Measures mit einer bestimmten Definition vorhanden waren.
- Tabellarisch: Das Problem wurde behoben, dass XEvent-Sitzungen nicht gelöscht werden konnten.
- Ein Fehler wurde behoben, bei dem der Versuch, AS-smproj-Dateien mit devenv.com zu erstellen, fehlschlug
- Ein Fehler wurde behoben, bei dem Änderungen am Text bei Verwendung des koreanischen IME im Titel von Registerkarten von Blättern im Tabellenmodell zu häufig abgeschlossen wurden
- Ein Fehler wurde behoben, bei dem IntelliSense für die DAX Related()-Funktion Spalten aus anderen Tabellen nicht ordnungsgemäß anzeigte
- Verbesserung des AS Tabular-Projektimports aus dem Datenbank-Dialogfeld durch Sortieren der Liste von AS-Datenbanken
- Ein Fehler wurde behoben, bei dem beim Erstellen berechneter Tabellen im AS-Tabellenmodell Tabellen nicht als vorgeschlagene Objekte im Ausdruck aufgelistet wurden
- Ein Fehler wurde behoben, bei dem Preview 1400-AS-Modelle nach dem Anzeigen von Code versuchten, den Integrated Workspace-Server zu öffnen
- Ein Fehler wurde behoben, der einige Datenquellen (ohne Unterstützung für den Anfangskatalog) davon abhielt, unter bestimmten Umständen ordnungsgemäß zu funktionieren 
- Deployment Wizard (Bereitstellungsassistent) sollte Änderungen auf berechnete Tabellenpartitionen anwenden, selbst wenn die Option zum Beibehalten von Partitionen aktiviert ist
- Ein Fehler wurde behoben, bei dem das Dialogfeld „Advanced Properties“ (Erweiterte Eigenschaften) für eine vorhandene AS-Verbindung erst nach erneuter Auswahl eine vollständige Liste anzeigte
- Es wurden einige Probleme mit abgeschnittenen String auf der Benutzeroberfläche behoben, die in manchen lokalisierten Builds auftraten
- Es wurde eine Reihe von Problemen behoben, die bei der Integration von Power Query in tabellarische AS-Modelle mit Kompatibilitätsgrad 1400 auftraten
- Es wurde ein Problem behoben, bei dem die Stilvorlagen des Berichts-Assistenten nicht korrekt angezeigt wurden
- Es wurde ein Problem mit dem Berichts-Assistenten behoben, das zu falschen Datenquelleneinstellungen führen konnte, wenn von SQL zu AS gewechselt wurde
- Es wurde ein Problem behoben, das in Analysis Services (tabellarisch) einen Projekterstellungsfehler über die Befehlszeile (devenv.com\exe) verursacht hat
- Es wurde ein Problem mit dem DAX-Measure-Parser behoben, damit beim Starten die hervorgehobene und korrekte Textfarbe von Buchstaben vor := angezeigt wird
- Es wurde ein Problem behoben, bei dem „ObjectRefException“ ausgelöst wurde, wenn die Pfade bei dem Versuch zu lang wurden, alle Dateien für ein tabellarisches Projekt im integrierten Arbeitsbereich anzuzeigen
- Es wurde ein Problem mit dem Datenquellen-Designer für den Compact 4.0-Clientdatenanbieter behoben, bei dem dieser als nicht verfügbar angezeigt wurde
- Es wurde ein Problem behoben, bei dem ein Fehler verursacht wurde, wenn das AS-Miningmodell in VS2017 durchsucht werden sollte
- Es wurde ein Problem im mehrdimensionalen AS-Modell in VS2017 behoben, bei dem das DSV-Diagramm beim Wechseln der Ansicht das Rendering beendet hat und anschließend eine Ausnahme auftritt
- Es wurde ein Fehler mit der Vorschau von Berichten bei einer fehlerhaften AS-Verbindung in VS2017 behoben
 

**RS-Projekte:**
- Ein Fehler wurde behoben, bei dem durch die meisten Änderungen beim Entwerfen von Berichten in SSDT die Strukturansicht von Parametern, Datenquellen und Datasets reduziert wurden 
- Das Problem wurde behoben, dass „Speichern“ die Version von RDL speichert und nicht die aktuellste Version.
- Das Problem wurde behoben, dass SSDT RS Dateien sichert, obwohl die Sicherung deaktiviert ist; auch einige weitere Probleme.
- Das Problem im Berichts-Generator wurde behoben, dass es beim Klicken auf „Zellen teilen“zu einem Fehler kam. [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3101818/ssdt-2015-ssrs-designer-error-by-matrix-cell-split)
- Das Problem wurde behoben, dass es durch das Zwischenspeichern zu inkorrekten Daten in einem Bericht kommen konnte. [Microsoft Connect-Artikel](http://connect.microsoft.com/SQLServer/feedback/details/3102158/ssdtbi-14-0-60812-report-preview-data-is-frequently-wrong-due-to-bad-caching)

**IS-Projekte:**
- Das Problem wurde behoben, dass Einstellungen für run64bitruntime nicht angenommen wurden.
- Das Problem wurde behoben, dass angezeigten Spalten von DataViewer nicht gespeichert wurden.
- Das Problem wurde behoben, dass Paketteile Anmerkungen verbergen. [Microsoft Connect-Artikel](https://connect.microsoft.com/SQLServer/feedback/details/3106624/package-parts-hide-annotations)
- Das Problem wurde behoben, das Package Parts Anmerkungen und Layouts von Data Flow verwirft. [Microsoft Connect-Artikel](https://connect.microsoft.com/SQLServer/feedback/details/3109241/package-parts-discard-data-flow-layouts-and-annotations)
- Das Problem wurde behoben, dass SSDT beim Importieren eines Projekts aus SQL Server abstürzt.
- Es wurde ein Fehler mit der Hadoop-Dateisystemaufgabe „TimeoutInMinutes default to 10“ behoben, der nach dem Öffnen des gespeicherten SSIS-Pakets und zur Laufzeit augetreten ist.

**Datenbankprojekte:**
- SSDT DACPAC Einstellung zurücksetzen für IgnoreColumnOrder bereitstellen [Connect item (Connect-Artikel)](https://connect.microsoft.com/SQLServer/feedback/details/1221587/ssdt-dacpac-deploy-add-setting-back-in-for-ignorecolumnorder)
- SSDT kompiliert nicht, wenn STRING_SPLIT verwendet wird [Connect item (Connect-Artikel)](http://connect.microsoft.com/SQLServer/feedback/details/2906200/ssdt-failing-to-compile-if-string-split-is-used)
- Einen Fehler beheben, bei dem DeploymentContributors auf das öffentliche Modell Zugriff haben, jedoch das Schema für die Sicherung nicht initialisiert wurde[Github issue (Github-Problem)](https://github.com/Microsoft/DACExtensions/issues/8)
- Zeitliche Behebung von DacFx für die FILEGROUP-Platzierung
- Beheben des Fehlers „Unresolved Reference“ (Nicht aufgelöster Verweis) für externe Synonyme. 
- „Always Encrypted“ (Immer verschlüsselt): Onlineverschlüsselung deaktiviert bei Abbruch nicht die Änderungsnachverfolgung und funktioniert nicht ordnungsgemäß, wenn die Änderungsnachverfolgung nicht vor dem Start der Verschlüsselung bereinigt wurde


## <a name="ssdt-165-supports-up-to-sql-server-2016"></a>SSDT 16.5 (Unterstützung bis SQL Server 2016)
Veröffentlicht: 20. Oktober 2016

Buildnummer: 14.0.61021.0

**Neuigkeiten**


### <a name="connection-improvements"></a>Verbesserung der Verbindung

* Mithilfe der neuen Suche auf der Registerkarte **Durchsuchen** können Sie Ihre lokalen Server, Netzwerkserver und Azure SQL-Datenbanken besser filtern. Dies bietet sich vor allem dann an, wenn in diesen Listen eine große Anzahl von Servern oder Datenbanken angezeigt werden.
* Die Registerkarte **Verlauf** verfügt über Optionen zum Fixieren bzw. Aufheben der Fixierung von Favoriten mit der rechten Maustaste sowie über eine neue Option, um Verbindungen aus dem Verlauf zu entfernen.

### <a name="sqlpackage-and-dacfx-api-improvements"></a>SqlPackage- und DacFx-API-Verbesserungen

Über SqlPackage.exe und die DacFx-APIs können Sie jetzt einen Bereitstellungsbericht und ein Bereitstellungsskript generieren und in einem einzigen Vorgang in einer Datenbank veröffentlichen. Dies bedeutet für jeden Benutzer, der gerne über einen Bericht zu den Veröffentlichungen während einer Bereitstellung verfügen möchte, eine Zeitersparnis. Ein weiterer Vorteil besteht darin, dass bei Azure-Szenarios für die master-Datenbank und die Bereitstellungszieldatenbank separate Skripts erstellt werden. Bislang wurde ein einziges Skript erstellt, das sich für wiederholte Bereitstellungen nicht eignete.

Für Veröffentlichungs- und Skriptaktionen mit SqlPackage wurden zwei neue Argumente hinzugefügt.

* DeployScriptPath (Kurzname: dsp). Dies ist ein optionaler Pfad, in den das Bereitstellungsskript geschrieben wird. Wenn bei Azure-Bereitstellungen TSQL-Befehle zum Erstellen oder Ändern der Datenbank verwendet werden, wird ein Master-Skript in den gleichen Pfad geschrieben, wobei der Name der Ausgabedatei „Dateiname_Master.sql“ lautet.
* DeployReportPath (Kurzname: drp). Dies ist ein optionaler Pfad, in den der Bereitstellungsbericht geschrieben wird.

Beachten Sie, dass für die Skriptaktion entweder die vorhandenen Ausgabepfadargumente oder das neue Skript bzw. berichtsspezifische Argumente, jedoch nicht beides zusammen verwendet werden sollten.

Beispiel für die Verwendung:

**Veröffentlichungsaktion**

```Sqlpackage.exe /a:Publish /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

**Skriptaktion**

```Sqlpackage.exe /a:Script /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

In DacFx wurden zwei neue APIs hinzugefügt: DacServices.Publish() und DacServices.Script(). Diese unterstützen zudem die Durchführung von Veröffentlichungs-, Skript- und Berichtsaktionen in einem einzigen Vorgang. Beispiel für die Verwendung:

```
DacServices service = new DacServices(connectionString);
using(DacPackage package = DacPackage.Load(@"C:\My\db.dacpac")) {
var options = new PublishOptions() {
    GenerateDeploymentScript = true, // Should a deployment script be created?
    GenerateDeploymentReport = true, // Should an xml deploy report be created?
    DatabaseScriptPath = @"C:\My\OutputScript.sql", // optional path to save script to
    MasterDbScriptPath = @"C:\My\OutputScript_Master.sql", // optional path to save master script to
    DeployOptions = new DacDeployOptions()
};

// Call publish and receive deployment script & report in the results
PublishResult result = service.Publish(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);

// Call script and receive deployment script & report in results
result = service.Script(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);
```

**Analysis Services und Reporting Services**

Der DAX-Parser des SSAS-Tabellen-Designers bietet bei der Arbeit mit großen DAX-Ausdrücken jetzt mehr Leistung.
Weitere Informationen finden Sie im [Blogbeitrag von Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/).

### <a name="fixed--improved-this-month"></a>Fehlerbehebungen und Verbesserungen dieses Monats

**Datenbanktools**

* [Verbindungsfehler 3055711](https://connect.microsoft.com/SQLServer/feedback/details/3055711/columns-cannot-be-selected-from-cross-apply-openjson-with-explicit-schema) – Spalten können nicht mit explizitem Schema aus CROSS APPLY OPENJSON ausgewählt werden.
* Behoben – Problem bei automatisch generierten Verlaufstabellenindizes, wobei DacFx den Index bei erneuter Bereitstellung löschte
* Behoben – Problem mit dem DacFx-Batch-Parser, der „]“-Zeichen mit Escapezeichen nicht analysierte, sodass die Veröffentlichung fehlschlug
* Verbessert – SqlPackage enthält jetzt Beschreibungen für jede Aktion in der Hilfeausgabe.
* Behoben – Die Option „Kennwort speichern“ im Verbindungsdialogfeld wurde in folgenden Fällen nicht beibehalten: beim Bearbeiten der erweiterten Optionen sowie beim Bearbeiten einer Verbindungszeichenfolge, die in Veröffentlichungs-, Schemavergleichs- und anderen Dateien gespeichert wurde.
* Behoben – Für Verbindungen, für die in der Registerkarte „Verlauf“ der Wert IntegratedAuthentication = true gilt, wurde das Authentifizierungsfeld in den Verbindungseigenschaften leer gelassen. Jetzt zeigt es wie erwartet „Windows-Authentifizierung“ an.
* Behoben – Änderungen an den Intellisense-Einstellungen der SQL Server-Tools unter Extras- > Optionen -> Text-Editor wurden nicht beibehalten.
* Verbessert – Die Schaltfläche zum Anheften und Lösen auf der Registerkarte „Verlauf“ im Verbindungsdialogfeld ist jetzt kompakter. Dadurch wird die Anzeige einer Bildlaufleiste weniger wahrscheinlich.
* Behoben – Im Verbindungsdialogfeld wurden verschiedene Probleme behoben.

**Analysis Services und Reporting Services**

* Folgendes Problem im SSDT AS-Tabellen-Designer wurde behoben: Durch Klicken auf den Ziehpunkt der Bildlaufleiste im Datenraster kam es in bestimmten Situationen zum Absturz.
* Folgendes Problem wurde behoben: Die Option, die Identität der Verbindung als aktueller Benutzer im SSDT AS-Tabellen-Designer zu übernehmen, war nicht verfügbar.
* Folgendes Problem im SSDT AS-Tabellen-Designer wurde behoben: Durch das zu starke Erweitern der Bearbeitungsleiste konnte das Projekt nicht erneut geöffnet werden.
* Folgendes Problem wurde behoben: Der SSDT AS-Tabellen-Designer stürzte ab, wenn die Tabellenregisterkarte ausgewählt und die Pfeiltaste gedrückt wurde.
* Folgendes Problem in SSDT AS-Projekten wurde behoben: „In Excel analysieren“ konnte keine Verbindung zu früheren AS-Serverversionen herstellen.

**Integration Services**

* Verbindungsfehler [1608896](https://connect.microsoft.com/SQLServer/feedback/details/1608896/move-multiple-integration-service-package-tasks) behoben: Verschieben mehrerer Integration Services-Pakettasks





## <a name="ssdt-164-for-sql-server-2016"></a>SSDT 16.4 (für SQL Server 2016)
Veröffentlicht: 20. September 2016

Buildnummer: 14.0.60918

**Neuigkeiten**

Schemavergleich wird jetzt in SqlPackage.exe und in der Data-Tier Application Framework-API (DacFx) unterstützt. Weitere Informationen finden Sie unter [Schema Compare in SqlPackage and the Data-Tier Application Framework (Schemavergleich in SqlPackage und Data-Tier Application Framework)](https://blogs.msdn.microsoft.com/ssdt/2016/09/20/schema-compare-in-sqlpackage-and-the-data-tier-application-framework-dacfx/).

**Analysis Services – Modus „Integrierter Arbeitsbereich“ für den SSDT-Tabellen-Designer (SSAS)**

Der SSDT-Tabellen-Designer umfasst jetzt eine interne SSAS-Instanz, die der SSDT-Tabellen-Designer automatisch im Hintergrund startet, falls der Modus „Integrierter Arbeitsbereich“ aktiviert ist. Auf diese Weise können Sie Tabellen, Spalten und Daten im Modell-Designer hinzufügen und anzeigen, ohne eine externe Arbeitsbereich-Serverinstanz bereitzustellen. Der Modus „Integrierter Arbeitsbereich“ verändert die Funktionsweise von SSDT für Analysis Services-Projekte für tabellarische Modelle mit einem Arbeitsbereichsserver und einer Arbeitsbereichsdatenbank nicht. Was sich ändert, ist der Ort, an dem SSDT für Analysis Services-Projekte für tabellarische Modelle die Arbeitsbereichsdatenbank hostet. Zum Aktivieren des Modus „Integrierter Arbeitsbereich“ wählen Sie im Dialogfeld „Designer für tabellarische Modelle“ die Option „Integrierter Arbeitsbereich“, wenn Sie ein neues Tabellenprojekt erstellen. Für vorhandene Tabellenprojekte, die derzeit einen expliziten Arbeitsbereichserver verwenden, können Sie in den Modus „Integrierter Arbeitsbereich“ wechseln, indem Sie den Parameter für den Modus „Integrierter Arbeitsbereich“ im Fenster „Eigenschaften“auf „True“ festlegen. Dieses Fenster wird angezeigt, wenn Sie im Projektmappen-Explorer die Model.bim-Datei auswählen. Weitere Informationen finden Sie im [Blogbeitrag von Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/).

**Datenbanktools für **
**Aktualisierungen und Fixes:**

- [Verbindungsfehler 3087775](https://connect.microsoft.com/SQLServer/feedback/details/3087775): temporale Tabellen in Visual Studio Data Tools Juli-Aktualisierung 14.0.60629.0 unterbrochen; „Wert darf nicht gleich NULL sein. Parametername: reportedElement“
- [Verbindungsfehler 1026648](https://connect.microsoft.com/SQLServer/feedback/details/1026648): IsPersistedNullable wird im SSDT-Vergleich als unterschiedlich angezeigt.
- [Verbindungsfehler 2054735](https://connect.microsoft.com/SQLServer/feedback/details/2054735): Identität wird beim Importieren einer BACPAC-Datei zurückgesetzt.
- [Verbindungsfehler 2900167](https://connect.microsoft.com/SQLServer/feedback/details/2900167): Nach dem Ausführen von SSDT- Komponententests bleiben temporäre Dateien zurück.
- [Verbindungsfehler 1807712](https://connect.microsoft.com/SQLServer/feedback/details/1807712): unterbrochene Abwärtskompatibilität – lokale Anwendungsdaten und Verwaltung über den Nuget-Paketmanager

**Analysis Services und Reporting Services**

* Folgendes Problem in SSDT wurde behoben: Popup-Fehlertipps störten beim Bearbeiten von DAX für mit DirectQuery berechneten Spalten.
* Folgendes Problem im SSDT AS-Tabellenraster wurde behoben: Das KPI-Symbol wurde im Measureraster nicht angezeigt, wenn der Windows-Skalierungsfaktor auf 200% + (hochauflösend) festgelegt wurde.
* Folgendes Problem im SSDT AS-Tabellen-Designer wurde behoben: Durch das Einfügen von großen Datenmengen konnte die Reaktion des Tabellenprojekts beeinträchtigt werden.
* Folgendes Problem im SSDT AS-Tabellen-Modell-Editor wurde behoben: Modelländerungen müssen gespeichert werden, wenn der Verbindungsanzeigenamen geändert wird.
* Folgendes Problem in SSDT AS-Tabellenprojekten wurde behoben: Die Spaltenbreite im Dialogfeld zur Verwaltung von Beziehungen konnte nicht verändert werden.
* Folgendes Problem in SSDT AS-Tabellenmodellen vom 1200-Typ wurde behoben: Beim Einfügen von Daten aus Excel wurde das Komma bei Gebietsschemaeinstellungen (z.B. für Deutsch) nicht ordnungsgemäß als Dezimaltrennzeichen behandelt.
* Folgendes Problem in SSDT AS-Projekten wurde behoben: Einige KPI-Symbolsätze gaben den folgenden Fehler aus: „Couldn't retrieve the data for this visual“ (Die Daten für diese visuelle Anzeige konnten nicht abgerufen werden).
* Folgendes Problem im Dialogfeld „Projekteigenschaften“ des SSDT AS-Tabellen-Designers wurde behoben: Das Dialogfeld wird jetzt bei einer hochauflösenden Skalierung ordnungsgemäß verankert.
* Folgendes Problem in SSDT-AS-Projekten wurde behoben: Die Aktualisierung bestimmter Modelle mit eingefügten Tabellen konnte einen Fehler verursachen.
* Folgendes Problem im SSDT AS-Tabellen-Designer wurde behoben: Das Einfügen gefüllter Blattreihen von Excel erfolgte sehr langsam, und es wurden zahlreiche unerwünschte Spalten erstellt.
* Folgendes Problem im SSDT AS-Tabellen-Designer wurde behoben: Die Analyse umfangreicher statischer DataTable-Ausdrücke erfolgte sehr langsam oder schien ein Hängenbleiben zu verursachen.
* Folgendes Problem im SSDT AS-Tabellen-Designer wurde behoben: Measures und KPI-Werte lassen sich jetzt zu der im Editor ausgewählten aktuellen Perspektive hinzufügen.
* Folgendes Problem in SSDT wurde behoben: Der Datenimport von SQL Azure in AS-Projekte unterstützt keine anderen Schematypen als „dbo“.



## <a name="ssdt-163-for-sql-server-2016"></a>SSDT 16.3 (für SQL Server 2016)
Veröffentlicht: 15. August 2016

Buildnummer: 14.0.60812.0  

**Neuigkeiten**

- **Versionsverwaltung und -nummerierung:** Versionen werden jetzt nummeriert und nicht mehr mit Monatsangaben versehen. Dies steht im Einklang mit der neuen SSMS-Richtlinie und vereinfacht Fälle, in denen mehrere Versionen oder Hotfixes in einem Monat veröffentlicht werden. Dies ist Version 16.3, d.h. die dritte Aktualisierung nach der RTM-Version. Hotfixes erhalten die Angabe 16.3.1 etc., während die nächste Aktualisierung (für den nächsten Monat geplant) die Angabe 16.4 erhält.
- **Analysis Services – Tabellarischer Modell-Explorer:** Mit dem tabellarischen Modell-Explorer können Sie bequem durch die verschiedenen Metadatenobjekte in einem Modell navigieren, wie z.B. Datenquellen, Tabellen, Measures und Beziehungen. Der Explorer besteht aus einem separaten Toolsfenster, das Sie über das Ansichtsmenü in Visual Studio anzeigen können. Zeigen Sie auf „Other Windows“ (Weitere Fenster), und klicken Sie anschließend auf „Tabellarischer Modell-Explorer“. Der tabellarische Modell-Explorer wird standardmäßig im Projektmappen-Explorer-Bereich auf einer separaten Registerkarte angezeigt. Der tabellarische Modell-Explorer ordnet die Metadatenobjekte in einer Struktur an, die dem Schema eines tabellarischen Modells vom 1200-Typ sehr ähnlich ist, und viele andere neue Funktionen.
- **Datenbanktools – Always Encrypted**: Diese Version bietet neue Dialogfelder zur [Schlüsselverwaltung für Always Encrypted](https://msdn.microsoft.com/library/mt708953.aspx). Dadurch lassen sich Spaltenhauptschlüssel oder Spaltenverschlüsselungsschlüssel problemlos zu Ihrem Datenbankprojekt oder einer Livedatenbank im SQL Server-Objekt-Explorer hinzufügen. Diese Version unterstützt Zertifikate im Windows-Zertifikatspeicher. In zukünftigen Versionen werden auch Azure Key Vault und CNG-Anbieter unterstützt.
    - Beim Erstellen des Spaltenhauptschlüssels oder Spaltenverschlüsselungsschlüssels spiegeln sich Änderungen möglicherweise nicht sofort im Objekt-Explorer von SQL Server wider, nachdem Sie auf „Datenbank aktualisieren“ geklickt haben. Um dieses Problem zu umgehen, aktualisieren Sie den Datenbankknoten im SQL Server-Objekt-Explorer.
    - Wenn Sie versuchen, eine Spalte in einer Tabelle mit Daten aus dem SQL Server-Objekt-Explorer zu verschlüsseln, können Fehler auftreten. Dieses Feature wird derzeit nur in SSDT-Datenbankprojekten und SSMS unterstützt. Die Unterstützung für den SQL Server-Objekt-Explorer ist für eine spätere Version geplant.


**Aktualisierungen und Fixes**
* **Datenbanktools:**
    - **SSDT:**
        - Verbindungsfehler 1898001:[ Das Problem der Beschränkung einer Spaltenbeschreibung auf 128 Zeichen wurde behoben](https://connect.microsoft.com/SQLServer/feedback/details/1898001/column-description-limited-to-128-characters).
        - Folgendes Problem wurde behoben: Beim Veröffentlichen einer Datenbank von VS wurde die DatabaseServiceObjective-Eigenschaft nicht im XML-Veröffentlichungsprofil angewendet.
        - Verbindungsfehler 2900167: [Das Problem der Testkomponenten, bei denen nicht ordnungsgemäß temporäre Dateien zurückbleiben, wurde behoben](http://connect.microsoft.com/SQLServer/feedback/details/2900167/running-ssdt-unit-tests-leaves-temp-files-behind).
        - Folgendes Problem wurde behoben: In den Datenbankeinstellungen ist das Kombinationsfeld für die Beibehaltungsdauer abgeschnitten.
        - Folgendes Problem wurde behoben: Beim Ändern des Kennworts erfolgt keine Überprüfung des alten leeren Kennworts in den SQL CLR-Projekteigenschaften.
    - **DACFx:**
        - Folgendes Problem wurde behoben: Für SqlAzureV12-Fehler wird der DACFx-Kompatibilitätsgrad nicht aktualisiert.
        - Folgendes Problem wurde behoben: Die IsAutoGeneratedHistoryTable-Eigenschaft ist fälschlicherweise aus dem Modellvergleich ausgeschlossen.

- **Analysis Services und Reporting Services**
    - **SSDT:**
        - Folgendes Problem wurde behoben: Das tabellarische Modell kann nicht gespeichert werden, wenn die Verbindung zum Server verlorengegangen ist.
        - Folgendes Problem wurde behoben: Aufgrund eines möglichen Endlosschleifenfehlers in AS reagiert SSDT nicht mehr.
        - Folgendes Problem wurde behoben: Je nachdem, wie Sie den Ausdruck committen, führt ein DAX-Ausdruck zu uneinheitlichem Verhalten.
        - Folgendes Problem wurde behoben: Beim Erstellen von KPIs stürzt VS ab.
        - Folgendes Problem wurde behoben: Für SQL Server 2008 R2, 2012 und 2014 werden ungültige Berichte generiert.
        - Folgendes Problem wurde behoben: Ein Fehler in der Hierarchieanordnung führte zu einem Endlosschleifenfehler für .dwpro-Projekte.
        - Folgendes RS-RDL-Problem wurde behoben: Bei der RDL-Herabstufung wurde ein vollständiger Rebuild erforderlich, der beim Benutzer für Verwirrung sorgte.
        - Folgendes KPI-Problem wurde behoben: „Aus Clienttools ausblenden“ zeigte keine Wirkung.
        

 
  
## <a name="ssdt-july-for-sql-server-2016"></a>SSDT Juli (für SQL Server 2016)  
Veröffentlicht: 30. Juni 2016  
  
Buildnummer: 14.0.60629.0  
  
**Neuigkeiten**  
* **Always Encrypted-Unterstützung:** Für Datenbanken, die Always Encrypted-Spalten enthalten, bietet diese Version über unsere Kern-APIs und unser Befehlszeilentool (SqlPackage.exe) vollständige Unterstützung für Always Encrypted. Sie können Datenbankprojekte erstellen und veröffentlichen und auf die vollständige Unterstützung für alle Always Encrypted-Funktionen zurückgreifen.  
* **Verbesserte Unterstützung für temporale Tabellen:** Die Erfahrung temporaler Tabellen wurde vereinfacht, indem ihre Verknüpfung vor Änderungen aufgehoben und nach Abschluss der Änderungen wiederhergestellt wurde. Dies bedeutet, dass zwischen temporalen Tabellen und anderen Tabellentypen (Standard- oder speicherinternen Tabellen) im Hinblick auf die Vorgänge, die unterstützt werden, Parität herrscht. 
* **SqlPackage.exe und Installationsänderungen:** Es wurden Änderungen durchgeführt, um SSDT vom SQL Server-Modul und von SSMS-Updates zu isolieren. Weitere Informationen finden Sie unter [Changes to SSDT and SqlPackage.exe installation and updates (Änderungen an SSDT und Installationen und Aktualisierungen von SqlPackage.exe)](https://blogs.msdn.microsoft.com/ssdt/2016/06/30/changes-to-ssdt-and-sqlpackage-exe-installation-and-updates/).

 

**Aktualisierungen und Fixes**
* **Datenbanktools:**
    * SSDT wird ab sofort niemals die transparente Datenverschlüsselung (TDE) in einer Datenbank deaktivieren. Da die Standardoption für die Verschlüsselung in den Datenbankeinstellungen eines Projekts bislang deaktiviert wurde, wurde auch die Verschlüsselung deaktiviert. Mithilfe dieses Fixes kann die Verschlüsselung während der Veröffentlichung aktiviert, jedoch nie deaktiviert werden. 
    * Die Wiederholungsanzahl und Resilienz von Azure SQL-Datenbankverbindungen während der ersten Verbindung wurde erhöht.
    * Ist die Standarddateigruppe nicht PRIMARY, schlug der Import/die Veröffentlichung auf Azure V12 fehl. Jetzt wird diese Einstellung bei einer Veröffentlichung ignoriert.
    * Folgendes Problem wurde behoben: Beim Exportieren einer Datenbank mit einem Objekt mit Bezeichner in Anführungszeichen schlug die Exportüberprüfung in einigen Fällen fehl.
    * Folgendes Problem wurde behoben: Die TEXTIMAGE_ON-Option wurde für das Erstellen von Hekaton-Tabellen an einer nicht zulässigen Stelle hinzugefügt.
    * Folgendes Problem wurde behoben: Der Export großer Datenmengen nahm viel Zeit in Anspruch. Dies war darauf zurückzuführen, dass nach Abschluss der Datenphase in die model.xml-Datei geschrieben wurde und die Inhalte der .bacpac-Datei daraufhin neu geschrieben wurden.
    * Folgendes Problem wurde behoben: Benutzer wurden nicht im Sicherheitsordner für Azure SQL Data Warehouse und APS-Verbindungen angezeigt.


 * **Analysis Services und Reporting Services:**
    * Folgendes SxS-Problem mit MSOLAP OLEDB-Anbieter wurde behoben: Nur der 32-Bit-Anbieter wurde installiert, was sich auf die Herstellung einer Verbindung zwischen 64-Bit-Excel 2016 und SQL Server 2014 auswirkte (nicht reproduzierbar mit ClickOnce-Installierungen von Office 365, sondern nur MSI Excel-Installation).
    * Folgendes Problem wurde behoben: In Grenzfällen konnten die bei der Aktualisierung des AS-Modells von Kompatibilitätsebene 1103 auf 1200 eingefügten Tabellen den Fehler „Relationship uses an invalid column ID“ (Beziehung verwendet eine ungültige Spalten-ID) auslösen.
    * Folgendes SxS-Problem wurde behoben: SSDT-BI 2013 konnte nach der Deinstallation von SSDT 2015 (Registrierungseinstellung für gemeinsam genutzte Cartridges) auf demselben Computer keine Daten mehr in den AS-Tabellen-Designer importieren.
    * Die Stabilität wurde erhöht, um mit Problemen und Abstürzen umzugehen, wenn die Verbindung mit dem AS-Modul unterbrochen wurde (d.h. SSDT bleibt über Nacht offen, und der AS-Server wird wiederverwendet und andere vorübergehende Unterbrechungen der Verbindung). 
    * Folgendes Problem wurde behoben: Dialogfelder wurden auf anderen Bildschirmen als VS in Szenarios mit mehreren Monitoren geöffnet. 
    * Folgendes Problem wurde behoben: Unterstützung zum Einfügen aus HTML-Tabellen (Rasterdaten) in eingefügte Tabellen des AS-Tabellen-Designers wurde aktiviert. 
    * Folgendes Problem wurde behoben: Bei einem Upgrade wurde eine leere einfügte Tabelle nicht auf 1200 aktualisiert (Verwendung nur als Containertabelle für Measures). 
    * Folgendes Problem wurde behoben: Das tabellarische AS-Modell wurde mit eingefügten Tabellen auf 1200 aktualisiert, um einen AS-Modulfehler bei Calc-Tabellen (die für eingefügte Tabellen in 1200 verwendet werden) zu umgehen. Jetzt wird nach dem Upgrade ein vollständiger Prozess auf die neuen Calc-Tabellen durchgeführt. 
    * Folgendes Problem wurde behoben: Beim Abbrechen der Erstellung einer neuen berechneten AS-Modelltabelle vom Typ 1200 mit unvollständigem DAX-Ausdruck konnte es zum Absturz kommen. 
    * Folgendes Problem wurde behoben: Beim Importieren eines Modells vom Typ 1200 von AS-Server in ein AS-Projekts in SSDT, bei dem Datenbankname und Tabellennamen identisch waren, konnte ein Fehler auftreten. 
    * Folgendes Problem wurde behoben: Beim Editieren einer KPI-Measure im tabellarischen Modell vom Typ 1103 konnte ein Fehler auftreten. 
    * Folgendes Problem wurde behoben: Eine Objektreferenz wurde nicht als Ausnahmetreffer festgelegt, während eine KPI-Measure in das Raster für ein AS-Modell vom Typ 1200 eingefügt wurde. 
    * Folgendes Problem wurde behoben: Eine Spalte in einer berechneten Tabelle konnte nicht aus der Diagrammsicht in Modellen vom Typ 1200 gelöscht werden. 
    * Folgendes Problem wurde behoben: Eine Objektreferenz wurde nicht als Ausnahmetreffer festgelegt, wenn die model.bim-Projektdateieigenschaften in der Codesicht angezeigt wurden. 
    * Folgendes Problem wurde behoben: Das Einfügen von Daten in ein AS-Modellraster, um eingefügte Tabellen zu erstellen, ergab falsche Werte für internationale Gebietsschemas, die Komma als Dezimaltrennzeichen verwenden. 
    * Folgendes Problem wurde behoben: Beim Öffnen eines 2008 RS-Projekts in SSDT wurde kein Upgrade ausgewählt. 
    * Folgendes Problem wurde behoben: In einer in Kompatibilitätsmodellen vom Typ 1200 berechneten Tabellenbenutzeroberfläche konnte ein Fehler auftreten, wenn für den Spaltentyp die Standardformatierung verwendet wurde, um eine Änderung des Formatierungstyps über die Benutzeroberfläche zu ermöglichen. 
    

## <a name="ssdt-june-for-sql-server-2016"></a>SSDT Juni (für SQL Server 2016)  
Veröffentlicht:1. Juni 2016  
  
Buildnummer: 14.0.60525.0 

SSDT General Availability (GA) ist nun erhältlich. Das Update von SSDT GA vom Juni 2016 bietet Unterstützung für die neuesten Updates von SQL Server 2016 RTM und verschiedene Fehlerbehebungen. Weitere Informationen finden Sie unter [SQL Server Data Tools GA update for June 2016 (Update von SQL Server Data Tools-GA vom Juni 2016)](https://blogs.msdn.microsoft.com/ssdt/2016/06/01/sql-server-data-tools-ga-update-for-june-2016/).

  
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen
  
[Herunterladen von SQL Server Data Tools &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[Vorgängerversionen von SQL Server Data Tools &#40;SSDT and SSDT-BI&#41;](../ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)  
[Neuigkeiten im Datenbankmodul](https://msdn.microsoft.com/library/bb510411.aspx)  
[Neuigkeiten in Analysis Services](https://msdn.microsoft.com/library/bb522628.aspx)  
[Neuigkeiten in Integration Services](https://msdn.microsoft.com/library/bb522534.aspx)  
  

