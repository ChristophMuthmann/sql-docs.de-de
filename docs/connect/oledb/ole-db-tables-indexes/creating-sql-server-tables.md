---
title: Erstellen von SQL Server-Tabellen | Microsoft Docs
description: Erstellen von SQL Server-Tabellen, die mithilfe von OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- OLE DB Driver for SQL Server, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 998b1d4c18ec626a7ef48a8ff141bdfa1e2fdd36
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="creating-sql-server-tables"></a>Erstellen von SQL Server-Tabellen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server macht die **itabledefinition:: CreateTable** -Funktion, ermöglicht es Consumern, erstellen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabellen. Consumer verwenden **CreateTable** zum Erstellen von dauerhaften Tabellen Consumer benannt und permanente oder temporäre Tabellen mit eindeutigen Namen, die von der OLE DB-Treiber für SQL Server generiert.  
  
 Wenn der Consumer ruft **itabledefinition:: CreateTable**, wenn der Wert der Eigenschaft DBPROP_TBL_TEMPTABLE VARIANT_TRUE fest, der OLE DB-Treiber für SQL Server einen temporären Tabellennamen für den Consumer generiert. Der Consumer legt den *pTableID* Parameter von der **CreateTable** Methode auf NULL. Die temporären Tabellen mit Namen, die von der OLE DB-Treiber für SQL Server generiert werden nicht angezeigt, der **Tabellen** Rowset, aber über zugänglich sind die **IOpenRowset** Schnittstelle.  
  
 Wenn Consumer geben den Tabellennamen in der *PwszName* Mitglied der *uName* -Vereinigung der *pTableID* Parameter, der OLE DB-Treiber für SQL Server erstellt eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Tabelle mit diesem Namen. Es gelten die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Einschränkungen für Tabellennamen, und der Tabellenname kann eine dauerhafte Tabelle angeben oder entweder eine lokale oder globale temporäre Tabelle. Weitere Informationen finden Sie unter [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md). Die *PpTableID* Parameter kann NULL sein.  
  
 Der OLE DB-Treiber für SQL Server können die Namen der permanente oder temporäre Tabellen zu generieren. Wenn der Consumer legt den *pTableID* Parameter auf NULL und legt *PpTableID* , zeigen Sie auf eine gültige DBID\*, OLE DB-Treiber für SQL Server gibt der generierte Name der Tabelle in der zurück.*PwszName* Mitglied der *uName* Kombination DBI gezeigt wird durch den Wert des *PpTableID*. Erstellen einen temporären, OLE DB-Treiber für SQL Server-namens Tabelle schließt der Consumer die OLE DB-Tabelleneigenschaft DBPROP_TBL_TEMPTABLE in einen tabelleneigenschaftensatz verwiesen wird, in der *RgPropertySets* Parameter. OLE DB-Treiber für SQL Server-benannte temporäre Tabellen sind lokal.  
  
 **CreateTable** gibt db_e_badtableid zurück, wenn die *eKind* Mitglied der *pTableID* -Parameters nicht dbkind_name.  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC-Verwendung  
 Der Consumer kann ein Spaltendatentyps angeben, indem Sie entweder die *PwszTypeName* Member oder die *wType* Member. Wenn der Consumer den Datentyp in gibt *PwszTypeName*, der OLE DB-Treiber für SQL Server ignoriert den Wert der *wType*.  
  
 Bei Verwendung der *PwszTypeName* Member, der Consumer gibt den Datentyp mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentypnamen. Gültige Datentypnamen sind die, die in der Spalte TYPE_NAME des PROVIDER_TYPES-Schemarowsets zurückgegeben werden.  
  
 Der OLE DB-Treiber für SQL Server erkennt eine Teilmenge der OLE DB aufgelisteten DBTYPE-Werten in der *wType* Member. Weitere Informationen finden Sie unter [Data Type Mapping itabledefinition](../../oledb/ole-db-data-types/data-type-mapping-in-itabledefinition.md).  
  
