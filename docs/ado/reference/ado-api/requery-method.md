---
title: Requery-Methode | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a6e81cda01f894b87d2741f80735b21b23423ce6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="requery-method"></a>Requery-Methode
Aktualisiert die Daten in einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt durch erneutes Ausführen der Abfrage auf der das Objekt basiert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>Parameter  
 *Optionen*  
 Optional. Eine Bitmaske, die enthält [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) und [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) Werte, die diesen Vorgang beeinflussen.  
  
> [!NOTE]
>  Wenn *Optionen* festgelegt ist, um **AdAsyncExecute**, diesen Vorgang wird asynchron ausgeführt und ein [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) Ereignis wird ausgegeben, wenn er abgeschlossen ist. Die **ExecuteOpenEnum** Werte **AdExecuteNoRecords** oder **AdExecuteStream** sollte nicht verwendet werden, mit **Requery**.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Requery** Methode, um den gesamten Inhalt Aktualisieren einer **Recordset** Objekt aus der Datenquelle, indem Sie den ursprünglichen Befehl erneut ausführen und Abrufen der Daten ein zweites Mal. Beim Aufrufen dieser Methode entspricht dem Aufrufen der [schließen](../../../ado/reference/ado-api/close-method-ado.md) und [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methoden hintereinander ausgeführt. Wenn Sie den aktuellen Datensatz bearbeiten oder einen neuen Datensatz hinzufügen, tritt ein Fehler auf.  
  
 Während der **Recordset** Objekt geöffnet ist, die Eigenschaften, die die Art des Cursors definieren ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md), [LockType](../../../ado/reference/ado-api/locktype-property-ado.md), [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md) usw.) sind schreibgeschützt. Daher die **Requery** Methode kann nur den aktuellen Cursor aktualisieren. Zum Ändern der Eigenschaften für Cursor und die Ergebnisse anzuzeigen, verwenden Sie die [schließen](../../../ado/reference/ado-api/close-method-ado.md) Methode, damit die Eigenschaften erneut Lese-/Schreibzugriff werden. Sie können anschließend ändern der Einstellungen der Eigenschaften und rufen die [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode, um den Cursor zu öffnen.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Führen Sie abzufragen und Clear-Methoden-Beispiel (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Führen Sie abzufragen und Clear-Methoden-Beispiel (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Führen Sie Requery und deaktivieren Sie die Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
