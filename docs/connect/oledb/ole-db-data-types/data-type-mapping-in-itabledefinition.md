---
title: Datentypzuordnung itabledefinition | Microsoft Docs
description: Datentypzuordnung itabledefinition
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- OLE DB Driver for SQL Server, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34c222d455be68ab8ce96d343593a80f66c94d7d
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="data-type-mapping-in-itabledefinition"></a>Datentypzuordnung zu ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Beim Erstellen von Tabellen mit der **itabledefinition:: CreateTable** -Funktion, die OLE DB-Treiber für SQL Server-Consumer festlegbaren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen in der *PwszTypeName* Mitglied der DBCOLUMNDESC-Arrays, übergeben wird. Wenn der Consumer den Datentyp einer Spalte namentlich angibt, OLE DB-datentypzuordnung, dargestellt durch die *wType* Element der DBCOLUMNDESC-Struktur wird ignoriert.  
  
 Beim Angeben von Datentypen neuer Spalten mit OLE DB-Datentypen, die mit der DBCOLUMNDESC-Struktur *wType* Member auf, der der OLE DB-Treiber für SQL Server OLE DB-Datentypen folgendermaßen zugeordnet.  
  
|OLE DB-Datentyp|SQL Server<br /><br /> Datentyp|Zusätzliche Informationen|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binäre**, **Varbinary**, **Bild** oder **varbinary(max)**|Der OLE DB-Treiber für SQL Server überprüft die *UlColumnSize* -Element der DBCOLUMNDESC-Struktur. Basierend auf den Wert und die Version der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Instanz, die OLE DB-Treiber für SQL Server wird den Typ, der zugeordnet **Image**.<br /><br /> Wenn der Wert der *UlColumnSize* ist kleiner als die maximale Länge von einer **binäre** Spalte vom Datentyp, und klicken Sie dann den OLE DB-Treiber für SQL Server der dbcolumndesc-Struktur untersucht *RgPropertySets*Member. Wenn DBPROP_COL_FIXEDLENGTH den Wert VARIANT_TRUE aufweist, ordnet der OLE DB-Treiber für SQL Server den Typ **binäre**. Wenn der Wert der Eigenschaft VARIANT_FALSE ist, ordnet der OLE DB-Treiber für SQL Server den Typ **Varbinary**. In beiden Fällen wird der dbcolumndesc-Struktur *UlColumnSize* Element bestimmt die Breite der SQL Server-Spalte erstellt.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|Der OLE DB-Treiber für SQL Server überprüft das DBCOLUMDESC *bPrecision* und *bScale* Elemente zum Bestimmen von Genauigkeit und Skalierung für die **numerischen** Spalte.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**Char**, **Varchar**, **Text** oder **varchar(max)**|Der OLE DB-Treiber für SQL Server überprüft die *UlColumnSize* -Element der DBCOLUMNDESC-Struktur. Basierend auf den Wert und die Version der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Instanz, die OLE DB-Treiber für SQL Server wird den Typ, der zugeordnet **Text**.<br /><br /> Wenn der Wert der *UlColumnSize* ist kleiner als die maximale Länge von einer Multibytezeichen-Datentypspalte, und klicken Sie dann auf die OLE DB-Treiber für SQL Server der dbcolumndesc-Struktur übergebenen *RgPropertySets* Member. Wenn DBPROP_COL_FIXEDLENGTH den Wert VARIANT_TRUE aufweist, ordnet der OLE DB-Treiber für SQL Server den Typ **Char**. Wenn der Wert der Eigenschaft VARIANT_FALSE ist, ordnet der OLE DB-Treiber für SQL Server den Typ **Varchar**. In beiden Fällen wird der dbcolumndesc-Struktur *UlColumnSize* Element bestimmt die Breite der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Spalte erstellt.|  
|DBTYPE_UDT|**UDT**|Die folgende Informationen werden in **DBCOLUMNDESC** von Strukturen **itabledefinition:: CreateTable** Wenn UDT-Spalten erforderlich sind:<br /><br /> *PwSzTypeName* wird ignoriert.<br /><br /> *RgPropertySets* umfasst eine **DBPROPSET_SQLSERVERCOLUMN** -Eigenschaft festgelegt wird, wie beschrieben im Abschnitt auf **DBPROPSET_SQLSERVERCOLUMN**im [Defined Types ](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**NCHAR**, **Nvarchar**, **Ntext** oder **nvarchar(max)**|Der OLE DB-Treiber für SQL Server überprüft die *UlColumnSize* -Element der DBCOLUMNDESC-Struktur. Anhand des Werts, ordnet der OLE DB-Treiber für SQL Server den Typ **Ntext**.<br /><br /> Wenn der Wert der *UlColumnSize* ist kleiner als die maximale Länge von einem Unicode-Zeichen-Datentypspalte, und klicken Sie dann auf den OLE DB-Treiber für SQL Server der dbcolumndesc-Struktur übergebenen *RgPropertySets* Member. Wenn DBPROP_COL_FIXEDLENGTH den Wert VARIANT_TRUE aufweist, ordnet der OLE DB-Treiber für SQL Server den Typ **Nchar**. Wenn der Wert der Eigenschaft VARIANT_FALSE ist, ordnet der OLE DB-Treiber für SQL Server den Typ **Nvarchar**. In beiden Fällen wird der dbcolumndesc-Struktur *UlColumnSize* Element bestimmt die Breite der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Spalte erstellt.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Wenn Sie eine neue Tabelle erstellen, ordnet der OLE DB-Treiber für SQL Server nur die OLE DB-Typ Enumeration Datenwerte in der obigen Tabelle angegeben. Durch den Versuch, eine Tabelle mit einer Spalte eines anderen OLE DB-Datentyps zu erstellen, wird ein Fehler erzeugt.  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40; OLE DB &#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
