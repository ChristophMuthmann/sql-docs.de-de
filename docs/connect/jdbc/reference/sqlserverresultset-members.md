---
title: SQLServerResultSet-Elemente | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2a438d5d-2d6a-46a0-a2ae-f35fbae4a472
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 767bc38218c81b81db91e5949bf2431ca4e98e95
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverresultset-members"></a>SQLServerResultSet-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Die folgenden Tabellen enthalten die Elemente, die von verfügbar gemacht werden die [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
 Keine.  
  
## <a name="fields"></a>Felder  
  
|Name|Description|  
|----------|-----------------|  
|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|Zur Angabe einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Lese-/Schreibzugriff Typs der vollständigen Parallelität ohne Zeilensperre.|  
|[CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|Zur Angabe einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Lese-/Schreibzugriff Typs der vollständigen Parallelität ohne Zeilensperre.|  
|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|Zur Angabe einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Lese-/Schreibzugriff Typs der vollständigen Parallelität mit Sperren auf Zeilenebene.|  
|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|Zur Angabe einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] schnelle Vorwärtscursor, schreibgeschützte Cursor-Typ.|  
|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|Zur Angabe einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] dynamischer Cursortyp.|  
|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|Zur Angabe einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Keyset-Cursor-Datentyps.|  
|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|Zur Angabe einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] statischen Cursortyps.|  
|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|Zur Angabe einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] schnelle Vorwärtscursor, schreibgeschützte Cursor-Typ.|  
  
## <a name="inherited-fields"></a>Geerbte Felder  
  
