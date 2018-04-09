---
title: SQL Server-Indizes erstellen | Microsoft Docs
description: Erstellen von SQL Server-Indizes, die mithilfe von OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
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
- CreateIndex function
- constraints [OLE DB]
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
- adding indexes
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e25313832eb7b16fb3febd2755c7944805f5ac5
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="creating-sql-server-indexes"></a>Erstellen von SQL Server-Indizes
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server macht die **iindexdefinition:: CreateIndex** -Funktion, ermöglicht es Consumern, neue Indizes für definieren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabellen.  
  
 Der OLE DB-Treiber für SQL Server erstellt Tabellenindizes entweder als Indizes oder Einschränkungen. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gewährt dem Tabellenbesitzer, Datenbankbesitzer und Mitgliedern bestimmter Administratorrollen die Berechtigung zum Erstellen von Einschränkungen. Standardmäßig kann nur der Tabellenbesitzer einen Index für eine Tabelle erstellen. Aus diesem Grund den Erfolg oder Misserfolg des **CreateIndex** abhängig ist, nicht nur auf die Zugriffsrechte des Anwendungsbenutzers, sondern auch von der Art des erstellten Indexes.  
  
 Consumer geben den Tabellennamen als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *pTableID* Parameter. Die *eKind* Mitglied *pTableID* muss DBKIND_NAME sein.  
  
 Die *pIndexID* Parameter kann NULL sein, und wenn dies der Fall, erstellt der OLE DB-Treiber für SQL Server einen eindeutigen Namen für den Index. Der Consumer kann den Namen des Indexes durch einen gültigen Zeiger auf eine DBID im Erfassen der *PpIndexID* Parameter.  
  
 Der Consumer kann den Indexnamen als Unicode-Zeichenfolge in angeben der *PwszName* Mitglied der *uName* der union der *pIndexID* Parameter. Die *eKind* Mitglied *pIndexID* muss DBKIND_NAME sein.  
  
 Der Consumer gibt die Spalte oder die Spalten an, die namentlich in den Index einbezogen werden. Für jede DBINDEXCOLUMNDESC-Struktur, die verwendet werden, **CreateIndex**, *eKind* Mitglied der *pColumnID* muss DBKIND_NAME sein. Der Name der Spalte wird angegeben, als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *pColumnID*.  
  
 Der OLE DB-Treiber für SQL Server und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützen die aufsteigende Reihenfolge auf die Werte im Index. Der OLE DB-Treiber für SQL Server gibt E_INVALIDARG zurück, wenn der Consumer die Spalte in einer DBINDEXCOLUMNDESC-Struktur gibt.  
  
 **CreateIndex** interpretiert Indexeigenschaften wie folgt.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Der OLE DB-Treiber für SQL Server unterstützt diese Eigenschaft nicht. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_CLUSTERED|R/w: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Steuert die Indexgruppierung.<br /><br /> VARIANT_TRUE: Der OLE DB-Treiber für SQL Server versucht, zum Erstellen eines gruppierten Indexes auf die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt maximal einen gruppierten Index pro Tabelle.<br /><br /> VARIANT_FALSE: Der OLE DB-Treiber für SQL Server versucht, zum Erstellen eines nicht gruppierten Indexes auf die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle.|  
|DBPROP_INDEX_FILLFACTOR|R/w: Lesen/Schreiben<br /><br /> Standard: 0<br /><br /> Beschreibung: Gibt den Prozentsatz einer für Speicher verwendeten Indexseite an. Weitere Informationen finden Sie unter [CREATE INDEX](../../../t-sql/statements/create-index-transact-sql.md).<br /><br /> Der Typ der Variante ist VT_I4. Der Wert muss größer als oder gleich 1 und kleiner als oder gleich 100 sein.|  
|DBPROP_INDEX_INITIALIZE|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Der OLE DB-Treiber für SQL Server unterstützt diese Eigenschaft nicht. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_NULLCOLLATION|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Der OLE DB-Treiber für SQL Server unterstützt diese Eigenschaft nicht. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_NULLS|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Der OLE DB-Treiber für SQL Server unterstützt diese Eigenschaft nicht. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_PRIMARYKEY|R/w: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE Beschreibung: Erstellt den Index als PRIMARY KEY-Einschränkung mit referenzieller Integrität.<br /><br /> VARIANT_TRUE: Der Index wird erstellt, um die PRIMARY KEY-Einschränkung der Tabelle zu unterstützen. Die Spalten dürfen keine NULL-Werte zulassen.<br /><br /> VARIANT_FALSE: Der Index wird nicht als PRIMARY KEY-Einschränkung für Zeilenwerte in der Tabelle verwendet.|  
|DBPROP_INDEX_SORTBOOKMARKS|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Der OLE DB-Treiber für SQL Server unterstützt diese Eigenschaft nicht. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_TEMPINDEX|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Der OLE DB-Treiber für SQL Server unterstützt diese Eigenschaft nicht. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_TYPE|R/w: Lesen/Schreiben<br /><br /> Standard: keiner<br /><br /> Beschreibung: Der OLE DB-Treiber für SQL Server unterstützt diese Eigenschaft nicht. Versucht, die Eigenschaft festzulegen, **CreateIndex** verursachen einen DB_S_ERRORSOCCURRED-Rückgabewert. Die *DwStatus* -Element der Eigenschaftsstruktur gibt dbpropstatus_badvalue an.|  
|DBPROP_INDEX_UNIQUE|R/w: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Erstellt den Index als UNIQUE-Einschränkung für die einbezogene(n) Spalte oder Spalten.<br /><br /> VARIANT_TRUE: Der Index wird verwendet, um Zeilenwerte in der Tabelle eindeutig einzuschränken.<br /><br /> VARIANT_FALSE: Der Index schränkt Zeilenwerte nicht eindeutig ein.|  
  
 Im anbieterspezifischen Eigenschaftensatz DBPROPSET_SQLSERVERINDEX definiert der OLE DB-Treiber für SQL Server die folgende Eigenschaft für Datenquelleninformationen.  
  
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
 [Tabellen und Indizes](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
