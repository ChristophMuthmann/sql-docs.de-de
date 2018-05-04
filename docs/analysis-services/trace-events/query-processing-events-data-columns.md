---
title: Query Processing Events Data Columns | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 81a522bd-440d-406c-a524-3af44a3af101
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 117cab8b57631b1a95dea9baa0e86e918cabf81f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="query-processing-events-data-columns"></a>Abfrageverarbeitungsereignisse – Datenspalten
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Die Ereigniskategorie "Abfrageverarbeitung" besitzt die folgenden Ereignisklassen:  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|70|Query Cube Begin|Beginn des Abfragecubes.|  
|71|Query Cube End|Ende des Abfragecubes.|  
|72|Calculate Non Empty Begin|Die Berechnung von nicht leeren Elementen wird gestartet.|  
|73|Calculate Non Empty Current|Die Berechnung nicht leerer Elemente wird ausgeführt.|  
|74|Calculate Non Empty End|Die Berechnung nicht leerer Elemente wird beendet.|  
|75|Serialize Results Begin|Die Serialisierung von Ergebnissen wird gestartet.|  
|76|Serialize Results Current|Die Serialisierung von Ergebnissen wird ausgeführt.|  
|77|Serialize Results End|Die Serialisierung von Ergebnissen wird beendet.|  
|78|Execute MDX Script Begin|Die Ausführung des MDX-Skripts wird gestartet.|  
|79|Execute MDX Script Current|Das MDX-Skript wird ausgeführt. Veraltet.|  
|80|Execute MDX Script End|Die Ausführung des MDX-Skripts wird beendet.|  
|81|Query Dimension|Die Abfragedimension.|  
|11|Query Subcube|Query Subcube für verwendungsbasierte Optimierung.|  
|12|Query Subcube Verbose|Query Subcube mit detaillierten Informationen. Dieses Ereignis kann sich bei Aktivierung negativ auf die Leistung auswirken.|  
|60|Get Data From Aggregation|Abfrage durch Abrufen von Daten aus der Aggregation beantworten. Dieses Ereignis kann sich bei Aktivierung negativ auf die Leistung auswirken.|  
|61|Get Data From Cache|Abfrage durch Abrufen von Daten aus einem der Caches beantworten. Dieses Ereignis kann sich bei Aktivierung negativ auf die Leistung auswirken.|  
|82|VertiPaq SE Query Begin|VertiPaq SE-Abfrage|  
|83|VertiPaq SE Query End|VertiPaq SE-Abfrage|  
|84|Resource Usage|Lese- und Schreibvorgänge für Berichte, CPU-Auslastung nach Ende von Befehlen und Abfragen.|  
|85|VertiPaq SE Query Cache Match|Cacheverwendung in VertiPaq SE-Abfrage|  
|98|Direct Query Begin|Beginn der direkten Abfrage.|  
|99|Direct Query End|Ende der direkten Abfrage.|  
  
 In den folgenden Tabellen sind die Datenspalten für jede dieser Ereignisklassen aufgeführt.  
  
## <a name="query-cube-begin"></a>Query Cube Begin  
  
|||||  
|-|-|-|-|  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="query-cube-end"></a>Query Cube End  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="calculate-non-empty-begin"></a>Calculate Non Empty Begin  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="calculate-non-empty-current"></a>Calculate Non Empty Current  
  
