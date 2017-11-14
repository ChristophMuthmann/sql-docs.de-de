---
title: "Persistenz-Provider für Microsoft OLE DB (ADO-Dienstanbieter) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508b983c514031587f2b6507b806d3f279e0f822
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Übersicht über die Microsoft OLE DB-Persistenz-Provider
Der Microsoft OLE DB-Persistenz-Provider ermöglicht Ihnen das Speichern einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt in eine Datei, und höhere Versionen wiederherstellen, die **Recordset** Objekt aus der Datei. Schemainformationen, Daten und ausstehende Änderungen werden beibehalten.

 Sie können speichern die **Recordset** im proprietären Format von Advanced Data Tabelle Gram (ADTG) oder open Extensible Markup Language (XML)-Format.

## <a name="provider-keyword"></a>Anbieter-Schlüsselwort
 Geben Sie zum Aufrufen von diesem Anbieter die folgenden-Schlüsselwort und Wert in der Verbindungszeichenfolge angegeben.

```
"Provider=MSPersist"
```

## <a name="errors"></a>Fehler
 Die folgenden Fehler ausgegeben, die von diesem Anbieter können in der Anwendung erkannt werden.

|Konstante|Description|
|--------------|-----------------|
|E_BADSTREAM|Die geöffnete Datei verfügt nicht über einem gültigen Format (d. h. das Format ist nicht ADTG oder XML).|
|E_CANTPERSISTROWSET|Die **Recordset** gespeichertes Objekt hat Merkmale, die verhindern, dass er gespeichert wird.|

## <a name="remarks"></a>Hinweise
 Microsoft OLE DB-Anbieter für Persistenz weist keine dynamischen Eigenschaften.

 Derzeit nur parametrisierte hierarchische **Recordset** Objekte können nicht gespeichert werden.

 Weitere Informationen zu dauerhaft speichern **Recordset** anzuzeigen, [Recordset Persistenz](../../../ado/guide/data/more-about-recordset-persistence.md).

 Bei Verendung ein Datenstrom zu öffnen eine **Recordset,** es darf keine Parameter angegeben, außer der *Quelle* Parameter von der **öffnen** Methode.

## <a name="see-also"></a>Siehe auch
[Persistenz-Provider für Microsoft OLE DB (ADO-Dienstanbieter)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

