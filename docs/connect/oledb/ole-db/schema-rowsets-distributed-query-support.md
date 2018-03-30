---
title: Unterstützung für verteilte Abfragen in Schemarowsets | Microsoft Docs
description: Unterstützung für verteilte Abfragen in Schemarowsets
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a1ac686e4dc9da7dee3b444adfbcbda801901d0
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="schema-rowsets---distributed-query-support"></a>Schemarowsets - Unterstützung für verteilte Abfragen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Zur Unterstützung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verteilte Abfragen, die OLE DB-Treiber für SQL Server **IDBSchemaRowset** Schnittstelle gibt Metadaten zu Verbindungsservern auf.  
  
 Wenn die DBPROPSET_SQLSERVERSESSION-Eigenschaft SSPROP_QUOTEDCATALOGNAMES auf VARIANT_TRUE festgelegt wurde, kann für den Katalognamen ein Bezeichner in Anführungszeichen angegeben werden (beispielsweise "my.catalog"). Bei der Ausgabe eines Schemarowsets anhand des Katalogs zu beschränken, erkennt der OLE DB-Treiber für SQL Server einen zweiteiligen Namen mit dem Verbindungsserver und der Name des Katalogs. Angeben von für die Schemarowsets in der folgenden Tabelle, eine mit dem zweiteiligen Katalognamens in Form *Linked_server***.*** Katalog* Ausgabe an den betreffenden Katalog des genannten Verbindungsservers beschränkt.  
  
|Schemarowset|Katalogeinschränkung|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  Um ein Schemarowset auf alle Kataloge eines Verbindungsservers zu beschränken, verwenden Sie die Syntax *Linked_server* (wobei Punkts als Trennzeichen Teil der namensspezifikation ist). Diese Syntax ist gleichbedeutend mit der Angabe von NULL für die Katalognamensbeschränkung und wird auch verwendet, wenn der Verbindungsserver eine Datenquelle angibt, die Kataloge nicht unterstützt.  
  
 Der OLE DB-Treiber für SQL Server definiert das Schemarowset LINKEDSERVERS, Rückgabe einer Liste von OLE DB-Datenquellen, die als Verbindungsserver registriert.  
  
## <a name="see-also"></a>Siehe auch  
 [Schemarowset-Unterstützung &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS-Rowset &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
