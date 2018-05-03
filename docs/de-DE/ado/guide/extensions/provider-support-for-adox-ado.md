---
title: Unterstützung von Zertifikatanbietern zur ADOX (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61cdd630dfefd4200007a3d3d1aad14aa68d9419
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="provider-support-for-adox-ado"></a>Unterstützung von Zertifikatanbietern zur ADOX (ADO)
Bestimmte Features von ADOX werden nicht unterstützt, abhängig von der OLE DB-Datenanbieter. ADOX wird vollständig unterstützt, mit der [OLE DB-Anbieter für Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md). Mit nicht unterstützten Funktionen der [Microsoft OLE DB-Anbieter für SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), [Microsoft OLE DB-Anbieter für ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md), oder die [Microsoft OLE DB-Anbieter für Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) sind in den folgenden Tabellen aufgeführt. ADOX wird nicht von Microsoft OLE DB-Anbietern unterstützt.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Microsoft OLE DB-Anbieter für SQLServer  
  
|Objekt oder einer Auflistung|Verwendungseinschränkung|  
|--------------------------|-----------------------|  
|**Tabellen** Auflistung|Eigenschaften sind Lese-/Schreibzugriff vor dem Erstellen von Objekten, und schreibgeschützt, wenn Sie ein vorhandenes Objekt zu verweisen.|  
|**Sichten** Auflistung|**Sichten** wird nicht unterstützt.|  
|**Prozeduren** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt.|  
|**Prozedur** Objekt|Die **Befehl** Eigenschaft wird nicht unterstützt.|  
|**Schlüssel** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt.|  
|**Benutzer** Auflistung|**Benutzer** wird nicht unterstützt.|  
|**Gruppen** Auflistung|**Gruppen** wird nicht unterstützt.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Microsoft OLE DB-Anbieter für ODBC  
  
|Objekt oder einer Auflistung|Verwendungseinschränkung|  
|--------------------------|-----------------------|  
|**Katalog** Objekt|Die **erstellen** Methode wird nicht unterstützt.|  
|**Tabellen** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt. Eigenschaften sind Lese-/Schreibzugriff vor dem Erstellen von Objekten, und schreibgeschützt, wenn Sie ein vorhandenes Objekt zu verweisen.|  
|**Prozeduren** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt.|  
|**Prozedur** Objekt|Die **Befehl** Eigenschaft wird nicht unterstützt.|  
|**Indizes** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt.|  
|**Schlüssel** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt.|  
|**Benutzer** Auflistung|**Benutzer** wird nicht unterstützt.|  
|**Gruppen** Auflistung|**Gruppen** wird nicht unterstützt.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Microsoft OLE DB-Anbieter für Oracle  
  
|Objekt oder einer Auflistung|Verwendungseinschränkung|  
|--------------------------|-----------------------|  
|**Katalog** Objekt|Die **erstellen** Methode wird nicht unterstützt.|  
|**Tabellen** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt. Eigenschaften sind Lese-/Schreibzugriff vor dem Erstellen von Objekten, und schreibgeschützt, wenn Sie ein vorhandenes Objekt zu verweisen.|  
|**Sichten** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt.|  
|**Ansicht** Objekt|Die **Befehl** Eigenschaft wird nicht unterstützt.|  
|**Prozeduren** Objekt|Die **Append** und **löschen** Methoden werden nicht unterstützt.|  
|**Prozedur** Objekt|Die **Befehl** Eigenschaft wird nicht unterstützt.|  
|**Indizes** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt.|  
|**Schlüssel** Auflistung|Die **Append** und **löschen** Methoden werden nicht unterstützt.|  
|**Benutzer** Auflistung|**Benutzer** wird nicht unterstützt.|  
|**Gruppen** Auflistung|**Gruppen** wird nicht unterstützt.|
