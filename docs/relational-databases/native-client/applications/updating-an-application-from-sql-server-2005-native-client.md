---
title: Aktualisieren einer Anwendung von SQL Server 2005 Native Client | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
caps.latest.revision: "42"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a0765a262b2775f81b35969a638ff6f3583357e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Aktualisieren einer Anwendung von SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In diesem Thema werden die aktuellen Änderungen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client seit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] erläutert.  
  
 Wenn Sie ein Upgrade von Microsoft Data Access Components (MDAC) auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client durchführen, werden Ihnen möglicherweise auch einige Unterschiede im Verhalten auffallen. Weitere Informationen finden Sie unter [Aktualisieren einer Anwendung von MDAC auf SQL Server Native Client](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 9.0 Lieferumfang [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 10.0 Lieferumfang [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 war im Lieferumfang von [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] enthalten. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 war im Lieferumfang von [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] und [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] enthalten.  
  
|Geändertes Verhalten in SQL Server Native Client seit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB füllt nur Zahlen bis zur definierten Anzahl von Dezimalstellen auf.|Für Konvertierungen, in denen Daten an den Server gesendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (ab [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) nachfolgende Nullen in Daten nur bis zu maximal füllt **"DateTime"** Werte. In SQL Server Native Client 9.0 wurden Zahlen bis zu 9 Stellen aufgefüllt.|  
|Überprüfen Sie DBTYPE_DBTIMESTAMP für ICommandWithParameter::SetParameterInfo.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client (ab [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) implementiert die OLE DB-Anforderung *bScale* in ICommandWithParameter::SetParameterInfo, um die Genauigkeit der Sekundenbruchteile für DBTYPE_DBTIMESTAMP festgelegt werden.|  
|Die **Sp_columns** gibt die gespeicherte Prozedur **"NO"** anstelle von **"NO"** für die Spalte IS_NULLABLE.|Ab [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]), **Sp_columns** gibt die gespeicherte Prozedur **"NO"** anstelle von **"NO"** für eine IS_NULLABLE-Spalte .|  
|SQLSetDescRec und SQLBindParameter SQLBindCol führen jetzt überprüft.|Vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 festlegen SQL_DESC_DATA_PTR nicht dazu führen, dass eine konsistenzprüfung für einen Deskriptortyp in SQLSetDescRec, SQLBindParameter oder SQLBindCol.|  
|SQLCopyDesc ist jetzt Deskriptor überprüft.|Vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 SQLCopyDesc keine konsistenzprüfung, wenn das SQL_DESC_DATA_PTR-Feld auf einen bestimmten Datensatz festgelegt wurde.|  
|SQLGetDescRec überprüft die deskriptorkonsistenz nicht mehr.|Vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ausgeführt SQLGetDescRec eine konsistenzprüfung an, wenn das SQL_DESC_DATA_PTR-Feld festgelegt wurde. Die ODBC-Spezifikation erfordert dies nicht, und in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) sowie in höheren Versionen wird diese Konsistenzprüfung nicht mehr ausgeführt.|  
|Es wird ein anderer Fehler zurückgegeben, wenn das Datum außerhalb des zulässigen Bereichs liegt.|Für die **"DateTime"** Typ, eine andere Fehlernummer von zurückgegeben werden, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (ab [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) für ein außerhalb des Bereichs Datum zurück als in früheren Versionen zurückgegeben wurde.<br /><br /> Insbesondere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 gab 22007 für alle außerhalb des gültigen Bereichs Jahreswerte in zeichenfolgenkonvertierungen **"DateTime"**, und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ab Version 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 22008 When zurückgibt das Datum liegt innerhalb des Bereichs von unterstützten **datetime2** aber außerhalb des Bereichs von unterstützten **"DateTime"** oder **Smalldatetime**.|  
|**"DateTime"** Wert Sekundenbruchteile abgeschnitten und nicht round If Rundung den Tag ändern wird.|Vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, das Clientverhalten für **"DateTime"** Werte, die an den Server gesendet wird, diese gerundet wird, auf das nächste 1/300stel einer Sekunde. Ab [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 werden in diesem Szenario die Sekundenbruchteile abgeschnitten, wenn die Rundung eine Änderung des Tags bewirkt.|  
|Mögliche Trunction der Sekunden für **"DateTime"** Wert.|Eine Anwendung, die mit [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (oder höher) erstellt wurde, die eine Verbindung mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005-Server herstellt, schneidet Sekunden und Sekundenbruchteile für den Zeitteil der Daten ab, die an den Server gesendet werden, wenn Sie an eine datetime-Spalte mit dem Typbezeichner DBTYPE_DBTIMESTAMP (OLE DB) oder SQL_TIMESTAMP (ODBC) und der Skala 0 binden.<br /><br /> Beispiel:<br /><br /> Eingabedaten: 1994-08-21 21:21:36.000<br /><br /> Einfügedaten: 1994-08-21 21:21:00.000|  
|Die OLE DB-Datenkonvertierung von DBTYPE_DBTIME in DBTYPE_DATE kann keine Änderung des Tages mehr bewirken.|In früheren Versionen als [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 bewirkte der OLE DB-Konvertierungscode eine Änderung des Tages, wenn der Uhrzeitanteil eines DBTYPE_DATE-Werts innerhalb einer halben Sekunde vor Mitternacht lag. Ab [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 wird der Tag nicht geändert (Sekundenbruchteile werden abgeschnitten und nicht gerundet).|  
|IBCPSession::BCColFmt Konvertierung ändert.|Ab [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, bei der Verwendung des IBCPSession::BCOColFmt konvertieren SQLDATETIME oder SQLDATETIME in einen Zeichenfolgen-Datentyp, ein Dezimalstellenwert exportiert. Wenn beispielsweise der Typ SQLDATETIME in den Typ SQLNVARCHARMAX konvertiert wird, gaben Vorgängerversionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client Folgendes zurück:<br /><br /> 1989-02-01 00:00:00. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 und höhere Versionen geben 1989-02-01 00:00:00.0000000 zurück.|  
|Die Größe der gesendeten Daten muss der in SQL_LEN_DATA_AT_EXEC angegebenen Länge entsprechen.|Wenn SQL_LEN_DATA_AT_EXEC verwendet wird, muss die Größe der Daten der Länge entsprechen, die Sie in SQL_LEN_DATA_AT_EXEC angegeben haben. Sie können SQL_DATA_AT_EXEC verwenden, aber der Einsatz von SQL_LEN_DATA_AT_EXEC bietet potenzielle Leistungsvorteile.|  
|Benutzerdefinierte Anwendungen, die die BCP API verwenden, können jetzt Warnungen anzeigen.|Die BCP API erzeugt jetzt für alle Typen Warnmeldungen, wenn die Datenlänge die angegebene Länge eines Felds überschreitet. Früher wurde diese Warnung nur für Zeichentypen ausgegeben, aber nicht für alle Typen.|  
|Einfügen einer leeren Zeichenfolge in eine **Sql_variant** gebunden, wie ein Datum/Uhrzeit-Typ einen Fehler generiert.|In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, Einfügen von eine leere Zeichenfolge in eine **Sql_variant** gebunden, wie ein Datum/Uhrzeit-Typ kein Fehler generiert. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 (und höher) generiert in dieser Situation ordnungsgemäß einen Fehler.|  
|Strengere SQL_C_TYPE _TIMESTAMP- und DBTYPE_DBTIMESTAMP-Parameterüberprüfung|Vor [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client **"DateTime"** Werte wurden entsprechend den Dezimalstellen gerundet **"DateTime"** und **Smalldatetime** Spalten nach [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (und höher) wendet jetzt die strengeren Validierungsregeln an, die in der ODBC-Hauptspezifikation für Sekundenbruchteile definiert sind. Wenn ein Parameterwert nicht mit den angegebenen oder vom Client implizierten Dezimalstellen in den SQL-Typ konvertiert werden kann, ohne dass nachfolgende Stellen abgeschnitten werden, dann wird ein Fehler zurückgegeben.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] kann andere Ergebnisse zurückgeben, wenn ein Trigger ausgeführt wird.|Eingeführten Änderungen [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] kann dazu führen, dass eine Anwendung andere Ergebnisse zurückgegeben, die von einer Anweisung, die aufgrund ein Triggers ausgeführt werden, wenn **NOCOUNT OFF** gültig war. In dieser Situation kann die Anwendung einen Fehler generieren. Um diesen Fehler zu beheben, legen **NOCOUNT ON** im Trigger, oder rufen Sie SQLMoreResults, um zum nächsten Ergebnis zu wechseln.|  
  
## <a name="see-also"></a>Siehe auch  
 [Programmierung für SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
