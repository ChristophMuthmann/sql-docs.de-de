---
title: ParentURL-Eigenschaft (ADO) | Microsoft Docs
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
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51a7a476352519f4756e4e8f19166aac3c84d7da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="parenturl-property-ado"></a>ParentURL-Eigenschaft (ADO)
Gibt eine absolute URL-Zeichenfolge, die auf das übergeordnete Element verweist [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) des aktuellen **Datensatz** Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Zeichenfolge** Wert an die URL des übergeordneten Elements **Datensatz**.  
  
## <a name="remarks"></a>Hinweise  
 Die **ParentURL** Eigenschaft hängt von der Quelle zum Öffnen der **Datensatz** Objekt. Z. B. die **Datensatz** geöffnet werden kann, mit einer Quelle, enthält der Name eines relativen Pfads, der ein Verzeichnis verweist, die [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) Eigenschaft.  
  
 Angenommen, das "zweite" ein Ordner unter "First" enthalten ist. Öffnen der **Datensatz** Objekt mit der folgenden Syntax:  
  
```  
record.ActiveConnection = "http://first"  
record.Open "second"  
```  
  
 Jetzt, den Wert der `the` **ParentURL** Eigenschaft ist `"http://first"`, die identisch mit **ActiveConnection**.  
  
 Die Quelle kann auch eine absolute URL wie z. B. `"http://first/second"`. Die **ParentURL** Eigenschaft ist dann `"http://first"`, der darüber liegenden Ebene `"second"`.  
  
 Diese Eigenschaft kann ein null-Wert sein, wenn:  
  
-   Es ist kein übergeordnetes Element für das aktuelle Objekt. beispielsweise, wenn die **Datensatz** Objekt stellt den Stamm eines Verzeichnisses dar.  
  
-   Die **Datensatz** Objekt stellt eine Entität, die mit einer URL angegeben werden kann.  
  
 Diese Eigenschaft ist schreibgeschützt.  
  
> [!NOTE]
>  Diese Eigenschaft wird nur unterstützt Dokument Anbietern, wie z. B. die [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [Datensätze und Felder vom Anbieter bereitgestellte](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Wenn der aktuelle Datensatz einen Datensatz aus einer ADO enthält **Recordset**, den Zugriff auf die **ParentURL** -Eigenschaft bewirkt, dass ein Laufzeitfehler, der angibt, dass keine URL möglich ist.  
  
## <a name="applies-to"></a>Gilt für  
 [Record-Objekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
