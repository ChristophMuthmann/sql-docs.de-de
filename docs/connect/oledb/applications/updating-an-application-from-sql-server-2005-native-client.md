---
title: Aktualisieren einer Anwendung von SQL Server 2005 Native Client | Microsoft Docs
description: Aktualisieren einer Anwendung von SQL Server 2005 Native Client
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ddeedf937de12337e8882bfa132461dd2c5f7a8
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Aktualisieren einer Anwendung von SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Artikel werden die Änderungen, die in OLE DB-Treiber für SQL Server seit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

 Beim upgrade von Microsoft Data Access Components (MDAC), OLE DB-Treiber für SQL Server u. u. auch einige Unterschiede im Verhalten angezeigt. Weitere Informationen finden Sie unter [Aktualisieren von einer Anwendung auf OLE DB-Treiber für SQL Server von MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 Lieferumfang [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 Lieferumfang [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 war im Lieferumfang von [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] enthalten. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 war im Lieferumfang von [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] und [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] enthalten.  

|Geändert von Verhalten in OLE DB-Treiber für SQL Server im Vergleich zur [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB füllt nur Zahlen bis zur definierten Anzahl von Dezimalstellen auf.|Für Konvertierungen, in dem konvertierte Daten an den Server gesendet werden, füllt der OLE DB-Treiber für SQL Server nachfolgende Nullen in Daten nur bis zu maximal **"DateTime"** Werte. In SQL Server Native Client 9.0 wurden Zahlen bis zu 9 Stellen aufgefüllt.|  
|Überprüfen Sie DBTYPE_DBTIMESTAMP für ICommandWithParameter::SetParameterInfo.|OLE DB-Treiber für SQL Server implementiert die OLE DB-Anforderung *bScale* in ICommandWithParameter::SetParameterInfo, um die Genauigkeit der Sekundenbruchteile für DBTYPE_DBTIMESTAMP festgelegt werden.|  
|Die **Sp_columns** gibt die gespeicherte Prozedur **"NO"** anstelle von **"NO"** für die Spalte IS_NULLABLE.|In OLE DB-Treiber für SQL Server **Sp_columns** gibt die gespeicherte Prozedur **"NO"** anstelle von **"NO"** für eine IS_NULLABLE-Spalte.|  
|SQLSetDescRec und SQLBindParameter SQLBindCol führen jetzt überprüft.|Vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 festlegen SQL_DESC_DATA_PTR nicht dazu führen, dass eine konsistenzprüfung für einen Deskriptortyp in SQLSetDescRec, SQLBindParameter oder SQLBindCol.|  
|SQLCopyDesc ist jetzt Deskriptor überprüft.|Vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 SQLCopyDesc keine konsistenzprüfung, wenn das SQL_DESC_DATA_PTR-Feld auf einen bestimmten Datensatz festgelegt wurde.|  
|SQLGetDescRec überprüft die deskriptorkonsistenz nicht mehr.|Vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ausgeführt SQLGetDescRec eine konsistenzprüfung an, wenn das SQL_DESC_DATA_PTR-Feld festgelegt wurde. Die ODBC-Spezifikation erfordert dies nicht, und in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) sowie in höheren Versionen wird diese Konsistenzprüfung nicht mehr ausgeführt.|  
|Es wird ein anderer Fehler zurückgegeben, wenn das Datum außerhalb des zulässigen Bereichs liegt.|Für die **"DateTime"** Typ, eine andere Fehlernummer von zurückgegeben werden, OLE DB-Treiber für SQL Server für einen Termin außerhalb des Bereichs als in früheren Versionen zurückgegeben wurde.<br /><br /> Insbesondere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 gab 22007 für alle außerhalb des gültigen Bereichs Jahreswerte in zeichenfolgenkonvertierungen **"DateTime"**, und der OLE DB-Treiber für SQL Server die Fehlernummer 22008 zurück, wenn das Datum innerhalb des Bereichs von unterstützt**datetime2** aber außerhalb des Bereichs von unterstützten **"DateTime"** oder **Smalldatetime**.|  
|**"DateTime"** Wert Sekundenbruchteile abgeschnitten und nicht round If Rundung den Tag ändern wird.|Vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, das Clientverhalten für **"DateTime"** Werte, die an den Server gesendet wird, diese gerundet wird, auf das nächste 1/300stel einer Sekunde. In OLE DB-Treiber für SQL Server bewirkt, dass dieses Szenario ein Abschneiden von Sekundenbruchteilen Wenn Rundung den Tag ändert.|  
|Mögliche Trunction der Sekunden für **"DateTime"** Wert.|Eine Anwendung, die mit OLE DB-Treiber für SQL Server die Herstellung der erstellten eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005-Server herstellt, schneidet Sekunden und Sekundenbruchteile für einen Zeitteil der Daten an den Server gesendet werden, wenn Sie an eine Datetime-Spalte mit einem Typbezeichner DBTYPE_DBTIMESTAMP (Binden OLE DB) oder SQL_TIMESTAMP (ODBC) und einer Skala von 0.<br /><br /> Beispiel:<br /><br /> Eingabedaten: 1994-08-21 21:21:36.000<br /><br /> Einfügedaten: 1994-08-21 21:21:00.000|  
|Die OLE DB-Datenkonvertierung von DBTYPE_DBTIME in DBTYPE_DATE kann keine Änderung des Tages mehr bewirken.|In früheren Versionen als [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 bewirkte der OLE DB-Konvertierungscode eine Änderung des Tages, wenn der Uhrzeitanteil eines DBTYPE_DATE-Werts innerhalb einer halben Sekunde vor Mitternacht lag. In OLE DB-Treiber für SQL Server, dem Tag wird nicht geändert (Sekundenbruchteile werden abgeschnitten und nicht gerundet).|  
|IBCPSession::BCColFmt Konvertierung ändert.|Bei Verwendung von IBCPSession::BCOColFmt SQLDATETIME oder SQLDATETIME in einen Zeichenfolgen-Datentyp zu konvertieren, wird im OLE DB-Treiber für SQL Server ein Dezimalstellenwert exportiert. Z. B. wenn der Typ SQLDATETIME in den Typ SQLNVARCHARMAX Versionen vor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 zurückgegeben<br /> 1989-02-01 00:00:00.<br />OLE DB-Treiber für SQL Server zurückgegeben. <br />1989-02-01 00:00:00.0000000.|  
|Benutzerdefinierte Anwendungen, die die BCP API verwenden, können jetzt Warnungen anzeigen.|Die BCP API erzeugt jetzt für alle Typen Warnmeldungen, wenn die Datenlänge die angegebene Länge eines Felds überschreitet. Früher wurde diese Warnung nur für Zeichentypen ausgegeben, aber nicht für alle Typen.|  
|Einfügen einer leeren Zeichenfolge in eine **Sql_variant** gebunden, wie ein Datum/Uhrzeit-Typ einen Fehler generiert.|In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, Einfügen von eine leere Zeichenfolge in eine **Sql_variant** gebunden, wie ein Datum/Uhrzeit-Typ kein Fehler generiert. OLE DB-Treiber für SQL Server generiert in dieser Situation ordnungsgemäß einen Fehler auf.|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] kann andere Ergebnisse zurückgeben, wenn ein Trigger ausgeführt wird.|Eingeführten Änderungen [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] kann dazu führen, dass eine Anwendung andere Ergebnisse zurückgegeben, die von einer Anweisung, die aufgrund ein Triggers ausgeführt werden, wenn **NOCOUNT OFF** gültig war. In dieser Situation kann die Anwendung einen Fehler generieren. Um diesen Fehler zu beheben, legen **NOCOUNT ON** im Trigger, oder rufen Sie SQLMoreResults, um zum nächsten Ergebnis zu wechseln.|  

## <a name="see-also"></a>Siehe auch   
 [OLE DB-Treiber für SQL Server-Programmierung](../../oledb/oledb-driver-for-sql-server-programming.md)
