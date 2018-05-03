---
title: Hinzufügen einer Spalte zu einer SQL Server-Tabelle | Microsoft Docs
description: Hinzufügen einer Spalte in einer SQL Server-Tabelle, die mithilfe von OLE DB-Treiber für SQL Server
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
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 32e128d22fb79875704292e80fe7c77aa3b17b6d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Hinzufügen einer Spalte zu einer SQL Server-Tabelle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server macht die **addColumn** Funktion. Dieser Funktion können Consumer eine Spalte Hinzufügen einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle.  
  
 Wenn Sie eine Spalte Hinzufügen einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle, die OLE DB-Treiber für SQL Server-Consumer wie folgt beschränkt ist:  
  
-   Wenn DBPROP_COL_AUTOINCREMENT VARIANT_TRUE ist, muss DBPROP_COL_NULLABLE VARIANT_FALSE sein.  
  
-   Wenn die Spalte, mithilfe definiert wird der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **Zeitstempel** -Datentyp, muss DBPROP_COL_NULLABLE VARIANT_FALSE sein.  
  
-   Für alle anderen Spaltendefinitionen muss DBPROP_COL_NULLABLE  VARIANT_TRUE sein.  
  
 Consumer geben den Tabellennamen als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *pTableID* Parameter. Die *eKind* Mitglied *pTableID* muss DBKIND_NAME sein.  
  
 Der neue Spaltenname wird angegeben, als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *Dbcid* Elements des DBCOLUMNDESC-Parameters *pColumnDesc*. Die *eKind* -Element muss DBKIND_NAME sein.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Indizes](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