|||||  
|-|-|-|-|  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 1: Get Data<br /><br /> 2: Process Calculated Members<br /><br /> 3: Post Order|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="calculate-non-empty-end"></a>Calculate Non Empty End  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="serialize-results-begin"></a>Serialize Results Begin  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="serialize-results-current"></a>Serialize Results Current  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 1: Serialize Axes<br /><br /> 2: Serialize Cells<br /><br /> 3: Serialize SQL Rowset<br /><br /> 4: Serialize Flattened Rowset|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="serialize-results-end"></a>Serialize Results End  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="execute-mdx-script-begin"></a>Execute MDX Script Begin  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 1: MDX Script<br /><br /> 2: MDX Script Command|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="execute-mdx-script-current"></a>Execute MDX Script Current  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="execute-mdx-script-end"></a>Execute MDX Script End  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 1: MDX Script<br /><br /> 2: MDX Script Command|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="query-dimension"></a>Query Dimension  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 1: Cache data<br /><br /> 2: Non-cache data|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectType|12|1|Objekttyp.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="query-subcube"></a>Query Subcube  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 1: Cache data<br /><br /> 2: Non-cache data<br /><br /> 3: Internal data<br /><br /> 4: SQL data<br /><br /> 11: Measure Group Structural Change<br /><br /> 12: Measure Group Deletion|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|SessionID|39|8|Sitzungs-GUID.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="query-subcube-verbose"></a>Query Subcube Verbose  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 21: Cache data<br /><br /> 22: Non-cache data<br /><br /> 23: Internal data<br /><br /> 24: SQL data|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|SessionID|39|8|Sitzungs-GUID.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="get-data-from-aggregation"></a>Get Data From Aggregation  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|SessionID|39|8|Sitzungs-GUID.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="get-data-from-cache"></a>Get Data From Cache  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 1: Get data from measure group cache<br /><br /> 2: Get data from flat cache<br /><br /> 3: Get data from calculation cache<br /><br /> 4: Get data from persisted cache|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|SessionID|39|8|Sitzungs-GUID.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="vertipaq-se-query-begin"></a>VertiPaq SE Query Begin  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 0: VertiPaq Scan<br /><br /> 1: Tabular Query<br /><br /> 2: User Hierarchy Processing Query<br /><br /> 10: VertiPaq Scan internal<br /><br /> 11: Tabular Query internal<br /><br /> 12: User Hierarchy Processing Query internal|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|JobID|7|1|Auftrags-ID für den Status.|  
|SessionType|8|8|Sitzungstyp (Entität, die den Vorgang verursacht hat).|  
|ObjectID|11|8|Objekt-ID (beachten Sie, dass dies eine Zeichenfolge ist).|  
|ObjectType|12|1|Objekttyp.|  
|ObjectName|13|8|Objektname.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ObjectReference|15|8|Objektverweis. Codiert als XML für alle übergeordneten Elemente, das Verwenden von Tags, um das Objekt zu beschreiben.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTUserName|32|8|Windows-Benutzername.|  
|NTDomainName|33|8|Windows-Domäne, zu der der Benutzer gehört.|  
|SessionID|39|8|Sitzungs-GUID.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="vertipaq-se-query-end"></a>VertiPaq SE Query End  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 0: VertiPaq Scan<br /><br /> 1: Tabular Query<br /><br /> 10: VertiPaq Scan internal<br /><br /> 11: Tabular Query internal|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|JobID|7|1|Auftrags-ID für den Status.|  
|SessionType|8|8|Sitzungstyp (Entität, die den Vorgang verursacht hat).|  
|ProgressTotal|9|1|Gesamter Fortschritt.|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectID|11|8|Objekt-ID (beachten Sie, dass dies eine Zeichenfolge ist).|  
|ObjectType|12|1|Objekttyp.|  
|ObjectName|13|8|Objektname.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ObjectReference|15|8|Objektverweis. Codiert als XML für alle übergeordneten Elemente, das Verwenden von Tags, um das Objekt zu beschreiben.|  
|Severity|22|1|Schweregrad einer Ausnahme.|  
|Success|23|1|1 = Erfolg 0 = Fehler (z. B. gibt 1 den Erfolg einer Berechtigungsüberprüfung und 0 einen Fehler bei dieser Überprüfung an).|  
|Fehler|24|1|Fehlernummer eines bestimmten Ereignisses.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTUserName|32|8|Windows-Benutzername.|  
|NTDomainName|33|8|Windows-Domäne, zu der der Benutzer gehört.|  
|SessionID|39|8|Sitzungs-GUID.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="resource-usage"></a>Resource Usage  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTUserName|32|8|Windows-Benutzername.|  
|NTDomainName|33|8|Windows-Domäne, zu der der Benutzer gehört.|  
|ClientProcessID|36|1|Die Prozess-ID der Clientanwendung.|  
|ApplicationName|37|8|Der Name der Clientanwendung, die die Verbindung mit dem Server hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|  
|SessionID|39|8|Sitzungs-GUID.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="vertipaq-se-query-cache-match"></a>VertiPaq SE Query Cache Match  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 0: VertiPaq Cache exact match|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|JobID|7|1|Auftrags-ID für den Status.|  
|SessionType|8|8|Sitzungstyp (Entität, die den Vorgang verursacht hat).|  
|ObjectID|11|8|Objekt-ID (beachten Sie, dass dies eine Zeichenfolge ist).|  
|ObjectType|12|1|Objekttyp.|  
|ObjectName|13|8|Objektname.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|ObjectReference|15|8|Objektverweis. Codiert als XML für alle übergeordneten Elemente, das Verwenden von Tags, um das Objekt zu beschreiben.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|NTUserName|32|8|Windows-Benutzername.|  
|NTDomainName|33|8|Windows-Domäne, zu der der Benutzer gehört.|  
|SessionID|39|8|Sitzungs-GUID.|  
|NTCanonicalUserName|40|8|Benutzername in kanonischer Form. Zum Beispiel "engineering.microsoft.com/software/someone".|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="direct-query-begin"></a>Direct Query Begin  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|JobID|7|1|Auftrags-ID für den Status.|  
|SessionType|8|8|Sitzungstyp (Entität, die den Vorgang verursacht hat).|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectID|11|8|Objekt-ID (beachten Sie, dass dies eine Zeichenfolge ist).|  
|ObjectType|12|1|Objekttyp.|  
|ObjectName|13|8|Objektname.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|Severity|22|1|Schweregrad einer Ausnahme.|  
|Success|23|1|1 = Erfolg 0 = Fehler (z. B. gibt 1 den Erfolg einer Berechtigungsüberprüfung und 0 einen Fehler bei dieser Überprüfung an).|  
|Fehler|24|1|Fehlernummer eines bestimmten Ereignisses.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|ClientProcessID|36|1|Die Prozess-ID der Clientanwendung.|  
|SessionID|39|8|Sitzungs-GUID.|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="direct-query-end"></a>Direct Query End  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|CurrentTime|2|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Der Zeitpunkt, zu dem das Ereignis begonnen hat (falls verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Der Zeitpunkt, zu dem das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Die Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|JobID|7|1|Auftrags-ID für den Status.|  
|SessionType|8|8|Sitzungstyp (Entität, die den Vorgang verursacht hat).|  
|IntegerData|10|1|Ganzzahlige Daten.|  
|ObjectID|11|8|Objekt-ID (beachten Sie, dass dies eine Zeichenfolge ist).|  
|ObjectType|12|1|Objekttyp.|  
|ObjectName|13|8|Objektname.|  
|ObjectPath|14|8|Objektpfad. Eine durch Trennzeichen getrennte Liste von übergeordneten Elementen, die beim übergeordneten Element des Objekts beginnt.|  
|Severity|22|1|Schweregrad einer Ausnahme.|  
|Success|23|1|1 = Erfolg 0 = Fehler (z. B. gibt 1 den Erfolg einer Berechtigungsüberprüfung und 0 einen Fehler bei dieser Überprüfung an).|  
|Fehler|24|1|Fehlernummer eines bestimmten Ereignisses.|  
|ConnectionID|25|1|Eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Name der Datenbank, in der die Anweisung des Benutzers ausgeführt wird.|  
|ClientProcessID|36|1|Die Prozess-ID der Clientanwendung.|  
|SessionID|39|8|Sitzungs-GUID.|  
|SPID|41|1|Serverprozess-ID. Hierdurch wird eine Benutzersitzung eindeutig gekennzeichnet. Dies entspricht direkt dem von XML/A verwendeten Sitzungs-GUID.|  
|TextData|42|9|Dem Ereignis zugeordnete Textdaten.|  
|ServerName|43|8|Name des Servers, der das Ereignis erzeugt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Abfrage Verarbeitung Events-Ereigniskategorie](../../analysis-services/trace-events/query-processing-events-category.md)  
  
  
