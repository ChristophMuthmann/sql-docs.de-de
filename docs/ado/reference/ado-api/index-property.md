---
title: Index-Eigenschaft | Microsoft Docs
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
f1_keywords: Recordset21::Index
helpviewer_keywords: Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e7dac3b9494e2c23de547bdf96ba0079a264af9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="index-property"></a>Index-Eigenschaft
Gibt den Namen des Indexes derzeit wirksamen für eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Zeichenfolge** Wert, der den Namen des Indexes angibt.  
  
## <a name="remarks"></a>Hinweise  
 Der Index mit dem Namen, indem Sie die **Index** Eigenschaft muss zuvor deklariert worden sein, für den zugrunde liegenden Basistabelle die **Recordset** Objekt. D. h., der Index muss deklariert worden sein, programmgesteuert entweder als eine ADOX [Index](../../../ado/reference/adox-api/index-object-adox.md) -Objekt, oder wenn die Basistabelle erstellt wurde.  
  
 Ein Laufzeitfehler treten auf, wenn der Index kann nicht festgelegt werden. Die **Index** Eigenschaft kann nicht festgelegt werden, in den folgenden Situationen:  
  
-   Innerhalb einer [WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) oder **RecordsetChangeComplete** -Ereignishandler.  
  
-   Wenn die **Recordset** noch ausgeführt wird, einen Vorgang (die kann bestimmt werden, indem Sie die [Zustand](../../../ado/reference/ado-api/state-property-ado.md) Eigenschaft).  
  
-   Wenn ein Filter festgelegt wurde auf die **Recordset** mit der [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft.  
  
 Die **Index** Eigenschaft kann immer erfolgreich festgelegt werden, wenn die **Recordset** wird geschlossen, aber die **Recordset** nicht erfolgreich geöffnet werden, oder der Index wird nicht verwendet werden. wenn die zugrunde liegende Anbieter unterstützt keine Indizes.  
  
 Wenn der Index festgelegt werden kann, kann die aktuelle Zeilenposition ändern. Dies bewirkt, dass ein Update für die [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) -Eigenschaft, und immer dann ausgelöst, die **WillChangeRecordset**, **RecordsetChangeComplete**, [WillMove ](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), und [MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md) Ereignisse.  
  
 Wenn der Index festgelegt werden kann und die [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) Eigenschaft ist **AdLockPessimistic** oder **AdLockOptimistic**, klicken Sie dann einen impliziten [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Vorgang wird ausgeführt. Dies gibt die aktuellen und dem betroffenen Gruppen frei. Alle vorhandener Filter freigegeben wird und die aktuelle Zeilenposition geändert wird, auf die erste Zeile der neu angeordneten **Recordset**.  
  
 Die **Index** Eigenschaft dient in Verbindung mit der [Seek](../../../ado/reference/ado-api/seek-method.md) Methode. Wenn die zugrunde liegenden Anbieter nicht unterstützt die **Index** -Eigenschaft, und somit die **Seek** -Methode, erwägen Sie die [suchen](../../../ado/reference/ado-api/find-method-ado.md) Methode stattdessen. Bestimmen, ob die **Recordset** Objekt unterstützt Indizes mit der [unterstützt](../../../ado/reference/ado-api/supports-method.md)**(AdIndex)** Methode.  
  
 Die integrierte **Index** Eigenschaft bezieht sich nicht in der dynamischen [optimieren](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) -Eigenschaft, obwohl beide Indizes zu verarbeiten.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Seek-Methode und Eigenschaft Beispiel eines Indexes (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Index-Objekt (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Seek-Methode](../../../ado/reference/ado-api/seek-method.md)