> [!NOTE]  
>  **CreateTable** gibt db_e_badtype zurück, wenn der Consumer die *pTypeInfo* oder *Pclsid* Member Datentyp der Spalte an.  
  
 Der Consumer gibt den Spaltennamen in der *PwszName* Mitglied der *uName* -Vereinigung des DBCOLUMNDESC *Dbcid* Member. Der Spaltenname wird als Unicode-Zeichenfolge angegeben. Die *eKind* Mitglied *Dbcid* muss DBKIND_NAME sein. **CreateTable** gibt db_e_badcolumnid zurück, wenn *eKind* ist ungültig, *PwszName* NULL ist, oder wenn der Wert der *PwszName* ist kein gültiger [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Bezeichner.  
  
 Alle Spalteneigenschaften sind in allen für die Tabelle definierten Spalten verfügbar. **CreateTable** kann DB_S_ERRORSOCCURRED oder DB_E_ERRORSOCCURRED zurückgeben werden, wenn in Konflikt stehende Werte festgelegt sind. **CreateTable** gibt einen Fehler zurück, wenn ungültige Spalteneigenschaften führen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -tabellenerstellung.  
  
 Spalteneigenschaften in DBCOLUMNDESC werden wie folgt interpretiert.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/w: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE-Beschreibung: Legt die IDENTITY-Eigenschaft der Spalte, die erstellt wird, fest. Für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ist die IDENTITY-Eigenschaft für eine einzelne Spalte innerhalb einer Tabelle gültig. Die Eigenschaft festlegen auf VARIANT_TRUE, für mehr als eine einzelne Spalte einen Fehler generiert, wenn der OLE DB-Treiber für SQL Server versucht, die Tabelle auf dem Server zu erstellen.<br /><br /> Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Identity-Eigenschaft ist nur gültig für die **Ganzzahl**, **numerischen**, und **decimal** Typen, wenn der Dezimalstellenwert 0 ist. Festlegen der Eigenschaft auf VARIANT_TRUE fest, auf eine Spalte mit einem beliebigen anderen Datentyp erzeugt einen Fehler, wenn der OLE DB-Treiber für SQL Server versucht, die Tabelle auf dem Server zu erstellen.<br /><br /> Der OLE DB-Treiber für SQL Server gibt DB_S_ERRORSOCCURRED zurück, wenn DBPROP_COL_AUTOINCREMENT als auch DBPROP_COL_NULLABLE den Wert VARIANT_TRUE haben und die *DwOption* von DBPROP_COL_NULLABLE ist nicht dbpropoptions_required ist. DB_E_ERRORSOCCURRED wird zurückgegeben, wenn DBPROP_COL_AUTOINCREMENT als auch DBPROP_COL_NULLABLE den Wert VARIANT_TRUE haben und die *DwOption* von DBPROP_COL_NULLABLE gleich dbpropoptions_required ist. Die Spalte definiert ist, mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Identity-Eigenschaft und das DBPROP_COL_NULLABLE *DwStatus* Element wird auf DBPROPSTATUS_CONFLICTING gesetzt.|  
|DBPROP_COL_DEFAULT|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Erstellt eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] DEFAULT-Einschränkung für die Spalte.<br /><br /> Die *vValue* DBPROP-Element kann eine beliebige Anzahl von Typen. Die *vValue.vt* Member sollte einen Typ, der kompatibel mit dem Datentyp der Spalte angeben. Beispielsweise ist BSTR N/A als Standardwert für eine Spalte geeignet, die als DBTYPE_WSTR definiert ist. Definieren die gleiche Standard für eine Spalte, die als DBTYPE_R8 einen Fehler generiert, wenn der OLE DB-Treiber für SQL Server, zum Erstellen der Tabelle auf dem Server versucht definiert.|  
|DBPROP_COL_DESCRIPTION|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Die Spalteneigenschaft dbprop_col_description wird für SQL Server nicht vom OLE DB-Treiber implementiert.<br /><br /> Die *DwStatus* -Element der DBPROP-Struktur gibt DBPROPSTATUS_NOTSUPPORTED zurück, wenn der Consumer versucht, den Eigenschaftenwert zu schreiben.<br /><br /> Festlegen der Eigenschaft stellt keinen schwerwiegenden Fehler für den OLE DB-Treiber für SQL Server dar. Wenn alle anderen Parameterwerte gültig sind, wird die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Tabelle erstellt.|  
|DBPROP_COL_FIXEDLENGTH|R/w: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Der OLE DB-Treiber für SQL Server verwendet DBPROP_COL_FIXEDLENGTH, um die datentypzuordnung zu bestimmen, wann der Consumer einen Spaltendatentyp mithilfe definiert die *wType* Mitglied der dbcolumndesc-Struktur. Weitere Informationen finden Sie unter [Data Type Mapping itabledefinition](../../oledb/ole-db-data-types/data-type-mapping-in-itabledefinition.md).|  
|DBPROP_COL_NULLABLE|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Beim Erstellen der Tabelle überprüfen, ob der OLE DB-Treiber für SQL Server die Spalte Nullwerte akzeptieren soll, wenn die Eigenschaft festgelegt ist. Ist die Eigenschaft nicht festgelegt, wird durch die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ANSI_NULLS-Standarddatenbankoption festgelegt, ob die Spalte NULL-Werte akzeptiert.<br /><br /> Der OLE DB-Treiber für SQL Server ist ein ISO-kompatibler Anbieter. Verbundene Sitzungen weisen ISO-Verhalten auf. Wenn der Consumer DBPROP_COL_NULLABLE nicht festlegt, akzeptieren die Spalten NULL-Werte.|  
|DBPROP_COL_PRIMARYKEY|R/w: Lesen/Schreiben<br /><br /> Standardwert: VARIANT_FALSE Beschreibung: Wenn VARIANT_TRUE ist, erstellt der OLE DB-Treiber für SQL Server die Spalte mit einer PRIMARY KEY-Einschränkung.<br /><br /> Wenn sie als Spalteneigenschaft definiert ist, kann nur eine einzelne Spalte die Einschränkung bestimmen. Festlegen der Eigenschaft VARIANT_TRUE für mehr als eine einzelne Spalte einen Fehler zurückgibt, wenn der OLE DB-Treiber für SQL Server beim Erstellen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle.<br /><br /> Hinweis: Der Consumer können **iindexdefinition:: CreateIndex** PRIMARY KEY-Einschränkung auf zwei oder mehr Spalten zu erstellen.<br /><br /> Der OLE DB-Treiber für SQL Server gibt DB_S_ERRORSOCCURRED zurück, wenn sowohl DBPROP_COL_PRIMARYKEY als auch dbprop_col_unique den Wert VARIANT_TRUE haben und die *DwOption* von DBPROP_COL_UNIQUE ist nicht dbpropoptions_required ist.<br /><br /> DB_E_ERRORSOCCURRED wird zurückgegeben, wenn sowohl DBPROP_COL_PRIMARYKEY als auch dbprop_col_unique den Wert VARIANT_TRUE haben und die *DwOption* von DBPROP_COL_UNIQUE gleich dbpropoptions_required ist. Die Spalte definiert ist, mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Identity-Eigenschaft und das DBPROP_COL_PRIMARYKEY *DwStatus* Element wird auf DBPROPSTATUS_CONFLICTING gesetzt.<br /><br /> Der OLE DB-Treiber für SQL Server zurück einen Fehler, wenn sowohl DBPROP_COL_PRIMARYKEY als auch DBPROP_COL_NULLABLE den Wert VARIANT_TRUE haben.<br /><br /> Der OLE DB-Treiber für SQL Server gibt einen Fehler aus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Wenn der Consumer versucht, erstellen Sie eine PRIMARY KEY-Einschränkung für eine Spalte mit ungültigen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp. PRIMARY KEY-Einschränkungen können nicht definiert werden, für Spalten erstellt, mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen **Bit**, **Text**, **Ntext**, und **Image**.|  
|DBPROP_COL_UNIQUE|R/w: Lesen/Schreiben<br /><br /> Standardwert: VARIANT_FALSE Beschreibung: Wendet eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] UNIQUE-Einschränkung auf die Spalte an.<br /><br /> Wenn sie als Spalteneigenschaft definiert ist, wird die Einschränkung nur auf eine einzelne Spalte angewendet. Der Consumer können **iindexdefinition:: CreateIndex** um eine UNIQUE-Einschränkung auf kombinierte Werte von zwei oder mehr Spalten anzuwenden.<br /><br /> Der OLE DB-Treiber für SQL Server gibt DB_S_ERRORSOCCURRED zurück, wenn sowohl DBPROP_COL_PRIMARYKEY als auch dbprop_col_unique den Wert VARIANT_TRUE haben und *DwOption* ist nicht dbpropoptions_required ist.<br /><br /> DB_E_ERRORSOCCURRED wird zurückgegeben, wenn sowohl DBPROP_COL_PRIMARYKEY als auch dbprop_col_unique den Wert VARIANT_TRUE haben und *DwOption* gleich dbpropoptions_required ist. Die Spalte definiert ist, mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Identity-Eigenschaft und das DBPROP_COL_PRIMARYKEY *DwStatus* Element wird auf DBPROPSTATUS_CONFLICTING gesetzt.<br /><br /> Der OLE DB-Treiber für SQL Server gibt DB_S_ERRORSOCCURRED zurück, wenn sowohl DBPROP_COL_NULLABLE als auch dbprop_col_unique den Wert VARIANT_TRUE haben und *DwOption* ist nicht dbpropoptions_required ist.<br /><br /> DB_E_ERRORSOCCURRED wird zurückgegeben, wenn sowohl DBPROP_COL_NULLABLE als auch dbprop_col_unique den Wert VARIANT_TRUE haben und *DwOption* gleich dbpropoptions_required ist. Die Spalte definiert ist, mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Identity-Eigenschaft und das DBPROP_COL_NULLABLE *DwStatus* Element wird auf DBPROPSTATUS_CONFLICTING gesetzt.<br /><br /> Der OLE DB-Treiber für SQL Server gibt einen Fehler aus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Wenn der Consumer versucht, erstellen Sie eine UNIQUE-Einschränkung für eine Spalte mit ungültigen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datentyp. UNIQUE-Einschränkungen können nicht definiert werden, für Spalten erstellt, mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **Bit** -Datentyp.|  
  
 Wenn der Consumer ruft **itabledefinition:: CreateTable**, OLE DB-Treiber für SQL Server Tabelleneigenschaften wie folgt interpretiert.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/w: Lesen/Schreiben<br /><br /> Standardwert: VARIANT_FALSE Beschreibung: Standardmäßig wird der OLE DB-Treiber für SQL Server erstellt Tabellen, die vom Consumer benannt. Wenn VARIANT_TRUE, die OLE DB-Treiber für SQL Server generiert einen temporären Tabellennamen für den Consumer. Der Consumer legt den *pTableID* Parameter **CreateTable** auf NULL. Die *PpTableID* Parameter muss einen gültigen Zeiger enthalten.|  
  
 Wenn der Consumer fordert, dass ein Rowset für eine erfolgreich erstellte Tabelle geöffnet werden, wird der OLE DB-Treiber für SQL Server ein durch Cursor unterstütztes Rowset geöffnet. Alle Rowseteigenschaften können in den übergebenen Eigenschaftensätzen angegeben werden.  
  
 Mit diesem Beispiel wird eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Tabelle erstellt.  
  
