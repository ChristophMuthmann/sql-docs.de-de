---
title: MoveRecord-Methode (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords: MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8d15de5adfe707e1fd32a3ce005d865d6bee16da
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="moverecord-method-ado"></a>MoveRecord-Methode (ADO)
Verschiebt die Entität, dargestellt durch eine [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) an einen anderen Speicherort.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Quelle*  
 Optional. Ein **Zeichenfolge** -Wert, eine URL identifiziert enthält, die **Datensatz** verschoben werden soll. Wenn *Quelle* ausgelassen wird oder eine leere Zeichenfolge, die von diesem dargestellten Objekts gibt **Datensatz** verschoben wird. Beispielsweise, wenn die **Datensatz** steht für eine Datei, den Inhalt der Datei in den vom angegebenen Speicherort verschoben werden *Ziel*.  
  
 *Ziel*  
 Optional. Ein **Zeichenfolge** -Wert enthält eine URL angeben des Speicherorts, in dem *Quelle* verschoben werden.  
  
 *UserName*  
 Optional. Ein **Zeichenfolge** Wert, der die Benutzer-ID, die enthält bei Bedarf den Zugriff auf autorisiert *Ziel*.  
  
 *Kennwort*  
 Optional. Ein **Zeichenfolge** , enthält das Kennwort, das bei Bedarf bestätigt *Benutzername*.  
  
 *enthalten*  
 Optional. Ein [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) Wert, dessen Standardwert **AdMoveUnspecified**. Gibt das Verhalten dieser Methode.  
  
 *Async*  
 Optional. Ein **booleschen** -Wert, wenn **"true"**, gibt dieser Vorgang asynchron sein sollte.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** Wert. In der Regel den Wert der *Ziel* zurückgegeben wird. Der genaue Wert zurückgegeben, ist jedoch vom Anbieter abhängig.  
  
## <a name="remarks"></a>Hinweise  
 Die Werte der *Quelle* und *Ziel* müssen nicht übereinstimmen, andernfalls tritt ein Laufzeitfehler auf. Mindestens Namen des Servers, der Pfad und der Ressource müssen sich unterscheiden.  
  
 Für Dateien, die per die Publishing Internetanbieter verschoben werden, aktualisiert diese Methode alle Hypertextlinks im Dateien verschoben werden, sofern nicht anders angegeben durch *Optionen*. Diese Methode schlägt fehl, wenn *Ziel* ein vorhandenes Objekt (z. B. eine Datei oder ein Verzeichnis) bezeichnet, es sei denn, **adMoveOverWrite an** angegeben ist.  
  
> [!NOTE]
>  Verwenden der **adMoveOverWrite an** Umsicht option. Beispielsweise wird Angabe dieser Option beim Verschieben einer Datei in ein Verzeichnis löschen Sie das Verzeichnis und die Datei ersetzt.  
  
 Bestimmte Attribute von der **Datensatz** Objekt, wie die [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) -Eigenschaft wird nicht aktualisiert werden, nachdem dieser Vorgang abgeschlossen wurde. Aktualisieren der **Datensatz** Objekteigenschaften schließende der **Datensatz**, und klicken Sie dann erneut mit der URL des Speicherorts öffnen, in dem die Datei oder das Verzeichnis verschoben wurde.  
  
 Wenn diese **Datensatz** abgerufen wurde, aus einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), der neue Speicherort der verschobene Datei oder des Verzeichnisses werden nicht sofort im berücksichtigt die **Recordset**. Aktualisieren der **Recordset** durch Schließen und erneut öffnen.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Record-Objekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Move-Methode (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext und MovePrevious-Methoden (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst-, MoveLast-, MoveNext- und MovePrevious-Methode (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
