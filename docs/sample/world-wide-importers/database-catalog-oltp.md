---
title: "\"Wideworldimporters\" Datenbankkatalog | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e47c0022-ce87-4ba5-a24b-df55efe66431
caps.latest.revision: 
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 0d458bc15530aa87bfa922787558fff3f07645f7
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="wideworldimporters-database-catalog"></a>Datenbankkatalog "wideworldimporters"
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die Datenbank "wideworldimporters" enthält alle der Transaktionsinformationen und Tagesdaten für und Verkäufe, sowie für Fahrzeuge und kalten Räume Sensordaten.

## <a name="schemas"></a>Schemas

"Wideworldimporters" verwendet Schemas für unterschiedliche Zwecke, z. B. Speichern von Daten, die definieren, wie Benutzer die Daten zugreifen können und die Bereitstellung von Objekten für die Entwicklung von Datawarehouse und die Integration an.

### <a name="data-schemas"></a>Datenschemas

Diese Schemas enthalten die Daten. Eine Reihe von Tabellen, die von allen anderen Schemas erforderlich sind und befinden sich im Anwendungsschema.

|Schema|Description|
|-----------------------------|---------------------|
|Application|Anwendungsweite Benutzer, Kontakte und Parameter. Dieses enthält auch Verweistabellen mit Daten, die von mehreren Schemas verwendet wird|
|Purchasing|Lagerartikel Käufe von Lieferanten und Details zu den Lieferanten.|  
|Sales|Stock Element sales, um Privatkunden und Details zu den Kunden und Umsätze Personen. |  
|Warehouse|Lagerartikel Softwareinventur und Transaktionen.|  

### <a name="secure-access-schemas"></a>Sicherer Zugriff schemas

Diese Schemas werden für externe Anwendungen verwendet, die nicht direkt auf die Tabellen zugreifen dürfen. Sie enthalten, Sichten und gespeicherte Prozeduren, die von externen Anwendungen verwendet wird.

|Schema|Description|
|-----------------------------|---------------------|
|Website|Alle Zugriffe auf die Datenbank von der Unternehmensportal-Website wird über dieses Schema.|
|Berichte|Alle Zugriffe auf die Datenbank von Reporting Services-Berichte erfolgt über dieses Schema.|
|PowerBI|Alle Zugriffe auf die Datenbank aus der Power BI-Dashboards über das Enterprise-Gateway ist über dieses Schema.|

Beachten Sie, dass die Berichte und PowerBI Schemas werden nicht in der ursprünglichen Version der Beispieldatenbank verwendet. Allerdings werden alle Reporting Services und Power BI-Beispiele baut auf den dieser Datenbank aufgefordert, diese Schemas verwendet.

### <a name="development-schemas"></a>Entwicklung von schemas

Spezielle schemas

|Schema|Description|
|-----------------------------|---------------------|
|Integration|Objekte und Verfahren für die Datawarehouse-Integration erforderlich sind (d. h. Migrieren der Daten in der Datenbank WideWorldImportersDW).|
|Sequenzen|Enthält die Sequenzen, die von allen Tabellen in der Anwendung verwendet.|

## <a name="tables"></a>Tabellen

Alle Tabellen in der Datenbank sind in den Daten.

### <a name="application-schema"></a>Anwendungsschema

Details der Parameter und Personen (Benutzer und Kontakte), zusammen mit (häufig auf mehrere andere Schemas) gemeinsamen Verweistabellen.

