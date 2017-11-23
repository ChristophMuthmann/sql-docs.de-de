---
title: Source-Eigenschaft (ADO-Datensatz) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::Source
- _Record::PutRefSource
- _Record::GetSource
- _Record::put_Source
- _Record::putref_Source
- _Record::get_Source
helpviewer_keywords: Source property [ADO Record]
ms.assetid: 2c18279e-6f35-4af0-b12e-8f1543d9ed20
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2e379bb3e2fce7899125c208251c8a04da1ea95
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="source-property-ado-record"></a>Source-Eigenschaft (ADO-Datensatz)
Gibt an, die Datenquelle oder das Objekt dargestellt wird, indem die [Datensatz](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Variant** -Wert, der die Entität, dargestellt durch die **Datensatz**.  
  
## <a name="remarks"></a>Hinweise  
 Die **Quelle** -Eigenschaft gibt die *Quelle* Argument der **Datensatz** Objekt [öffnen](../../../ado/reference/ado-api/open-method-ado-record.md) Methode. Sie können eine absolute oder relative URL-Zeichenfolge enthalten. Eine absolute URL verwendet werden kann, ohne die Einstellung der [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) Eigenschaft direkt öffnen die **Datensatz** Objekt. Eine implizite **Verbindung** Objekt wird in diesem Fall erstellt.  
  
 Die **Quelle** Eigenschaft kann auch einen Verweis auf ein bereits geöffnetes enthalten **Recordset**, daraufhin eine **Datensatz** Objekt, das in die aktuelle Zeile darstellt. die  **Recordset**.  
  
 Die **Quelle** Eigenschaft kann auch enthalten einen Verweis auf eine [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt, das eine einzelne Zeile mit Daten vom Anbieter zurückgegeben.  
  
 Wenn die **ActiveConnection** Eigenschaft auch festgelegt ist, und klicken Sie dann die **Quelle** Eigenschaft muss zeigen Sie auf ein Objekt, das innerhalb des Bereichs dieser Verbindung vorhanden ist. Z. B. in strukturierten Namespaces verwendet Wenn die **Quelle** Eigenschaft eine absolute URL enthält, muss er zeigen Sie auf einen Knoten, der innerhalb des Bereichs des Knotens identifiziert durch die URL in der Verbindungszeichenfolge vorhanden ist. Wenn die **Quelle** Eigenschaft enthält eine relative URL, dann wird es innerhalb des Kontexts festlegen, indem überprüft die **ActiveConnection** Eigenschaft.  
  
 Die **Quelle** Eigenschaft ist Lese-/Schreibzugriff, während die **Datensatz** Objekt ist geschlossen, und ist schreibgeschützt, während die **Datensatz** Objekt geöffnet ist.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Record-Objekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Source-Eigenschaft (ADO-Fehler)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source-Eigenschaft (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
