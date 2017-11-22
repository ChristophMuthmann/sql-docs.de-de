---
title: Verwenden von benutzerdefinierten Typen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [SQL Server Native Client]
- user-defined types [SQL Server], SQL Server Native Client
- SQL Server Native Client OLE DB provider, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- SQLNCLI, user-defined types
- SQL Server Native Client, user-defined types
- data access [SQL Server Native Client], user-defined types
- ISSCommandWithParameters interface
ms.assetid: e15d8169-3517-4323-9c9e-0f5c34aff7df
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3bc82bed550b790ffc191d4d10463d2255368ff8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="using-user-defined-types"></a>Verwenden von benutzerdefinierten Typen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] wurden benutzerdefinierte Typen (User-Defined Types, UDTs) eingeführt. UDTs erweitern das SQL-Typsystem, sodass Sie zum Speichern von Objekten und benutzerdefinierte Datenstrukturen in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank. UDTs können mehrere Datentypen enthalten und Verhalten zeigen, das sie von den herkömmlichen Aliasdatentypen aus einem einzelnen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Systemdatentyp unterscheidet. UDTs werden in einer beliebigen, von .NET CLR (Common Language Runtime) unterstützten Sprache definiert, die überprüfbaren Code generiert. Dies schließt Microsoft Visual C#-<sup>®</sup> und Visual Basic<sup>®</sup> .NET. Die Daten werden in Feldern und Eigenschaften einer .NET-Klasse oder -Struktur verfügbar gemacht. Das Verhalten wird durch die Methoden der Klasse oder Struktur definiert.  
  
 Ein UDT als Spaltendefinition einer Tabelle, als Variable in verwendet werden kann eine [!INCLUDE[tsql](../../../includes/tsql-md.md)] Batch oder als Argument einer [!INCLUDE[tsql](../../../includes/tsql-md.md)] Funktion oder gespeicherten Prozedur.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB-Anbieter  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt UDTs als Binärtypen mit Metadateninformationen, mit dem Sie UDTs als Objekte verwalten können. UDT-Spalten werden als DBTYPE_UDT verfügbar gemacht, und ihre Metadaten werden verfügbar gemacht, über die OLE DB-Kernschnittstelle **IColumnRowset**, und der neuen [ISSCommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) Schnittstelle.  
  
> [!NOTE]  
>  Die **irowsetfind:: FindNextRow** -Methode funktioniert nicht mit dem UDT-Datentyp. DB_E_BADCOMPAREOP wird zurückgegeben, wenn der UDT als Suchspaltentyp verwendet wird.  
  
### <a name="data-bindings-and-coercions"></a>Datenbindungen und -umwandlungen  
 Die folgende Tabelle veranschaulicht die Bindung und Umwandlung bei Verwendung der aufgeführten Datentypen mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-UDT. UDT-Spalten werden verfügbar gemacht, durch die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter als DBTYPE_UDT. Die Metadaten können Sie über die entsprechenden Schemarowsets abrufen und so Ihre benutzerdefinierten Typen als Objekte verwalten.  
  
