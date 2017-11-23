---
title: "Hinzufügen einer Spalte zu einer SQL Server-Tabelle | Microsoft Docs"
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
- AddColumn function
- SQL Server Native Client OLE DB provider, columns
- adding columns
ms.assetid: 22bae18a-bc9d-4617-8660-ed8b17a468d4
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 42ee958f2647a03745259b4a3b975309d515f321
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Hinzufügen einer Spalte zu einer SQL Server-Tabelle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht die **addColumn** Funktion. Dieser Funktion können Consumer eine Spalte Hinzufügen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle.  
  
 Beim Hinzufügen einer Spalteninhalts in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Consumer der Native Client OLE DB-Anbieter wird wie folgt eingeschränkt:  
  
-   Wenn DBPROP_COL_AUTOINCREMENT VARIANT_TRUE ist, muss DBPROP_COL_NULLABLE VARIANT_FALSE sein.  
  
-   Wenn die Spalte, mithilfe definiert wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Zeitstempel** -Datentyp, muss DBPROP_COL_NULLABLE VARIANT_FALSE sein.  
  
-   Für alle anderen Spaltendefinitionen muss DBPROP_COL_NULLABLE  VARIANT_TRUE sein.  
  
 Consumer geben den Tabellennamen als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *pTableID* Parameter. Die *eKind* Mitglied *pTableID* muss DBKIND_NAME sein.  
  
 Der neue Spaltenname wird angegeben, als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *Dbcid* Elements des DBCOLUMNDESC-Parameters *pColumnDesc*. Die *eKind* -Element muss DBKIND_NAME sein.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Indizes](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
