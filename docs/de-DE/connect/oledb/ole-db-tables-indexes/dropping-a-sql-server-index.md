---
title: Löschen eines SQL Server-Index | Microsoft Docs
description: Löschen eines Sql Server-Index mithilfe von OLE DB-Treiber für SQL Server
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
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: fcca3d266ae8ec5415e0affb29f64b085bdb2829
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dropping-a-sql-server-index"></a>Löschen eines SQL Server-Index

  Der OLE DB-Treiber für SQL Server macht die **Iindexdefinition** Funktion. Dies ermöglicht es Consumern, entfernen Sie einen Index aus einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle.  
  
 Der OLE DB-Treiber für SQL Server stellt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PRIMARY KEY- und UNIQUE-Einschränkungen als Indizes. Der Tabellenbesitzer, Datenbankbesitzer und einige Mitglieder der Administratorrolle können ändern, eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle Löschen einer Einschränkung. Standardmäßig kann nur der Tabellenbesitzer einen vorhandenen Index löschen. Aus diesem Grund **DropIndex** Erfolg oder Misserfolg hängt nicht nur von Zugriffsrechte des Anwendungsbenutzers, sondern auch für den Typ des angegebenen Index ab.  
  
 Consumer geben den Tabellennamen als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *pTableID* Parameter. Die *eKind* Mitglied *pTableID* muss DBKIND_NAME sein.  
  
 Consumer geben den Indexnamen als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *pIndexID* Parameter. Die *eKind* Mitglied *pIndexID* muss DBKIND_NAME sein. Der OLE DB-Treiber für SQL Server unterstützt nicht die OLE DB-Funktion von löschen alle Indizes für eine Tabelle beim *pIndexID* ist null. Wenn *pIndexID* ist null, wird E_INVALIDARG zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Indizes](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