|Datentyp|Zu Server<br /><br /> **UDT**|Zu Server<br /><br /> **nicht-UDT**|Von Server<br /><br /> **UDT**|Von Server<br /><br /> **nicht-UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|Unterstützt<sup>6</sup>|Fehler<sup>1</sup>|Unterstützt<sup>6</sup>|Fehler<sup>5</sup>|  
|DBTYPE_BYTES|Unterstützt<sup>6</sup>|N/A<sup>2</sup>|Unterstützt<sup>6</sup>|N/A<sup>2</sup>|  
|DBTYPE_WSTR|Unterstützt<sup>3,6</sup>|N/A<sup>2</sup>|Unterstützt<sup>4,6</sup>|N/A<sup>2</sup>|  
|DBTYPE_BSTR|Unterstützt<sup>3,6</sup>|N/A<sup>2</sup>|Unterstützt<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_STR|Unterstützt<sup>3,6</sup>|N/A<sup>2</sup>|Unterstützt<sup>4,6</sup>|N/A<sup>2</sup>|  
|DBTYPE_IUNKNOWN|Nicht unterstützt|N/A<sup>2</sup>|Nicht unterstützt|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Unterstützt<sup>6</sup>|N/A<sup>2</sup>|Unterstützt<sup>4</sup>|N/A<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Unterstützt<sup>3,6</sup>|N/A<sup>2</sup>|–|N/A<sup>2</sup>|  
  
 <sup>1</sup>, wenn ein anderer Servertyp als DBTYPE_UDT mit Indexparametern **ICommandWithParameters:: SetParameterInfo** und ist der Accessortyp DBTYPE_UDT, ein Fehler auftritt, wenn die Anweisung ausgeführt wird (DB_E_ERRORSOCCURRED; das Parameterstatus ist DBSTATUS_E_BADACCESSOR). Andernfalls werden die Daten an den Server gesendet, der Server gibt jedoch einen Fehler zurück und zeigt an, dass keine implizite Umwandlung des UDT in den Parameterdatentyp erfolgt.  
  
 <sup>2</sup>Gegenstand dieses Themas.  
  
 <sup>3</sup> Datenkonvertierung einer hexadezimalen Zeichenfolge in binäre Daten.  
  
 <sup>4</sup> Datenkonvertierung von Binärdaten in eine hexadezimale Zeichenfolge.  
  
 <sup>5</sup>Überprüfung ausgeführt werden kann bei Erstellen des Accessors oder zum Zeitpunkt der Abruf der Fehler lautet DB_E_ERRORSOCCURRED, Bindungsstatus auf DBBINDSTATUS_UNSUPPORTEDCONVERSION festgelegt.  
  
 <sup>6</sup>BY_REF kann verwendet werden.  
  
 DBTYPE_NULL und DBTYPE_EMPTY können für Eingabeparameter gebunden werden, aber nicht für Ausgabeparameter oder Ergebnisse. Wenn für Eingabeparameter gebunden ist, muss der Status auf DBSTATUS_S_ISNULL oder DBSTATUS_S_DEFAULT festgelegt werden.  
  
 DBTYPE_UDT kann auch in DBTYPE_EMPTY und DBTYPE_NULL umgewandelt werden, DBTYPE_NULL und DBTYPE_EMPTY können jedoch nicht in DBTYPE_UDT umgewandelt werden. Dies stimmt mit DBTYPE_BYTES überein.  
  
> [!NOTE]  
>  Eine neue Schnittstelle wird verwendet, für den Umgang mit UDTs als Parameter **ISSCommandWithParameters**, erbt die **ICommandWithParameters**. Anwendungen müssen diese Schnittstelle verwenden, um mindestens SSPROP_PARAM_UDT_NAME der DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe für UDT-Parameter festzulegen. Wenn dies nicht erfolgt, **ICommand:: Execute** DB_E_ERRORSOCCURRED zurück. Diese Schnittstelle und Eigenschaftengruppe werden im weiteren Verlauf dieses Themas erläutert.  
  
 Wenn Sie ein benutzerdefinierten Typ in eine Spalte eingefügt, die nicht groß genug für alle ihre Daten ist **ICommand:: Execute** S_OK mit dem Status DB_E_ERRORSOCCURRED zurück.  
  
 Datenkonvertierungen durch OLE DB-Basisdienste (**IDataConvert**) sind nicht in DBTYPE_UDT anwendbar. Es werden keine weiteren Bindungen unterstützt.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Hinzufügungen und Änderungen am OLE DB-Rowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Schemarowsets.  
  
#### <a name="the-procedureparameters-schema-rowset"></a>Das PROCEDURE_PARAMETERS-Schemarowset  
 Die folgenden Hinzufügungen wurden am PROCEDURE_PARAMETERS-Schemarowset vorgenommen.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.|  
