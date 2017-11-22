---
title: Entfernen einer Spalte aus einer SQL Server-Tabelle | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e07945062153d260d9f188fcffcb76fb7adb45aa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="removing-a-column-from-a-sql-server-table"></a>Entfernen einer Spalte aus einer SQL Server-Tabelle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht die **Dropcolumn** Funktion. Dies ermöglicht es Consumern, entfernen Sie eine Spalte aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle.  
  
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
 [Tabellen und Indizes](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
