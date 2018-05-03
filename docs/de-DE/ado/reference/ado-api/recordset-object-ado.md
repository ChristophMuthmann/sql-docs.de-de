---
title: Recordset-Objekt (ADO) | Microsoft Docs
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
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86f328c60ebb3d2edbdf591c94995936a642af16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="recordset-object-ado"></a>Recordset-Objekt (ADO)
Stellt die gesamte Gruppe von Datensätzen aus einer Basistabelle oder die Ergebnisse eines ausgeführten Befehls dar. Zu jedem Zeitpunkt die **Recordset** Objekt bezieht sich auf nur einen einzelnen Datensatz in der Gruppe als der aktuelle Datensatz.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie **Recordset** Objekte, um Daten von einem Anbieter zu bearbeiten. Wenn Sie ADO verwenden, bearbeiten Sie Daten mithilfe von fast vollständig **Recordset** Objekte. Alle **Recordset** Objekte bestehen aus Datensätzen (Zeilen) und Feldern (Spalten). Abhängig von den Funktionen, die vom Anbieter unterstützt einige **Recordset** Methoden oder Eigenschaften möglicherweise nicht zur Verfügung.  
  
 ADODB. Recordset ist die Programm-ID, die verwendet werden soll, zum Erstellen einer **Recordset** Objekt. Vorhandene Anwendungen, die veraltete ADOR verweisen. Recordset ProgID funktionieren auch weiterhin ohne neu zu kompilieren, aber neue Entwicklungen sollten ADODB verweisen. Recordset.  
  
 Es gibt vier verschiedenen Cursortypen, die in ADO definiert:  
  
-   **Dynamische Cursor** können Sie hinzufügen, ändern oder Löschen von anderen Benutzern; anzeigen können alle Typen der Bewegung durch die **Recordset** , keine Lesezeichen; abhängig und können Sie Lesezeichen aus, wenn der Anbieter unterstützt Diese.  
  
-   **Keyset-Cursor** verhält sich wie einen dynamischen Cursor, mit dem Unterschied, dass die It verhindert sehen Datensätze, die von anderen Benutzern hinzufügen und verhindert den Zugriff auf die von anderen Benutzern gelöschten Datensätze. Datenänderungen von anderen Benutzern werden weiterhin angezeigt. Er unterstützt immer das Lesezeichen und aus diesem Grund können alle Typen der Bewegung durch die **Recordset**.  
  
-   **Statische Cursor** stellt eine statische Kopie einer Gruppe von Datensätzen für die Sie zum Suchen von Daten oder zum Generieren von Berichten verwenden; immer können Lesezeichen und daher alle Typen der Bewegung durch die **Recordset**. Hinzufügungen, Änderungen oder löschungen von anderen Benutzern werden nicht angezeigt. Dies ist der einzige Typ von Cursor zulässig, wenn Sie eine clientseitige öffnen **Recordset** Objekt.  
  
