---
title: Microsoft Data strukturiert werden, Dienst für OLE DB (ADO-Dienstanbieter) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3020789835820519e07ac3e465899c3ac93b0ae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft Data strukturiert werden, Dienst für OLE DB-Übersicht
> [!IMPORTANT]
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen sollten stattdessen XML verwenden.

 Microsoft--Datenstrukturierungsdiensts für OLE DB-Service-Anbieter unterstützt das Erstellen von hierarchischen (strukturiert) [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekte von einem Datenanbieter.

## <a name="provider-keyword"></a>Anbieter-Schlüsselwort
 Um-Datenstrukturierungsdiensts für OLE DB-aufrufen, geben Sie die folgenden-Schlüsselwort und Wert in der Verbindungszeichenfolge ein.

```
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>Dynamische Eigenschaften
 Wenn dieser Dienstanbieter aufgerufen wird, die folgenden dynamischen Eigenschaften hinzugefügt werden die [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung von der[Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt.

|Name der dynamischen Eigenschaft|Description|
|---------------------------|-----------------|
|**Eindeutige umformen Namen**|Gibt an, ob **Recordset** Objekte mit doppelten Werten für ihre **umformen Namen** Eigenschaften sind zulässig. Wenn diese dynamische Eigenschaft **"true"** und eine neue **Recordset** wird erstellt, mit demselben Namen wie ein vorhandenes benutzerdefiniertes umformen **Recordset**, klicken Sie dann die neue  **Recordset** umformen der Objektname wurde geändert, um eindeutig zu machen. Wenn diese Eigenschaft ist **"false"** und eine neue **Recordset** wird erstellt, mit demselben Namen wie die vorhandene benutzerdefinierte umformen **Recordset**, beide **Recordset**  Objekte müssen den gleichen umformen Namen. Aus diesem Grund keine **Recordset** Form werden können, solange beide Objekte vorhanden sind.<br /><br /> Der Standardwert der Eigenschaft ist **"false"**.|
|**Datenanbieter**|Gibt den Namen des Anbieters, der Zeilen zum Strukturieren geliefert wird. Mögliche Werte sind NONE, wenn ein Anbieter nicht zum Bereitstellen von Zeilen verwendet wird.|

 Sie können auch beschreibbare dynamische Eigenschaften festlegen, durch deren Namen als Schlüsselwörter in der Verbindungszeichenfolge angeben. Legen Sie z. B. in Microsoft Visual Basic die **Datenanbieter** dynamische Eigenschaft auf "MSDASQL" durch Angabe:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 Sie können auch festlegen, oder rufen Sie eine dynamische Eigenschaft durch Angabe ihres Namens als Index für die [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Eigenschaft. Z. B. im folgenden Codebeispiel wird abgerufen, und gibt den aktuellen Wert der **Datenanbieter** dynamische Eigenschaft klicken Sie dann ein neuer Wert festgelegt, wenn Cn. "DataProvider" auf "MSDataShape" festgelegt wurde (entweder direkt oder indirekt über die Verbindungszeichenfolge) und die Verbindung wurde nicht geöffnet:

```
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  Die dynamische Eigenschaft **Datenanbieter**, kann nur festgelegt, auf eine geöffnete **Verbindung** Objekt. Sobald die Verbindung geöffnet wird, die **Datenanbieter** Eigenschaft ist schreibgeschützt.

 Weitere Informationen zu Daten strukturieren, finden Sie unter [Datenstrukturierung](../../../ado/guide/data/data-shaping-overview.md).

## <a name="see-also"></a>Siehe auch
 [Anhang A: Daten und Dienstanbieter](../../../ado/guide/appendixes/appendix-a-providers.md)