```  
// This CREATE TABLE statement shows the details of the table created by   
// the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//    CONSTRAINT PK_OrderDetails  
//         PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
// The PRIMARY KEY constraint is created in an additional example.  
HRESULT CreateTable  
    (  
    ITableDefinition* pITableDefinition  
    )  
    {  
    DBID            dbidTable;  
    const ULONG     nCols = 5;  
    ULONG           nCol;  
    ULONG           nProp;  
    DBCOLUMNDESC    dbcoldesc[nCols];  
  
    HRESULT         hr;  
  
    // Set up column descriptions. First, set default property values for  
    //  the columns.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbcoldesc[nCol].pwszTypeName = NULL;  
        dbcoldesc[nCol].pTypeInfo = NULL;  
        dbcoldesc[nCol].rgPropertySets = new DBPROPSET;  
        dbcoldesc[nCol].pclsid = NULL;  
        dbcoldesc[nCol].cPropertySets = 1;  
        dbcoldesc[nCol].ulColumnSize = 0;  
        dbcoldesc[nCol].dbcid.eKind = DBKIND_NAME;  
        dbcoldesc[nCol].wType = DBTYPE_I4;  
        dbcoldesc[nCol].bPrecision = 0;  
        dbcoldesc[nCol].bScale = 0;  
  
        dbcoldesc[nCol].rgPropertySets[0].rgProperties =   
            new DBPROP[NCOLPROPS_MAX];  
        dbcoldesc[nCol].rgPropertySets[0].cProperties = NCOLPROPS_MAX;  
        dbcoldesc[nCol].rgPropertySets[0].guidPropertySet =  
            DBPROPSET_COLUMN;  
  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                dwOptions = DBPROPOPTIONS_REQUIRED;  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].colid  
                 = DB_NULLID;  
  
            VariantInit(  
                &(dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                    vValue));  
  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt = VT_BOOL;  
            }  
        }  
  
    // Set the column-specific information.  
    dbcoldesc[0].dbcid.uName.pwszName = L"OrderID";  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[0].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[1].dbcid.uName.pwszName = L"ProductID";  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[1].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[2].dbcid.uName.pwszName = L"UnitPrice";  
    dbcoldesc[2].wType = DBTYPE_CY;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[2].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[3].dbcid.uName.pwszName = L"Quantity";  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[3].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[4].dbcid.uName.pwszName = L"Discount";  
    dbcoldesc[4].wType = DBTYPE_NUMERIC;  
    dbcoldesc[4].bPrecision = 2;  
    dbcoldesc[4].bScale = 2;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].dwPropertyID =   
        DBPROP_COL_DEFAULT;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.vt = VT_BSTR;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.bstrVal =  
        SysAllocString(L"0");  
    dbcoldesc[4].rgPropertySets[0].cProperties = 2;  
  
    // Set up the dbid for OrderDetails.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    if (FAILED(hr = pITableDefinition->CreateTable(NULL, &dbidTable,  
        nCols, dbcoldesc, NULL, 0, NULL, NULL, NULL)))  
        {  
        DumpError(pITableDefinition, IID_ITableDefinition);  
        goto SAFE_EXIT;  
        }  
  
SAFE_EXIT:  
    // Clean up dynamic allocation in the property sets.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            if (dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt == VT_BSTR)  
                {  
                SysFreeString(dbcoldesc[nCol].rgPropertySets[0].  
                    rgProperties[nProp].vValue.bstrVal);  
                }  
            }  
  
        delete [] dbcoldesc[nCol].rgPropertySets[0].rgProperties;  
        delete [] dbcoldesc[nCol].rgPropertySets;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Indizes](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
