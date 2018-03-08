---
title: Datentypzuordnung zu Rowsets und Parametern | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- DBTYPE_SQLVARIANT data type
- SQL Server Native Client OLE DB provider, data types
- rowsets [OLE DB], data type mapping
- data types [OLE DB]
- GetColumnInfo function
- parameters [OLE DB]
- SSPROP_ALLOWNATIVEVARIANT property
- GetParameterInfo function
- OLE DB, data types
ms.assetid: 3d831ff8-3b79-4698-b2c1-2b5dd2f8235c
caps.latest.revision: "41"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 721f1891aefadf29070fdaf714c449bebb806ee7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="data-type-mapping-in-rowsets-and-parameters"></a>Datentypzuordnung zu Rowsets und Parametern
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In Rowsets und als Parameterwerte stellt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten über die folgenden OLE DB definierten Datentypen, die in den Funktionen gemeldet **IColumnsInfo:: GetColumnInfo** und  **ICommandWithParameters:: GetParameterInfo**.  
  
|SQL Server-Datentyp|OLE DB-Datentyp|  
|--------------------------|----------------------|  
|**bigint**|DBTYPE_I8|  
|**binary**|DBTYPE_BYTES|  
|**bit**|DBTYPE_BOOL|  
|**char**|DBTYPE_STR|  
|**datetime**|DBTYPE_DBTIMESTAMP|  
|**datetime2**|DBTYPE_DBTIME2|  
|**decimal**|DBTYPE_NUMERIC|  
|**float**|DBTYPE_R8|  
|**image**|DBTYPE_BYTES|  
|**int**|DBTYPE_I4|  
|**money**|DBTYPE_CY|  
|**nchar**|DBTYPE_WSTR|  
|**ntext**|DBTYPE_WSTR|  
|**numeric**|DBTYPE_NUMERIC|  
|**nvarchar**|DBTYPE_WSTR|  
|**real**|DBTYPE_R4|  
|**smalldatetime**|DBTYPE_DBTIMESTAMP|  
|**smallint**|DBTYPE_I2|  
|**smallmoney**|DBTYPE_CY|  
|**sql_variant**|DBTYPE_VARIANT, DBTYPE_SQLVARIANT|  
|**sysname**|DBTYPE_WSTR|  
|**text**|DBTYPE_STR|  
|**timestamp**|DBTYPE_BYTES|  
|**tinyint**|DBTYPE_UI1|  
|**UDT**|DBTYPE_UDT|  
|**uniqueidentifier**|DBTYPE_GUID|  
|**varbinary**|DBTYPE_BYTES|  
|**varchar**|DBTYPE_STR|  
|**XML**|DBTYPE_XML|  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt vom Consumer angeforderte datenkonvertierungen, wie in der Abbildung dargestellt.  
  
 Die **Sql_variant** Objekte können Daten jedes enthalten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datentyp mit Ausnahme von Text, Ntext, Image, varchar(max), nvarchar(max), varbinary(max), Xml, Timestamp und Microsoft .NET Framework common Language Runtime (CLR) Benutzerdefinierte Typen. Eine Instanz der sql_variant-Daten darf außerdem nicht sql_variant als zugrunde liegenden Basisdatentyp aufweisen. Die Spalte kann z. B. enthalten **"smallint"** Werte für einige Zeilen **"float"** Werte für die anderen Zeilen hat und **Char**/**Nchar**Werte in den Rest.  
  
> [!NOTE]  
>  Die **Sql_variant** -Datentyp ist der Variant-Datentyp in Microsoft Visual Basic® und den Typen DBTYPE_VARIANT, DBTYPE_SQLVARIANT in OLEDB ähnlich.  
  
 Wenn **Sql_variant** Daten als DBTYPE_VARIANT abgerufen werden, wird es in einer VARIANT-Struktur im Puffer abgelegt. Die Untertypen in der VARIANT-Struktur können nicht definierten Untertypen zugeordnet, aber die **Sql_variant** -Datentyp. Die **Sql_variant** Daten müssen dann als DBTYPE_SQLVARIANT abgerufen werden, in der Reihenfolge für alle Untertypen zugeordnet.  
  
## <a name="dbtypesqlvariant-data-type"></a>DBTYPE_SQLVARIANT Data Type  
 Zur Unterstützung der **Sql_variant** -Datentyp, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter stellt einen anbieterspezifischen Datentyp Namen DBTYPE_SQLVARIANT zur Verfügung. Wenn **Sql_variant** Daten als DBTYPE_SQLVARIANT abgerufen werden, erfolgt die Speicherung in einer anbieterspezifischen SSVARIANT-Struktur. Die SSVARIANT-Struktur enthält alle Untertypen, die den Untertypen des der **Sql_variant** -Datentyp.  
  
 Die Sitzungseigenschaft SSPROP_ALLOWNATIVEVARIANT muss außerdem auf TRUE festgelegt werden.  
  
## <a name="provider-specific-property-sspropallownativevariant"></a>Anbieterspezifische Eigenschaft SSPROP_ALLOWNATIVEVARIANT  
 Beim Abrufen von Daten können Sie explizit angeben, welcher Datentyp für eine Spalte oder einen Parameter zurückgegeben werden soll. **IColumnsInfo** kann auch verwendet werden, die Spalteninformationen abrufen und verwenden, um die Bindung verwenden. Wenn **IColumnsInfo** wird zum Abrufen von Spalteninformationen für Bindungszwecke verwendet, wenn die SSPROP_ALLOWNATIVEVARIANT-Sitzung, die Eigenschaft ist "false" (Standardwert), DBTYPE_VARIANT zurückgegeben wird **Sql_variant**Spalten. Wenn die SSPROP_ALLOWNATIVEVARIANT-Eigenschaft FALSE ist, wird DBTYPE_SQLVARIANT nicht unterstützt. Wenn die SSPROP_ALLOWNATIVEVARIANT-Eigenschaft auf TRUE festgelegt ist, wird der Spaltentyp als DBTYPE_SQLVARIANT zurückgegeben. In diesem Fall enthält der Puffer die SSVARIANT-Struktur. Abrufen von **Sql_variant** -Daten als DBTYPE_SQLVARIANT, die Sitzungseigenschaft SSPROP_ALLOWNATIVEVARIANT muss festgelegt werden auf "true".  
  
 Die SSPROP_ALLOWNATIVEVARIANT-Eigenschaft ist ein Teil des anbieterspezifischen DBPROPSET_SQLSERVERSESSION-Eigenschaftssatzes und eine Sitzungseigenschaft.  
  
 DBTYPE_VARIANT gilt für alle anderen OLE DB-Anbieter.  
  
## <a name="sspropallownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT ist eine Sitzungseigenschaft und ein Teil des DBPROPSET_SQLSERVERSESSION-Eigenschaftssatzes.  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|Typ: VT_BOOL<br /><br /> R/W: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Bestimmt, ob die Daten als DBTYPE_VARIANT oder DBTYPE_SQLVARIANT abgerufen werden.<br /><br /> VARIANT_TRUE: Der Spaltentyp wird als DBTYPE_SQLVARIANT zurückgegeben. In diesem Fall enthält der Puffer die SSVARIANT-Struktur.<br /><br /> VARIANT_FALSE: Der Spaltentyp wird als DBTYPE_VARIANT zurückgegeben und der Puffer enthält die VARIANT-Struktur.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
