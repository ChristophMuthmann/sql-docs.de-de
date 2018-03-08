---
title: Save-Methode | Microsoft Docs
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
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ca1aa95841be1331ad1b214b2a8b377622883d3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="save-method"></a>Save-Methode
Speichert die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) in einer Datei oder [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>Parameter  
 *Ziel*  
 Optional. Ein **Variant** , die den vollständigen Pfadnamen der Datei darstellt, in dem die **Recordset** gespeichert werden soll, oder ein Verweis auf eine **Stream** Objekt.  
  
 *PersistFormat*  
 Optional. Ein [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md) -Wert, der das Format, in dem angibt die **Recordset** (XML oder ADTG) gespeichert werden soll. Der Standardwert ist **AdPersistADTG**.  
  
## <a name="remarks"></a>Hinweise  
 Die [Save-Methode](../../../ado/reference/ado-api/save-method.md) Methode kann nur aufgerufen werden, auf ein offenes **Recordset**. Verwenden der [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode, um spätere Wiederherstellung der **Recordset** aus *Ziel*.  
  
 Wenn die [Filtereigenschaft](../../../ado/reference/ado-api/filter-property.md) Eigenschaft gilt für die **Recordset**, und klicken Sie dann nur die Zeilen, die unter dem Filter zugänglichen gespeichert werden. Wenn die **Recordset** ist hierarchisch aufgebaut ist, klicken Sie dann auf der aktuellen untergeordneten **Recordset** und seine untergeordneten Elemente gespeichert sind, einschließlich der übergeordneten **Recordset**. Wenn die Save-Methode einer untergeordneten **Recordset** wird aufgerufen, das untergeordnete Element und alle seine untergeordneten Elemente werden gespeichert, das übergeordnete Element ist jedoch nicht.  
  
 Beim ersten Sie speichern die **Recordset**, ist er optional an *Ziel*. Wenn Sie weglassen *Ziel*, wird eine neue Datei erstellt werden, mit einem Namen, die auf den Wert der Source-Eigenschaft des festgelegt die **Recordset**.  
  
 Lassen Sie *Ziel* beim anschließend aufrufen **speichern** nach dem ersten Speichern oder einen Fehler zur Laufzeit erfolgt. Wenn anschließend Sie rufen **speichern** mit einem neuen *Ziel*, die **Recordset** in das neue Ziel gespeichert wird. Allerdings wird das neue Ziel des ursprünglichen Zieles beide geöffnet werden.  
  
 **Speichern** schließt nicht die **Recordset** oder *Ziel*, damit Sie fortfahren können, mit der **Recordset** und die neuesten Änderungen zu speichern. *Ziel* bleibt geöffnet, bis die **Recordset** geschlossen wird.  
  
 Aus Gründen der Sicherheit die **speichern** Methode erlaubt nur die Verwendung von Sicherheit niedrig und benutzerdefinierte Einstellungen aus einem Skript, das von Microsoft Internet Explorer ausgeführt.  
  
 Wenn die **speichern** Methode wird aufgerufen, während eines asynchronen **Recordset** abzurufen, ausführen oder Aktualisieren der Vorgang wird ausgeführt, klicken Sie dann **speichern** wartet, bis der asynchrone Vorgang ist abgeschlossen.  
  
 Datensätze gespeichert werden, beginnend mit der ersten Zeile der **Recordset**. Wenn die **speichern** Methode abgeschlossen ist, wird die aktuelle Zeilenposition in der ersten Zeile der verschoben der **Recordset**.  
  
 Legen Sie für optimale Ergebnisse die [CursorLocation-Eigenschaft (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft **AdUseClient** mit **speichern**. Wenn Ihr Anbieter nicht alle Funktionen, die zum Speichern erforderlichen unterstützt **Recordset** Objekte aufweist, der Cursor-Dienst stellt diese Funktionalität bereit.  
  
 Wenn eine **Recordset** wird beibehalten, mit der **CursorLocation** -Eigenschaftensatz auf **AdUseServer**, die Update-Funktion für die **Recordset**ist beschränkt. In der Regel nur einzelne Tabelle Updates, einfügungen und löschungen (hängt Anbieterfunktionen) zulässig sind. Die [Resync-Methode](../../../ado/reference/ado-api/resync-method.md) Methode ist auch in dieser Konfiguration nicht verfügbar.  
  
> [!NOTE]
>  Speichern einer **Recordset** mit **Felder** des Typs **AdVariant**, **AdIDispatch**, oder **AdIUnknown** ist nicht von ADO unterstützt und kann zu unvorhersehbare Ergebnissen führen.  
  
 Nur in Form von Zeichenfolgen Kriterien gefiltert (z. B. OrderDate > ' 12/31/1999 ') wirken sich auf den Inhalt einer permanenten **Recordset**. Filter, die mit einem Array von erstellten **Lesezeichen** oder mithilfe eines Wertes aus der [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) wirkt sich nicht auf den Inhalt des beibehaltenen **Recordset**. Diese Regeln gelten für **Recordset**s mit Client- oder serverseitige Cursor erstellt wurde.  
  
 Da die *Ziel* Parameter akzeptiert jedes Objekt, das die OLE DB-IStream-Schnittstelle unterstützt, können Sie speichern eine **Recordset** direkt an die ASP-Response-Objekt. Weitere Informationen finden Sie unter der **Speicherszenario für XML-Recordset**.  
  
 Sie können auch Speichern einer **Recordset** im XML-Format mit einer Instanz von einem MSXML DOM-Objekt, wie im folgenden Visual Basic-Code dargestellt ist:  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=Northwind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistXML   'Save Recordset directly into a DOM tree.  
...  
```  
  
> [!NOTE]
>  Zwei Einschränkungen gelten beim hierarchische Recordsets (Daten-Shapes) im XML-Format zu speichern. Sie können in XML speichern, wenn die hierarchische **Recordset** enthält ausstehende Updates, und Sie können nicht gespeichert werden eine parametrisierte hierarchische **Recordset**.  
  
 Ein **Recordset** gespeichert in XML-Element wird mit UTF-8-Format Format gespeichert. Wenn eine solche Datei in eine ADO-Stream geladen wird, das Datenstromobjekt versucht nicht, öffnen Sie eine **Recordset** aus dem Stream, wenn der Charset-Eigenschaft des Streams auf den entsprechenden Wert für das UTF-8-Format festgelegt ist.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Speichern Sie und öffnen Sie die Methoden-Beispiel (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Speichern Sie und öffnen Sie die Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open-Methode (ADO-Datenstrom)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [SaveToFile-Methode](../../../ado/reference/ado-api/savetofile-method.md)
