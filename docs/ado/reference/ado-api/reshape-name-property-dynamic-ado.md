---
title: Umstrukturieren von Name-Eigenschaft dynamisch (ADO) | Microsoft Docs
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
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a1d81e91edfcab8b6938f5898ae4fd46cc38b67
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="reshape-name-property-dynamic-ado"></a>Umstrukturieren von Name-Eigenschaft dynamisch (ADO)
Gibt einen Namen für die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **Zeichenfolge** Wert, der den Namen der **Recordset**.  
  
## <a name="remarks"></a>Hinweise  
 Namen für die Dauer der Verbindung oder bis zum Beibehalten der **Recordset** geschlossen wird.  
  
 Die **umformen Namen** Eigenschaft dient in erster Linie zur Verwendung mit der neu strukturieren Funktion von der [Microsoft-Datenstrukturierungsdiensts für OLE DB-](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) Dienstanbieter. Namen müssen zur Teilnahme an neu strukturiert werden, eindeutig sein.  
  
 Diese Eigenschaft ist schreibgeschützt, aber können indirekt festgelegt werden, wenn eine **Recordset** wird erstellt. Z. B. wenn eine Klausel dieses Shape-Befehl erstellt eine **Recordset** und ein Aliasnamens mithilfe von bietet die **AS** -Schlüsselwort, Alias zugewiesen ist die **umformen Namen** Eigenschaft. Wenn kein Alias deklariert wird, die **umformen Namen** Eigenschaft ist einen eindeutigen Name generiert, durch die Daten strukturieren Dienst zugewiesen. Wenn der Aliasname identisch mit dem Namen eines vorhandenen ist **Recordset**, weder **Recordset** Form werden kann, bis eine von ihnen freigegeben wird. Das Standardverhalten kann geändert werden, indem Sie einen eindeutigen Namen der [umformen Namen](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) Eigenschaft für die ADO-Verbindung mit **"true"**. Durch Festlegen dieser Eigenschaft ermöglicht die Daten strukturieren Service-Berechtigung so ändern Sie den Namen des Benutzers zugewiesen, bei Bedarf, um Eindeutigkeit sicherzustellen. Weitere Informationen zu umformen, finden Sie unter [Microsoft-Datenstrukturierungsdiensts für OLE DB (ADO-Dienstanbieter)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md).  
  
 Verwenden der **umformen Namen** Eigenschaft, wenn Sie möchten eine **Recordset** in einer Shape-Befehl, oder wenn Sie den Namen nicht kennen, weil sie von der-Datenstrukturierungsdiensts generiert wurde. In diesem Fall generieren Sie einen SHAPE-Befehl, indem Sie den Befehl aus, um die zurückgegebene Zeichenfolge Verketten der **umformen Namen** Eigenschaft.  
  
 **Umformen Name** ist eine dynamische Eigenschaft angefügt der **Recordset** des Objekts [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung bei der [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft auf festgelegtist**AdUseClient**.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Data strukturiert werden, Dienst für OLE DB (ADO-Dienstanbieter)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
