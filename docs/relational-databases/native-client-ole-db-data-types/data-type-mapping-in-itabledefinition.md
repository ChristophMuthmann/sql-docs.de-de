---
title: Datentypzuordnung itabledefinition | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- SQL Server Native Client OLE DB provider, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
ms.assetid: 13292d1f-c17e-4d11-bf98-3460a10cbb18
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f87118e72b1ab36a72c8ee28369551792e37d677
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-mapping-in-itabledefinition"></a>Datentypzuordnung zu ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Beim Erstellen von Tabellen mithilfe der **itabledefinition:: CreateTable** -Funktion, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter-Consumer kann angeben, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datentypen in der *PwszTypeName* Elements des DBCOLUMNDESC-Arrays, das übergeben wird. Wenn der Consumer den Datentyp einer Spalte namentlich angibt, OLE DB-datentypzuordnung, dargestellt durch die *wType* Element der DBCOLUMNDESC-Struktur wird ignoriert.  
  
 Beim Angeben von Datentypen neuer Spalten mit OLE DB-Datentypen, die mit der DBCOLUMNDESC-Struktur *wType* Member auf, der die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter OLE DB-Datentypen folgendermaßen zugeordnet.  
  
|OLE DB-Datentyp|SQL Server<br /><br /> Datentyp|Zusätzliche Informationen|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binäre**, **Varbinary**, **Bild** oder **varbinary(max)**|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter überprüft die *UlColumnSize* -Element der DBCOLUMNDESC-Struktur. Basierend auf den Wert und die Version der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter ordnet den Typ **Image**.<br /><br /> Wenn der Wert der *UlColumnSize* ist kleiner als die maximale Länge des eine **binäre** -Datentypspalte, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter überprüft der dbcolumndesc-Struktur *RgPropertySets* Member. Wenn DBPROP_COL_FIXEDLENGTH den Wert VARIANT_TRUE, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter ordnet den Typ **binäre**. Wenn der Wert der Eigenschaft VARIANT_TRUE, dann ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter ordnet den Typ **Varbinary**. In beiden Fällen wird der dbcolumndesc-Struktur *UlColumnSize* Element bestimmt die Breite der SQL Server-Spalte erstellt.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter überprüft das DBCOLUMDESC *bPrecision* und *bScale* Elemente zum Bestimmen von Genauigkeit und Skalierung für die **numerischen** Spalte.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**Char**, **Varchar**, **Text** oder **varchar(max)**|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter überprüft die *UlColumnSize* -Element der DBCOLUMNDESC-Struktur. Basierend auf den Wert und die Version der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter ordnet den Typ **Text**.<br /><br /> Wenn der Wert der *UlColumnSize* ist kleiner als die maximale Länge von einer Multibytezeichen-Datentypspalte, und klicken Sie dann die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter überprüft der dbcolumndesc-Struktur *RgPropertySets* Member. Wenn DBPROP_COL_FIXEDLENGTH den Wert VARIANT_TRUE, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter ordnet den Typ **Char**. Wenn der Wert der Eigenschaft VARIANT_TRUE, dann ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter ordnet den Typ **Varchar**. In beiden Fällen wird der dbcolumndesc-Struktur *UlColumnSize* Element bestimmt die Breite der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Spalte erstellt.|  
|DBTYPE_UDT|**UDT**|Die folgende Informationen werden in **DBCOLUMNDESC** von Strukturen **itabledefinition:: CreateTable** Wenn UDT-Spalten erforderlich sind:<br /><br /> *PwSzTypeName* wird ignoriert.<br /><br /> *RgPropertySets* umfasst eine **DBPROPSET_SQLSERVERCOLUMN** -Eigenschaft festgelegt wird, wie beschrieben im Abschnitt auf **DBPROPSET_SQLSERVERCOLUMN**im [Defined Types ](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**NCHAR**, **Nvarchar**, **Ntext** oder **nvarchar(max)**|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter überprüft die *UlColumnSize* -Element der DBCOLUMNDESC-Struktur. Anhand des Werts der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter ordnet den Typ **Ntext**.<br /><br /> Wenn der Wert der *UlColumnSize* ist kleiner als die maximale Länge von einem Unicode-Zeichen-Datentypspalte, und klicken Sie dann die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter überprüft der dbcolumndesc-Struktur *RgPropertySets* Member. Wenn DBPROP_COL_FIXEDLENGTH den Wert VARIANT_TRUE, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter ordnet den Typ **Nchar**. Wenn der Wert der Eigenschaft VARIANT_TRUE, dann ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter ordnet den Typ **Nvarchar**. In beiden Fällen wird der dbcolumndesc-Struktur *UlColumnSize* Element bestimmt die Breite der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Spalte erstellt.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Beim Erstellen einer neuen Tabelle ordnet der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nur die in der vorstehenden Tabelle angegebenen Enumerationswerte für OLE DB-Datenwerte zu. Durch den Versuch, eine Tabelle mit einer Spalte eines anderen OLE DB-Datentyps zu erstellen, wird ein Fehler erzeugt.  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
