---
title: "SQL Server Integration Services-Datentypen | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Ändern von Datentypen"
  - "Datentypen [Integration Services], Liste"
  - "Datentypen [Integration Services]"
  - "Spaltendatentypen [Integration Services]"
  - "SSIS, Datentypen"
  - "Integration Services, Datentypen"
  - "SQL Server Integration Services, Datentypen"
ms.assetid: 896fc3e8-3aa6-4396-ba82-5d7741cffa56
caps.latest.revision: 98
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 98
---
# SQL Server Integration Services-Datentypen
  Wenn Daten an einen Datenfluss in einem Paket weitergegeben werden, konvertiert die Quelle, die die Daten extrahiert, diese in einen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentyp. Numerischen Daten wird ein numerischer Datentyp, Zeichenfolgendaten wird ein Zeichendatentyp und Daten ein Datumsdatentyp zugewiesen. Anderen Daten, wie z. B. GUIDs und BLOBs (Binary Large Object Blocks), werden ebenfalls entsprechende [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Datentypen zugewiesen. Falls Daten von einem Datentyp sind, der nicht in einen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentyp konvertiert werden kann, tritt ein Fehler auf.  
  
 Einige Datenflusskomponenten konvertieren [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentypen in verwaltete Datentypen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Weitere Informationen zur Zuordnung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zu verwalteten Datentypen finden Sie unter [Verwenden von Datentypen im Datenfluss](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
 In der folgenden Tabelle sind die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentypen aufgeführt. Bei einigen der Datentypen in der Tabelle werden auch die für sie geltende Genauigkeit und die Anzahl der Dezimalstellen genannt. Weitere Informationen zu Genauigkeit und Dezimalstellen finden Sie unter [Genauigkeit, Dezimalstellen und Länge &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
|Datentyp|Description|  
|---------------|-----------------|  
|DT_BOOL|Ein boolescher Wert.|  
|DT_BYTES|Ein binärer Datenwert. Die Länge ist variabel, und die maximale Länge beträgt 8000 Bytes.|  
|DT_CY|Ein Währungswert. Dieser Datentyp ist eine 8-Bit-Ganzzahl mit Vorzeichen mit 4 Dezimalstellen und einer maximalen Genauigkeit von 19 Stellen.|  
|DT_DATE|Eine Datumsstruktur bestehend aus dem Jahr, dem Monat, dem Tag, der Stunde, der Minute, der Sekunde und Sekundenbruchteilen.  Die Sekundenbruchteile besitzen einen festen Bereich von 7 Dezimalstellen.<br /><br /> Der DT_DATE-Datentyp wird mithilfe einer 8-Byte-Gleitkommazahl implementiert. Tage werden durch ganze Zahlen dargestellt, die jeweils auf die nächsthöhere Zahl erhöht werden, beginnend am 30. Dezember 1899 um 0 Uhr Mitternacht. Stundenwerte werden als absolute Werte der Stellen hinter dem Dezimalpunkt dargestellt. Ein Gleitkommawert kann jedoch nicht alle reellen Werte darstellen. Daher ist der im DT_DATE-Datentyp darstellbare Datumsbereich begrenzt.<br /><br /> Im Vergleich dazu enthält der DT_DBTIMESTAMP-Datentyp intern eine Struktur mit einzelnen Feldern zur Darstellung von Jahren, Monaten, Tagen, Stunden, Minuten, Sekunden und Millisekunden. Dieser Datentyp kann größere Datumsbereiche darstellen.|  
|DT_DBDATE|Eine Datumsstruktur bestehend aus dem Jahr, dem Monat und dem Tag.|  
|DT_DBTIME|Eine Zeitstruktur bestehend aus der Stunde, der Minute und der Sekunde.|  
|DT_DBTIME2|Eine Zeitstruktur bestehend aus der Stunde, der Minute, der Sekunde und Sekundenbruchteilen. Die Sekundenbruchteile besitzen maximal 7 Dezimalstellen.|  
|DT_DBTIMESTAMP|Eine Timestampstruktur bestehend aus dem Jahr, dem Monat, dem Tag, der Stunde, der Minute, der Sekunde und Sekundenbruchteilen. Die Sekundenbruchteile besitzen maximal 3 Dezimalstellen.|  
|DT_DBTIMESTAMP2|Eine Timestampstruktur bestehend aus dem Jahr, dem Monat, dem Tag, der Stunde, der Minute, der Sekunde und Sekundenbruchteilen. Die Sekundenbruchteile besitzen maximal 7 Dezimalstellen.|  
|DT_DBTIMESTAMPOFFSET|Eine Timestampstruktur bestehend aus dem Jahr, dem Monat, dem Tag, der Stunde, der Minute, der Sekunde und Sekundenbruchteilen. Die Sekundenbruchteile besitzen maximal 7 Dezimalstellen.<br /><br /> Im Gegensatz zu den Datentypen DT_DBTIMESTAMP und DT_DBTIMESTAMP2 verfügt der DT_DBTIMESTAMPOFFSET-Datentyp über einen Zeitzonenoffset. Dieser Offset gibt die Zahl der Stunden und Minuten an, um die die Zeit gegenüber der koordinierten Weltzeit (UTC) versetzt ist. Der Zeitzonenoffset wird vom System verwendet, um die Ortszeit zu bestimmen.<br /><br /> Der Zeitzonenoffset muss ein Vorzeichen (plus oder minus) enthalten, das angibt, ob der Offset zur UTC addiert oder von dieser subtrahiert wird. Die gültige Anzahl der Stunden im Offsetwert liegt zwischen -14 und +14. Das Vorzeichen für den Minutenoffset hängt von dem Vorzeichen für den Stundenoffset ab:<br /><br /> Wenn das Vorzeichen des Stundenoffsets negativ ist, muss der Minutenoffset negativ oder null sein.<br /><br /> Wenn das Vorzeichen des Stundenoffsets positiv ist, muss der Minutenoffset positiv oder null sein.<br /><br /> Wenn der Stundenoffset null ist, kann der Minutenoffset einen Wert im Bereich -0,59 bis +0,59 annehmen.|  
|DT_DECIMAL|Ein genauer numerischer Wert mit einer festen Genauigkeit und festen Dezimalstellen. Dieser Datentyp ist eine ganze Zahl ohne Vorzeichen und einer Länge von 12 Bytes, mit 0 bis 28 Dezimalstellen und einer maximalen Genauigkeit von 29.|  
|DT_FILETIME|Ein 64-Bit-Wert, der die Anzahl von 100-Nanosekunden-Intervallen seit dem 1. Januar 1601 darstellt. Die Sekundenbruchteile besitzen maximal 3 Dezimalstellen.|  
|DT_GUID|Ein global eindeutiger Bezeichner (GUID, Globally Unique Identifier).|  
|DT_I1|Eine ganze Zahl mit Vorzeichen und einer Länge von 1 Byte.|  
|DT_I2|Eine ganze Zahl mit Vorzeichen und einer Länge von 2 Bytes.|  
|DT_I4|Eine ganze Zahl mit Vorzeichen und einer Länge von 4 Bytes.|  
|DT_I8|Eine ganze Zahl mit Vorzeichen und einer Länge von 8 Bytes.|  
|DT_NUMERIC|Ein genauer numerischer Wert mit einer festen Genauigkeit und festen Dezimalstellen. Dieser Datentyp ist eine ganze Zahl ohne Vorzeichen und einer Länge von 16 Bytes, mit 0 bis 38 Dezimalstellen und einer maximalen Genauigkeit von 38.|  
|DT_R4|Ein Gleitkommawert mit einfacher Genauigkeit|  
|DT_R8|Ein Gleitkommawert mit doppelter Genauigkeit|  
|DT_STR|Eine NULL-terminierte [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS-Zeichenfolge mit einer maximalen Länge von 8000 Zeichen. (Wenn ein Spaltenwert zusätzliche Nullabschlusszeichen enthält, wird die Zeichenfolge bei der ersten Null abgeschnitten.)|  
|DT_UI1|Eine ganze Zahl ohne Vorzeichen und einer Länge von 1 Byte.|  
|DT_UI2|Eine ganze Zahl ohne Vorzeichen und einer Länge von 2 Bytes.|  
|DT_UI4|Eine ganze Zahl ohne Vorzeichen und einer Länge von 4 Bytes.|  
|DT_UI8|Eine ganze Zahl ohne Vorzeichen und einer Länge von 8 Bytes.|  
|DT_WSTR|Eine NULL-terminierte Unicode-Zeichenfolge mit einer maximalen Länge von 4000 Zeichen. (Wenn ein Spaltenwert zusätzliche Nullabschlusszeichen enthält, wird die Zeichenfolge bei der ersten Null abgeschnitten.)|  
|DT_IMAGE|Ein Binärwert mit einer maximalen Länge von 2^31-1 (2.147.483.647) Bytes. .|  
|DT_NTEXT|Eine Unicode-Zeichenfolge mit einer maximalen Länge von 2^30-1 (1.073.741.823) Zeichen.|  
|DT_TEXT|Eine [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS-Zeichenfolge mit einer maximalen Länge von 2^31-1 (2.147.483.647) Zeichen.|  
  
## Datentypkonvertierung  
 Falls die Daten in einer Spalte nicht die vom Quelldatentyp zugeordnete normale Breite benötigen, können Sie den Datentyp der Spalte ändern. Wenn jede Datenzeile so schmal wie möglich ist, wird die Leistung beim Übertragen von Daten optimiert, denn umso schmaler eine Zeile ist, desto schneller werden die Daten von der Quelle an das Ziel verschoben.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält einen vollständigen Satz numerischer Datentypen, sodass der Datentyp in hohem Maß auf die Größe der Daten abgestimmt werden kann. Wenn z. B. die Werte in einer Spalte mit einem DT_UI8-Datentyp immer ganze Zahlen zwischen 0 und 3000 sind, können Sie den Datentyp in DT_UI2 ändern. Wenn entsprechend eine Spalte mit dem DT_CY-Datentyp die Datenanforderungen des Pakets erfüllen kann, indem stattdessen ein ganzzahliger Datentyp verwendet wird, können Sie den Datentyp in DT_I4 ändern.  
  
 Es gibt folgende Möglichkeiten, um den Datentyp einer Spalte zu ändern:  
  
-   Verwenden Sie einen Ausdruck, um Datentypen implizit zu konvertieren. Weitere Informationen finden Sie unter [Integration Services-Datentypen in Ausdrücken](../../integration-services/expressions/integration-services-data-types-in-expressions.md), [Integration Services-Datentypen in Ausdrücken](../../integration-services/expressions/integration-services-data-types-in-expressions.md) und [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
-   Verwenden Sie den Typumwandlungsoperator, um Datentypen zu konvertieren. Weitere Informationen finden Sie unter [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
-   Verwenden Sie die Transformation für Datenkonvertierung, um den Datentyp einer Spalte von einem Datentyp in einen anderen umzuwandeln. Weitere Informationen finden Sie unter [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
-   Verwenden Sie die Transformation für abgeleitete Spalten, um eine Kopie einer Spalte zu erstellen, die einen anderen Datentyp als die ursprüngliche Spalte aufweist. Weitere Informationen finden Sie unter [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
### Konvertieren zwischen Zeichenfolgen und Datums-/Uhrzeitdatentypen  
 In der folgenden Tabelle sind die Ergebnisse der Umwandlung oder der Konvertierung zwischen Datums- und Uhrzeitdatentypen und Zeichenfolgen aufgelistet:  
  
-   Mit dem Umwandlungsoperator oder der Transformation für Datenkonvertierung wird der Datums- oder Uhrzeitdatentyp in die entsprechende Zeichenfolge umgewandelt. Zum Beispiel wird der DT_DBTIME-Datentyp in eine Zeichenfolge im Format "hh:mm:ss" konvertiert.  
  
-   Zur Umwandlung einer Zeichenfolge in einen Datums- oder Zeitdatentyp muss die Zeichenfolge in einem Zeichenfolgenformat vorliegen, das zum entsprechenden Datums- oder Zeitdatentyp passt. Um z. B. Datumszeichenfolgen erfolgreich in den DT_DBDATE-Datentyp umzuwandeln, müssen diese Zeichenfolgen im Format "yyyy-mm-dd" vorliegen.  
  
    |Datentyp|Zeichenfolgenformat|  
    |---------------|-------------------|  
    |DT_DBDATE|yyyy-mm-dd|  
    |DT_FILETIME|yyyy-mm-dd hh:mm:ss:fff|  
    |DT_DBTIME|hh:mm:ss|  
    |DT_DBTIME2|hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMP|yyyy-mm-dd hh:mm:ss[.fff]|  
    |DT_DBTIMESTAMP2|yyyy-mm-dd hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMPOFFSET|yyyy-mm-dd hh:mm:ss[.fffffff] [{+&#124;-} hh:mm]|  
  
 Beim Datumsformat für DT_FILETIME und DT_DBTIMESTAMP stellt fff einen Wert zwischen 0 und 999 dar, der die Sekundenbruchteile angibt.  
  
 Beim Datumsformat für DT_DBTIMESTAMP2, DT_DBTIME2 und DT_DBTIMESTAMPOFFSET, stellt fffffff einen Wert zwischen 0 und 9999999 dar, der die Sekundenbruchteile angibt.  
  
 Das Datumsformat für DT_DBTIMESTAMPOFFSET schließt auch ein Zeitzonenelement ein. Es gibt ein Leerzeichen zwischen dem Zeitelement und dem Zeitzonenelement.  
  
### Konvertieren von Datums- und Zeitdatentypen  
 Sie können den Datentyp einer Spalte mit Datums-/Zeitdaten ändern, um den Datums- oder Zeitteil der Daten zu extrahieren. Die folgende Tabelle führt die Ergebnisse der Umwandlung von einem Datums- und Zeitdatentyp in einen anderen Datums- und Zeitdatentyp auf.  
  
#### Konvertieren von DT_FILETIME  
  
|Konvertieren von DT_FILETIME in|Ergebnis|  
|-----------------------------|------------|  
|DT_FILETIME|Keine Änderung.|  
|DT_DATE|Konvertiert den Datentyp.|  
|DT_DBDATE|Entfernt den Zeitwert.|  
|DT_DBTIME|Entfernt den Datumswert.<br /><br /> Entfernt den Wert für die Bruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIME enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Entfernt den durch den DT_FILETIME-Datentyp dargestellten Datumswert.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIME2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Konvertiert den Datentyp.|  
|DT_DBTIMESTAMP2|Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMP2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Legt das Zeitzonenfeld im DT_DBTIMESTAMPOFFSET-Datentyp auf Null fest.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMPOFFSET enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### Konvertieren von DT_DATE  
  
|Konvertieren von DT_DATE in|Ergebnis|  
|-------------------------|------------|  
|DT_FILETIME|Konvertiert den Datentyp.|  
|DT_DATE|Keine Änderung.|  
|DT_DBDATE|Entfernt den durch den DT_DATA-Datentyp dargestellten Zeitwert.|  
|DT_DBTIME|Entfernt den durch den DT_DATA-Datentyp dargestellten Datumswert.|  
|DT_DBTIME2|Entfernt den durch den DT_DATA-Datentyp dargestellten Datumswert.|  
|DT_DBTIMESTAMP|Konvertiert den Datentyp.|  
|DT_DBTIMESTAMP2|Konvertiert den Datentyp.|  
|DT_DBTIMESTAMPOFFSET|Legt das Zeitzonenfeld im DT_DBTIMESTAMPOFFSET-Datentyp auf Null fest.|  
  
#### Konvertieren von DT_DBDATE  
  
|Konvertieren von DT_DBDATE in|Ergebnis|  
|---------------------------|------------|  
|DT_FILETIME|Legt die Zeitfelder im DT_FILETIME-Datentyp auf Null fest.|  
|DT_DATE|Legt die Zeitfelder im DT_DATE-Datentyp auf Null fest.|  
|DT_DBDATE|Keine Änderung.|  
|DT_DBTIME|Legt die Zeitfelder im DT_DBTIME-Datentyp auf Null fest.|  
|DT_DBTIME2|Legt die Zeitfelder im DT_DBTIME2-Datentyp auf Null fest.|  
|DT_DBTIMESTAMP|Legt die Zeitfelder im DT_DBTIMESTAMP-Datentyp auf Null fest.|  
|DT_DBTIMESTAMP2|Legt die Zeitfelder im DT_DBTIMESTAMP-Datentyp auf Null fest.|  
|DT_DBTIMESTAMPOFFSET|Legt die Zeitfelder und das Zeitzonenfeld im DT_DBTIMESTAMPOFFSET-Datentyp auf Null fest.|  
  
#### Konvertieren von DT_DBTIME  
  
|Konvertieren von DT_DBTIME in|Ergebnis|  
|---------------------------|------------|  
|DT_FILETIME|Legt das Datumsfeld im DT_FILETIME-Datentyp auf das aktuelle Datum fest.|  
|DT_DATE|Legt das Datumsfeld im DT_DATE-Datentyp auf das aktuelle Datum fest.|  
|DT_DBDATE|Legt das Datumsfeld im DT_DBDATE-Datentyp auf das aktuelle Datum fest.|  
|DT_DBTIME|Keine Änderung.|  
|DT_DBTIME2|Konvertiert den Datentyp.|  
|DT_DBTIMESTAMP|Legt das Datumsfeld im DT_DBTIMESTAMP-Datentyp auf das aktuelle Datum fest.|  
|DT_DBTIMESTAMP2|Legt das Datumsfeld im DT_DBTIMESTAMP2-Datentyp auf das aktuelle Datum fest.|  
|DT_DBTIMESTAMPOFFSET|Legt das Datumsfeld und das Zeitzonenfeld im DT_DBTIMESTAMPOFFSET-Datentyp auf das aktuelle Datum beziehungsweise auf Null fest.|  
  
#### Konvertieren von DT_DBTIME2  
  
|Konvertieren von DT_DBTIME2 in|Ergebnis|  
|----------------------------|------------|  
|DT_FILETIME|Legt das Datumsfeld im DT_FILETIME-Datentyp auf das aktuelle Datum fest.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_FILETIME enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DATE|Legt das Datumsfeld im DT_DATE-Datentyp auf das aktuelle Datum fest.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DATE enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Legt das Datumsfeld im DT_DBDATE-Datentyp auf das aktuelle Datum fest.|  
|DT_DBTIME|Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIME enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Zieldatentyp DT_DBTIME2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Legt das Datumsfeld im DT_DBTIMESTAMP-Datentyp auf das aktuelle Datum fest.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMP enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Legt das Datumsfeld im DT_DBTIMESTAMP2-Datentyp auf das aktuelle Datum fest.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMP2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Legt das Datumsfeld und das Zeitzonenfeld im DT_DBTIMESTAMPOFFSET-Datentyp auf das aktuelle Datum beziehungsweise auf Null fest.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMPOFFSET enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### Konvertieren von DT_DBTIMESTAMP  
  
|Konvertieren von DT_DBTIMESTAMP in|Ergebnis|  
|--------------------------------|------------|  
|DT_FILETIME|Konvertiert den Datentyp.|  
|DT_DATE|Überschreitet der durch den DT_DBTIMESTAMP-Datentyp dargestellte Wert den für den DT_DATE-Datentyp gültigen Bereich, wird der DB_E_DATAOVERFLOW-Fehler zurückgegeben. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Entfernt den durch den DT_DBTIMESTAMP-Datentyp dargestellten Zeitwert.|  
|DT_DBTIME|Entfernt den durch den DT_DBTIMESTAMP-Datentyp dargestellten Datumswert.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIME enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Entfernt den durch den DT_DBTIMESTAMP-Datentyp dargestellten Datumswert.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIME2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Keine Änderung.|  
|DT_DBTIMESTAMP2|Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMP2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Legt das Zeitzonenfeld im DT_DBTIMESTAMPOFFSET-Datentyp auf Null fest.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMPOFFSET enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### Konvertieren von DT_DBTIMESTAMP2  
  
|Konvertieren von DT_DBTIMESTAMP2 in|Ergebnis|  
|---------------------------------|------------|  
|DT_FILETIME|Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_FILETIME enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DATE|Überschreitet der durch den DT_DBTIMESTAMP2-Datentyp dargestellte Wert den für den DT_DATE-Datentyp gültigen Bereich, wird der DB_E_DATAOVERFLOW-Fehler zurückgegeben. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DATE enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Entfernt den durch den DT_DBTIMESTAMP2-Datentyp dargestellten Zeitwert.|  
|DT_DBTIME|Entfernt den durch den DT_DBTIMESTAMP2-Datentyp dargestellten Datumswert.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIME enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Entfernt den durch den DT_DBTIMESTAMP2-Datentyp dargestellten Datumswert.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIME2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Überschreitet der durch den DT_DBTIMESTAMP2-Datentyp dargestellte Wert den für den DT_DBTIMESTAMP-Datentyp gültigen Bereich, wird der DB_E_DATAOVERFLOW-Fehler zurückgegeben.<br /><br /> DT_DBTIMESTAMP2 wird dem SQL Server-Datentyp "datetime2" mit dem Bereich vom 1. Januar 1 n. Chr. bis zum 31. Dezember 9999 zugeordnet. DT_DBTIMESTAMP wird dem SQL Server-Datentyp datetime mit dem kleineren Bereich vom 1. Januar 1753 bis zum 31. Dezember 9999 zugeordnet.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMP enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert.<br /><br /> Weitere Informationen zu Fehlern finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Zieldatentyp DT_DBTIMESTAMP2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Legt das Zeitzonenfeld im DT_DBTIMESTAMPOFFSET-Datentyp auf Null fest.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMPOFFSET enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### Konvertieren von DT_DBTIMESTAMPOFFSET  
  
|Konvertieren von DT_DBTIMESTAMPOFFSET in|Ergebnis|  
|--------------------------------------|------------|  
|DT_FILETIME|Ändert den durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellten Zeitwert in die koordinierte Weltzeit (UTC).<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_FILETIME enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DATE|Ändert den durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellten Zeitwert in UTC.<br /><br /> Überschreitet der durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellte Wert den für den DT_DATE-Datentyp gültigen Bereich, wird der DB_E_DATAOVERFLOW-Fehler zurückgegeben.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DATE enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert.<br /><br /> Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Ändert den durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellten Zeitwert in UTC, was sich auf den Datumswert auswirken kann. Dann wird der Zeitwert entfernt.|  
|DT_DBTIME|Ändert den durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellten Zeitwert in UTC.<br /><br /> Entfernt den durch den DT_DBTIMESTAMPEOFFSET-Datentyp dargestellten Datumswert.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIME enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Ändert den durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellten Zeitwert in UTC.<br /><br /> Entfernt den durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellten Datumswert.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIME2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Ändert den durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellten Zeitwert in UTC.<br /><br /> Überschreitet der durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellte Wert den für den DT_DBTIMESTAMP-Datentyp gültigen Bereich, wird der DB_E_DATAOVERFLOW-Fehler zurückgegeben.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMP enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert.<br /><br /> Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Ändert den durch den DT_DBTIMESTAMPOFFSET-Datentyp dargestellten Zeitwert in UTC.<br /><br /> Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Datentyp DT_DBTIMESTAMP2 enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Entfernt den Wert für die Sekundenbruchteile, wenn die Anzahl der Dezimalstellen größer als die Anzahl ist, die der Zieldatentyp DT_DBTIMESTAMPOFFSET enthalten kann. Nach dem Entfernen des Werts für die Sekundenbruchteile wird ein Bericht über dieses Abschneiden der Daten generiert. Weitere Informationen finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md).|  
  
## Zuordnen von SQL Server Integration Services-Datentypen zu Datenbank-Datentypen  
 Die folgenden Tabelle gibt Hinweise für die Zuordnung von Datentypen bestimmter Datenbanken zu [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentypen. Diese Zuordnungen sind den Zuordnungsdateien entnommen, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten beim Importieren von Daten aus den betreffenden Quellen verwendet werden. Weitere Informationen zu diesen Zuordnungsdateien finden Sie unter [SQL Server-Import/Export-Assistent](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md).  
  
> [!IMPORTANT]  
>  Die Zuordnungen sind nicht als strenge Entsprechungen zu verstehen, sondern stellen lediglich Anhaltspunkte dar. In bestimmten Fällen muss möglicherweise ein anderer Dateityp als der in der Tabelle angegebene verwendet werden.  
  
> [!NOTE]  
>  Sie können die Größe entsprechender Datum-/Uhrzeit-Datentypen von Integration Services mithilfe der SQL Server-Datentypen schätzen.  
  
|Datentyp|SQL Server<br /><br /> (SQLOLEDB; SQLNCLI10)|SQL Server (SqlClient)|Jet|Oracle<br /><br /> (OracleClient)|DB2<br /><br /> (DB2OLEDB)|DB2<br /><br /> (IBMDADB2)|  
|---------------|--------------------------------------------|------------------------------|---------|---------------------------------|--------------------------|--------------------------|  
|DT_BOOL|bit|bit|Bit||||  
|DT_BYTES|binary, varbinary, timestamp|binary, varbinary, timestamp|BigBinary, VarBinary|RAW|||  
|DT_CY|smallmoney, money|smallmoney, money|Währung||||  
|DT_DATE|||||||  
|DT_DBDATE|[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)|[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)||Datum|Datum|Datum|  
|DT_DBTIME||||timestamp|Uhrzeit|Uhrzeit|  
|DT_DBTIME2|[time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)(p)|[time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md) (p)|||||  
|DT_DBTIMESTAMP|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md), [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md), [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|DateTime|TIMESTAMP, DATE, INTERVAL|TIME, TIMESTAMP, DATE|TIME, TIMESTAMP, DATE|  
|DT_DBTIMESTAMP2|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)||timestamp|timestamp|timestamp|  
|DT_DBTIMESTAMPOFFSET|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)(p)|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md) (p)||timestampoffset|timestamp,<br /><br /> varchar|timestamp,<br /><br /> varchar|  
|DT_DECIMAL|||||||  
|DT_FILETIME|||||||  
|DT_GUID|uniqueidentifier|uniqueidentifier|GUID||||  
|DT_I1|||||||  
|DT_I2|smallint|smallint|Short||smallint|SMALLINT|  
|DT_I4|int|int|Long||INTEGER|INTEGER|  
|DT_I8|bigint|bigint|||BIGINT|bigint|  
|DT_NUMERIC|decimal, numeric|decimal, numeric|Decimal|NUMBER, INT|DECIMAL, NUMERIC|decimal, numeric|  
|DT_R4|real|real|Single||real|real|  
|DT_R8|float|float|Double|FLOAT, REAL|FLOAT, DOUBLE|FLOAT, DOUBLE|  
|DT_STR|char, varchar||varchar||char, varchar|CHAR, VARCHAR|  
|DT_UI1|tinyint|tinyint|Byte||||  
|DT_UI2|||||||  
|DT_UI4|||||||  
|DT_UI8|||||||  
|DT_WSTR|nchar, nvarchar, sql_variant, xml|char, varchar, nchar, nvarchar, sql_variant, xml|LongText|CHAR, ROWID, VARCHAR2, NVARCHAR2, NCHAR|GRAPHIC, VARGRAPHIC|GRAPHIC, VARGRAPHIC|  
|DT_IMAGE|image|image|LongBinary|LONG RAW, BLOB, LOBLOCATOR, BFILE, VARGRAPHIC, LONG VARGRAPHIC, benutzerdefiniert|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA, BLOB|  
|DT_NTEXT|ntext|text, ntext||LONG, CLOB, NCLOB, NVARCHAR, TEXT|LONG VARCHAR, NCHAR, NVARCHAR, TEXT|LONG VARCHAR, DBCLOB, NCHAR, NVARCHAR, TEXT|  
|DT_TEXT|text||||LONG VARCHAR FOR BIT DATA|LONG VARCHAR FOR BIT DATA, CLOB|  
  
 Weitere Informationen zur Zuordnung von Datentypen im Datenfluss finden Sie unter [Verwenden von Datentypen im Datenfluss](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## Verwandte Inhalte  
 Blogeintrag, [Performance Comparison between Data Type Conversion Techniques in SSIS 2008](http://go.microsoft.com/fwlink/?LinkId=220823), auf blogs.msdn.com.  
  
## Siehe auch  
 [Daten in Datenflüssen](../../integration-services/data-flow/data-in-data-flows.md)  
  
  