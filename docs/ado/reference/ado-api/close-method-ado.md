---
title: Close-Methode (ADO) | Microsoft Docs
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
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 693f6adc51682fec4f9890d7d7618aa53e43593d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="close-method-ado"></a>Close-Methode (ADO)
Schließt einen geöffneten Objekt und alle abhängigen Objekte.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **schließen** Methode zum Schließen einer [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md), [Datensatz](../../../ado/reference/ado-api/record-object-ado.md), eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), oder ein [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt Um alle zugeordneten Systemressourcen frei. Schließen ein Objekt entfernt diesen nicht aus dem Arbeitsspeicher; Sie können die eigenschafteneinstellungen ändern und öffnen Sie es später erneut. Um ein Objekt aus dem Arbeitsspeicher vollständig zu vermeiden, schließen Sie das Objekt, und legen Sie dann auf die Objektvariable *nichts* (in Visual Basic).  
  
## <a name="connection"></a>Verbindung  
 Mithilfe der **schließen** Methode zum Schließen einer **Verbindung** Objekt schließt auch keine aktiven **Recordset** Objekte, die der Verbindung zugeordnet. Ein [Befehl](../../../ado/reference/ado-api/command-object-ado.md) zugeordnete Objekt der **Verbindung** bleiben erhalten, Sie schließen das, Objekt, aber es nicht mehr zugeordnet wird eine **Verbindung** -Objekt, d. h. seine [ ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) -Eigenschaftensatz auf **nichts**. Darüber hinaus die **Befehl** des Objekts [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung aller Anbieter definierte Parameter werden gelöscht.  
  
 Sie können später aufrufen, die [öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md) Methode, um die Verbindung mit der gleichen oder einer anderen Datenquelle erneut herzustellen. Während der **Verbindung** -Objekt ist geschlossen, Aufrufen von Methoden, die eine offene Verbindung zur Datenquelle erforderlich ist, wird ein Fehler generiert.  
  
 Schließen einer **Verbindung** -Objekt während geöffnet sind **Recordset** Objekte für die Verbindung Rollback für alle ausstehenden Änderungen in allen der **Recordset** Objekte. Explizit schließen eine **Verbindung** Objekt (Aufrufen der **schließen** Methode) während eine Transaktion wird ausgeführt wird ein Fehler generiert. Wenn eine **Verbindung** Objekt außerhalb des gültigen Bereichs liegt, während eine Transaktion ausgeführt wird, ADO automatisch ein Rollback der Transaktions.  
  
## <a name="recordset-record-stream"></a>Recordset, Datensatz, streamen.  
 Mithilfe der **schließen** Methode zum Schließen einer **Recordset**, **Datensatz**, oder **Stream** Objekt frei, die zugeordneten Daten und keinen exklusiven Zugriff Sie können auf die Daten über das jeweilige Objekt erstellt wurde. Sie können später aufrufen, die [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Attribute der Methode, um das Objekt mit dem gleichen oder geänderten erneut öffnen.  
  
 Während einer **Recordset** -Objekt ist geschlossen, Aufrufen von Methoden, einen live-Cursor erfordern, wird ein Fehler generiert.  
  
 Ist eine Bearbeitung ausgeführt, während Sie sich im sofortupdatemodus, Aufrufen der **schließen** Methode wird ein Fehler generiert, rufen Sie stattdessen die [aktualisieren](../../../ado/reference/ado-api/update-method.md) oder [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Methode erste. Wenn Sie schließen die **Recordset** Objekt im Batch-Updatemodus, alle Änderungen seit dem letzten [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Aufruf verloren.  
  
 Bei Verwendung der [Klon](../../../ado/reference/ado-api/clone-method-ado.md) Methode zum Erstellen von Kopien eines geöffneten **Recordset** -Objekt, schließen die ursprünglichen oder einen Klon hat keinen Einfluss auf andere Kopien.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record-Objekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Eröffnungs- und Methoden (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Öffnen Sie und schließen Sie die Methoden-Beispiel (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Öffnen Sie und schließen Sie die Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save-Methode](../../../ado/reference/ado-api/save-method.md)