|SS_UDT_NAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Die Assembly qualifizierte Name, darunter den vollständigen Typnamen sowie alle der Assembly-Referenzierung erforderlichen Angaben von der CLR verwiesen wird.|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>Das SQL_ASSEMBLIES-Schemarowset  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht ein neues anbieterspezifisches Schemarowset, die die registrierten UDTs beschreibt. Der ASSEMBLY-Server wird möglicherweise als DBTYPE_WSTR angegeben, ist aber nicht im Rowset vorhanden. Ohne Angabe wird das Rowset standardmäßig für den aktuellen Server festgelegt. Das SQL_ASSEMBLIES-Schemarowset wird in der folgenden Tabelle definiert.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Der Katalogname der Assembly, die den Typ enthält.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Der Name des Schemas oder der Eigentümername der Assembly, die den Typ enthält. Obwohl der Bereich einer Assembly durch die Datenbank und nicht durch ein Schema definiert wird, hat sie einen Eigentümer, der hier angegeben wird.|  
|ASSEMBLY_NAME|DBTYPE_WSTR|Der Name der Assembly, die den Typ enthält.|  
|ASSEMBLY_ID|DBTYPE_UI4|Die Objekt-ID der Assembly, die den Typ enthält.|  
|PERMISSION_SET|DBTYPE_WSTR|Ein Wert, der den Zugriffsbereich für die Assembly angibt. Zulässige Werten sind "SAFE", "EXTERNAL_ACCESS" und "UNSAFE".|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|Die Binärdarstellung der Assembly.|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>Das SQL_ASSEMBLIES_ DEPENDENCIES-Schemarowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB-Anbieter macht ein neues anbieterspezifischen Schemarowset, das die Assemblyabhängigkeiten für einen bestimmten Server beschreibt. ASSEMBLY_SERVER wird möglicherweise vom Aufrufer als DBTYPE_WSTR angegeben, ist aber nicht im Rowset vorhanden. Ohne Angabe wird das Rowset standardmäßig für den aktuellen Server festgelegt. Das SQL_ASSEMBLY_DEPENDENCIES-Schemarowset wird in der folgenden Tabelle definiert.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Der Katalogname der Assembly, die den Typ enthält.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Der Name des Schemas oder der Eigentümername der Assembly, die den Typ enthält. Obwohl Assemblys durch die Datenbank und nicht durch ein Schema zugeordnet sind, müssen sie noch einen Besitzer, der hier angegeben wird.|  
|ASSEMBLY_ID|DBTYPE_UI4|Die Objekt-ID der Assembly.|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|Die Objekt-ID der referenzierten Assembly.|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>Das SQL_USER_TYPES-Schemarowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB-Anbieter verfügbar macht, neues Schemarowset, SQL_USER_TYPES, die beschreibt, wann die registrierten UDTs für einen bestimmten Server hinzugefügt wird. UDT_SERVER muss vom Aufrufer als DBTYPE_WSTR angegeben werden, ist aber nicht im Rowset vorhanden. Das SQL_USER_TYPES-Schemarowset wird in der folgenden Tabelle definiert.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|UDT_SCHEMANAME|DBTYPE_WSTR|Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Schemas angibt, in dem der UDT definiert ist.|  
|UDT_NAME|DBTYPE_WSTR|Der Name der Assembly, die die UDT-Klasse enthält.|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Vollständiger Typname (AQN) einschließlich Typname mit Namespace als Präfix (falls zutreffend).|  
  
#### <a name="the-columns-schema-rowset"></a>Das COLUMNS-Schemarowset  
 Dem COLUMNS-Schemarowset wurden unter anderem die folgenden Spalten hinzugefügt.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Schemas angibt, in dem der UDT definiert ist.|  
