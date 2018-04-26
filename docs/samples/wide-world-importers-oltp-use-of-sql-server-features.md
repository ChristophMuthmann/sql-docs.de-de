---
title: Verwendung von SQL Server-Features und Funktionen | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
caps.latest.revision: 2
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: a2b0ccfba8baf0f52245a7beba44e846b481cfa8
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="use-of-sql-server-features-and-capabilities"></a>Verwendung von SQL Server-Features und Funktionen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
"Wideworldimporters" Verwenden von SQL Server-Features und Funktionen in der OLTP-Datenbank.

"Wideworldimporters" dient zur Veranschaulichung viele der wichtigsten Funktionen von SQL Server, einschließlich der neuesten Funktionen in SQL Server 2016 eingeführt. Im folgenden finden eine Liste von SQL Server-Funktionen, Funktionen und eine Beschreibung, wie sie in "wideworldimporters" verwendet werden.

|SQL Server-Feature oder Funktion|Verwendung in "wideworldimporters"|
|-----------------------------|---------------------|
|Temporale Tabellen|Es gibt zahlreiche temporale Tabellen enthält, einschließlich aller Nachschlagetabellen, Stil-Verweis und main Entitäten wie z. B. StockItems, Kunden und Lieferanten. Bei temporalen Tabellen kann, um bequem zu verfolgen den Verlauf dieser Entitäten.|
|AJAX-Aufrufe für JSON|Die Anwendung verwendet AJAX-Aufrufe häufig auf diese Tabellen Abfragen: Personen, Kunden und Lieferanten, StockItems. Der Aufruf zurück, JSON-Nutzlasten (d. h. ist die Daten, die zurückgegeben werden als JSON-Daten formatiert). Anzeigen, z. B. die gespeicherte Prozedur `Website.SearchForCustomers`.|
|JSON-Eigenschaft/Wert-Sammlungen|Eine Reihe von Tabellen muss Spalten mit JSON-Daten in die relationale Daten in der Tabelle zu erweitern. Beispielsweise `Application.SystemParameters` enthält eine Spalte für Anwendungseinstellungen und `Application.People` besitzt eine Spalte zum Erfassen der benutzereinstellungen. Diese Tabellen verwenden ein `nvarchar(max)` Spalte zum Aufzeichnen der JSON-Daten zusammen mit einer CHECK-Einschränkung mit der integrierten Funktion `ISJSON` um sicherzustellen, dass die Spalte Werte sind gültige JSON.|
|Sicherheit auf Zeilenebene (RLS)|Zeile Level Security (RLS) wird verwendet, um den Zugriff auf die Customers-Tabelle, basierend auf der Rollenmitgliedschaft einzuschränken. Jedes Vertriebsgebiet verfügt über eine Rolle und Benutzer. Um dies in Aktion sehen, verwenden Sie das entsprechende Skript in der Beispiel-script.zip, die Teil von der [Version des Beispiels](http://go.microsoft.com/fwlink/?LinkID=800630).|
|Operative Echtzeitanalyse|(Vollständige Version der Datenbank) Die transaktionale Haupttabellen `Sales.InvoiceLines` und `Sales.OrderLines` beide verfügen über einen nicht gruppierten Columnstore-Index, effiziente Ausführung von Analyseabfragen in die Transaktionsdatenbank mit minimaler Auswirkung auf die betrieblichen arbeitsauslastung zu unterstützen. Ausführen von Transaktionen und Analysen in der gleichen Datenbank wird auch als bezeichnet [Hybrid transaktional/Analytical Processing (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP)). Um dies in Aktion sehen, verwenden Sie das entsprechende Skript in der Beispiel-script.zip, die Teil von der [Version des Beispiels](http://go.microsoft.com/fwlink/?LinkID=800630).|
|PolyBase|Auf diese PolyBase in Aktion, mit einer externen Tabelle mit einem öffentlichen Dataset in Azure BLOB-Speicher gehosteten finden Sie unter Verwenden Sie das entsprechende Skript in der Beispiel-script.zip, die Teil von der [Version des Beispiels](http://go.microsoft.com/fwlink/?LinkID=800630).|
|In-Memory OLTP|(Vollständige Version der Datenbank) Die Tabellentypen sind aller speicheroptimierten, sodass speicheroptimierung-Tabellenwertparameter (TVPs) alle profitieren.<br/><br/>Die zwei Überwachungstabellen `Warehouse.VehicleTemperatures` und `Warehouse.ColdRoomTemperatures`, Speicheroptimierte sind. Dadurch wird die Tabelle ColdRoomTemperatures mit höherer Geschwindigkeit als eine herkömmliche datenträgerbasierte Tabelle aufgefüllt werden. Die VehicleTemperatures-Tabelle enthält die JSON-Nutzlast und eignet sich für die Erweiterung nach IoT-Szenarien. Die VehicleTemperatures Tabelle weitere eignet sich für Szenarien mit EventHubs und Stream Analytics Power BI.<br/><br/>Die gespeicherte Prozedur `Website.RecordColdRoomTemperatures` zur weiteren Verbesserung der Leistung aufzeichnen kalte Platz Temperaturen systemintern kompiliert wird.<br/><br/>Ein Beispiel für In-Memory OLTP in Aktion finden Sie unter der Fahrzeug Speicherorte Arbeitslast Treiber in arbeitsauslastung-drivers.zip, die Teil von der [Version des Beispiels](http://go.microsoft.com/fwlink/?LinkID=800630).|
|Gruppierter Columnstore-Index|(Vollständige Version der Datenbank) Die Tabelle `Warehouse.StockItemTransactions` verwendet einen gruppierten columnstore-Index. Die Anzahl der Zeilen in dieser Tabelle ist zu groß werden erwartet und der gruppierten columnstore-Index erheblich reduziert die Größe auf dem Datenträger, der Tabelle und verbessert die abfrageleistung. Die Änderung auch in dieser Tabelle werden nur einfügungen – es ist kein Update/Delete für die Tabelle in der online-arbeitsauslastung - und gruppierter columnstore-Index führt für die Insert-arbeitsauslastungen geeignet.|
|Dynamische Datenmaskierung|In das Datenbankschema Datenmaskierung angewendet wurde, die Details der Bank für Lieferanten, in der Tabelle gespeicherten `Purchasing.Suppliers`. Ohne Administratorrechte Mitarbeiter müssen nicht den Zugriff auf diese Informationen.|
|Always Encrypted|Ein Verwendungsbeispiel für Always Encrypted ist enthalten, in dem herunterladbaren samples.zip, die Teil von der [Version des Beispiels](http://go.microsoft.com/fwlink/?LinkID=800630)... Die Demo erstellt einen Verschlüsselungsschlüssel, der eine Tabelle, die Verwendung der Verschlüsselung für vertrauliche Daten und einer kleinen beispielanwendung, die Daten in die Tabelle einfügt.|
|Stretch-Datenbank|Die `Warehouse.ColdRoomTemperatures` Tabelle als eine temporale Tabelle implementiert wurde, und in der vollständigen Version der Beispieldatenbank speicheroptimiert ist. Die remotedatenarchiv-Tabelle basiert auf Datenträger und Azure gestreckt werden.|
|Volltextindizes|Volltextindizes verbessern sucht nach Mitarbeitern, Kunden und StockItems. Die Indizes werden auf Abfragen angewendet werden, nur, wenn Sie Volltextindizierung für Ihre SQL Server-Instanz installiert haben. Eine nicht persistente berechnete Spalte wird verwendet, um die Daten zu erstellen, die Volltext-ist in der Tabelle StockItems indiziert.<br/><br/>`CONCAT` Dient zum Verketten die Felder zum SearchData zu erstellen, die volltextindiziert ist.<br/>Zum Aktivieren der Verwendung von Volltextindizes im Beispiel die folgende Anweisung in der Datenbank ausführen:<br/><br/>    `EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>Die Prozedur erstellt einen Standard-Volltextkatalogs Wenn eine nicht bereits vorhanden ist, ersetzt die Search-Ansichten mit Volltext-Versionen dieser Ansichten).<br/><br/>Beachten Sie, dass mithilfe von Volltextindizes in SQL Server erforderlich ist, wählen Sie die Option Volltext-während der Installation. Azure SQL-Datenbank ist nicht erforderlich und besondere Konfiguration für die Volltextindizes zu aktivieren.|
|Indizierte permanente berechnete Spalten|Indizierte permanente berechnete Spalten, die bei der SupplierTransactions und CustomerTransactions verwendet.|
|Check-Einschränkungen|Eine relativ komplexe Check-Einschränkung wird `Sales.SpecialDeals`. Dadurch wird sichergestellt, dass eine und nur eine der DiscountAmount DiscountPercentage, und UnitPrice konfiguriert ist.|
|Unique-Einschränkungen|Eine m: viele Konstruktion (und unique-Einschränkungen) sind für Warehouse.StockItemStockGroups eingerichtet.|
|Tabellenpartitionierung|(Vollständige Version der Datenbank) Die Tabellen `Sales.CustomerTransactions` und `Purchasing.SupplierTransactions` werden nach Jahr, mit die Partitionsfunktion partitioniert `PF_TransactionDate` und das Partitionsschema `PS_TransactionDate`. Partitionierung wird verwendet, um die Verwaltbarkeit großer Tabellen zu verbessern.|
|Liste Verarbeitung|Ein Beispiel Tabellentyp `Website.OrderIDList` bereitgestellt wird. Er wird durch eine Beispielprozedur verwendet `Website.InvoiceCustomerOrders`. Das Verfahren werden allgemeine Tabellenausdrücke (CTEs), TRY/CATCH JSON_MODIFY, XACT_ABORT, NOCOUNT, throw- und XACT_STATE verwendet, um veranschaulicht die Möglichkeit zum Verarbeiten einer Liste der Aufträge, anstatt nur einen einzelnen Auftrag aus der Anwendung mit dem Datenbankmodul Roundtrips zu minimieren.|
|GZip-Komprimierung.|Die `Warehouse.VehicleTemperature`s-Tabelle enthält die vollständige Sensordaten jedoch, wenn diese Daten mehr als ein paar Monate ist, wird komprimiert zum Einsparen von Speicherplatz, die mithilfe der Funktion COMPRESS, mit dem GZip-Komprimierung verwendet.<br/><br/>Die Ansicht `Website.VehicleTemperatures` verwendet die DECOMPRESS-Funktion, beim Abrufen von Daten, die zuvor komprimiert wurde.|
|Abfragespeicher|Der Abfragespeicher ist für die Datenbank aktiviert. Öffnen Sie nach einigen Abfragen ausführen die Datenbank in Management Studio aus, öffnen Sie den Knoten Abfragespeicher, d. h. unter der Datenbank, und öffnen Sie den Bericht Abfragen mit höchstem Ressourcenverbrauch, finden in der abfrageausführungen und die Pläne für Abfragen, die Sie soeben ausgeführt haben.|
|STRING_SPLIT|Die Spalte `DeliveryInstructions` in der Tabelle `Sales.Invoices`verfügt über eine durch Trennzeichen getrennte-Wert, der verwendet werden kann, um STRING_SPLIT zu veranschaulichen.|
|Überwachen von|SQL Server Audit können für diese Beispieldatenbank aktiviert werden, indem Sie die folgende Anweisung in der Datenbank ausführen:<br/><br/>    `EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>In Azure SQL-Datenbank, Aktivierung der Überwachung über die [Azure-Portal](https://portal.azure.com/).<br/><br/>Sicherheitsvorgänge im Zusammenhang mit Anmeldungen, werden Rollen und Berechtigungen auf allen Systemen protokolliert, Überwachung (einschließlich standard Edition-Systeme) aktiviert ist. Überwachung wird in das Anwendungsprotokoll umgeleitet werden, da dies auf allen Systemen verfügbar ist und keine zusätzliche Berechtigungen erfordert. Eine Warnung handelt, davon ausgehend, dass zum Erhöhen der Sicherheit, es in das Sicherheitsprotokoll oder in eine Datei in einem sicheren Ordner umgeleitet werden sollen. Ein Link wird bereitgestellt, um die erforderliche zusätzliche Konfiguration beschreiben.<br/><br/>Für Systeme Evaluierung, Developer, Enterprise Edition wird den Zugriff auf alle finanzielle Transaktionsdaten überwacht.|
