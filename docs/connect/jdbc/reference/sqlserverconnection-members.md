---
title: SQLServerConnection-Elemente | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3115a533-756b-4c78-aee9-4ba7253c85e0
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 917a5561dd3de7f9f45434aef88bd2eb98661473
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverconnection-members"></a>SQLServerConnection-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Die folgenden Tabellen enthalten die Elemente, die von verfügbar gemacht werden die [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
 Keine.  
  
## <a name="fields"></a>Felder  
  
|Name|Description|  
|----------|-----------------|  
|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|Dient zum Angeben der Transaktionsisolationsstufe für Momentaufnahmen.|  
  
## <a name="inherited-fields"></a>Geerbte Felder  
  
|Klasse geerbt von:|Description|  
|---------------------------|-----------------|  
|java.sql.Connection|TRANSACTION_NONE, TRANSACTION_READ_COMMITTED, TRANSACTION_READ_UNCOMMITTED, TRANSACTION_REPEATABLE_READ, TRANSACTION_SERIALIZABLE|  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverconnection.md)|Löscht alle für diesen gemeldeten Warnungen [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[Schließen Sie](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)|Die Datenbank für diesen frei [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt und JDBC-Ressourcen sofort gewartet, sondern deren automatische Freigabe sein.|  
|[Commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)|Macht alle Änderungen, die seit dem letzten Commit oder Rollback permanente vorgenommen wurden, und hebt sämtliche Datenbanksperren an, die derzeit von diesem aufrechterhalten werden [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)|Erstellt eine **java.sql.Blob** Objekt ohne Daten.|  
|[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)|Erstellt eine **java.sql.Clob** Objekt ohne Daten.|  
|[createNClob](../../../connect/jdbc/reference/createnclob-method-sqlserverconnection.md)|Erstellt eine **java.sql.NClob** Objekt ohne Daten.|  
|[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)|Erstellt eine [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt zum Senden von SQL-Anweisungen an die Datenbank.|  
|[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)|Erstellt eine **java.sql.SQLXML** Objekt ohne Daten.|  
|[getAutoCommit](../../../connect/jdbc/reference/getautocommit-method-sqlserverconnection.md)|Ruft ab den aktuellen Autocommit-Modus für diese [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[getCatalog](../../../connect/jdbc/reference/getcatalog-method-sqlserverconnection.md)|Ruft ab den aktuellen Katalognamen für dieses [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[GetClientConnectionID-Methode &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|Ruft die Verbindungs-ID des letzten Versuchs der Verbindungsherstellung ab, wobei es keine Rolle spielt, ob dieser Versuch erfolgreich war oder fehlgeschlagen ist.|  
|[getClientInfo](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)|Ruft Informationen zu den Eigenschaften für Clientinformationen ab, die vom JDBC-Treiber unterstützt werden.|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverconnection.md)|Ruft die aktuelle Haltbarkeit von [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die erstellt werden, mithilfe dieses [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)|Ruft eine [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) Objekt, das Metadaten zu dem diese Datenbank enthält [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt stellt eine Verbindung dar.|  
|[getTransactionIsolation](../../../connect/jdbc/reference/gettransactionisolation-method-sqlserverconnection.md)|Ruft die aktuelle Transaktionsisolationsstufe für dieses [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[getTypeMap](../../../connect/jdbc/reference/gettypemap-method-sqlserverconnection.md)|Ruft die Map-Objekt, das mit dieser verknüpft ist [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)|Ruft die erste Warnung gemeldet von Aufrufen für dieses [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverconnection.md)|Gibt an, ob dies [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt geschlossen wurde.|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverconnection.md)|Gibt an, ob dies [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt befindet sich im schreibgeschützten Modus.|  
|[isValid](../../../connect/jdbc/reference/isvalid-method-sqlserverconnection.md)|Gibt an, ob dies [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt wurde nicht geschlossen, und noch gültig ist.|  
|[nativeSQL](../../../connect/jdbc/reference/nativesql-method-sqlserverconnection.md)|Konvertiert die angegebene SQL-Anweisung zur systemeigenen SQL-Grammatik des Datenbankservers.|  
|[prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)|Erstellt eine [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) Objekt für die Datenbank gespeicherten Prozeduren aufrufen.|  
|[prepareStatement](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)|Erstellt eine [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Objekt zum Senden parametrisierter SQL-Anweisungen in der Datenbank.|  
|[releaseSavepoint](../../../connect/jdbc/reference/releasesavepoint-method-sqlserverconnection.md)|Entfernt das angegebene [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) Objekt aus der aktuellen Transaktion.|  
|[Rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)|Macht alle in der aktuellen Transaktion vorgenommenen Änderungen rückgängig und hebt sämtliche Datenbanksperren derzeit aufrecht erhalten werden von diesem [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
|[setAutoCommit](../../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)|Legt den Autocommit-Modus für diese [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt, das dem angegebenen Status.|  
|[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)|Legt den angegebenen Katalognamen auf einen Teilbereich davon [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objektspezifischen-Datenbank, in dem Sie arbeiten.|  
|[setClientInfo](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)|Legt den Wert der Eigenschaften für Clientinformationen fest.|  
|[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)|Ändert die Haltbarkeit von [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte, die erstellt werden, mithilfe dieses [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) Objekt zur angegebenen Haltbarkeit.|  
|[setReadOnly](../../../connect/jdbc/reference/setreadonly-method-sqlserverconnection.md)|Dies setzt [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt im Nur-Lese-Modus als Hinweis für die JDBC-Treiber die datenbankoptimierungen aktiviert.|  
|[setSavepoint](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)|Erstellt einen unbenannten Sicherungspunkt in der aktuellen Transaktion und gibt die neue [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) Objekt, das sie darstellt.|  
|[setTransactionIsolation](../../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)|So ändern Sie die Transaktionsisolationsstufe für dieses versucht [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) mit dem angegebenen Objekt.|  
|[setTypeMap](../../../connect/jdbc/reference/settypemap-method-sqlserverconnection.md)|Installiert das angegebene Objekt der TypeMap als Typzuordnung für dieses [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.lang.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