|SS_UDT_NAME|DBTYPE_WSTR|Der Name des UDT.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Vollständiger Typname (AQN) einschließlich Typname mit Namespace als Präfix (falls zutreffend).|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Hinzufügungen und Änderungen an der OLE DB-Eigenschaftengruppe  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Eigenschaft legt.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>Die DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe  
 Um UDTs durch OLE DB zu unterstützen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementiert die neue DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe mit folgenden Werten.  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.<br /><br /> Bei UDT-Parametern ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.<br /><br /> Bei UDT-Parametern ist diese Eigenschaft eine Zeichenfolge, die den Namen des Schemas angibt, in dem der UDT definiert ist.|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.<br /><br /> Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den einteiligen Namen des UDT angibt.|  
  
 SSPROP_PARAM_UDT_NAME ist erforderlich. SSPROP_PARAM_UDT_CATALOGNAME und SSPROP_PARAM_UDT_SCHEMANAME sind optional. Wenn Eigenschaften falsch angegeben werden, wird DB_E_ERRORSINCOMMAND zurückgegeben. Werden weder SSPROP_PARAM_UDT_CATALOGNAME noch SSPROP_PARAM_UDT_SCHEMANAME angegeben, muss der UDT in derselben Datenbank und im selben Schema definiert werden wie die Tabelle. Befindet sich der UDT nicht im selben Schema wie die Tabelle (aber in derselben Datenbank), muss SSPROP_PARAM_UDT_SCHEMANAME angegeben werden. Befindet sich die UDT-Definition in einer anderen Datenbank, müssen SSPROP_PARAM_UDT_CATALOGNAME und SSPROP_PARAM_UDT_SCHEMANAME angegeben werden.  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>Die DBPROPSET_SQLSERVERCOLUMN-Eigenschaftengruppe  
 Unterstützt die Erstellung von Tabellen in der **ITableDefinition** Schnittstelle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client der DBPROPSET_SQLSERVERCOLUMN-Eigenschaftensatz die folgenden drei neue Spalten hinzugefügt.  
  
|Name|Description|Typ|Description|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|Bei Spalten vom Typ DBTYPE_UDT ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|Bei Spalten vom Typ DBTYPE_UDT ist diese Eigenschaft eine Zeichenfolge, die den Namen des Schemas angibt, in dem der UDT definiert ist.|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|Bei Spalten vom Typ DBTYPE_UDT ist diese Eigenschaft eine Zeichenfolge, die den einteiligen Namen des UDT angibt. Für andere Spaltentypen gibt diese Eigenschaft eine leere Zeichenfolge.|  
  
> [!NOTE]  
>  UDTs werden nicht im PROVIDER_TYPES-Schemarowset angezeigt. Alle Spalten haben Lese- und Schreibzugriff.  
  
 ADO verweist mit dem entsprechenden Eintrag aus der Beschreibungsspalte auf diese Eigenschaften.  
  
 SSPROP_COL_UDTNAME ist erforderlich. SSPROP_COL_UDT_CATALOGNAME und SSPROP_COL_UDT_SCHEMANAME sind optional. Wenn Eigenschaften falsch angegeben werden **DB_E_ERRORSINCOMMAND** zurückgegeben werden.  
  
 Werden weder SSPROP_COL_UDT_CATALOGNAME noch SSPROP_COL_UDT_SCHEMANAME angegeben, muss der UDT in derselben Datenbank und im selben Schema definiert werden wie die Tabelle.  
  
 Befindet sich der UDT nicht im selben Schema wie die Tabelle (aber in derselben Datenbank), muss SSPROP_COL_UDT_SCHEMANAME angegeben werden.  
  
 Befindet sich die UDT-Definition in einer anderen Datenbank, müssen SSPROP_COL_UDT_CATALOGNAME und SSPROP_COL_UDT_SCHEMANAME angegeben werden.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Hinzufügungen und Änderungen an der OLE DB-Schnittstelle  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Schnittstellen.  
  
#### <a name="the-isscommandwithparameters-interface"></a>Die ISSCommandWithParameters-Schnittstelle  
 Um UDTs durch OLE DB zu unterstützen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementiert eine Reihe von Änderungen, z. B. das Hinzufügen der **ISSCommandWithParameters** Schnittstelle. Diese neue Schnittstelle erbt von der OLE DB-Kernschnittstelle **ICommandWithParameters**. Zusätzlich zu den drei von geerbten Methoden **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, und **SetParameterInfo**; **ISSCommandWithParameters** bietet die **GetParameterProperties** und **SetParameterProperties** Methoden, die verwendet werden, um Datentypen zu behandeln.  
  
> [!NOTE]  
>  Die **ISSCommandWithParameters** -Schnittstelle nutzt auch verwenden, die neue ssparamprops Struktur.  
  