|Klasse geerbt von:|Description|  
|---------------------------|-----------------|  
|java.sql.ResultSet|CLOSE_CURSORS_AT_COMMIT, CONCUR_READ_ONLY, CONCUR_UPDATABLE, FETCH_FORWARD, FETCH_REVERSE, FETCH_UNKNOWN, HOLD_CURSORS_OVER_COMMIT, TYPE_FORWARD_ONLY, TYPE_SCROLL_INSENSITIVE, TYPE_SCROLL_SENSITIVE|  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[absolute](../../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)|Verschiebt den Cursor in die angegebene Zeile in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[afterLast](../../../connect/jdbc/reference/afterlast-method-sqlserverresultset.md)|Verschiebt den Cursor hinter der letzten Zeile dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[beforeFirst](../../../connect/jdbc/reference/beforefirst-method-sqlserverresultset.md)|Verschiebt den Cursor vor der ersten Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[cancelRowUpdates](../../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)|Bricht die Aktualisierungen an der aktuellen Zeile in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverresultset.md)|Löscht alle für dieses gemeldeten Warnungen [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[Schließen Sie](../../../connect/jdbc/reference/close-method-sqlserverresultset.md)|Dies frei [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objektspezifischen Datenbank- und JDBC-Ressourcen sofort gewartet, sondern dies so erfolgen kann, wenn sie automatisch geschlossen wird.|  
|[deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)|Löscht die aktuelle Zeile aus dieser[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt und der zugrunde liegenden Datenbank.|  
|[Abschließen](../../../connect/jdbc/reference/finalize-method-sqlserverresultset.md)|Schließt dies explizit [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[findColumn](../../../connect/jdbc/reference/findcolumn-method-sqlserverresultset.md)|Ruft den Index des ersten übereinstimmenden Spalte für den angegebenen Spaltennamen in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[erste](../../../connect/jdbc/reference/first-method-sqlserverresultset.md)|Verschiebt den Cursor in die erste Zeile dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als ein Arrayobjekt.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als Datenstrom von ASCII-Zeichen.|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)|Ruft den Wert des angegebenen Spaltenindexes in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als "java.Math.BigDecimal".|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekts als Binärdatenstrom nicht interpretierter Bytes.|  
|[getBlob](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als Blob-Objekt in der Programmiersprache Java ab.|  
|[getBoolean](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **booleschen** in der Programmiersprache Java ab.|  
|[getByte](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **Byte** in der Programmiersprache Java ab.|  
|[getBytes](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **Byte** Array in der Programmiersprache Java ab.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekts als java.io.Reader-Objekt.|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als Clob-Objekt in der Programmiersprache Java ab.|  
|[getConcurrency](../../../connect/jdbc/reference/getconcurrency-method-sqlserverresultset.md)|Ruft den Parallelitätsmodus dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getCursorName](../../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)|Ruft den Namen der SQL-Cursor, die mit dem von diesem [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekts als java.sql.Date-Objekt in der Programmiersprache Java ab.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte als eine["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md) Objekt.|  
|[getDouble](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **doppelte** in der Programmiersprache Java ab.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverresultset.md)|Ruft die abrufrichtung für dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)|Ruft die Abrufgröße für dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getFloat](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **"float"** in der Programmiersprache Java ab.|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverresultset.md)|Ruft die Haltbarkeit dieses ab [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **Int** in der Programmiersprache Java ab.|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **lange** in der Programmiersprache Java ab.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)|Ruft die Anzahl, Typen und Eigenschaften dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Spalten des Objekts.|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile ab der [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als Readerobjekt.|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile ab der [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)-Objekt als eine **NClob** Objekt in der Programmiersprache Java ab.|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile ab der [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als eine Zeichenfolge in der Java-Programmiersprache.|  
|[getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als Objekt in der Programmiersprache Java ab.|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als Ref-Objekt in der Programmiersprache Java ab.|  
|[getRow](../../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)|Ruft die aktuelle Zeilennummer ab.|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **kurze** in der Programmiersprache Java ab.|  
|[getStatement](../../../connect/jdbc/reference/getstatement-method-sqlserverresultset.md)|Ruft die [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, das Dies erzeugt [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **Zeichenfolge** in der Programmiersprache Java ab.|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile ab der [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **SQLXML** Objekt.|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekts als java.sql.Time-Objekt in der Programmiersprache Java ab.|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekts als java.sql.Timestamp-Objekt in der Programmiersprache Java ab.|  
|["GetType"](../../../connect/jdbc/reference/gettype-method-sqlserverresultset.md)|Ruft den Cursortyp dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getUnicodeStream](../../../connect/jdbc/reference/getunicodestream-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als Stream von Unicode-Zeichen.|  
|["getURL"](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)|Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als URL-Objekt.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverresultset.md)|Ruft die erste Warnung gemeldet von Aufrufen für dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)|Fügt den Inhalt der Einfügezeile in dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt und in der Datenbank.|  
|[isAfterLast](../../../connect/jdbc/reference/isafterlast-method-sqlserverresultset.md)|Ruft ab, ob der Cursor befindet sich nach der letzten Zeile in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[isBeforeFirst](../../../connect/jdbc/reference/isbeforefirst-method-sqlserverresultset.md)|Ruft ab, ob der Cursor befindet sich vor der ersten Zeile in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverresultset.md)|Gibt an, ob dies [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt geschlossen wurde.|  
|[isFirst](../../../connect/jdbc/reference/isfirst-method-sqlserverresultset.md)|Ruft ab, ob der Cursor, auf die erste Zeile dieser befindet [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[isLast](../../../connect/jdbc/reference/islast-method-sqlserverresultset.md)|Ruft ab, ob der Cursor in der letzten Zeile dieser ist [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[letzte](../../../connect/jdbc/reference/last-method-sqlserverresultset.md)|Verschiebt den Cursor auf die letzte Zeile in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[moveToCurrentRow](../../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)|Verschiebt den Cursor an die gespeicherte Cursorposition in der Regel die aktuelle Zeile.|  
|[moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)|Versetzt den Cursor in die Einfügezeile.|  
|[Weiter](../../../connect/jdbc/reference/next-method-sqlserverresultset.md)|Versetzt den Cursor von seiner aktuellen Position aus um eine Zeile nach unten.|  
|[Vorherige](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md)|Verschiebt den Cursor zur vorherigen Zeile in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[refreshRow](../../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md)|Aktualisiert die aktuelle Zeile mit dem aktuellen Wert aus der Datenbank.|  
|[relative](../../../connect/jdbc/reference/relative-method-sqlserverresultset.md)|Verschiebt den Cursor der angegebenen Anzahl von Zeilen, relativ zur aktuellen Zeile, in eine positive Zahl oder einer negativen Richtung.|  
|[rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)|Ruft ab, ob eine Zeile gelöscht wurde.|  
|[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)|Ruft ab, ob in der aktuellen Zeile eine Einfügung vorgenommen wurde.|  
|[rowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md)|Ruft ab, ob die aktuelle Zeile aktualisiert wurde.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md)|Gibt Aufschluss über die Richtung, in dem die Zeilen in dieser [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt verarbeitet werden.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)|Gibt dem JDBC-Treiber für die Anzahl der Zeilen, die aus der Datenbank abgerufen werden sollen, wenn weitere Zeilen, für diesen benötigt werden [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[updateArray](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem Arrayobjekt.|  
|[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem ASCII-Datenstromwert.|  
|[updateBigDecimal](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem BigDecimal-Objekt.|  
|[updateBinaryStream](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem Binärdatenstromwert.|  
|[updateBlob](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem java.sql.Blob-Wert.|  
|[updateBoolean](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **booleschen** Wert.|  
|[updateByte](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **Byte** Wert.|  
|[updateBytes](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem Array von **Byte** Werte.|  
|[updateCharacterStream](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem Zeichendatenstromwert.|  
|[updateClob](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem java.sql.Clob-Wert.|  
|[updateDate](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem Datumswert.|  
|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)|Updates einer ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md) Spalte.|  
|[updateDouble](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **doppelte** Wert.|  
|[updateFloat](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **"float"** Wert.|  
|[updateInt](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **Int** Wert.|  
|[updateLong](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **lange** Wert.|  
|[updateNCharacterStream](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem Zeichendatenstromwert.|  
|[updateNClob](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit dem angegebenen Objektwert.|  
|[updateNString](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **Zeichenfolge** Wert.|  
|[updateNull](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem NULL-Wert.|  
|[updateObject](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **Objekt** Wert.|  
|[updateRef](../../../connect/jdbc/reference/updateref-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem java.sql.Ref-Wert.|  
|[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)|Aktualisiert die zugrunde liegenden Datenbank mit dem neuen Inhalt der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[updateShort](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **kurze** Wert.|  
|[updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **Zeichenfolge** Wert.|  
|[updateSQLXML](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem **SQLXML** Wert.|  
|[updateTime](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem Uhrzeitwert.|  
|[updateTimestamp](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)|Aktualisiert die angegebene Spalte mit einem Zeitstempelwert.|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlserverresultset.md)|Überprüft, ob beim letzte gelesenen Wert ein null-Wert wurde.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
