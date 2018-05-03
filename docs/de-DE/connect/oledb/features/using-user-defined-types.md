---
title: Verwenden von benutzerdefinierten Typen | Microsoft Docs
description: Verwenden von benutzerdefinierten Typen mit OLE DB-Treiber für SQLServer
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
- DBPROPSET_DATASOURCEINFO property set
- UDTs [OLE DB Driver for SQL Server]
- user-defined types [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- MSOLEDBSQL, user-defined types
- OLE DB Driver for SQL Server, user-defined types
- data access [OLE DB Driver for SQL Server], user-defined types
- ISSCommandWithParameters interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e58706dcd208188475f88913f4cab9e8ba15e80a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-user-defined-types"></a>Verwenden von benutzerdefinierten Typen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] wurden benutzerdefinierte Typen (User-Defined Types, UDTs) eingeführt. UDTs erweitern das SQL-Typsystem, sodass Sie zum Speichern von Objekten und benutzerdefinierte Datenstrukturen in einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank. UDTs können mehrere Datentypen enthalten und Verhalten zeigen, das sie von den herkömmlichen Aliasdatentypen aus einem einzelnen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Systemdatentyp unterscheidet. UDTs werden in einer beliebigen, von .NET CLR (Common Language Runtime) unterstützten Sprache definiert, die überprüfbaren Code generiert. Dies schließt Microsoft Visual C#-<sup>®</sup> und Visual Basic<sup>®</sup> .NET. Die Daten werden in Feldern und Eigenschaften einer .NET-Klasse oder -Struktur verfügbar gemacht. Das Verhalten wird durch die Methoden der Klasse oder Struktur definiert.  
  
 Ein UDT als Spaltendefinition einer Tabelle, als Variable in verwendet werden kann eine [!INCLUDE[tsql](../../../includes/tsql-md.md)] Batch oder als Argument einer [!INCLUDE[tsql](../../../includes/tsql-md.md)] Funktion oder gespeicherten Prozedur.  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQLServer  
 Der OLE DB-Treiber für SQL Server unterstützt UDTs als Binärtypen mit Metadateninformationen, mit dem Sie UDTs als Objekte verwalten können. UDT-Spalten werden als DBTYPE_UDT verfügbar gemacht, und ihre Metadaten werden verfügbar gemacht, über die OLE DB-Kernschnittstelle **IColumnRowset**, und der neuen [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) Schnittstelle.  
  
> [!NOTE]  
>  Die **irowsetfind:: FindNextRow** -Methode funktioniert nicht mit dem UDT-Datentyp. DB_E_BADCOMPAREOP wird zurückgegeben, wenn der UDT als Suchspaltentyp verwendet wird.  
  
### <a name="data-bindings-and-coercions"></a>Datenbindungen und -umwandlungen  
 Die folgende Tabelle veranschaulicht die Bindung und Umwandlung bei Verwendung der aufgeführten Datentypen mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-UDT. UDT-Spalten werden über den OLE DB-Treiber für SQL Server als DBTYPE_UDT verfügbar gemacht. Die Metadaten können Sie über die entsprechenden Schemarowsets abrufen und so Ihre benutzerdefinierten Typen als Objekte verwalten.  
  
|Datentyp|Zu Server<br /><br /> **UDT**|Zu Server<br /><br /> **non-UDT**|Von Server<br /><br /> **UDT**|Von Server<br /><br /> **non-UDT**|  
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
  
 <sup>2</sup>würde den Rahmen dieses Artikels sprengen.  
  
 <sup>3</sup> Datenkonvertierung einer hexadezimalen Zeichenfolge in binäre Daten.  
  
 <sup>4</sup> Datenkonvertierung von Binärdaten in eine hexadezimale Zeichenfolge.  
  
 <sup>5</sup>Überprüfung ausgeführt werden kann bei Erstellen des Accessors oder zum Zeitpunkt der Abruf der Fehler lautet DB_E_ERRORSOCCURRED, Bindungsstatus auf DBBINDSTATUS_UNSUPPORTEDCONVERSION festgelegt.  
  
 <sup>6</sup>BY_REF kann verwendet werden.  
  
 DBTYPE_NULL und DBTYPE_EMPTY können für Eingabeparameter gebunden werden, aber nicht für Ausgabeparameter oder Ergebnisse. Wenn für Eingabeparameter gebunden ist, muss der Status auf DBSTATUS_S_ISNULL oder DBSTATUS_S_DEFAULT festgelegt werden.  
  
 DBTYPE_UDT kann auch in DBTYPE_EMPTY und DBTYPE_NULL umgewandelt werden, DBTYPE_NULL und DBTYPE_EMPTY können jedoch nicht in DBTYPE_UDT umgewandelt werden. Dies stimmt mit DBTYPE_BYTES überein.  
  
> [!NOTE]  
>  Eine neue Schnittstelle wird verwendet, für den Umgang mit UDTs als Parameter **ISSCommandWithParameters**, erbt die **ICommandWithParameters**. Anwendungen müssen diese Schnittstelle verwenden, um mindestens SSPROP_PARAM_UDT_NAME der DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe für UDT-Parameter festzulegen. Wenn dies nicht erfolgt, **ICommand:: Execute** DB_E_ERRORSOCCURRED zurück. Diese Schnittstelle und Eigenschaftengruppe werden weiter unten in diesem Artikel beschrieben.  
  
 Wenn Sie ein benutzerdefinierten Typ in eine Spalte eingefügt, die nicht groß genug für alle ihre Daten ist **ICommand:: Execute** S_OK mit dem Status DB_E_ERRORSOCCURRED zurück.  
  
 Datenkonvertierungen durch OLE DB-Basisdienste (**IDataConvert**) sind nicht in DBTYPE_UDT anwendbar. Es werden keine weiteren Bindungen unterstützt.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Hinzufügungen und Änderungen am OLE DB-Rowset  
 OLE DB-Treiber für SQL Server fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Schemarowsets.  
  
#### <a name="the-procedureparameters-schema-rowset"></a>Das PROCEDURE_PARAMETERS-Schemarowset  
 Die folgenden Hinzufügungen wurden am PROCEDURE_PARAMETERS-Schemarowset vorgenommen.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.|  
|SS_UDT_NAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Die Assembly qualifizierte Name, darunter den vollständigen Typnamen sowie alle der Assembly-Referenzierung erforderlichen Angaben von der CLR verwiesen wird.|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>Das SQL_ASSEMBLIES-Schemarowset  
 Der OLE DB-Treiber für SQL Server macht ein neues anbieterspezifischen Schemarowset, das die registrierten UDTs beschreibt. Der ASSEMBLY-Server wird möglicherweise als DBTYPE_WSTR angegeben, ist aber nicht im Rowset vorhanden. Ohne Angabe wird das Rowset standardmäßig für den aktuellen Server festgelegt. Das SQL_ASSEMBLIES-Schemarowset wird in der folgenden Tabelle definiert:  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Der Katalogname der Assembly, die den Typ enthält.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Der Name des Schemas oder der Eigentümername der Assembly, die den Typ enthält. Obwohl der Bereich einer Assembly durch die Datenbank und nicht durch ein Schema definiert wird, hat sie einen Eigentümer, der hier angegeben wird.|  
|ASSEMBLY_NAME|DBTYPE_WSTR|Der Name der Assembly, die den Typ enthält.|  
|ASSEMBLY_ID|DBTYPE_UI4|Die Objekt-ID der Assembly, die den Typ enthält.|  
|PERMISSION_SET|DBTYPE_WSTR|Ein Wert, der den Zugriffsbereich für die Assembly angibt. Zulässige Werten sind "SAFE", "EXTERNAL_ACCESS" und "UNSAFE".|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|Die Binärdarstellung der Assembly.|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>Das SQL_ASSEMBLIES_ DEPENDENCIES-Schemarowset  
 OLE DB-Treiber für SQL Server macht ein neues anbieterspezifischen Schemarowset, das die Assemblyabhängigkeiten für einen bestimmten Server beschreibt. ASSEMBLY_SERVER wird möglicherweise vom Aufrufer als DBTYPE_WSTR angegeben, ist aber nicht im Rowset vorhanden. Ohne Angabe wird das Rowset standardmäßig für den aktuellen Server festgelegt. Das SQL_ASSEMBLY_DEPENDENCIES-Schemarowset wird in der folgenden Tabelle definiert:  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Der Katalogname der Assembly, die den Typ enthält.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Der Name des Schemas oder der Eigentümername der Assembly, die den Typ enthält. Obwohl Assemblys durch die Datenbank und nicht durch ein Schema zugeordnet sind, müssen sie noch einen Besitzer, der hier angegeben wird.|  
|ASSEMBLY_ID|DBTYPE_UI4|Die Objekt-ID der Assembly.|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|Die Objekt-ID der Assembly, auf die verwiesen wird.|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>Das SQL_USER_TYPES-Schemarowset  
 OLE DB-Treiber für SQL Server macht neues Schemarowset, SQL_USER_TYPES, die beschreibt, wann die registrierten UDTs für einen bestimmten Server hinzugefügt werden. UDT_SERVER muss vom Aufrufer als DBTYPE_WSTR angegeben werden, ist aber nicht im Rowset vorhanden. Das SQL_USER_TYPES-Schemarowset wird in der folgenden Tabelle definiert.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|Für UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|UDT_SCHEMANAME|DBTYPE_WSTR|Für UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die mit dem Namen des Schemas, in dem der UDT definiert ist.|  
|UDT_NAME|DBTYPE_WSTR|Der Name der Assembly, die die UDT-Klasse enthält.|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Vollständiger Typname (AQN) einschließlich Typname mit Namespace als Präfix (falls zutreffend).|  
  
#### <a name="the-columns-schema-rowset"></a>Das COLUMNS-Schemarowset  
 Ergänzungen für das COLUMNS-Schemarowset unter anderem die folgenden Spalten:  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Für UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Für UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die mit dem Namen des Schemas, in dem der UDT definiert ist.|  
|SS_UDT_NAME|DBTYPE_WSTR|Der Name des UDT.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Vollständiger Typname (AQN) einschließlich Typname mit Namespace als Präfix (falls zutreffend).|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Hinzufügungen und Änderungen an der OLE DB-Eigenschaftengruppe  
 OLE DB-Treiber für SQL Server fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Eigenschaft legt.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>Die DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe  
 Um UDTs durch OLE DB zu unterstützen, implementiert die OLE DB-Treiber für SQL Server die neue DBPROPSET_SQLSERVERPARAMETER-Eigenschaftengruppe mit folgenden Werten:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.<br /><br /> Bei UDT-Parametern ist diese Eigenschaft eine Zeichenfolge, die den Namen des Katalogs angibt, in dem der UDT definiert ist.|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.<br /><br /> Bei UDT-Parametern ist diese Eigenschaft eine Zeichenfolge, die den Namen des Schemas angibt, in dem der UDT definiert ist.|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|Der dreiteilige Namensbezeichner.<br /><br /> Bei UDT-Spalten ist diese Eigenschaft eine Zeichenfolge, die den einteiligen Namen des UDT angibt.|  
  
 SSPROP_PARAM_UDT_NAME ist erforderlich. SSPROP_PARAM_UDT_CATALOGNAME und SSPROP_PARAM_UDT_SCHEMANAME sind optional. Wenn Eigenschaften falsch angegeben werden, wird DB_E_ERRORSINCOMMAND zurückgegeben. Werden weder SSPROP_PARAM_UDT_CATALOGNAME noch SSPROP_PARAM_UDT_SCHEMANAME angegeben, muss der UDT in derselben Datenbank und im selben Schema definiert werden wie die Tabelle. Befindet sich der UDT nicht im selben Schema wie die Tabelle (aber in derselben Datenbank), muss SSPROP_PARAM_UDT_SCHEMANAME angegeben werden. Wenn die UDT-Definition in einer anderen Datenbank ist, müssen SSPROP_PARAM_UDT_CATALOGNAME und SSPROP_PARAM_UDT_SCHEMANAME angegeben werden.  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>Die DBPROPSET_SQLSERVERCOLUMN-Eigenschaftengruppe  
 Unterstützt die Erstellung von Tabellen in der **ITableDefinition** -Schnittstelle, OLE DB-Treiber für SQL Server DBPROPSET_SQLSERVERCOLUMN-Eigenschaftensatz die folgenden drei neue Spalten hinzugefügt.  
  
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
 OLE DB-Treiber für SQL Server fügt neue Werte oder Änderungen in zahlreichen Core-OLE DB-Schnittstellen.  
  
#### <a name="the-isscommandwithparameters-interface"></a>Die ISSCommandWithParameters-Schnittstelle  
 Um UDTs durch OLE DB zu unterstützen, implementiert die OLE DB-Treiber für SQL Server eine Anzahl von Änderungen, z. B. das Hinzufügen der **ISSCommandWithParameters** Schnittstelle. Diese neue Schnittstelle erbt von der OLE DB-Kernschnittstelle **ICommandWithParameters**. Zusätzlich zu den drei von geerbten Methoden **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, und **SetParameterInfo**; **ISSCommandWithParameters** bietet die **GetParameterProperties** und **SetParameterProperties** Methoden, die bestimmten Handle-zu-Server verwendet werden Datentypen.  
  
> [!NOTE]  
>  Die **ISSCommandWithParameters** -Schnittstelle nutzt auch verwenden, die neue ssparamprops Struktur.  
  
#### <a name="the-icolumnsrowset-interface"></a>Die IDBColumnsRowset-Schnittstelle  
 Zusätzlich zu den **ISSCommandWithParameters** Schnittstelle, OLE DB-Treiber für SQL Server auch die neuen Werte auf das vom Aufruf zurückgegebene Rowset sorgt die **IColumnsRowset:: Getcolumnrowset** einschließlich der Methode die folgenden.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|Ein UDT-Katalognamensbezeichner.|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|Ein UDT-Schemanamensbezeichner.|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|Ein UDT-Namensbezeichner.|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Der qualifizierte Name der Assembly mit dem Typnamen und allen zur CLR-Referenzierung erforderlichen Angaben zur Assembly-ID.|  
  
 Sie können eine Server-UDT-Spalte von anderen Binärtypen unterscheiden, wenn DBCOLUMN_TYPE auf DBTYPE_UDT festgelegt ist, durch einen Blick auf die UDT-Metadaten in der obigen Tabelle angegeben. Sind diese Daten teilweise vollständig, handelt es sich bei dem Servertyp um einen UDT. Für Nicht-UDT-Servertypen werden diese Spalten immer als NULL zurückgegeben.  
 
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Funktionen](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
