---
title: Datenabschnitt | Microsoft Docs
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
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc7a8e66765d35d4c8a8a7f74f63720dec4d9429
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-section"></a>Datenabschnitt
Der Datenabschnitt definiert die Daten des Schemarowsets zusammen mit allen ausstehenden Updates, einfügungen oder löschungen. Der Datenabschnitt kann NULL oder mehr Zeilen enthalten. Es kann nur Daten aus einem Rowset enthalten, in die Zeile durch das Schema definiert ist. Darüber hinaus können wie bereits erwähnt, Spalten ohne Daten ausgelassen werden. Wenn ein Attribut oder ein Unterelement im Datenabschnitt verwendet wird, und das Konstrukt nicht im Schema-Abschnitt definiert wurde, wird es ignoriert.  
  
## <a name="string"></a>String  
 Reservierte XML-Zeichen in Textdaten müssen durch entsprechende Zeichenentitäten ersetzt werden. Beispielsweise muss in den Firmennamen "Jürgens Werkstatt", das einfache Anführungszeichen durch eine Entität ersetzt. Die tatsächliche Zeile würde folgendermaßen aussehen:  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 Die folgenden Zeichen sind in XML reserviert und müssen ersetzt werden, indem Sie Zeichenentitäten: {",", &,\<, >}.  
  
## <a name="binary"></a>Binär (Binary)  
 Binärdaten sind bin.hex codiert werden (d. h. ein Byte sind zwei Zeichen zugeordnet, ein Zeichen pro Nibble).  
  
## <a name="datetime"></a>datetime  
 Variante VT_DATE-Format wird von XML-Data-Datentypen nicht direkt unterstützt. Das richtige Format für Datumsangaben, mit der Komponente eine Daten und die Uhrzeit lautet jjjj-mm-ddTHH.  
  
 Weitere Informationen zu Datumsformaten gemäß XML finden Sie unter der [W3C XML-Data-Spezifikation](https://go.microsoft.com/fwlink/?LinkId=5692).  
  
 Wenn die XML-Data-Spezifikation definiert zwei äquivalente Datentypen (z. B. i4 == Int), ADO ausgeschrieben werden der Anzeigename wird jedoch in beiden lesen.  
  
## <a name="managing-pending-changes"></a>Verwalten von ausstehenden Änderungen  
 Ein Recordset in sofortige geöffnet werden kann oder die Aktualisierung im Batchmodus. Wenn sie im Batchmodus für Update mit clientseitigen Cursorn geöffnet sind, werden alle Änderungen an das Recordset im Status "Ausstehend", bis die UpdateBatch-Methode aufgerufen wird. Ausstehende Änderungen werden auch beibehalten, wenn das Recordset gespeichert wird. In XML, werden sie durch die Verwendung von "Update"-Elemente, die im Urn: Schemas definierten dargestellt-Microsoft-Com:rowset. Darüber hinaus, wenn ein Rowset aktualisiert werden kann, die aktualisierbare Eigenschaft muss festgelegt werden in der Definition der Zeile "true". Definieren, die Shippers-Tabelle enthält ausstehende Änderungen, die Zeilendefinition würde beispielsweise aussehen ähneln folgenden.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 Das weist den Persistenz-Provider Daten, damit ADO ein aktualisierbares Recordset-Objekt erstellen kann.  
  
 Die folgenden Beispieldaten wird gezeigt, wie Einfüge-, Änderungen und löschungen in der permanenten Datei suchen.  
  
```  
<rs:data>  
  <z:row ShipperID="2" CompanyName="United Package"   
    Phone="(503) 555-3199"/>  
<rs:update>  
  <rs:original>  
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>  
  </rs:original>  
  <z:row Phone="(503) 552-7134"/>  
</rs:update>  
<rs:insert>  
  <z:row ShipperID="12" CompanyName="Lightning Shipping"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="13" CompanyName="Thunder Overnight"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="14" CompanyName="Blue Angel Air Delivery"   
    Phone="(505) 111-2222"/>  
</rs:insert>  
<rs:delete>  
  <z:row ShipperID="1" CompanyName="Speedy Express" Phone="(503) 555-9831"/>  
</rs:delete>  
</rs:data>  
```  
  
 Ein Update enthält immer die gesamte ursprüngliche Zeilendaten, gefolgt von Daten aus der geänderten Zeile. Alle Spalten oder nur die Spalten, die tatsächlich geändert wurden, kann die geänderte Zeile enthalten. Im vorherigen Beispiel die Zeile für Shipper 2 wird nicht geändert, und nur in die Spalte Phone Shipper 3 Werte geändert wurde und daher die einzige Spalte, die in der geänderten Zeile enthalten ist. Die eingefügten Zeilen für Shippers 12, 13 und 14 werden im Batchmodus zusammen unter einer Rs: Insert-Tag. Beachten Sie, dass es sich bei gelöschte Zeilen auch zusammen als Batch verarbeitet werden können, auch wenn dies im vorherigen Beispiel nicht angezeigt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)
