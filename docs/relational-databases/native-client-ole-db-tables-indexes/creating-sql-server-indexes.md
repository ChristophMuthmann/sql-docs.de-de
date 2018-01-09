---
title: SQL Server-Indizes erstellen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
- adding indexes
ms.assetid: 6239d440-2818-4b98-bb79-732dced41952
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 395992ef9885bd38f72e8b18699a6fcbe11016aa
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="creating-sql-server-indexes"></a>Erstellen von SQL Server-Indizes
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht die **iindexdefinition:: CreateIndex** -Funktion, ermöglicht es Consumern, neue Indizes für definieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabellen.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter erstellt Tabellenindizes entweder als Indizes oder Einschränkungen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gewährt dem Tabellenbesitzer, Datenbankbesitzer und Mitgliedern bestimmter Administratorrollen die Berechtigung zum Erstellen von Einschränkungen. Standardmäßig kann nur der Tabellenbesitzer einen Index für eine Tabelle erstellen. Aus diesem Grund den Erfolg oder Misserfolg des **CreateIndex** abhängig ist, nicht nur auf die Zugriffsrechte des Anwendungsbenutzers, sondern auch von der Art des erstellten Indexes.  
  
 Consumer geben den Tabellennamen als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *pTableID* Parameter. Die *eKind* Mitglied *pTableID* muss DBKIND_NAME sein.  
  
 Die *pIndexID* Parameter kann NULL sein, und wenn dies der Fall, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter erstellt einen eindeutigen Namen für den Index. Der Consumer kann den Namen des Indexes durch einen gültigen Zeiger auf eine DBID im Erfassen der *PpIndexID* Parameter.  
  
 Der Consumer kann den Indexnamen als Unicode-Zeichenfolge in angeben der *PwszName* Mitglied der *uName* der union der *pIndexID* Parameter. Die *eKind* Mitglied *pIndexID* muss DBKIND_NAME sein.  
  
 Der Consumer gibt die Spalte oder die Spalten an, die namentlich in den Index einbezogen werden. Für jede DBINDEXCOLUMNDESC-Struktur, die verwendet werden, **CreateIndex**, *eKind* Mitglied der *pColumnID* muss DBKIND_NAME sein. Der Name der Spalte wird angegeben, als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *pColumnID*.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen die aufsteigende Reihenfolge auf die Werte im Index. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter gibt E_INVALIDARG zurück, wenn der Consumer die Spalte in einer DBINDEXCOLUMNDESC-Struktur gibt.  
  
 **CreateIndex** interpretiert Indexeigenschaften wie folgt.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter diese Eigenschaft nicht unterstützt. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_CLUSTERED|R/w: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Steuert die Indexgruppierung.<br /><br /> VARIANT_TRUE: Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter versucht, einen gruppierten Index erstellen, auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt maximal einen gruppierten Index pro Tabelle.<br /><br /> VARIANT_FALSE: Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter versucht, erstellen Sie einen nicht gruppierten Index auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle.|  