#### <a name="the-icolumnsrowset-interface"></a>Die IDBColumnsRowset-Schnittstelle  
 Zusätzlich zu den **ISSCommandWithParameters** -Schnittstelle, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client fügt neue Werte auch auf das vom Aufruf zurückgegebene Rowset die **IColumnsRowset:: Getcolumnrowset** Methode u. a. folgende aus.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|Ein UDT-Katalognamensbezeichner.|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|Ein UDT-Schemanamensbezeichner.|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|Ein UDT-Namensbezeichner.|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Der qualifizierte Name der Assembly mit dem Typnamen und allen zur CLR-Referenzierung erforderlichen Angaben zur Assembly-ID.|  
  
 Ist DBCOLUMN_TYPE auf DBTYPE_UDT festgelegt, können Sie eine Server-UDT-Spalte von anderen Binärtypen unterscheiden, indem Sie die oben genannten neuen UDT-Metadaten betrachten. Sind diese Daten teilweise vollständig, handelt es sich bei dem Servertyp um einen UDT. Für Nicht-UDT-Servertypen werden diese Spalten immer als NULL zurückgegeben.  
  
## <a name="sql-server-native-client-odbc-driver"></a>ODBC-Treiber für SQL Server Native Client  
 Eine Reihe von Änderungen vorgenommen wurden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber um UDTs zu unterstützen. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ordnet die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UDT SQL_SS_UDT-treiberspezifischen SQL Data geben Bezeichner. UDT-Spalten werden als SQL_SS_UDT angegeben. Wenn Sie eine UDT-Spalte explizit in einen anderen Typ in einer SQL­Anweisung mit Zuordnen der **ToString** oder **ToXMLString** Methoden des UDT oder über die **CAST/CONVERT** -Funktion, die den Typ die Spalte im Resultset widerspiegelt Satz den tatsächlichen Typ in die Spalte konvertiert wurde  
  
### <a name="sqlcolattribute-sqldescribeparam-sqlgetdescfield"></a>SQLColAttribute, SQLDescribeParam, SQLGetDescField  
 Vier neue treiberspezifische deskriptorfelder wurden hinzugefügt, um zusätzliche Informationen für entweder eine UDT-Spalte eines Resultsets oder einem UDT-Parameter der gespeicherten Prozedur/parametrisierten Abfrage über abgerufen werden sollen bieten die [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md), und [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md) Funktionen.  
  
 Die vier neuen Deskriptorfelder sind SQL_CA_SS_UDT_CATALOG_NAME, SQL_CA_SS_UDT_SCHEMA_NAME, SQL_CA_SS_UDT_TYPE_NAME und SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="sqlcolumns-sqlprocedurecolumns"></a>SQLColumns, SQLProcedureColumns  
 Darüber hinaus von zurückgegebene Resultset drei neue treiberspezifische Spalten hinzugefügt werden die [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) und [SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md) Funktionen für die zusätzliche Informationen zu einer UDT-Resultsetspalte Legen Sie die Spalte oder eine UDT-Parameter. Diese drei neuen Spalten sind SS_UDT_CATALOG_NAME, SS_UDT_SCHEMA_NAME und SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="supported-conversions"></a>Unterstützte Umwandlungen  
 Bei der Umwandlung von SQL- in C-Datentypen können SQL_C_WCHAR, SQL_C_BINARY und SQL_C_CHAR in SQL_SS_UDT umgewandelt werden. Beachten Sie jedoch, dass Binärdaten bei der Umwandlung der SQL-Datentypen SQL_C_WCHAR und SQL_C_CHAR in eine hexadezimale Zeichenfolge umgewandelt werden.  
  
 Bei der Umwandlung von C- in SQL-Datentypen können SQL_C_WCHAR, SQL_C_BINARY und SQL_C_CHAR in SQL_SS_UDT umgewandelt werden. Beachten Sie jedoch, dass binäre Daten in eine hexadezimale Zeichenfolge konvertiert werden, wenn von den Datentypen SQL_C_WCHAR und SQL_C_CHAR SQL zu konvertieren.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Funktionen](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40; OLE DB &#41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
