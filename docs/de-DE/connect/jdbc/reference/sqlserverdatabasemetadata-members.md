---
title: SQLServerDatabaseMetaData-Elemente | Microsoft Docs
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
ms.assetid: 327ba0bc-438a-494c-b119-1cd4a096bb58
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e62c58e037b0b14112f91a1392ca0670fe1f2e84
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverdatabasemetadata-members"></a>SQLServerDatabaseMetaData-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Die folgenden Tabellen enthalten die Elemente, die von verfügbar gemacht werden die [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
 Keine.  
  
## <a name="fields"></a>Felder  
 Keine.  
  
## <a name="inherited-fields"></a>Geerbte Felder  
  
|Name|Description|  
|----------|-----------------|  
|java.sql.DatabaseMetaData|attributeNoNulls, attributeNullable, attributeNullableUnknown, bestRowNotPseudo, bestRowPseudo, bestRowSession, bestRowTemporary, bestRowTransaction, bestRowUnknown, columnNoNulls, columnNullable, columnNullableUnknown, importedKeyCascade, importedKeyInitiallyDeferred, importedKeyInitiallyImmediate, importedKeyNoAction, importedKeyNotDeferrable, importedKeyRestrict, importedKeySetDefault, importedKeySetNull, procedureColumnIn, procedureColumnInOut, procedureColumnOut, procedureColumnResult, procedureColumnReturn, procedureColumnUnknown, procedureNoNulls, procedureNoResult, procedureNullable, procedureNullableUnknown, procedureResultUnknown, procedureReturnsResult, sqlStateSQL, sqlStateSQL99, sqlStateXOpen, tableIndexClustered, tableIndexHashed, tableIndexOther, tableIndexStatistic, typeNoNulls, typeNullable, typeNullableUnknown, typePredBasic, typePredChar, typePredNone, typeSearchable, versionColumnNotPseudo, versionColumnPseudo, versionColumnUnknown|  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[allProceduresAreCallable](../../../connect/jdbc/reference/allproceduresarecallable-method-sqlserverdatabasemetadata.md)|Ruft ab, ob der aktuelle Benutzer über Berechtigungen zum Aufrufen aller Prozeduren zurückgegebenes verfügt die [GetProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md) Methode.|  
|[allTablesAreSelectable](../../../connect/jdbc/reference/alltablesareselectable-method-sqlserverdatabasemetadata.md)|Ruft ab, ob der aktuelle Benutzer Berechtigungen für die Verwendung von zurückgegebenen Tabellen verfügt die [GetTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md) Methode in einer SELECT-Anweisung.|  
|[autoCommitFailureClosesAllResultSets](../../../connect/jdbc/reference/autocommitfailureclosesallresultsets-method-sqlserverdatabasemetadata.md)|Gibt an, ob vom JDBC-Treiber alle geöffneten Resultsets (einschließlich Resultsets mit Haltbarkeit) geschlossen werden, wenn ein automatischer Commit aktiviert und eine Ausnahme ausgelöst wird.|  
|[dataDefinitionCausesTransactionCommit](../../../connect/jdbc/reference/datadefinitioncausestransactioncommit-method-sqlserverdatabasemetadata.md)|Ruft ab, ob durch eine Datendefinitionsanweisung innerhalb einer Transaktion ein Commit der Transaktion erzwungen wird.|  
|[dataDefinitionIgnoredInTransactions](../../../connect/jdbc/reference/datadefinitionignoredintransactions-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank eine Datendefinitionsanweisung innerhalb einer Transaktion ignoriert wird.|  
|[deletesAreDetected](../../../connect/jdbc/reference/deletesaredetected-method-sqlserverdatabasemetadata.md)|Abgerufen, und zwar unabhängig davon, ob eine sichtbare Zeile löschen, können erkannt werden, durch Aufrufen der [RowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse.|  
|[doesMaxRowSizeIncludeBlobs](../../../connect/jdbc/reference/doesmaxrowsizeincludeblobs-method-sqlserverdatabasemetadata.md)|Ruft ab, ob der Rückgabewert für die [GetMaxRowSize](../../../connect/jdbc/reference/getmaxrowsize-method-sqlserverdatabasemetadata.md) Methode enthält die SQL-Datentypen LONGVARCHAR und LONGVARBINARY.|  
|[GetAttributes](../../../connect/jdbc/reference/getattributes-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung des angegebenen Attributs vom angegebenen Typ für einen benutzerdefinierten Typ ab, der im angegebenen Schema und Katalog verfügbar ist.|  
|[getBestRowIdentifier](../../../connect/jdbc/reference/getbestrowidentifier-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der optimalen Gruppe von Spalten einer Tabelle ab, durch die eine Zeile eindeutig identifiziert wird.|  
|[getCatalogs](../../../connect/jdbc/reference/getcatalogs-method-sqlserverdatabasemetadata.md)|Ruft die Katalognamen ab, die auf dem Server verfügbar sind, mit dem eine Verbindung besteht.|  
|[getCatalogSeparator](../../../connect/jdbc/reference/getcatalogseparator-method-sqlserverdatabasemetadata.md)|Ruft die **Zeichenfolge** , die diese Datenbank wird als Trennzeichen zwischen einem Katalog- und Tabellenname verwendet.|  
|[getCatalogTerm](../../../connect/jdbc/reference/getcatalogterm-method-sqlserverdatabasemetadata.md)|Ruft den bevorzugten Begriff des Datenbankherstellers für "catalog" ab.|  
|[getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)|Ruft eine Liste mit den Eigenschaften für Clientinformationen ab, die vom Treiber unterstützt werden.|  
|[getColumnPrivileges](../../../connect/jdbc/reference/getcolumnprivileges-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Zugriffsrechte für die Spalten in einer Tabelle ab.|  
|[getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Tabellenspalten ab, die im angegebenen Katalog verfügbar sind.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatabasemetadata.md)|Ruft die Verbindung ab, von der dieses Metadatenobjekt erstellt wurde.|  
|[getCrossReference](../../../connect/jdbc/reference/getcrossreference-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Fremdschlüsselspalten in der angegebenen Fremdschlüsseltabelle ab, von der auf die Primärschlüsselspalten der angegebenen Primärschlüsseltabelle verwiesen wird.|  
|[getDatabaseMajorVersion](../../../connect/jdbc/reference/getdatabasemajorversion-method-sqlserverdatabasemetadata.md)|Ruft die Hauptversionsnummer der zugrunde liegenden Datenbank ab.|  
|[getDatabaseMinorVersion](../../../connect/jdbc/reference/getdatabaseminorversion-method-sqlserverdatabasemetadata.md)|Ruft die Nebenversionsnummer der zugrunde liegenden Datenbank ab.|  
|[getDatabaseProductName](../../../connect/jdbc/reference/getdatabaseproductname-method-sqlserverdatabasemetadata.md)|Ruft den Namen dieses Datenbankprodukts ab.|  
|[getDatabaseProductVersion](../../../connect/jdbc/reference/getdatabaseproductversion-method-sqlserverdatabasemetadata.md)|Ruft die Versionsnummer dieses Datenbankprodukts ab.|  
|[getDefaultTransactionIsolation](../../../connect/jdbc/reference/getdefaulttransactionisolation-method-sqlserverdatabasemetadata.md)|Ruft die standardmäßige Transaktionsisolationsstufe für diese Datenbank ab.|  
|[getDriverMajorVersion](../../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md)|Ruft die Hauptversionsnummer dieses JDBC-Treibers ab.|  
|[getDriverMinorVersion](../../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md)|Ruft die Nebenversionsnummer dieses JDBC-Treibers ab.|  
|[getDriverName](../../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md)|Ruft den Namen dieses JDBC-Treibers ab.|  
|[getDriverVersion](../../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)|Ruft die Versionsnummer dieses JDBC-Treibers ab.|  
|[getExportedKeys](../../../connect/jdbc/reference/getexportedkeys-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Fremdschlüsselspalten, die Primärschlüsselspalten der angegebenen Tabelle verweisen.|  
|[getExtraNameCharacters](../../../connect/jdbc/reference/getextranamecharacters-method-sqlserverdatabasemetadata.md)|Ruft die zusätzlichen Zeichen, die in Bezeichnernamen, z. B. a-Z, A-Z, 0-9 und _ verwendet werden können.|  
|[getFunctions](../../../connect/jdbc/reference/getfunctions-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der System- und Benutzerfunktionen ab.|  
|[getFunctionColumns](../../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der System- oder Benutzerfunktionsparameter des angegebenen Katalogs sowie den Rückgabetyp ab.|  
|[getIdentifierQuoteString](../../../connect/jdbc/reference/getidentifierquotestring-method-sqlserverdatabasemetadata.md)|Ruft die **Zeichenfolge** dient außerdem zur SQL-Bezeichner in Anführungszeichen.|  
|[getImportedKeys](../../../connect/jdbc/reference/getimportedkeys-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Primärschlüsselspalten, auf den Fremdschlüsselspalten einer Tabelle verwiesen werden.|  
|[getIndexInfo](../../../connect/jdbc/reference/getindexinfo-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Indizes und der Statistik der angegebenen Tabelle ab.|  
|[getJDBCMajorVersion](../../../connect/jdbc/reference/getjdbcmajorversion-method-sqlserverdatabasemetadata.md)|Ruft die JDBC-Hauptversionsnummer für diesen Treiber ab.|  
|[getJDBCMinorVersion](../../../connect/jdbc/reference/getjdbcminorversion-method-sqlserverdatabasemetadata.md)|Ruft die JDBC-Nebenversionsnummer für diesen Treiber ab.|  
|[getMaxBinaryLiteralLength](../../../connect/jdbc/reference/getmaxbinaryliterallength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Hexadezimalzeichen ab, die bei dieser Datenbank für ein Inline-Binärliteral zulässig sind.|  
|[getMaxCatalogNameLength](../../../connect/jdbc/reference/getmaxcatalognamelength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Zeichen ab, die bei dieser Datenbank für einen Katalognamen zulässig sind.|  
|[getMaxCharLiteralLength](../../../connect/jdbc/reference/getmaxcharliterallength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Zeichen ab, die bei dieser Datenbank für ein Zeichenliteral zulässig sind.|  
|[getMaxColumnNameLength](../../../connect/jdbc/reference/getmaxcolumnnamelength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Zeichen ab, die bei dieser Datenbank für einen Spaltennamen zulässig sind.|  
|[getMaxColumnsInGroupBy](../../../connect/jdbc/reference/getmaxcolumnsingroupby-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Spalten ab, die bei dieser Datenbank in einer GROUP BY-Klausel zulässig sind.|  
|[getMaxColumnsInIndex](../../../connect/jdbc/reference/getmaxcolumnsinindex-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Spalten ab, die bei dieser Datenbank in einem Index zulässig sind.|  
|[getMaxColumnsInOrderBy](../../../connect/jdbc/reference/getmaxcolumnsinorderby-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Spalten ab, die bei dieser Datenbank in einer ORDER BY-Klausel zulässig sind.|  
|[getMaxColumnsInSelect](../../../connect/jdbc/reference/getmaxcolumnsinselect-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Spalten ab, die bei dieser Datenbank in einer SELECT-Liste zulässig sind.|  
|[getMaxColumnsInTable](../../../connect/jdbc/reference/getmaxcolumnsintable-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Spalten ab, die bei dieser Datenbank in einer Tabelle zulässig sind.|  
|[getMaxConnections](../../../connect/jdbc/reference/getmaxconnections-method-sqlserverdatabasemetadata.md)|Ruft die maximal mögliche Anzahl gleichzeitiger Verbindungen mit dieser Datenbank ab.|  
|[getMaxCursorNameLength](../../../connect/jdbc/reference/getmaxcursornamelength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Zeichen ab, die bei dieser Datenbank für einen Cursornamen zulässig sind.|  
|[getMaxIndexLength](../../../connect/jdbc/reference/getmaxindexlength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Bytes, die dieser Datenbank für einen Index, einschließlich alle Teile des Indexes zulässig.|  
|[getMaxProcedureNameLength](../../../connect/jdbc/reference/getmaxprocedurenamelength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Zeichen ab, die bei dieser Datenbank für einen Prozedurnamen zulässig sind.|  
|[getMaxRowSize](../../../connect/jdbc/reference/getmaxrowsize-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Bytes ab, die bei dieser Datenbank in einer einzelnen Zeile zulässig sind.|  
|[getMaxSchemaNameLength](../../../connect/jdbc/reference/getmaxschemanamelength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Zeichen ab, die bei dieser Datenbank für einen Schemanamen zulässig sind.|  
|[getMaxStatementLength](../../../connect/jdbc/reference/getmaxstatementlength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Zeichen, die dieser Datenbank in eine SQL-Anweisung zulässig.|  
|[getMaxStatements](../../../connect/jdbc/reference/getmaxstatements-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl aktiver Anweisungen an diese Datenbank ab, die gleichzeitig geöffnet sein können.|  
|[getMaxTableNameLength](../../../connect/jdbc/reference/getmaxtablenamelength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Zeichen ab, die bei dieser Datenbank für einen Tabellennamen zulässig sind.|  
|[getMaxTablesInSelect](../../../connect/jdbc/reference/getmaxtablesinselect-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Tabellen, die dieser Datenbank in einer SELECT-Anweisung zulässig.|  
|[getMaxUserNameLength](../../../connect/jdbc/reference/getmaxusernamelength-method-sqlserverdatabasemetadata.md)|Ruft die maximale Anzahl von Zeichen ab, die bei dieser Datenbank für einen Benutzernamen zulässig sind.|  
|[getNumericFunctions](../../../connect/jdbc/reference/getnumericfunctions-method-sqlserverdatabasemetadata.md)|Ruft eine durch Trennzeichen getrennte Liste mit mathematischen Funktionen ab, die für diese Datenbank verfügbar sind.|  
|[getPrimaryKeys](../../../connect/jdbc/reference/getprimarykeys-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Primärschlüsselspalten der angegebenen Tabelle ab.|  
|[getProcedureColumns](../../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Parameter gespeicherter Prozeduren und Ergebnisspalten ab.|  
|[getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der gespeicherten Prozeduren ab, die im angegebenen Katalog, Schema oder Namensmuster für gespeicherte Prozeduren verfügbar sind.|  
|[getProcedureTerm](../../../connect/jdbc/reference/getprocedureterm-method-sqlserverdatabasemetadata.md)|Ruft den bevorzugten Begriff für "procedure" in dieser Datenbank ab.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverdatabasemetadata.md)|Ruft die Standardhaltbarkeit von Resultsets für diese Datenbank ab.|  
|[getRowIdLifetime](../../../connect/jdbc/reference/getrowidlifetime-method-sqlserverdatabasemetadata.md)|Gibt einen Status zurück, mit dem angegeben wird, ob der SQL-Datentyp "RowId" unterstützt wird. Sofern unterstützt, wird die Lebensdauer zurückgegeben, für die ein RowId-Objekt gültig ist.|  
|[getSchemas](../../../connect/jdbc/reference/getschemas-method.md)|Ruft die Schemanamen ab, die in der aktuellen Datenbank verfügbar sind.|  
|[getSchemaTerm](../../../connect/jdbc/reference/getschematerm-method-sqlserverdatabasemetadata.md)|Ruft den bevorzugten Begriff für "schema" in dieser Datenbank ab.|  
|[getSearchStringEscape](../../../connect/jdbc/reference/getsearchstringescape-method-sqlserverdatabasemetadata.md)|Ruft die **Zeichenfolge** , die verwendet werden kann, um die Platzhalterzeichen mit Escapezeichen versehen.|  
|[getSQLKeywords](../../../connect/jdbc/reference/getsqlkeywords-method-sqlserverdatabasemetadata.md)|Ruft eine durch Trennzeichen getrennte Liste mit allen SQL-Schlüsselwörtern dieser Datenbank ab, bei denen es sich nicht gleichzeitig um SQL92-Schlüsselwörter handelt.|  
|[getSQLStateType](../../../connect/jdbc/reference/getsqlstatetype-method-sqlserverdatabasemetadata.md)|Gibt an, ob die von der SQLException.getSQLState-Methode zurückgegebene SQLSTATE X / Open (jetzt als Open Group bezeichnet), SQL CLI "," SQL99 (JDBC 3.0) oder SQL: 2003 (JDBC 4.0).|  
|[getStringFunctions](../../../connect/jdbc/reference/getstringfunctions-method-sqlserverdatabasemetadata.md)|Ruft eine durch Trennzeichen getrennte Liste von **Zeichenfolge** Funktionen, die diese Datenbank verfügbar sind.|  
|[getSuperTables](../../../connect/jdbc/reference/getsupertables-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Tabellenhierarchien ab, die in einem bestimmten Schema in dieser Datenbank definiert sind.|  
|[getSuperTypes](../../../connect/jdbc/reference/getsupertypes-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der benutzerdefinierten Typhierarchien ab, die in einem bestimmten Schema in dieser Datenbank definiert sind.|  
|[getSystemFunctions](../../../connect/jdbc/reference/getsystemfunctions-method-sqlserverdatabasemetadata.md)|Ruft eine durch Trennzeichen getrennte Liste mit Systemfunktionen ab, die für diese Datenbank verfügbar sind.|  
|[getTablePrivileges](../../../connect/jdbc/reference/gettableprivileges-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Zugriffsrechte für die einzelnen Tabellen ab, die im angegebenen Katalog, Schema oder Tabellennamenmuster verfügbar sind.|  
|[GetTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Tabellen ab, die im angegebenen Katalog, Schema oder Tabellennamenmuster verfügbar sind.|  
|[getTableTypes](../../../connect/jdbc/reference/gettabletypes-method-sqlserverdatabasemetadata.md)|Ruft die Tabellentypen ab, die in der aktuellen Datenbank verfügbar sind.|  
|[getTimeDateFunctions](../../../connect/jdbc/reference/gettimedatefunctions-method-sqlserverdatabasemetadata.md)|Ruft eine durch Trennzeichen getrennte Liste mit den Uhrzeit- und Datumsfunktionen ab, die für diese Datenbank verfügbar sind.|  
|[GetTypeInfo](../../../connect/jdbc/reference/gettypeinfo-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung aller standardmäßigen SQL-Typen ab, die von der aktuellen Datenbank unterstützt werden.|  
|[getUDTs](../../../connect/jdbc/reference/getudts-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der benutzerdefinierten Typen ab, die in einem bestimmten Schema definiert sind.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatabasemetadata.md)|Ruft die URL für diese Datenbank ab.|  
|[GetUserName](../../../connect/jdbc/reference/getusername-method-sqlserverdatabasemetadata.md)|Ruft den Benutzernamen gemäß der Angabe für diese Datenbank ab.|  
|[getVersionColumns](../../../connect/jdbc/reference/getversioncolumns-method-sqlserverdatabasemetadata.md)|Ruft eine Beschreibung der Spalten einer Tabelle ab, die automatisch aktualisiert wird, wenn ein Wert in einer Zeile aktualisiert wird.|  
|[insertsAreDetected](../../../connect/jdbc/reference/insertsaredetected-method-sqlserverdatabasemetadata.md)|Ruft ob Einfügen einer sichtbaren Zeile durch Aufrufen der Methode erkannt werden kann [RowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse.|  
|[isCatalogAtStart](../../../connect/jdbc/reference/iscatalogatstart-method-sqlserverdatabasemetadata.md)|Ruft ab, ob sich ein Katalog am Beginn eines vollqualifizierten Tabellennamens befindet.|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverdatabasemetadata.md)|Ruft ab, ob die Datenbank schreibgeschützt ist.|  
|[locatorsUpdateCopy](../../../connect/jdbc/reference/locatorsupdatecopy-method-sqlserverdatabasemetadata.md)|Gibt an, ob Aktualisierungen für ein LOB an einer Kopie oder direkt am LOB vorgenommen werden.|  
|[nullPlusNonNullIsNull](../../../connect/jdbc/reference/nullplusnonnullisnull-method-sqlserverdatabasemetadata.md)|Gibt an, ob von dieser Datenbank unterstützt wird, dass Verkettungen zwischen NULL-Werten und Werten ungleich NULL einen NULL-Wert ergeben.|  
|[nullsAreSortedAtEnd](../../../connect/jdbc/reference/nullsaresortedatend-method-sqlserverdatabasemetadata.md)|Ruft ab, ob NULL-Werte am Ende unabhängig von der Sortierreihenfolge sortiert werden.|  
|[nullsAreSortedAtStart](../../../connect/jdbc/reference/nullsaresortedatstart-method-sqlserverdatabasemetadata.md)|Ruft ab, ob NULL-Werte zu Beginn unabhängig von der Sortierreihenfolge sortiert werden.|  
|[nullsAreSortedHigh](../../../connect/jdbc/reference/nullsaresortedhigh-method-sqlserverdatabasemetadata.md)|Ruft ab, ob NULL-Werte bei der Sortierung als hohe Werte behandelt werden.|  
|[nullsAreSortedLow](../../../connect/jdbc/reference/nullsaresortedlow-method-sqlserverdatabasemetadata.md)|Ruft ab, ob NULL-Werte bei der Sortierung als niedrige Werte behandelt werden.|  
|[othersDeletesAreVisible](../../../connect/jdbc/reference/othersdeletesarevisible-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von anderen ausgeführte Löschvorgänge sichtbar sind.|  
|[othersInsertsAreVisible](../../../connect/jdbc/reference/othersinsertsarevisible-method-sqlserverdatabasemetadata.md)|Ruft ab, ob die von anderen vorgenommenen einfügungen sichtbar sind.|  
|[othersUpdatesAreVisible](../../../connect/jdbc/reference/othersupdatesarevisible-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von anderen ausgeführte Aktualisierungen sichtbar sind.|  
|[ownDeletesAreVisible](../../../connect/jdbc/reference/owndeletesarevisible-method-sqlserverdatabasemetadata.md)|Ruft ab, ob die eigenen Löschvorgänge eines Resultsets sichtbar sind.|  
|[ownInsertsAreVisible](../../../connect/jdbc/reference/owninsertsarevisible-method-sqlserverdatabasemetadata.md)|Ruft ab, ob die eigenen Einfügevorgänge eines Resultsets sichtbar sind.|  
|[ownUpdatesAreVisible](../../../connect/jdbc/reference/ownupdatesarevisible-method-sqlserverdatabasemetadata.md)|Ruft ab, ob die eigenen Aktualisierungen des Resultsets sichtbar sind.|  
|[storesLowerCaseIdentifiers](../../../connect/jdbc/reference/storeslowercaseidentifiers-method-sqlserverdatabasemetadata.md)|Ruft ab, ob bei SQL-Bezeichnern mit gemischter Groß-/Kleinschreibung, die nicht in Anführungszeichen gesetzt sind, die Groß-/Kleinschreibung nicht berücksichtigt wird und die Bezeichner in Kleinbuchstaben gespeichert werden.|  
|[storesLowerCaseQuotedIdentifiers](../../../connect/jdbc/reference/storeslowercasequotedidentifiers-method-sqlserverdatabasemetadata.md)|Ruft ab, ob bei SQL-Bezeichnern mit gemischter Groß-/Kleinschreibung, die in Anführungszeichen gesetzt sind, die Groß-/Kleinschreibung nicht berücksichtigt wird und die Bezeichner in Kleinbuchstaben gespeichert werden.|  
|[storesMixedCaseIdentifiers](../../../connect/jdbc/reference/storesmixedcaseidentifiers-method-sqlserverdatabasemetadata.md)|Ruft ab, ob bei SQL-Bezeichnern mit gemischter Groß-/Kleinschreibung, die nicht in Anführungszeichen gesetzt sind, die Groß-/Kleinschreibung nicht berücksichtigt wird und die Bezeichner mit gemischter Groß-/Kleinschreibung gespeichert werden.|  
|[storesMixedCaseQuotedIdentifiers](../../../connect/jdbc/reference/storesmixedcasequotedidentifiers-method-sqlserverdatabasemetadata.md)|Ruft ab, ob bei SQL-Bezeichnern mit gemischter Groß-/Kleinschreibung, die in Anführungszeichen gesetzt sind, die Groß-/Kleinschreibung nicht berücksichtigt wird und die Bezeichner mit gemischter Groß-/Kleinschreibung gespeichert werden.|  
|[storesUpperCaseIdentifiers](../../../connect/jdbc/reference/storesuppercaseidentifiers-method-sqlserverdatabasemetadata.md)|Ruft ab, ob bei SQL-Bezeichnern mit gemischter Groß-/Kleinschreibung, die nicht in Anführungszeichen gesetzt sind, die Groß-/Kleinschreibung nicht berücksichtigt wird und die Bezeichner in Großbuchstaben gespeichert werden.|  
|[storesUpperCaseQuotedIdentifiers](../../../connect/jdbc/reference/storesuppercasequotedidentifiers-method-sqlserverdatabasemetadata.md)|Ruft ab, ob bei SQL-Bezeichnern mit gemischter Groß-/Kleinschreibung, die in Anführungszeichen gesetzt sind, die Groß-/Kleinschreibung nicht berücksichtigt wird und die Bezeichner in Großbuchstaben gespeichert werden.|  
|[supportsAlterTableWithAddColumn](../../../connect/jdbc/reference/supportsaltertablewithaddcolumn-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank "ALTER TABLE" mit "add column" unterstützt wird.|  
|[supportsAlterTableWithDropColumn](../../../connect/jdbc/reference/supportsaltertablewithdropcolumn-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank "ALTER TABLE" mit "drop column" unterstützt wird.|  
|[supportsANSI92EntryLevelSQL](../../../connect/jdbc/reference/supportsansi92entrylevelsql-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die ANSI92-SQL-Einstiegsgrammatik unterstützt wird.|  
|[supportsANSI92FullSQL](../../../connect/jdbc/reference/supportsansi92fullsql-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die vollständige ANSI92-SQL-Grammatik unterstützt wird.|  
|[supportsANSI92IntermediateSQL](../../../connect/jdbc/reference/supportsansi92intermediatesql-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die ANSI92-SQL-Zwischengrammatik unterstützt wird.|  
|[supportsBatchUpdates](../../../connect/jdbc/reference/supportsbatchupdates-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Batchaktualisierungen unterstützt werden.|  
|[supportsCatalogsInDataManipulation](../../../connect/jdbc/reference/supportscatalogsindatamanipulation-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Datenbearbeitungsanweisung ein Katalogname verwendet werden kann.|  
|[supportsCatalogsInIndexDefinitions](../../../connect/jdbc/reference/supportscatalogsinindexdefinitions-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Indexdefinitionsanweisung ein Katalogname verwendet werden kann.|  
|[supportsCatalogsInPrivilegeDefinitions](../../../connect/jdbc/reference/supportscatalogsinprivilegedefinitions-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Berechtigungsdefinitionsanweisung ein Katalogname verwendet werden kann.|  
|[supportsCatalogsInProcedureCalls](../../../connect/jdbc/reference/supportscatalogsinprocedurecalls-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Prozeduraufrufanweisung ein Katalogname verwendet werden kann.|  
|[supportsCatalogsInTableDefinitions](../../../connect/jdbc/reference/supportscatalogsintabledefinitions-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Tabellendefinitionsanweisung ein Katalogname verwendet werden kann.|  
|[supportsColumnAliasing](../../../connect/jdbc/reference/supportscolumnaliasing-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Spaltenaliasing unterstützt wird.|  
|[supportsConvert](../../../connect/jdbc/reference/supportsconvert-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die CONVERT-Funktion für SQL-Typen unterstützt wird.|  
|[supportsCoreSQLGrammar](../../../connect/jdbc/reference/supportscoresqlgrammar-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die ODBC-SQL-Kerngrammatik unterstützt wird.|  
|[supportsCorrelatedSubqueries](../../../connect/jdbc/reference/supportscorrelatedsubqueries-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank korrelierte Unterabfragen unterstützt werden.|  
|[supportsDataDefinitionAndDataManipulationTransactions](../../../connect/jdbc/reference/supportsdatadefinitionanddatamanipulationtransactions-method.md)|Ruft ab, ob von dieser Datenbank in einer Transaktion sowohl Datendefinitions- als auch Datenbearbeitungsanweisungen unterstützt werden.|  
|[supportsDataManipulationTransactionsOnly](../../../connect/jdbc/reference/supportsdatamanipulationtransactionsonly-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank in einer Transaktion nur Datenbearbeitungsanweisungen unterstützt werden.|  
|[supportsDifferentTableCorrelationNames](../../../connect/jdbc/reference/supportsdifferenttablecorrelationnames-method-sqlserverdatabasemetadata.md)|Ruft ab, ob sich abhängige Tabellennamen (sofern diese unterstützt werden) von den Namen der Tabellen unterscheiden müssen.|  
|[supportsExpressionsInOrderBy](../../../connect/jdbc/reference/supportsexpressionsinorderby-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Ausdrücke in ORDER BY-Listen unterstützt werden.|  
|[supportsExtendedSQLGrammar](../../../connect/jdbc/reference/supportsextendedsqlgrammar-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die erweiterte ODBC-SQL-Grammatik unterstützt wird.|  
|[supportsFullOuterJoins](../../../connect/jdbc/reference/supportsfullouterjoins-method-sqlserverdatabasemetadata.md)|Ruft ab, ob geschachtelte äußere Joins von dieser Datenbank vollständig unterstützt werden.|  
|[supportsGetGeneratedKeys](../../../connect/jdbc/reference/supportsgetgeneratedkeys-method-sqlserverdatabasemetadata.md)|Ruft ab, ob automatisch generierte Schlüssel nach dem Ausführen einer Anweisung abgerufen werden können.|  
|[supportsGroupBy](../../../connect/jdbc/reference/supportsgroupby-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank eine Form der GROUP BY-Klausel unterstützt wird.|  
|[supportsGroupByBeyondSelect](../../../connect/jdbc/reference/supportsgroupbybeyondselect-method-sqlserverdatabasemetadata.md)|Ruft ab, ob es sich bei dieser Datenbank unterstützt die Verwendung von Spalten, die nicht in der SELECT-Anweisung in einer GROUP BY-Klausel enthalten, vorausgesetzt, dass alle Spalten in der SELECT-Anweisung in der GROUP BY-Klausel enthalten sind.|  
|[supportsGroupByUnrelated](../../../connect/jdbc/reference/supportsgroupbyunrelated-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die Verwendung einer Spalte, die sich nicht in der SELECT-Anweisung befindet, in einer GROUP BY-Klausel unterstützt wird.|  
|[supportsIntegrityEnhancementFacility](../../../connect/jdbc/reference/supportsintegrityenhancementfacility-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die SQL-Integritätserweiterungsfunktion unterstützt wird.|  
|[supportsLikeEscapeClause](../../../connect/jdbc/reference/supportslikeescapeclause-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank das Angeben einer LIKE-Escapeklausel unterstützt wird.|  
|[supportsLimitedOuterJoins](../../../connect/jdbc/reference/supportslimitedouterjoins-method-sqlserverdatabasemetadata.md)|Ruft ab, ob äußere Joins von dieser Datenbank in eingeschränktem Maß unterstützt werden.|  
|[supportsMinimumSQLGrammar](../../../connect/jdbc/reference/supportsminimumsqlgrammar-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die minimale ODBC-SQL-Grammatik unterstützt wird.|  
|[supportsMixedCaseIdentifiers](../../../connect/jdbc/reference/supportsmixedcaseidentifiers-method-sqlserverdatabasemetadata.md)|Ruft ab, ob bei SQL-Bezeichnern mit gemischter Groß-/Kleinschreibung, die nicht in Anführungszeichen gesetzt sind, die Groß-/Kleinschreibung nicht berücksichtigt wird und die Bezeichner mit gemischter Groß-/Kleinschreibung gespeichert werden.|  
|[supportsMixedCaseQuotedIdentifiers](../../../connect/jdbc/reference/supportsmixedcasequotedidentifiers-method-sqlserverdatabasemetadata.md)|Ruft ab, ob bei SQL-Bezeichnern mit gemischter Groß-/Kleinschreibung, die in Anführungszeichen gesetzt sind, die Groß-/Kleinschreibung nicht berücksichtigt wird und die Bezeichner mit gemischter Groß-/Kleinschreibung gespeichert werden.|  
|[supportsMultipleOpenResults](../../../connect/jdbc/reference/supportsmultipleopenresults-method-sqlserverdatabasemetadata.md)|Ruft ab, ob es möglich ist, mehrere [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) zurückgegebenen Objekte eine [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) -Objekts gleichzeitig.|  
|[supportsMultipleResultSets](../../../connect/jdbc/reference/supportsmultipleresultsets-method-sqlserverdatabasemetadata.md)|Ruft ab, ob dieser Datenbank unterstützt mehrere erste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekte aus einem einzigen Aufruf der [ausführen](../../../connect/jdbc/reference/execute-method.md) Methode der [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)Klasse.|  
|[supportsMultipleTransactions](../../../connect/jdbc/reference/supportsmultipletransactions-method-sqlserverdatabasemetadata.md)|Ruft ab, ob bei dieser Datenbank gleichzeitig mehrere Transaktionen für unterschiedliche Verbindungen geöffnet sein können.|  
|[supportsNamedParameters](../../../connect/jdbc/reference/supportsnamedparameters-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank benannte Parameter in aufrufbaren Anweisungen unterstützt werden.|  
|[supportsNonNullableColumns](../../../connect/jdbc/reference/supportsnonnullablecolumns-method-sqlserverdatabasemetadata.md)|Ruft ab, ob Spalten in dieser Datenbank als Spalten definiert werden können, in denen keine NULL-Werte zulässig sind.|  
|[supportsOpenCursorsAcrossCommit](../../../connect/jdbc/reference/supportsopencursorsacrosscommit-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank unterstützt wird, dass Cursor über Commits hinaus geöffnet bleiben.|  
|[supportsOpenCursorsAcrossRollback](../../../connect/jdbc/reference/supportsopencursorsacrossrollback-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank unterstützt wird, dass Cursor über Rollbacks hinaus geöffnet bleiben.|  
|[supportsOpenStatementsAcrossCommit](../../../connect/jdbc/reference/supportsopenstatementsacrosscommit-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank unterstützt wird, dass Anweisungen über Commits hinaus geöffnet bleiben.|  
|[supportsOpenStatementsAcrossRollback](../../../connect/jdbc/reference/supportsopenstatementsacrossrollback-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank unterstützt wird, dass Anweisungen über Rollbacks hinaus geöffnet bleiben.|  
|[supportsOrderByUnrelated](../../../connect/jdbc/reference/supportsorderbyunrelated-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die Verwendung einer Spalte, die sich nicht in der SELECT-Anweisung befindet, in einer ORDER BY-Klausel unterstützt wird.|  
|[supportsOuterJoins](../../../connect/jdbc/reference/supportsouterjoins-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank eine Form von äußeren Joins unterstützt wird.|  
|[supportsPositionedDelete](../../../connect/jdbc/reference/supportspositioneddelete-method-sqlserverdatabasemetadata.md)|Ruft ab, ob positionierte DELETE-Anweisungen von dieser Datenbank unterstützt werden.|  
|[supportsPositionedUpdate](../../../connect/jdbc/reference/supportspositionedupdate-method-sqlserverdatabasemetadata.md)|Ruft ab, ob positionierte UPDATE-Anweisungen von dieser Datenbank unterstützt werden.|  
|[supportsResultSetConcurrency](../../../connect/jdbc/reference/supportsresultsetconcurrency-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank der angegebene Parallelitätstyp in Kombination mit dem angegebenen Resultsettyp unterstützt wird.|  
|[supportsResultSetHoldability](../../../connect/jdbc/reference/supportsresultsetholdability-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die angegebene Resultsethaltbarkeit unterstützt wird.|  
|[supportsResultSetType](../../../connect/jdbc/reference/supportsresultsettype-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank der angegebene Resultsettyp unterstützt wird.|  
|[supportsSavepoints](../../../connect/jdbc/reference/supportssavepoints-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Sicherungspunkte unterstützt werden.|  
|[supportsSchemasInDataManipulation](../../../connect/jdbc/reference/supportsschemasindatamanipulation-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Datenbearbeitungsanweisung ein Schemaname verwendet werden kann.|  
|[supportsSchemasInIndexDefinitions](../../../connect/jdbc/reference/supportsschemasinindexdefinitions-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Indexdefinitionsanweisung ein Schemaname verwendet werden kann.|  
|[supportsSchemasInPrivilegeDefinitions](../../../connect/jdbc/reference/supportsschemasinprivilegedefinitions-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Berechtigungsdefinitionsanweisung ein Schemaname verwendet werden kann.|  
|[supportsSchemasInProcedureCalls](../../../connect/jdbc/reference/supportsschemasinprocedurecalls-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Prozeduraufrufanweisung ein Schemaname verwendet werden kann.|  
|[supportsSchemasInTableDefinitions](../../../connect/jdbc/reference/supportsschemasintabledefinitions-method-sqlserverdatabasemetadata.md)|Ruft ab, ob in einer Tabellendefinitionsanweisung ein Schemaname verwendet werden kann.|  
|[supportsSelectForUpdate](../../../connect/jdbc/reference/supportsselectforupdate-method-sqlserverdatabasemetadata.md)|Ruft ab, ob positionierte SELECT FOR UPDATE-Anweisungen von dieser Datenbank unterstützt werden.|  
|[supportsStatementPooling](../../../connect/jdbc/reference/supportsstatementpooling-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Anweisungspools unterstützt werden.|  
|[supportsStoredFunctionsUsingCallSyntax](../../../connect/jdbc/reference/supportsstoredfunctionsusingcallsyntax-method-sqlserverdatabasemetadata.md)|Gibt an, ob von der aktuellen Datenbank das Aufrufen benutzer- oder herstellerdefinierter Funktionen mithilfe der Escapesyntax für gespeicherte Prozeduren unterstützt wird.|  
|[supportsStoredProcedures](../../../connect/jdbc/reference/supportsstoredprocedures-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank gespeicherte Prozeduraufrufe unterstützt werden, bei denen die Escapesyntax für gespeicherte Prozeduren verwendet wird.|  
|[supportsSubqueriesInComparisons](../../../connect/jdbc/reference/supportssubqueriesincomparisons-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Unterabfragen in Vergleichsausdrücken unterstützt werden.|  
|[supportsSubqueriesInExists](../../../connect/jdbc/reference/supportssubqueriesinexists-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Unterabfragen in EXISTS-Ausdrücken unterstützt werden.|  
|[supportsSubqueriesInIns](../../../connect/jdbc/reference/supportssubqueriesinins-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Unterabfragen in IN-Ausdrücken unterstützt werden.|  
|[supportsSubqueriesInQuantifieds](../../../connect/jdbc/reference/supportssubqueriesinquantifieds-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Unterabfragen in quantifizierten Ausdrücken unterstützt werden.|  
|[supportsTableCorrelationNames](../../../connect/jdbc/reference/supportstablecorrelationnames-method-sqlserverdatabasemetadata.md)|Ruft ab, ob abhängige Tabellennamen von dieser Datenbank unterstützt werden.|  
|[supportsTransactionIsolationLevel](../../../connect/jdbc/reference/supportstransactionisolationlevel-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank die angegebene Transaktionsisolationsstufe unterstützt wird.|  
|[supportsTransactions](../../../connect/jdbc/reference/supportstransactions-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank Transaktionen unterstützt werden.|  
|[supportsUnion](../../../connect/jdbc/reference/supportsunion-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank "SQL UNION" unterstützt wird.|  
|[supportsUnionAll](../../../connect/jdbc/reference/supportsunionall-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank "SQL UNION ALL" unterstützt wird.|  
|[updatesAreDetected](../../../connect/jdbc/reference/updatesaredetected-method-sqlserverdatabasemetadata.md)|Abgerufen, und zwar unabhängig davon, ob Aktualisieren einer sichtbaren Zeile durch Aufrufen von erkannt werden kann, die [RowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse.|  
|[usesLocalFilePerTable](../../../connect/jdbc/reference/useslocalfilepertable-method-sqlserverdatabasemetadata.md)|Ruft ab, ob von dieser Datenbank für jede Tabelle eine Datei verwendet wird.|  
|[usesLocalFiles](../../../connect/jdbc/reference/useslocalfiles-method-sqlserverdatabasemetadata.md)|Ruft ab, ob Tabellen von dieser Datenbank in einer lokalen Datei gespeichert werden.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
