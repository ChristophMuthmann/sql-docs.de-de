---
title: "Durchführen von Massenkopiervorgängen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- bulk copy [SQL Server Native Client]
- data access [SQL Server Native Client], bulk copy operations
- SQL Server Native Client, bulk copy operations
- SQLNCLI, bulk copy operations
ms.assetid: 50d8456b-e6a1-4b25-bc7e-56946ed654a7
caps.latest.revision: "28"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea17b70786b4b059417c8cf0f8b514fc6a6208e4
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="performing-bulk-copy-operations"></a>Durchführen von Massenkopiervorgängen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Die Massenkopierfunktion von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt die Übertragung großer Datenmengen in bzw. aus einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Tabelle oder Sicht. Daten können auch mithilfe einer SELECT-Anweisung aus einer Tabelle oder Sicht übertragen werden. Die Daten können zwischen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und einer Betriebssystemdatendatei verschoben werden, z. B. eine ASCII-Datei. Datendateien können verschiedene Formate aufweisen. Das Format wird in einer Formatdatei definiert. Optional können die Daten in Programmvariablen geladen und mithilfe von Massenkopierfunktionen und -methoden in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] übertragen werden.  
  
 Eine beispielanwendung, die diese Funktion veranschaulicht wird, finden Sie unter [Bulk Daten mithilfe von IRowsetFastLoad &#40; OLE DB &#41;](../../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md).  
  
 Eine Anwendung verwendet Massenkopiervorgänge in der Regel in einer der folgenden Arten:  
  
-   Massenkopieren aus einer Tabelle, Sicht oder dem Resultset einer Transact-SQL-Anweisung in eine Datendatei, in der die Daten im selben Format gespeichert werden wie in der Tabelle bzw. Sicht.  
  
     Diese Datei wird als Datendatei im einheitlichen Modus bezeichnet.  
  
-   Massenkopieren aus einer Tabelle, Sicht oder dem Resultset einer Transact-SQL-Anweisung in eine Datendatei, in der die Daten in einem anderen Format gespeichert werden als in der Tabelle bzw. Sicht.  
  
     In diesem Fall wird eine separate Formatdatei erstellt, in der die Charakteristika (Datentyp, Position, Länge, Abschlusszeichen, usw.) der einzelnen, in der Datendatei zu speichernden Spalten definiert werden. Wenn alle Spalten in Zeichenformat konvertiert werden, wird die resultierende Datei als Datendatei im Zeichenmodus bezeichnet.  
  
-   Massenkopieren aus einer Datendatei in eine Tabelle oder Sicht.  
  
     Gegebenenfalls wird eine Formatdatei verwendet, um das Layout der Datendatei zu bestimmen.  
  
-   Laden der Daten in Programmvariablen und anschließender Import der Daten in eine Tabelle oder Sicht unter Verwendung der Massenkopierfunktionen für das Massenkopieren von jeweils einer Zeile.  
  
 Datendateien, die von Massenkopierfunktionen verwendet werden, brauchen nicht von einem anderen Massenkopierprogramm erstellt worden sein. Beliebige andere Systeme können entsprechend den Massenkopierdefinitionen Datendateien und Formatdateien generieren. Diese Dateien können dann mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Massenkopierprogramm verwendet werden, um Daten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zu importieren. Beispielsweise könnten Sie Daten aus einer Kalkulationstabelle in eine durch Tabstopps getrennte Datei exportieren, eine die durch Tabstopps getrennte Datei in einer Formatdatei beschreiben und schließlich mithilfe eines Massenkopierprogramms die Daten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] importieren. Datendateien, die mit einer Massenkopierfunktion generiert wurden, können auch in andere Anwendungen importiert werden. Beispielsweise könnten Sie Massenkopierfunktionen verwenden, um Daten aus einer Tabelle oder Sicht in eine durch Tabstopps getrennte Datei zu exportieren, die Sie dann in eine Kalkulationstabelle laden.  
  
 Programmierern von Anwendungen, die Massenkopierfunktionen verwenden, wird empfohlen, folgende allgemeine Regeln zu beachten, um die Leistung des Massenkopierens zu gewähren. Weitere Informationen zur Unterstützung für Massenkopiervorgänge in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], finden Sie unter [Massenimport und-Export von Daten &#40; SQLServer &#41; ](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Ein CLR-benutzerdefinierter Typ (User Defined Type, UDT) muss als Binärdaten gebunden werden. Auch wenn eine Formatdatei SQLCHAR als Datentyp für eine Ziel-UDT-Spalte angibt, verarbeitet das BCP-Hilfsprogramm die Daten als Binärdaten.  
  
 SET FMTONLY OFF kann nicht mit Massenkopiervorgängen verwendet werden. SET FMTONLY OFF führt möglicherweise bei Massenkopiervorgängen zu unerwarteten Ergebnissen oder Fehlern.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB-Anbieter  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter implementiert zwei Methoden zum Ausführen von Massenkopiervorgängen mit einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank. Die erste Methode umfasst die Verwendung der [IRowsetFastLoad](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) -Schnittstelle für speicherbasierte Massenkopiervorgänge; und das zweite umfasst die Verwendung der [IBCPSession](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md) -Schnittstelle für dateibasierte Massenkopiervorgänge.  
  
### <a name="using-memory-based-bulk-copy-operations"></a>Verwenden von speicherbasierten Massenkopiervorgängen  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter implementiert die **IRowsetFastLoad** Schnittstelle, um Unterstützung für verfügbar machen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] speicherbasierte Massenkopiervorgänge. Die **IRowsetFastLoad** -Schnittstelle implementiert die [IRowsetFastLoad:: Commit](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md) und [IRowsetFastLoad:: InsertRow](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md) Methoden.  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>Aktivieren einer Sitzung für IRowsetFastLoad  
 Der Consumer benachrichtigt den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieter, dass ein Massenkopiervorgang erforderlich ist, indem er für die SSPROP_ENABLEFASTLOAD-Eigenschaft, die für den systemeigenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client-OLE DB-Anbieter spezifisch ist, VARIANT_TRUE festlegt. Wenn die Datenquelle für die Eigenschaft festgelegt wurde, erstellt der Consumer eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbietersitzung. Die neue Sitzung lässt den Consumerzugriff auf die **IRowsetFastLoad** Schnittstelle.  
  
> [!NOTE]  
>  Wenn die **IDataInitialize** Schnittstelle für die Initialisierung der Datenquelle verwendet wird, und es ist notwendig, die SSPROP_IRowsetFastLoad-Eigenschaft festgelegt wird, der *RgPropertySets* Parameter von der  **IOpenRowset:: OPENROWSET** Methode ist, andernfalls der Aufruf der **OpenRowset** Methode E_NOINTERFACE zurück.  
  
 Das Aktivieren einer Sitzung zum Massenkopieren schränkt die Unterstützung des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieters für Schnittstellen in dieser Sitzung ein. Eine Sitzung mit aktivierter Massenkopierfunktion bietet lediglich die folgenden Schnittstellen:  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 Um die Erstellung massenkopierter Rowsets zu deaktivieren und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbietersitzung auf die Standardverarbeitungsweise zurückzusetzen, legen Sie für SSPROP_ENABLEFASTLOAD den Parameter VARIANT_FALSE fest.  
  
#### <a name="irowsetfastload-rowsets"></a>IRowsetFastLoad Rowsets  
 Die massenkopierten Rowsets im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieter weisen nur Schreibzugriff auf, machen jedoch Schnittstellen verfügbar, die dem Consumer ermöglichen, die Struktur einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Tabelle zu bestimmen. Die folgenden Schnittstellen sind in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieterrowsets verfügbar, in denen die Massenkopierfunktion aktiviert ist:  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 Die anbieterspezifischen Eigenschaften SSPROP_FASTLOADOPTIONS, SSPROP_FASTLOADKEEPNULLS und SSPROP_FASTLOADKEEPIDENTITY steuern die Verhalten des Massenkopierrowsets eines [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieters. Die Eigenschaften werden angegeben, der *RgProperties* Mitglied eine * RgPropertySets ***IOpenRowset**Parameterelements.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|Spalte: No<br /><br /> R/w: Lesen/Schreiben<br /><br /> Typ: VT_BOOL<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Verwaltet vom Consumer angegebene Identitätswerte.<br /><br /> VARIANT_FALSE: Werte für eine Identitätsspalte in der Tabelle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] werden von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] generiert. Jeder Wert gebunden wird, für die Spalte von ignoriert wird die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter.<br /><br /> VARIANT_TRUE: Der Consumer bindet einen Accessor, der einen Wert für eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Identitätsspalte bereitstellt. Die Identity-Eigenschaft ist nicht verfügbar für Spalten, die NULL ist, akzeptieren, damit der Consumer einen eindeutigen Wert für jedes bietet **Identity** aufrufen.|  