|DBPROP_INDEX_FILLFACTOR|R/w: Lesen/Schreiben<br /><br /> Standard: 0<br /><br /> Beschreibung: Gibt den Prozentsatz einer für Speicher verwendeten Indexseite an. Weitere Informationen finden Sie unter [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md).<br /><br /> Der Typ der Variante ist VT_I4. Der Wert muss größer als oder gleich 1 und kleiner als oder gleich 100 sein.|  
|DBPROP_INDEX_INITIALIZE|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter diese Eigenschaft nicht unterstützt. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_NULLCOLLATION|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter diese Eigenschaft nicht unterstützt. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_NULLS|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter diese Eigenschaft nicht unterstützt. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_PRIMARYKEY|R/w: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE Beschreibung: Erstellt den Index als PRIMARY KEY-Einschränkung mit referenzieller Integrität.<br /><br /> VARIANT_TRUE: Der Index wird erstellt, um die PRIMARY KEY-Einschränkung der Tabelle zu unterstützen. Die Spalten dürfen keine NULL-Werte zulassen.<br /><br /> VARIANT_FALSE: Der Index wird nicht als PRIMARY KEY-Einschränkung für Zeilenwerte in der Tabelle verwendet.|  
|DBPROP_INDEX_SORTBOOKMARKS|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter diese Eigenschaft nicht unterstützt. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_TEMPINDEX|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter diese Eigenschaft nicht unterstützt. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_TYPE|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter diese Eigenschaft nicht unterstützt. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_UNIQUE|R/w: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Erstellt den Index als UNIQUE-Einschränkung für die einbezogene(n) Spalte oder Spalten.<br /><br /> VARIANT_TRUE: Der Index wird verwendet, um Zeilenwerte in der Tabelle eindeutig einzuschränken.<br /><br /> VARIANT_FALSE: Der Index schränkt Zeilenwerte nicht eindeutig ein.|  
  
 Im anbieterspezifischen Eigenschaftensatz DBPROPSET_SQLSERVERINDEX der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter definiert die folgende Eigenschaft für Datenquelleninformationen.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|Typ: VT_BOOL (R/W)<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Wenn diese Eigenschaft mit dem Wert VARIANT_TRUE mit IIndexDefinition::CreateIndex angegeben wird, wird ein primärer XML-Index erstellt, der der zu indizierenden Spalte entspricht. Wenn diese Eigenschaft VARIANT_TRUE ist, sollte cIndexColumnDescs 1 sein; andernfalls tritt ein Fehler auf.|  
  
 In diesem Beispiel wird ein Primärschlüsselindex erstellt:  
  
```  
// This CREATE TABLE statement shows the referential integrity and   
// PRIMARY KEY constraint on the OrderDetails table that will be created   
// by the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//        CONSTRAINT PK_OrderDetails  
//        PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
HRESULT CreatePrimaryKey  
    (  
    IIndexDefinition* pIIndexDefinition  
    )  
    {  
    HRESULT             hr = S_OK;  
  
    DBID                dbidTable;  
    DBID                dbidIndex;  
    const ULONG         nCols = 2;  
    ULONG               nCol;  
    const ULONG         nProps = 2;  
    ULONG               nProp;  
  
    DBINDEXCOLUMNDESC   dbidxcoldesc[nCols];  
    DBPROP              dbpropIndex[nProps];  
    DBPROPSET           dbpropset;  
  
    DBID*               pdbidIndexOut = NULL;  
  
    // Set up identifiers for the table and index.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    dbidIndex.eKind = DBKIND_NAME;  
    dbidIndex.uName.pwszName = L"PK_OrderDetails";  
  
    // Set up column identifiers.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbidxcoldesc[nCol].pColumnID = new DBID;  
        dbidxcoldesc[nCol].pColumnID->eKind = DBKIND_NAME;  
  
        dbidxcoldesc[nCol].eIndexColOrder = DBINDEX_COL_ORDER_ASC;  
        }  
    dbidxcoldesc[0].pColumnID->uName.pwszName = L"OrderID";  
    dbidxcoldesc[1].pColumnID->uName.pwszName = L"ProductID";  
  
    // Set properties for the index. The index is clustered,  
    // PRIMARY KEY.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        dbpropIndex[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        dbpropIndex[nProp].colid = DB_NULLID;  
  
        VariantInit(&(dbpropIndex[nProp].vValue));  
  
        dbpropIndex[nProp].vValue.vt = VT_BOOL;  
        }  
    dbpropIndex[0].dwPropertyID = DBPROP_INDEX_CLUSTERED;  
    dbpropIndex[0].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropIndex[1].dwPropertyID = DBPROP_INDEX_PRIMARYKEY;  
    dbpropIndex[1].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropset.rgProperties = dbpropIndex;  
    dbpropset.cProperties = nProps;  
    dbpropset.guidPropertySet = DBPROPSET_INDEX;  
  
    hr = pIIndexDefinition->CreateIndex(&dbidTable, &dbidIndex, nCols,  
        dbidxcoldesc, 1, &dbpropset, &pdbidIndexOut);  
  
    // Clean up dynamically allocated DBIDs.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        delete dbidxcoldesc[nCol].pColumnID;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Indizes](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
