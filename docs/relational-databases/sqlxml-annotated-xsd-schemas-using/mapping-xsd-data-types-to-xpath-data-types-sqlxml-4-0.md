---
title: Zuordnen von XSD-Datentypen zu XPath-Datentypen (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b41676bcf1cfe655fd7ed7f5c68b5b924c0f9814
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>Zuordnen von XSD-Datentypen zu XPath-Datentypen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Wenn eine XPath-Abfrage für ein XSD-Schema ausgeführt wird und der XSD-Typ wird angegeben, der **xsd: Type** -Attribut, verwendet XPath den Datentyp, der beim Verarbeiten der Abfrage angegeben.  
  
 Der XPath-Datentyp eines Knotens wird vom XSD-Datentyp in dem Schema abgeleitet, wie in der folgenden Tabelle dargestellt. (Der Knoten "EmployeeID" dient zur Veranschaulichung.)  
  
|XSD-Datentyp|XDR-Datentyp|Entsprechung<br /><br /> XPath-Datentyp|SQL Server<br /><br /> verwendete Konvertierung|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **hexBinary**|**InclusionThresholdSetting**<br /><br /> **bin.base64bin.hex**|**Nicht verfügbar**|Keine<br /><br /> EmployeeID|  
|**Boolean**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**Decimal, ganze Zahl, "float", Byte, Short, Int, long, float, double, UnsignedByte, UnsignedShort, UnsignedInt, unsignedLong wird**|**Anzahl, Int, Float, i1, i2, i4, i8, r4, r8ui1, Anwenderschnittstelle: 2, UI4 sein, ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**ID, Idref, Idrefsentity, Entitäten, Notation, Nmtoken, Nmtokens, "DateTime", "string", "AnyURI**|**ID, Idref, Idrefsentity, Entitäten, Enumeration, Notation, Nmtoken, Nmtokens, Char, "DateTime", dateTime.tz, String, Uri, uuid**|**Zeichenfolge**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**dem fixed14. 4**|**Nicht zutreffend (es gibt keinen Datentyp in XPath, der fixed14. 4 XDR-Datentyp entspricht.)**|CONVERT(money, EmployeeID)|  
|**Datum**|**Datum**|**Zeichenfolge**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**Uhrzeit**|**Uhrzeit**<br /><br /> **time.tz**|**Zeichenfolge**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
