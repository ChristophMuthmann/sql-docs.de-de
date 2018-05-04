---
title: SQLServerCallableStatement Mitgliedern | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: Assembly
ms.assetid: 5ebdc186-e50f-4d14-bbf4-95af5051e4a4
caps.latest.revision: 50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc3d57de1793645a64784ad0eea0dacdfbab9e7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlservercallablestatement-members"></a>SQLServerCallableStatement-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Die folgenden Tabellen enthalten die Elemente, die von verfügbar gemacht werden die [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
 Keine.  
  
## <a name="fields"></a>Felder  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="inherited-fields"></a>Geerbte Felder  
 Keine.  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Fügt einen Satz von Parametern für den Batch von Befehlen für dieses Objekt CallableStatement an.|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Bricht die SQL-Anweisung, die derzeit von diesem Objekt CallableStatement ausgeführt wird.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Leert die aktuelle Liste der SQL-Befehlen für dieses CallableStatement-Objekt.|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Löscht umgehend die aktuellen Parameterwerte.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Löscht alle Warnungen, die für dieses Objekt CallableStatement gemeldet werden.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Gibt die Datenbank und der JDBC-Ressourcen dieses Objekts CallableStatement sofort gewartet, sondern deren automatische Freigabe werden frei.|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Führt die SQL-Anweisung in diesem CallableStatement-Objekt, um einen beliebigen SQL-Anweisung handeln kann.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Übermittelt einen Befehlsbatch zur Ausführung an die Datenbank. Werden alle Befehle erfolgreich ausgeführt, wird ein Array mit Updatezählungen zurückgegeben.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Führt die SQL-Abfrage in diesem CallableStatement-Objekt und gibt die [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, das von der Abfrage generiert wird.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Führt die SQL-Anweisung in diesem CallableStatement-Objekt, eine SQL INSERT, UPDATE, MERGE oder DELETE-Anweisung werden muss; oder eine SQL-Anweisung, die nichts, z. B. eine DDL-Anweisung zurückgibt.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) -Objekt, das dieses Objekt CallableStatement erstellt wurde.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|Ruft den Wert der angegebenen Spalte als eine ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md) Objekt.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die Richtung zum Abrufen von Zeilen aus Datenbanktabellen ist die standardmäßig für Resultsets, die von diesem Objekt CallableStatement generiert.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die Anzahl von Resultsetzeilen, die die standardmäßige Abrufgröße für Resultsetobjekte set-Objekte, die aus diesem Objekt CallableStatement generiert.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft sämtliche automatisch generierte Schlüssel, die als Ergebnis der Ausführung dieses CallableStatement-Objekts erstellt werden.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die maximale Anzahl von Bytes, die für Zeichen- und Binärspaltenwerte in zurückgegeben werden, kann eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) von diesem Objekt CallableStatement erstellte Objekt.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die maximale Anzahl der Zeilen ab, die eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) von diesem Objekt CallableStatement erstellte Objekt enthalten kann.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Ruft eine [SQLServerResultSetMetaData-Klasse](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) Objekt, das Informationen zu den Spalten der enthält die [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, das zurückgegeben werden, wenn dieses Objekt CallableStatement ausgeführt wird.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Wechselt zum nächsten Ergebnis dieses CallableStatement-Objekt.|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Ruft die Anzahl, Typen und Eigenschaften der Parameter für dieses Objekt CallableStatement.|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als Arrayobjekt ab.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als Datenstrom von **ASCII** Zeichen.|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als "java.math.BigDecimal" ab.|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als Binärdatenstrom mit unterbrechungsfreien Bytes ab.|  
|[GetBlob](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen JDBC-Blob-Parameters als Blob-Objekt in der Programmiersprache Java ab.|  
|[GetBoolean](../../../connect/jdbc/reference/getboolean-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als eine **booleschen** Wert.|  
|[GetByte](../../../connect/jdbc/reference/getbyte-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als eine **Byte** Wert.|  
|[GetBytes](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als Bytearray ab.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als java.io.Reader-Objekt ab.|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen JDBC-Blob-Parameters als Clob-Objekt in der Programmiersprache Java ab.|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als java.sql.Date-Objekt in der Programmiersprache Java ab.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|Ruft den Wert der angegebenen Spalte als eine["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md) Objekt.|  
|[GetDouble](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als eine **doppelte** in der Programmiersprache Java ab.|  
|[GetFloat](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als eine **"float"** in der Programmiersprache Java ab.|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als ein **Int** in der Programmiersprache Java ab.|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als eine **lange** in der Programmiersprache Java ab.|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als Readerobjekt ab.|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen JDBC **NCLOB** Parameter als ein **NClob** Objekt in der Programmiersprache Java ab.|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)|Ruft den Wert der festgelegten **NCHAR**, **NVARCHAR** oder **LONGNVARCHAR** Parameter als eine Zeichenfolge in der Java-Programmiersprache.|  
|[GetObject](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als Objekt in der Programmiersprache Java ab.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die Anzahl der Sekunden ab dem [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wartet auf dieses Objekt CallableStatement ausgeführt.|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als Ref-Objekt in der Programmiersprache Java ab.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft den antwortpuffermodus für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft das aktuelle Ergebnis als eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft das Resultset Parallelität für [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die von diesem Objekt CallableStatement generiert werden.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft das Ergebnis für resultsethaltbarkeit [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die von diesem Objekt CallableStatement generiert werden.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft den Resultsettyp für [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die von diesem Objekt CallableStatement generiert werden.|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als eine **kurze** in der Programmiersprache Java ab.|  
|[GetString](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als eine **Zeichenfolge** in der Programmiersprache Java ab.|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als java.sql.SQLXML-Objekt ab.|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als java.sql.Time-Objekt in der Programmiersprache Java ab.|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als java.sql.Timestamp-Objekt in der Programmiersprache Java ab.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft das aktuelle Ergebnis als Updatezählung ab.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)|Ruft den Wert des angegebenen Parameters als URL-Objekt in der Programmiersprache Java ab.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die erste Warnung, die von Aufrufen für dieses Objekt CallableStatement gemeldet wurde.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Gibt an, ob dieses Statement-Objekt geschlossen wurde.|  
|[von isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Gibt einen Wert zurück, durch den angegeben wird, ob dem vom Benutzer bereitgestellten Anwendungspool eine Anweisung hinzugefügt werden kann.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)|Gibt an, ob es sich bei diesem Anweisungsobjekt um einen Wrapper für die angegebene Schnittstelle handelt.|  
|[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)|Registriert den OUT-Parameter.|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Legt die angegebene Parameternummer auf das angegebene Array-Objekt fest.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen Eingabedatenstrom fest.|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlservercallablestatement.md)|Legt die angegebene Parameternummer auf das angegebene BigDecimal Objekt fest.|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen Eingabedatenstrom fest.|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Legt den angegebenen Parameter mit dem angegebenen Blob-Objekt.|  
|[SetBoolean](../../../connect/jdbc/reference/setboolean-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen **booleschen** Wert.|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen **Byte** Wert.|  
|[SetBytes](../../../connect/jdbc/reference/setbytes-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf das angegebene Array von **Byte** Werte.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter mit dem angegebenen Reader-Objekt.|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Legt den angegebenen Parameter auf das angegebene Objekt fest.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt den SQL-Cursornamen auf die angegebene Zeichenfolge fest, die dann für nachfolgende Ausführungsmethoden verwendet wird.|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen Datumswert fest.|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)|Legt den Wert der angegebenen Spalte auf die ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md) Wert.|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen **doppelte** Wert.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt den Escapeverarbeitungsmodus fest.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Gibt für den JDBC-Treiber die Richtung an, in der die Resultsetzeilen verarbeitet werden sollen.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Gibt für den JDBC-Treiber an, wie viele Zeilen aus der Datenbank abgerufen werden sollen, wenn weitere Zeilen benötigt werden.|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen **"float"** Wert.|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen **Int** Wert.|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen **lange** Wert.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt das Limit für die maximale Anzahl von Bytes in einem [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Spalte Zeichen- oder Binärwerte auf die angegebene Anzahl von Bytes gespeichert werden.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Das Limit für die maximale Anzahl von Zeilen, die von jedem legt [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt enthalten kann, auf die angegebene Anzahl.|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter mit dem angegebenen Reader-Objekt.|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf das angegebene Objekt fest.|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf das angegebene String-Objekt.|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter unter Berücksichtigung des festzulegenden Parametertyps auf einen NULL-Wert fest.|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)|Legt den Wert des angegebenen Parameters unter Verwendung des angegebenen Objekts.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Sendet eine Anforderung, dass dem Pool eine Anweisung hinzugefügt bzw. nicht hinzugefügt werden soll. Standardmäßig wird ein SQLServerCallableStatement-Objekt dem Pool hinzugefügt werden, wenn erstellt.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt die Anzahl der Sekunden, die Treiber für ein Objekt CallableStatement auszuführende auf die angegebene Anzahl von Sekunden gewartet wird.|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Legt den angegebenen Parameter mit dem angegebenen Ref-Objekt.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt den antwortpuffermodus für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, Groß-/Kleinschreibung **vollständige Zeichenfolge** oder **adaptive**.|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen **kurze** Wert.|  
|[SetString](../../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen Java **Zeichenfolge** Wert.|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen **SQLXML** Objekt.|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen Uhrzeitwert fest.|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen Zeitstempelwert fest.|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|(Geerbt von [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) Legt die angegebene Parameternummer auf den angegebenen Eingabedatenstrom, mit der angegebenen Anzahl von Bytes fest.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlservercallablestatement.md)|Legt den angegebenen Parameter auf den angegebenen URL-Wert fest.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)|Gibt ein Objekt, das für den Zugriff auf die angegebene Schnittstelle implementiert die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-spezifischen Methoden.|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlservercallablestatement.md)|Ruft ab, ob der letzte gelesene OUT-Parameter den Wert "SQL NULL" besaß.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement|addBatch, clearBatch, clearParameters, close, execute, executeBatch, executeQuery, executeUpdate, getMetaData, getParameterMetaData, setArray, setAsciiStream, setBigDecimal, setBinaryStream, setBlob, setboolean, setByte, setBytes, setCharacterStream, setClob, setDate, setDouble, setFloat, setInt, setLong, setNull, setObject, setRef, setShort, setString, setTime, setTimestamp, setUnicodeStream, setURL|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|class java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait,|  
|java.sql.PreparedStatement|addBatch, clearParameters, execute, executeQuery, executeUpdate, getMetaData, getParameterMetaData, getSQLXML, setArray, setAsciiStream, setBigDecimal, setBinaryStream, setBlob, setboolean, setByte, setBytes, setCharacterStream, setClob, setDate, setDate, setDouble, setFloat, setInt, setLong, setNull, setObject, setRef, setShort, setString, setSQLXML, setTime, setTimestamp, setUnicodeStream, setURL|  
|java.sql.Statement|addBatch, cancel, clearBatch, clearWarnings, close, execute, executeBatch, executeQuery, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