-   **Vorwärtscursor** ermöglicht es Ihnen, nur vorwärts durch die **Recordset**. Hinzufügungen, Änderungen oder löschungen von anderen Benutzern werden nicht angezeigt. Dies verbessert die Leistung in Situationen, in denen Sie nur eine Pass-through vornehmen müssen, eine **Recordset**.  
  
 Festlegen der [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) Eigenschaft vor dem Öffnen der **Recordset** wählen den Cursor, oder übergeben ein *CursorType* Argument mit der [Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md)Methode. Einige Anbieter unterstützen nicht alle Cursortypen. Überprüfen Sie die Dokumentation für den Anbieter. Wenn Sie einen anderer Cursortyp angeben, wird die ADO einen Vorwärtscursor standardmäßig geöffnet.  
  
 Wenn die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) -Eigenschaftensatz auf **AdUseClient** So öffnen eine **Recordset**, die **OriginalValue** Eigenschaft [Feld](../../../ado/reference/ado-api/field-object.md) Objekte ist nicht verfügbar in der zurückgegebenen **Recordset** Objekt. Einige Anbieter (z. B. der Microsoft ODBC-Datenanbieter für OLE DB in Verbindung mit Microsoft SQL Server) verwendet, können Sie erstellen **Recordset** Objekte unabhängig von einem zuvor definierten [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md)-Objekt durch Übergeben einer Verbindungszeichenfolge mit den **öffnen** Methode. ADO erstellt dennoch ein [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt, sondern eine Objektvariable dieses Objekt nicht zuweisen. Jedoch, wenn Sie mehrere öffnen **Recordset** Objekte über dieselbe Verbindung explizit erstellen, und öffnen Sie eine **Verbindung** Objekt; dieser weist die **Verbindung**Objekt, das eine Objektvariable. Wenn Sie diese Objektvariable nicht, beim Öffnen verwenden der **Recordset** Objekte aufweist, ADO erstellt ein neues **Verbindung** -Objekt für jedes neue **Recordset**, selbst wenn Sie die gleiche übergeben Verbindungszeichenfolge.  
  
 Sie können beliebig viele erstellen **Recordset** Objekte nach Bedarf.  
  
 Beim Öffnen einer **Recordset**, der aktuelle Datensatz positioniert, dass Sie den ersten Datensatz (sofern vorhanden) und die [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) und [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) Eigenschaften werden festgelegt, um **"false"**. Es sind keine Datensätze der **BOF** und **EOF** eingestellter **"true"**.  
  
 Sie können die [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**, und **MovePrevious** Methoden; das [verschieben](../../../ado/reference/ado-api/move-method-ado.md) -Methode. und die [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), und [Filter](../../../ado/reference/ado-api/filter-property.md) zu positionieren den aktuellen Datensatz, sofern der Anbieter unterstützt die relevanten Eigenschaften die Funktionalität. Vorwärtscursor **Recordset** Objekte unterstützen nur die [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) Methode. Bei Verwendung der **verschieben** Methoden, um jeden Datensatz besuchen (oder durchlaufen die **Recordset**), können Sie die **BOF** und **EOF** Eigenschaften Bestimmen Sie, ob Sie am Anfang oder Ende überschritten haben die **Recordset**.  
  
 Vor der Verwendung der Funktionen einer **Recordset** -Objekt, rufen Sie die **unterstützt** Methode für das Objekt, um sicherzustellen, dass die Funktionalität unterstützt oder verfügbar ist. Sie müssen nicht die Funktionalität verwenden bei der **unterstützt** Methode "false" zurückgegeben. Beispielsweise können Sie die **MovePrevious** Methode nur, wenn `Recordset.Supports(adMovePrevious)` gibt **"true"**. Andernfalls wird eine Fehlermeldung erhalten, da die **Recordset** -Objekt wurde geschlossen und die Funktionalität für die Instanz nicht verfügbar dargestellt. Wenn eine Funktion, die Sie interessiert sind, nicht unterstützt wird, **unterstützt** wird auch "false" zurückgeben. In diesem Fall sollten Sie die entsprechende Eigenschaft oder Methode aufrufen, auf die **Recordset** Objekt.  
  
 **Recordset** Objekte unterstützen zwei Typen von aktualisieren: sofortige als auch im Batchmodus. In das sofortige Aktualisieren, alle Änderungen an Daten geschrieben werden sofort mit der zugrunde liegenden Datenquelle nach Aufrufen der [Update](../../../ado/reference/ado-api/update-method.md) Methode. Sie können Arrays von Werten auch übergeben, als Parameter mit der [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) und **aktualisieren** Methoden und gleichzeitig mehrere Felder in einem Datensatz aktualisieren.  
  
 Wenn BatchUpdates von einem Anbieter unterstützt, können Sie den Anbieter, Änderungen an mehr als ein Datensatz Zwischenspeichern und übertragen sie in einem einzigen Aufruf der Datenbank mit der [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode. Dies gilt für Änderungen, die mit der **AddNew**, **Update**, und [löschen](../../../ado/reference/ado-api/delete-method-ado-recordset.md) Methoden. Nach dem Aufruf der **UpdateBatch** -Methode, die Sie verwenden die [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) Eigenschaft, um alle Datenkonflikte vornimmt, um diese zu lösen.  
  
> [!NOTE]
>  Zum Ausführen einer Abfrage ohne Verwendung einer [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt, und übergeben Sie eine Abfragezeichenfolge enthält, die die **öffnen** Methode eine **Recordset** Objekt. Allerdings eine **Befehl** Objekt ist erforderlich, wenn den Befehlstext beibehalten und erneut ausgeführt wird, oder verwenden Sie Abfrageparameter werden sollen.  
  
 Die [Modus](../../../ado/reference/ado-api/mode-property-ado.md) Eigenschaft steuert die Zugriffsberechtigungen.  
  
 Die **Felder** Auflistung ist das Standardelement der **Recordset** Objekt. Dies hat zur Folge, dass der Code für die folgenden beiden Anweisungen äquivalent.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 Wenn eine **Recordset** -Objekts übergeben wird, über Prozesse, nur die **Rowset** Werte gemarshallt werden, und die Eigenschaften des der **Recordset** Objekt werden ignoriert. Während der unmarshalling, die **Rowset** ist in einer neu erstellten entpackten **Recordset** Objekt, das auch die Eigenschaften auf die Standardwerte festlegt.  
  
 Die **Recordset** Objekt für die Skripterstellung sicher ist.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Recordset-Objekt Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Fields-Auflistung (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Anhang A: Daten und Dienstanbieter](../../../ado/guide/appendixes/appendix-a-providers.md)