|SSPROP_FASTLOADKEEPNULLS|Spalte: No<br /><br /> R/w: Lesen/Schreiben<br /><br /> Typ: VT_BOOL<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Behält NULL-Werte für Spalten mit einer DEFAULT-Einschränkung bei. Betrifft nur [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Spalten, die NULL-Werte akzeptieren und eine DEFAULT-Einschränkung aufweisen.<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fügt den Standardwert für die Spalte ein, wenn der Consumer des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieters eine Zeile einfügt, die einen NULL-Wert für die Spalte enthält.<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fügt einen NULL-Wert in die Spalte ein, wenn der Consumer des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieters eine Zeile einfügt, die einen NULL-Wert für die Spalte enthält.|  
|SSPROP_FASTLOADOPTIONS|Spalte: No<br /><br /> R/w: Lesen/Schreiben<br /><br /> Typ: VT_BSTR<br /><br /> Standardwert: keiner<br /><br /> Beschreibung: Diese Eigenschaft ist identisch mit der **-h** "*Hinweis*[,...  *n* ] "-Option von der **Bcp** Hilfsprogramm. Die folgende(n) Zeichenfolge(n) kann/können beim Massenkopieren von Daten in eine Tabelle optional verwendet werden.<br /><br /> **ORDER**(*column*[**ASC** &#124; **DESC**][,...*n*]): Sort order of data in the data file. Die Leistung des Massenkopierens wird verbessert, wenn die zu ladende Datendatei entsprechend dem gruppierten Index der Tabelle sortiert ist.<br /><br /> **ROWS_PER_BATCH** = *bb*: Anzahl der Datenzeilen pro Batch (als *bb*). Der Server optimiert das Massenladen entsprechend dem Wert von *bb*. Standardmäßig **ROWS_PER_BATCH** ist unbekannt.<br /><br /> **KILOBYTES_PER_BATCH** = *cc*: Anzahl der Kilobytes (KB) an Daten pro Batch (als cc). Standardmäßig **KILOBYTES_PER_BATCH** ist unbekannt.<br /><br /> **TABLOCK**: eine Sperre auf Tabellenebene für die Dauer des Massenkopiervorgangs aktiviert ist. Diese Option verbessert die Leistung beträchtlich, da weniger Sperrkonflikte für die Tabelle auftreten, wenn diese nur während des Massenkopiervorgangs gesperrt wird. Eine Tabelle kann werden von mehreren Clients gleichzeitig geladen, wenn die Tabelle keine Indizes aufweist und **TABLOCK** angegeben ist. Standardmäßig wird das Sperrverhalten durch die Tabellenoption bestimmt **Tabellensperre auf Massenladen**.<br /><br /> **Check_constraints**: alle Einschränkungen für *Table_name* werden während des Massenkopiervorgangs überprüft. Standardmäßig werden Einschränkungen ignoriert.<br /><br /> **FIRE_TRIGGER**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendet die zeilenversionsverwaltung für Trigger und speichert die Zeilenversionen im Versionsspeicher in **Tempdb**. Deshalb sind Massenprotokollierungsoptimierungen verfügbar, auch wenn Trigger aktiviert sind. Vor dem Massenimport eines Batches mit einer großen Anzahl von Zeilen mit aktivierten Triggern, müssen Sie möglicherweise die Größe von **Tempdb**.|  
  
### <a name="using-file-based-bulk-copy-operations"></a>Verwenden von dateibasierten Massenkopiervorgängen  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter implementiert die **IBCPSession** Schnittstelle, um Unterstützung für verfügbar machen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dateibasierte Massenkopiervorgänge. Die **IBCPSession** -Schnittstelle implementiert die [ibcpsession:: BCPColFmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md), [ibcpsession:: BCPColumns](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md), [ibcpsession:: Bcpcontrol](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md), [IBCPSession::BCPDone](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md), [Ibcpsession](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md), [Ibcpsession](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md), [ibcpsession:: Bcpreadfmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md), und [Bcpwritefmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)Methoden.  
  
## <a name="sql-server-native-client-odbc-driver"></a>ODBC-Treiber für SQL Server Native Client  
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber unterstützt Massenkopiervorgänge in derselben Weise wie in Vorgängerversionen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] des ODBC-Treibers. Informationen über Massenkopiervorgänge mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber finden Sie unter [Durchführen von Massenkopiervorgängen &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Funktionen](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Datenquelleneigenschaften &#40; OLE DB &#41;](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [Massenimport und-Export von Daten &#40; SQLServer &#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)   
 [IBCPSession &#40; OLE DB &#41;](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [Optimieren der Leistung des Massenimportierens](http://msdn.microsoft.com/library/ms190421\(SQL.105\).aspx)  
  
  