|Tabelle|Description|
|-----------------------------|---------------------|
|SystemParameters|Enthält eine systemweite konfigurierbaren Parameter.|
|Personen|Enthält die Benutzernamen, Kontaktinformationen für alle Benutzer, die die Anwendung verwenden, und für die Personen, die die Wide World Importers am kundenorganisationen behandelt. Dies schließt Mitarbeitern, Kunden, Lieferanten und alle anderen Kontakte. Für Personen, die vom System oder der Website mit Berechtigung erteilt wurde, enthält die Informationen über Anmeldeinformationen.|
|Städte|Es gibt viele Adressen, die in das System für Personen, Unternehmen Übermittlung Kundenadressen pickup Adressen an Lieferanten usw. gespeichert. Wenn eine Adresse gespeichert wird, besteht ein Verweis auf eine Stadt in dieser Tabelle. Es gibt auch eine räumliche Position jeder Stadt.|
|StateProvinces|Städte sind Teil der Bundesstaaten oder Provinzen. Diese Tabelle weist Details davon, wie z. B. räumliche Daten für die Beschreibung der Grenzen jeder Bundesland oder Kanton.|
|Länder|Sind Teil der Länder, Bundesstaaten oder Provinzen. Die Tabelle enthält Details davon, wie z. B. räumliche Daten, die die Grenzen der einzelnen Länder beschreibt.|
|DeliveryMethods|Optionen für die Übermittlung von vordefinierten Elemente (z. B. LKW/van, Post, Pickup, Courier, usw.)|
|PaymentMethods|Optionen zum Durchführen von Zahlungen (z. B. Bar, Scheck EFT, usw.)|
|TransactionTypes|Arten von Kunden, Lieferanten oder vordefinierten Transaktionen (z. B. Rechnung, Gutschrift, usw.)|

### <a name="purchasing-schema"></a>Erwerb von Schemas

Details des Lieferanten und der Lagerartikel Käufe.

|Tabelle|Description|
|-----------------------------|---------------------|
|Suppliers|Main Entitätstabelle für Lieferanten (Organisationen)|
|SupplierCategories|Kategorien für Lieferanten (z. B. Novelties, Toys, clothing, Verpackung usw.)|
|SupplierTransactions|Alle finanzielle Transaktionen, die Lieferanten-bezogene (Rechnungen, Zahlungen) sind.|
|PurchaseOrders|Details des Lieferanten Bestellungen|
|PurchaseOrderLines|Detailzeilen vom Lieferanten Bestellungen|

 
### <a name="sales-schema"></a>Sales-Schema

Details der Kunden, Vertriebsmitarbeiter, und der Lagerartikel Verkäufe.

|Tabelle|Description|
|-----------------------------|---------------------|
|Customers|Hauptentität Tabellen für Kunden (Organisationen oder Einzelpersonen)|
|CustomerCategories|Kategorien für Kunden (d. h. Neuheit speichert, Supermärkten, usw.)|
|BuyingGroups|Kundenorganisationen können Gruppen angehören, die größer Onlineshopping Power ausüben|
|CustomerTransactions|Alle finanzielle Transaktionen, denen kundenbezogene (Rechnungen, Zahlungen)|
|SpecialDeals|Vorzugspreis. Dadurch können festen Preise enthalten, für den Rabatt in Dollar oder Rabatt in Prozent.|
|Orders|Details der kundenbestellungen|
|OrderLines|Detailzeilen von Kundenaufträgen|
|Rechnungen|Details der Customer-Rechnungen|
|InvoiceLines|Detailzeilen von Kunden Rechnungen|

### <a name="warehouse-schema"></a>Warehouse-Schemas

Details der stock-Elemente, deren betrieben und Transaktionen.

