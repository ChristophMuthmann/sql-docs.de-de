---
title: "Microsoft Data strukturiert werden, Dienst für OLE DB (ADO-Dienstanbieter) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 624bc851727e9d929c4d83721ac64352669cf643
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Microsoft Data strukturiert werden, Dienst für OLE DB-Übersicht
> [!IMPORTANT]
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen sollten stattdessen XML verwenden.

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
