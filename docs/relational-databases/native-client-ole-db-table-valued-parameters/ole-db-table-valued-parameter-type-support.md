---
title: Unterstützung des OLE DB-Tabellenwertparameter-Typ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
ms.assetid: 147036a0-260e-4f81-8b3b-89209e023a32
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c5e3643eb70e25a9725c439c2375fe4c633aa760
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-table-valued-parameter-type-support"></a>OLE DB-Typunterstützung für Tabellenwertparameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In diesem Thema wird die OLE DB-Typunterstützung für Tabellenwertparameter beschrieben.  
  
## <a name="table-valued-parameter-rowset-object"></a>Tabellenwertparameter-Rowsetobjekt  
 Sie können ein spezielles Rowsetobjekt für Tabellenwertparameter erstellen. Sie erstellen das Tabellenwertparameter-Rowsetobjekt mit ITableDefinitionWithConstraints::CreateTableWithConstraints oder IOpenRowset:: OPENROWSET. Zu diesem Zweck legen Sie die *eKind* Mitglied der *pTableID* -Parameters auf dbkind_guid_name fest, und geben Sie die CLSID_ROWSET_INMEMORY der *Guid* Member. Der servertypname für den Tabellenwertparameter muss angegeben werden, der *PwszName* Mitglied *pTableID* Verwendung IOpenRowset:: OPENROWSET. Das Tabellenwertparameter-Rowsetobjekt verhält sich wie ein reguläres Objekt des OLE DB-Anbieters von SQL Server Native Client.  
  
```  
const GUID CLSID_ROWSET_TVP =   
{0xc7ef28d5, 0x7bee, 0x443f, {0x86, 0xda, 0xe3, 0x98, 0x4f, 0xcd, 0x4d, 0xf9}};  
  
CoType RowsetTVP  
{  
[mandatory] interface IAccessor;  
[mandatory] interface IColumnsInfo;  
[mandatory] interface IConvertType;  
[mandatory] interface IRowset;  
[mandatory] interface IRowsetInfo;  
[optional]  interface IColumnsRowset;  
[optional]  interface IRowsetChange;  
[optional]  interface ISupportErrorInfo;  
};  
```  
  
## <a name="dbtypetable"></a>DBTYPE_TABLE  
 Der neue Typ DBTYPE_TABLE stellt einen Tabellentyp dar. Dieser Typ gibt Tabellenwertparameter in verschiedenen OLE DB-Schnittstellen an, wo ein DBTYPE erforderlich ist.  
  
```  
#define DBTYPE_TABLE (143)  
```  
  
 DBTYPE_TABLE hat das gleiche Format wie DBTYPE_IUNKNOWN. Es ist ein Zeiger auf ein Objekt im Datenpuffer. Für die vollständige Spezifikation in den Bindungen füllt der Consumer den DBOBJECT-Puffer mit *Iid* auf eine der Schnittstellen des Rowsetobjekts (IID_IRowset) festgelegt. Wenn DBOBJECT in den Bindungen angegeben wird, wird der IID_IRowset davon ausgegangen werden.  
  
 Konvertierungen zu und von DBTYPE_TABLE für andere Typen werden nicht unterstützt. IConvertType::CanConvert gibt S_FALSE für nicht unterstützte Konvertierung für jede Anforderung als DBTYPE_TABLE an DBTYPE_TABLE Konvertierung zurück. Dies geht davon aus DBCONVERTFLAGS_PARAMETER für das Command-Objekt.  
  
## <a name="methods"></a>Methoden  
 Weitere Informationen zu OLE DB-Methoden, die Tabellenwertparameter unterstützen, finden Sie unter [OLE DB Table-Valued Parameter unterstützt &#40;Methoden&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md).  
  
## <a name="properties"></a>Eigenschaften  
 Weitere Informationen zu OLE DB-Eigenschaften, die Tabellenwertparameter unterstützen, finden Sie unter [OLE DB Table-Valued Parameter unterstützt &#40;Eigenschaften&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenwertparameter &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Verwenden des Table-Valued Parameters & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