|Tabelle|Description|
|-----------------------------|---------------------|
|StockItems|Main Entitätstabelle für vordefinierte Elemente|
|StockItemHoldings|Non-temporal Spalten für vordefinierte Elemente. Hierbei handelt es sich um häufig aktualisierten Spalten.|
|StockGroups|Gruppen, die zum Kategorisieren von vordefinierten Elemente (z. B. Novelties, Toys, eßbare Novelties, usw.)|
|StockItemStockGroups|Die vordefinierten Elemente sind in der Stock (m: n) gruppiert|
|Farben|Stock Elemente können (optional) Farben aufweisen.|
|PackageTypes|Methoden, mit denen Elemente stock verpackt werden können (z. B. Feld, Kartons, Palette, kg usw.|
|StockItemTransactions|Transaktionen, die für alle Bewegungen aller vordefinierten Elemente (Empfang, Verkauf, auf null)|
|VehicleTemperatures|Regelmäßig aufgezeichneten Temperaturen Fahrzeug chillers|
|ColdRoomTemperatures|Temperaturen kalte Platz Chillers regelmäßig aufgezeichnet|


## <a name="design-considerations"></a>Überlegungen zum Entwurf

Datenbankentwurf subjektive ist, und es gibt keine Möglichkeit falsch oder eine Datenbank entwerfen. Zeigen die Schemas und Tabellen in dieser Datenbank Ideen zur wie Sie Ihre eigene Datenbank entwerfen können.

### <a name="schema-design"></a>Schemaentwurf

"Wideworldimporters" verwendet eine kleine Anzahl von Schemas, sodass es einfach ist zu verstehen, die Datenbank-Managementsystem und Datenbank-Prinzipien veranschaulichen.  

Nach Möglichkeit collocates die Datenbank die Tabellen, die häufig zusammen im gleichen Schema Join Komplexität minimieren abgefragt werden.

Das Datenbankschema wurde generierten Code basierend auf einer Reihe von Tabellen mit Replikationsmetadaten in einer anderen Datenbank WWI_Preparation. Dies bietet "wideworldimporters" auf einen sehr hohen Grad an Entwurf Consistency, Konsistenz und Vollständigkeit. Weitere Informationen wie der Generierung des Schemas des Quellcodes finden Sie: [Wide-Welt-Importers/Schlachtfeld-Datenbank-Skripts](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>Tabellenentwurf

- Alle Tabellen haben einzelne Spalte Primärschlüsseln aus Gründen der Einfachheit Join.
- Alle Schemas, Tabellen, Spalten, Indizes und Check-Einschränkungen haben eine Beschreibung, die erweiterte Eigenschaft, die verwendet werden kann, um den Zweck des Objekts oder der Spalte zu identifizieren. Speicheroptimierte Tabellen sind eine Ausnahme aus, da sie derzeit Unterstützung für erweiterte Eigenschaften besitzen.
- Alle Fremdschlüssel werden automatisch indiziert werden, es sei denn, es ist einem anderen nicht gruppierten Index, der die gleiche linke Komponente verfügt.
- Automatische Nummerierung in Tabellen basiert auf Sequenzen. Diese Sequenzen sind einfacher zu arbeiten über Verbindungsserver und ähnlichen Umgebungen als IDENTITY-Spalten. Speicheroptimierte Tabellen verwenden IDENTITY-Spalten aus, da sie in SQL Server 2016 nicht unterstützt.
- Wird eine einzige Sequenz (Transaktions-ID) für diese Tabellen verwendet: CustomerTransactions SupplierTransactions und StockItemTransactions. Dies zeigt, wie eine Gruppe von Tabellen eine einzige Sequenz aufweisen kann.
- Einige Spalten haben entsprechende Standardwerte.

### <a name="security-schemas"></a>Sicherheit-schemas

Aus Sicherheitsgründen lässt "wideworldimporters" Datenschemas direkten Zugriff auf externe Anwendungen nicht zu. Um den Zugriff zu isolieren, wird "wideworldimporters" Sicherheitszugriff Schemas, die Daten nicht aufnehmen, aber enthält Sichten und gespeicherten Prozeduren verwendet. Externe Anwendungen verwenden die Sicherheit Schemas zum Abrufen der Daten, die sie anzeigen dürfen.  Auf diese Weise können Benutzer nur die Sichten und gespeicherten Prozeduren in den sicheren Zugriff ausführen

In diesem Beispiel wird angenommen, Power BI-Dashboards enthält. Eine externe Anwendung greift diese Power BI-Dashboards aus dem Power BI-Gateway als ein Benutzer mit Leseberechtigung für das Power BI-Schema auf.  Für schreibgeschützte Berechtigung benötigt der Benutzer nur SELECT- und EXECUTE-Berechtigung für das Power BI-Schema. Ein Datenbankadministrator am Schlachtfeld weist diese Berechtigungen nach Bedarf.

## <a name="stored-procedures"></a>Gespeicherte Prozeduren

Gespeicherte Prozeduren sind in Schemas organisiert. Die meisten der Schemas werden für die Konfiguration oder Beispielzwecken verwendet.

Die `Website` Schema enthält die gespeicherten Prozeduren, die von einer Web-Front-End verwendet werden können.

Die `Reports` und `PowerBI` Schemas für die reporting Services und Power BI-Zwecke vorgesehen sind. Alle Erweiterungen des Beispiels werden empfohlen, diese Schemas für Berichtszwecke verwenden.

### <a name="website-schema"></a>Website-schema

Hierbei handelt es sich um die Verfahren, die von einer Clientanwendung, z. B. einer Web-Front-End verwendet.

|Verfahren|Zweck|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|Erlaubt einem Benutzer (aus `Application.People`) auf die Website zugreifen.|
|ChangePassword|Ändert das Kennwort eines Benutzers (für Benutzer, die keine externen Authentifizierungsmechanismen verwenden).|
|InsertCustomerOrders|Ermöglicht es, eine oder mehrere kundenbestellungen (einschließlich der Auftragspositionen) einfügen.|
|InvoiceCustomerOrders|Eine Liste von Bestellungen in Rechnung zu stellende und verarbeitet die Rechnungen.|
|RecordColdRoomTemperatures|Akzeptiert eine Datenliste Sensor als ein Tabellenwertparameter (TVP), und wendet die Daten auf den `Warehouse.ColdRoomTemperatures` temporale Tabelle.|
|RecordVehicleTemperature|Akzeptiert ein JSON-Array und verwendet, um die Aktualisierung `Warehouse.VehicleTemperatures`.|
|SearchForCustomers|Sucht nach Kunden anhand des Namens oder der Teil des Namens (den Firmennamen oder der Personenname).|
|SearchForPeople|Sucht nach Personen anhand des Namens oder der Teil des Namens.|
|SearchForStockItems|Sucht nach vordefinierten Elemente nach Namen oder einen Teil des Namens oder marketing Kommentare.|
|SearchForStockItemsByTags|Sucht nach vordefinierten Elemente mit Tags.|
|SearchForSuppliers|Sucht nach Lieferanten anhand des Namens oder der Teil des Namens (den Firmennamen oder der Personenname).|

### <a name="integration-schema"></a>Integration Schema

Die gespeicherten Prozeduren in diesem Schema werden von der ETL-Prozess verwendet. Sie erhalten die benötigten Daten aus verschiedenen Tabellen für den Zeitraum erforderlich die [ETL-Pakets](etl-workflow.md).

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation-Schema

Simuliert eine arbeitsauslastung, die Verkäufe und Einkäufe einfügt. Die wichtigste gespeicherte Prozedur ist `PopulateDataToCurrentDate`, der verwendet wird, legen Sie die Beispieldaten bis zum aktuellen Datum.

|Verfahren|Zweck|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|Abonnementtyps Verfahren benötigt für Daten Simulation geladen werden. Dies ist erforderlich für das Zusammenführen der Daten bis zum aktuellen Datum.|
|Configuration_RemoveDataLoadSimulationProcedures|Dies entfernt das Verfahren erneut nach Daten Simulation abgeschlossen ist.|
|DeactiveTemporalTablesBeforeDataLoad|Entfernt den temporale Charakter alle temporalen Tabellen und, sofern zutreffend, wird einen Trigger angewendet, sodass Änderungen vorgenommen werden können, als wären sie auf ein früheres Datum als das Sys-temporale Tabellen ermöglichen angewendet werden.|
|PopulateDataToCurrentDate|Verwendet, um die Daten bis zum aktuellen Datum zu bringen. Sollte vor alle anderen Konfigurationsoptionen, die Sie nach dem Wiederherstellen der Datenbank aus einer Sicherung ausgeführt werden.|
|ReactivateTemporalTablesAfterDataLoad|Stellt die temporale Tabellen, einschließlich, überprüft die Konsistenz der Daten erneut her. (Die zugeordneten Trigger wird entfernt).|


### <a name="application-schema"></a>Anwendungsschema

Diese Prozeduren werden zum Konfigurieren des Beispiels verwendet. Sie werden verwendet, um Funktionen der Enterprise Edition auf die standard Edition-Version des Beispiels und auch die Überwachung hinzufügen und die Volltextindizierung anzuwenden.

|Verfahren|Zweck|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|Fügt ein Mitglied einer Rolle, wenn das Element bereits in der Rolle nicht|
|Configuration_ApplyAuditing|Bietet die Überwachung. Server-Überwachung wird für standard Edition-Datenbanken angewendet. zusätzliche datenbanküberwachung ist für die Enterprise Edition hinzugefügt.|
|Configuration_ApplyColumnstoreIndexing|Wendet Columnstore Indizierung `Sales.OrderLines` und `Sales.InvoiceLines` und reindexes entsprechend.|
|Configuration_ApplyFullTextIndexing|Wendet die Volltextindizes zu `Application.People`, `Sales.Customers`, `Purchasing.Suppliers`, und `Warehouse.StockItems`. Ersetzt `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers`, `Website.SearchForStockItems`, `Website.SearchForStockItemsByTags` mit Ersatzprozeduren, die die Volltextindizierung verwenden.|
|Configuration_ApplyPartitioning|Wendet die Tabellenpartitionierung zu `Sales.CustomerTransactions and `'Purchasing.SupplierTransactions und sortiert die Indizes entsprechend.|
|Configuration_ApplyRowLevelSecurity|Filter Kunden Sicherheit auf Zeilenebene betrifft, Sales Territory-bezogenen Rollen.|
|Configuration_ConfigureForEnterpriseEdition|Columnstore-Index, Volltextsuche, im Arbeitsspeicher, Polybase und Partitionierung angewendet.|
|Configuration_EnableInMemory|Fügt eine Speicheroptimierte Dateigruppe (wenn nicht in Azure arbeiten), ersetzt `Warehouse.ColdRoomTemperatures`, `Warehouse.VehicleTemperatures` mit InMemory-äquivalente, und die Daten migriert wird, erstellt der `Website.OrderIDList`, `Website.OrderList`, `Website.OrderLineList`, `Website.SensorDataList` gelöscht und neu erstellt die Prozeduren Tabellentypen mit den entsprechenden Speicheroptimierte `Website.InvoiceCustomerOrders`, `Website.InsertCustomerOrders`, und `Website.RecordColdRoomTemperatures` , verwendet diese Tabellentypen.|
|Configuration_RemoveAuditing|Entfernt die Überwachungskonfiguration.|
|Configuration_RemoveRowLevelSecurity|Entfernt die Zeile Sicherheit auf Zeilenebene-Konfiguration (Dies ist für Änderungen an den zugeordneten Tabellen erforderlich).|
|CreateRoleIfNonExistant|Erstellt eine Datenbankrolle aus, wenn er nicht bereits vorhanden.|


### <a name="sequences-schema"></a>Sequences Schema

Verfahren zum Konfigurieren von Sequenzen in der Datenbank.

|Verfahren|Zweck|
|-----------------------------|---------------------|
|ReseedAllSequences|Ruft die Prozedur ReseedSequenceBeyondTableValue für alle Sequenzen.|
|ReseedSequenceBeyondTableValue|Verwendet, um den nächsten Sequenzwert hinter dem Wert in einer beliebigen Tabelle neu zu positionieren, die die gleiche Sequenz verwendet. (Z. B. einem DBCC CHECKIDENT für die Identität Spalten entspricht, für die Sequenzen, aber auf potenziell mehrere Tabellen).|
