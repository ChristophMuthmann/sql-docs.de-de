---
title: Entfernen einer Spalte aus einer SQL Server-Tabelle | Microsoft Docs
description: Entfernen einer Spalte aus einer SQL Server-Tabelle, die mithilfe von OLE DB-Treiber für SQL Server
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
- columns [OLE DB]
- removing columns
- DropColumn function
- OLE DB Driver for SQL Server, columns
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c5a0d279c4d44ba11a6b87223afedc99183c488
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="removing-a-column-from-a-sql-server-table"></a>Entfernen einer Spalte aus einer SQL Server-Tabelle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server macht die **Dropcolumn** Funktion. Dies ermöglicht es Consumern, entfernen Sie eine Spalte aus einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle.  
  
 Consumer geben den Tabellennamen als Unicode-Zeichenfolge in der *PwszName*Mitglied der *uName* -Vereinigung der *pTableID* Parameter. Die *eKind*Mitglied *pTableID* muss DBKIND_NAME sein.  
  
 Der Consumer gibt einen Spaltennamen in der *PwszName*Mitglied der *uName* -Vereinigung der *pColumnID* Parameter. Der Spaltenname ist eine Unicode-Zeichenfolge. Die *eKind* Mitglied *pColumnID* muss DBKIND_NAME sein.  
  
## <a name="example"></a>Beispiel  
  
### <a name="code"></a>Code  
  
```  
DBID TableID;  
DBID ColumnID;  
HRESULT hr;  
  
TableID.eKind = DBKIND_NAME;  
TableID.uName.pwszName = L"MyTableName";  
  
ColumnID.eKind = DBKIND_NAME;  
ColumnID.uName.pwszName = L"MyColumnName";  
  
hr = m_pITableDefinition->DropColumn(&TableID, &ColumnID);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Indizes](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
