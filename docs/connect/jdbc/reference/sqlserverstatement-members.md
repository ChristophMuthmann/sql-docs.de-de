---
title: SQLServerStatement-Elemente | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 828cbaa9-ea7a-4986-95c3-5ba0d7d01d83
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 15d9d6ee7e1ba03ac87157ae9aee02826ab77bca
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverstatement-members"></a>SQLServerStatement-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Die folgenden Tabellen enthalten die Elemente, die von verfügbar gemacht werden die [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
 Keine.  
  
## <a name="fields"></a>Felder  
 Keine.  
  
## <a name="inherited-fields"></a>Geerbte Felder  
  
|Name|Description|  
|----------|-----------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverstatement.md)|Fügt den angegebenen SQL-Befehl der aktuellen Liste mit Befehlen für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[Abbrechen](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|Bricht die SQL-Anweisung, die derzeit von diesem ausgeführt wird [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverstatement.md)|Leert die aktuelle Liste der SQL-Befehlen für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|Löscht alle Warnungen, die für dieses gemeldet werden [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[Schließen Sie](../../../connect/jdbc/reference/close-method-sqlserverstatement.md)|Dies frei [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objektspezifischen Datenbank- und JDBC-Ressourcen sofort gewartet, sondern deren automatische Freigabe sein.|  
|[Führen Sie](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)|Führt die angegebene SQL-Anweisung aus. Hierbei können mehrere Ergebnisse zurückgegeben werden.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)|Übermittelt einen Befehlsbatch zur Ausführung an die Datenbank. Werden alle Befehle erfolgreich ausgeführt, wird ein Array mit Updatezählungen zurückgegeben.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)|Führt die angegebene SQL-Anweisung und gibt ein einzelnes [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)|Führt die angegebene SQL-Anweisung aus. Hierbei kann es sich um eine Anweisung vom Typ "INSERT", "UPDATE", "MERGE" oder "DELETE" oder um eine SQL-Anweisung handeln, von der nichts zurückgegeben wird (beispielsweise eine SQL-DDL-Anweisung).|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|Ruft die [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) -Objekt, das Dies erzeugt [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|Ruft die Richtung ab, für das Abrufen von Zeilen aus Datenbanktabellen, die die standardmäßig für Resultsets, die von diesem generierten ist [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|Ruft die Anzahl der Resultsets festgelegt, der die standardmäßige Abrufgröße für Objekte, die von diesem generierten Resultset Zeilen [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|Ruft sämtliche automatisch generierte Schlüssel, die aufgrund der Ausführung dieser erstellt werden [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|Ruft die maximale Anzahl von Bytes, die für Zeichen- und Binärspaltenwerte in zurückgegeben werden, kann eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, das von diesem erzeugt wird [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|Ruft die maximale Anzahl der Zeilen ab, die eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt, das von diesem erzeugt wird [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt enthalten kann.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|Wechselt zum nächsten Ergebnis dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|Ruft die Anzahl der Sekunden ab dem [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wartet, bis diese [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt ausgeführt werden.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|Ruft den antwortpuffermodus für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|Ruft das aktuelle Ergebnis als eine [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|Ruft das Resultset Parallelität für [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die von diesem generierten [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|Ruft das Ergebnis für resultsethaltbarkeit [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die von diesem generierten [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|Ruft den Resultsettyp für [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die von diesem generierten [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|Ruft das aktuelle Ergebnis als Updatezählung ab.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|Ruft die erste Warnung ab, die von Aufrufen für dieses gemeldet wurde [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|Gibt an, ob dies [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt geschlossen wurde.|  
|[von isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|Gibt einen Wert zurück, durch den angegeben wird, ob dem vom Benutzer bereitgestellten Anwendungspool eine Anweisung hinzugefügt werden kann.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)|Gibt an, ob es sich bei diesem Anweisungsobjekt um einen Wrapper für die angegebene Schnittstelle handelt.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|Legt den SQL-Cursornamen auf die angegebene Zeichenfolge fest, die dann für nachfolgende Ausführungsmethoden verwendet wird.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|Legt den Escapeverarbeitungsmodus fest.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|Gibt für den JDBC-Treiber die Richtung an, in der die Resultsetzeilen verarbeitet werden sollen.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|Gibt für den JDBC-Treiber an, wie viele Zeilen aus der Datenbank abgerufen werden sollen, wenn weitere Zeilen benötigt werden.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|Legt das Limit für die maximale Anzahl von Bytes in einem [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Spalte Zeichen- oder Binärwerte auf die angegebene Anzahl von Bytes gespeichert werden.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|Das Limit für die maximale Anzahl von Zeilen, die von jedem legt [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt enthalten kann, auf die angegebene Anzahl.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|Sendet eine Anforderung, dass dem Pool eine Anweisung hinzugefügt bzw. nicht hinzugefügt werden soll.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|Legt die Anzahl der Sekunden, die der Treiber wartet eine [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, auf die angegebene Anzahl von Sekunden ausgeführt.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|Legt den antwortpuffermodus für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, Groß-/Kleinschreibung **vollständige Zeichenfolge** oder **adaptive**.|  
|[Entpacken](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)|Gibt ein Objekt, das für den Zugriff auf die angegebene Schnittstelle implementiert die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-spezifischen Methoden.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
