---
title: OLE DB-Treiber für SQL Server-Funktionen | Microsoft Docs
description: OLE DB-Treiber für SQL Server-Funktionen
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 197a3dec6f56c615d8731472e44c224b002feba1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-driver-for-sql-server-features"></a>OLE DB-Treiber für SQL Server-Funktionen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Zusätzlich zu den Funktionen von Windows (früher Microsoft) Data Access Components (WDAC) verfügbar gemacht werden, implementiert die OLE DB-Treiber für SQL Server auch viele weitere Funktionen verfügbar machen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Funktionalität.  
  
## <a name="in-this-section"></a>In diesem Abschnitt    
 [Verwenden der Datenbankspiegelung](../../oledb/features/using-database-mirroring.md)  
 Erläutert, wie die Verwendung von gespiegelten Datenbanken, OLE DB-Treiber für SQL Server unterstützt die Möglichkeit, eine Kopie oder Spiegelserver, der beibehalten wird eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank auf einem Standbyserver.  
  
 [Ausführen asynchroner Vorgänge](../../oledb/features/performing-asynchronous-operations.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server für asynchrone Vorgänge unterstützt, das ist die Fähigkeit, Rückgaben unverzüglich, ohne den aufrufenden Thread blockieren.  
  
 [Verwenden von Multiple Active Result Sets &#40;MARS&#41;](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server mehrere aktive Resultsets (MARS) unterstützt. MARS ermöglichen es Ihnen, mehrere Resultsets mithilfe einer einzigen Datenbankverbindung auszuführen und zu empfangen.  
  
 [Verwenden von XML-Datentypen](../../oledb/features/using-xml-data-types.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server den XML-Datentyp unterstützt, also eine XML-basierte Datentyp, der als ein Spaltentyp, Variablentyp, Parametertyp oder Funktionsrückgabetyp verwendet werden kann.  
  
 [Verwenden von benutzerdefinierten Typen](../../oledb/features/using-user-defined-types.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server für benutzerdefinierte Typen (UDT), unterstützt die SQL-Typsystem erweitert, sodass Sie zum Speichern von Objekten und benutzerdefinierte Datenstrukturen in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank.  
  
 [Verwenden von Datentypen mit umfangreichen Werten](../../oledb/features/using-large-value-types.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server von Datentypen mit großen Werten, unterstützt die großen Objektdatentypen (LOB) sind.  
  
 [Programmgesteuertes Ändern von Kennwörtern](../../oledb/features/changing-passwords-programmatically.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server so, dass Kennwörter jetzt auf dem Client ohne Eingreifen eines Administrators geändert werden können, die Handhabung abgelaufener Kennwörter unterstützt.  
  
 [Arbeiten mit Momentaufnahmeisolation](../../oledb/features/working-with-snapshot-isolation.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server-Erweiterung aus der zeilenversionsverwaltung unterstützt, die die datenbankleistung verbessert, indem Leser-schreiberblockierungsszenarien vermieden.  
  
 [Arbeiten mit Abfragebenachrichtigungen](../../oledb/features/working-with-query-notifications.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server die Benachrichtigung von Consumern bei rowsetänderungen unterstützt.  
  
 [Durchführen von Massenkopiervorgängen](../../oledb/features/performing-bulk-copy-operations.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server Vorgänge für das Massenkopieren unterstützt, die die Übertragung großer Datenmengen in bzw. aus der ermöglichen eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle oder Sicht.  
  
 [Verwenden von Verschlüsselung ohne Überprüfung](../../oledb/features/using-encryption-without-validation.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server zum Verschlüsseln von Daten an den Server gesendet werden, ohne dass das Zertifikat überprüft.  
  
 [Tabellenwertparameter &#40;OLE DB-Treiber für SQLServer&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 Erläutert, OLE DB-Treiber für SQL Server-Unterstützung für den Tabellenwertparameter.  
  
 [Große benutzerdefinierte CLR-Typen](../../oledb/features/large-clr-user-defined-types.md)  
 Erläutert die Unterstützung für große CLR-benutzerdefinierte Typen (Common Language Runtime).  
  
 [FILESTREAM-Unterstützung](../../oledb/features/filestream-support.md)  
 Erläutert, OLE DB-Treiber für SQL Server-Unterstützung für die verbesserte FILESTREAM-Funktion.  
  
 [Dienstprinzipalnamen &#40;SPN&#41; -Unterstützung in Clientverbindungen](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 Erläutert, auf welche Weise die Unterstützung für Dienstprinzipalnamen (Service Principal Names, SPN) erweitert wurde, damit die gegenseitige Authentifizierung über alle Protokolle hinweg möglich ist.  
  
 [Unterstützung von Spalten mit geringer Dichte im OLE DB-Treiber für SQL Server](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 Erläutert, OLE DB-Treiber für SQL Server-Unterstützung für Spalten mit geringer Dichte.  
  
 [Verbesserungen bei Datum und Zeit](../../oledb/features/date-and-time-improvements.md)  
 Erläutert die Unterstützung für OLE DB-Treiber für SQL Server für die Datentypen für Datum und Uhrzeit.  
  
 [Metadatenermittlung](../../oledb/features/metadata-discovery.md)  
 Erläutert Verbesserungen der Metadatenermittlung in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [UTF-16-Unterstützung im OLE DB-Treiber für SQL Server (OLE DB)](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 Erläutert eine mit [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] eingeführte Verhaltensänderung. Wenn Sie beim Binden eines Spaltenergebnisses oder Ausgabeparameters einen Puffer fester Länge übergeben und die **Wchar** Zeichen, die in den Puffer geschrieben wird, vor das abschließende Zeichen ein hoher Ersatzzeichencodepunkt eines Ersatzzeichenpaars und wenn das nächste **Wchar** Zeichen ist ein niedriger Ersatzzeichencodepunkt, OLE DB-Treiber für SQL Server wird nicht die hoher Ersatzzeichencodepunkt hinzugefügt, in den Puffer.  
  
 [OLE DB-Treiber für SQL Server-Unterstützung für Hochverfügbarkeit, Notfallwiederherstellung](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 Erläutert, wie die Anwendung konfiguriert werden kann, um die hohe Verfügbarkeit und notfallwiederherstellung nutzen Funktionen, in hinzugefügt [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Zugreifen auf Diagnoseinformationen im Protokoll der erweiterten Ereignisse](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Erläutert Erweiterungen zu OLE DB-Treiber für SQL Server und -datenablaufverfolgung, die Sie Zugriff auf Diagnoseinformationen im Ringpuffer und XEvents-Protokoll bietet.  
  
 [OLE DB-Treiber für SQL Server-Unterstützung für LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 Wird die OLE DB-Treiber für SQL Server-Unterstützung für die "LocalDB"-Funktion erläutert.  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQLServer](../../oledb/oledb-driver-for-sql-server.md)      
 [OLE DB-Themen zur Vorgehensweise](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [Installation des OLE DB-Treibers für SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
