---
title: SQLServerPreparedStatement-Elemente | Microsoft Docs
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
ms.topic: article
ms.assetid: 2363902f-d4c6-4cd4-a5fc-86079eb9e418
caps.latest.revision: 38
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1926d376ac2653dcc7b4d6b0481bbe968d9469d6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverpreparedstatement-members"></a>SQLServerPreparedStatement-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Die folgenden Tabellen enthalten die Elemente, die von verfügbar gemacht werden die [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
 Keine.  
  
## <a name="fields"></a>Felder  
 Keine.  
  
## <a name="inherited-fields"></a>Geerbte Felder  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|Der Batch von Befehlen für dieses Objekt für die Anweisung hinzugefügt einen Satz von Parametern.|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Bricht die SQL-Anweisung, die derzeit von diesem Anweisungsobjekt ausgeführt wird.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|Leert die aktuelle Liste der SQL-Befehlen für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|Löscht umgehend die aktuellen Parameterwerte.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Löscht alle Warnungen, die auf diesem Anweisungsobjekt gemeldet werden.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|Gibt die Datenbank und der JDBC-Ressourcen von diesem Anweisungsobjekt sofort gewartet, sondern deren automatische Freigabe werden frei.|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|Führt die SQL-Anweisung in diesem Anweisungsobjekt, die einen beliebigen SQL-Anweisung handeln kann.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|Übermittelt einen Befehlsbatch zur Ausführung an die Datenbank. Werden alle Befehle erfolgreich ausgeführt, wird ein Array mit Updatezählungen zurückgegeben.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|Führt die SQL-Abfrage in diesem Anweisungsobjekt und gibt die [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, das von der Abfrage generiert wird.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|Führt die SQL-Anweisung in diesem Anweisungsobjekt, der eine SQL INSERT, UPDATE, MERGE oder DELETE-Anweisung sein muss; oder eine SQL-Anweisung, die nichts, z. B. eine DDL-Anweisung zurückgibt.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) -Objekt, das dieses Objekt Anweisung erstellt wurde.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die Richtung zum Abrufen von Zeilen aus Datenbanktabellen ist die standardmäßig für Resultsets, die von diesem Anweisungsobjekt generiert.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die Anzahl von Resultsetzeilen, die die standardmäßige Abrufgröße für Resultsetobjekte ist set-Objekte, die aus diesem Anweisungsobjekt generiert.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft sämtliche automatisch generierte Schlüssel, die aufgrund der Ausführung dieses Statement-Objekt erstellt werden.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die maximale Anzahl von Bytes, die für Zeichen- und Binärspaltenwerte in zurückgegeben werden, kann eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) von diesem Anweisungsobjekt erstellte Objekt.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die maximale Anzahl der Zeilen ab, die eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) von diesem Anweisungsobjekt erstellte Objekt enthalten kann.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|Ruft eine [SQLServerResultSetMetaData-Klasse](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) Objekt, das Informationen zu den Spalten der enthält die [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, das zurückgegeben werden, wenn es sich bei diesem Anweisungsobjekt ausgeführt wird.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Wechselt zum nächsten Ergebnis dieses Statement-Objekt.|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|Ruft ab, das Anzahl, Typen und Eigenschaften der Parameter für dieses Statement-Objekt.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft den antwortpuffermodus für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die Anzahl der Sekunden ab dem [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wartet auf die Ausführung dieser Anweisung-Objekts.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft das aktuelle Ergebnis als eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft das Resultset Parallelität für [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die von diesem Anweisungsobjekt generiert werden.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft das Ergebnis für resultsethaltbarkeit [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die von diesem Anweisungsobjekt generiert werden.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft den Resultsettyp für [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die von diesem Anweisungsobjekt generiert werden.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md),) Ruft das aktuelle Ergebnis als updatezählung ab.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ruft die erste Warnung, die von Aufrufen für dieses Statement-Objekt gemeldet wurde.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Gibt an, ob dieses Statement-Objekt geschlossen wurde.|  
|[von isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Gibt einen Wert zurück, durch den angegeben wird, ob dem vom Benutzer bereitgestellten Anwendungspool eine Anweisung hinzugefügt werden kann.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)|Gibt an, ob es sich bei diesem Anweisungsobjekt um einen Wrapper für die angegebene Schnittstelle handelt.|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|Legt die angegebene Parameternummer auf das angegebene Array-Objekt fest.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)|Legt die angegebene Parameternummer auf das angegebene InputStream-Objekt fest.|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlserverpreparedstatement.md)|Legt die angegebene Parameternummer auf das angegebene BigDecimal Objekt fest.|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen Eingabedatenstrom fest.|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter mit dem angegebenen Blob-Objekt.|  
|[SetBoolean](../../../connect/jdbc/reference/setboolean-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen **booleschen** Wert.|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen **Byte** Wert.|  
|[SetBytes](../../../connect/jdbc/reference/setbytes-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter in das angegebene Array von Bytes an.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter mit dem angegebenen Reader-Objekt.|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter mit dem angegebenen Clob-Objekt.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt die SQL-Cursornamen auf die angegebene Zeichenfolge, die durch nachfolgende verwendet werden ausführen Methoden.|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen Datumswert fest.|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|Legt den Wert der angegebenen Spalte auf die ["DateTimeOffset"-Klasse](../../../connect/jdbc/reference/datetimeoffset-class.md) Wert.|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen **doppelte** Wert.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt den Escapeverarbeitungsmodus fest.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Gibt für den JDBC-Treiber die Richtung an, in der die Resultsetzeilen verarbeitet werden sollen.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Gibt für den JDBC-Treiber an, wie viele Zeilen aus der Datenbank abgerufen werden sollen, wenn weitere Zeilen benötigt werden.|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen **"float"** Wert.|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen **Int** Wert.|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen **lange** Wert.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt das Limit für die maximale Anzahl von Bytes in einem [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Spalte Zeichen- oder Binärwerte auf die angegebene Anzahl von Bytes gespeichert werden.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Das Limit für die maximale Anzahl von Zeilen, die von jedem legt [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt enthalten kann, auf die angegebene Anzahl.|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter mit dem angegebenen Reader-Objekt.|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf das angegebene Objekt fest.|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter unter Berücksichtigung des festzulegenden Parametertyps auf einen NULL-Wert fest.|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)|Legt den angegebenen Parameter auf den angegebenen **Zeichenfolge** Objekt.|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)|Legt den Wert des angegebenen Parameters unter Verwendung des angegebenen Objekts.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Sendet eine Anforderung, dass dem Pool eine Anweisung hinzugefügt bzw. nicht hinzugefügt werden soll. Standardmäßig wird ein SQLServerPreparedStatement-Objekt dem Pool hinzugefügt werden, wenn erstellt.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt die Anzahl der Sekunden, die vom Treiber ein Statement-Objekt, führen Sie auf die angegebene Anzahl von Sekunden gewartet wird.|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter mit dem angegebenen Ref-Objekt.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(Geerbt von [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Legt den antwortpuffermodus für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, Groß-/Kleinschreibung **vollständige Zeichenfolge** oder **adaptive**.|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen **kurze** Wert.|  
|[SetString](../../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen **Zeichenfolge** Wert.|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen **SQLXML** Objekt.|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen Uhrzeitwert fest.|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen Zeitstempelwert fest.|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|Legt die angegebene Parameternummer auf den angegebenen Eingabedatenstrom mit der angegebenen Anzahl von Bytes fest.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverpreparedstatement.md)|Legt den angegebenen Parameter auf den angegebenen URL-Wert fest.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)|Gibt ein Objekt, das für den Zugriff auf die angegebene Schnittstelle implementiert die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-spezifischen Methoden.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Statement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
