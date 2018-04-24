---
title: Hierarchische Recordsets in XML | Microsoft Docs
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
helpviewer_keywords:
- hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 86fa04ed8be926982464d10fd4d63996df358d1f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="hierarchical-recordsets-in-xml"></a>Hierarchische Recordsets im XML-Format
ADO ermöglicht Persistenz hierarchische Recordset-Objekte in XML. Mit hierarchischen Recordset-Objekte ist der Wert eines Felds in der übergeordneten Recordset eine andere Recordset. Diese Felder werden als untergeordnete Elemente in der XML-Datenstrom, anstatt ein Attribut dargestellt.  
  
## <a name="remarks"></a>Hinweise  
 Das folgende Beispiel veranschaulicht diesen Fall:  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 Im folgenden finden das XML-Format des beibehaltenen Recordsets:  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
    xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="stor_id" rs:number="1"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="4"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="stor_name" rs:number="2" rs:nullable="true"   
        rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="40"/>   
      </s:AttributeType>   
      <s:AttributeType name="state" rs:number="3" rs:nullable="true"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="2"   
          rs:fixedlength="true"/>   
      </s:AttributeType>   
      <s:ElementType name="rsSales" content="eltOnly"   
        rs:updatable="true" rs:relation="010000000100000000000000">   
        <s:AttributeType name="stor_id" rs:number="1"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="4"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_num" rs:number="2"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="20"   
            rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_date" rs:number="3"   
          rs:writeunknown="true">   
            <s:datatype dt:type="dateTime" dt:maxLength="16"   
              rs:scale="3" rs:precision="23" rs:fixedlength="true"   
              rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="qty" rs:number="4" rs:writeunknown="true">   
          <s:datatype dt:type="i2" dt:maxLength="2" rs:precision="5"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:extends type="rs:rowbase"/>   
      </s:ElementType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  <rs:data>   
    <z:row stor_id="6380" stor_name="Eric the Read Books" state="WA">   
      <rsSales stor_id="6380" ord_num="6871"   
        ord_date="1994-09-14T00:00:00" qty="5"/>   
      <rsSales stor_id="6380" ord_num="722a"   
        ord_date="1994-09-13T00:00:00" qty="3"/>   
    </z:row>   
    <z:row stor_id="7066" stor_name="Barnum's" state="CA">   
      <rsSales stor_id="7066" ord_num="A2976"   
        ord_date="1993-05-24T00:00:00" qty="50"/>   
      <rsSales stor_id="7066" ord_num="QA7442.3"   
        ord_date="1994-09-13T00:00:00" qty="75"/>   
    </z:row>   
    <z:row stor_id="7067" stor_name="News & Brews" state="CA">   
      <rsSales stor_id="7067" ord_num="D4482"   
        ord_date="1994-09-14T00:00:00" qty="10"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="40"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
    </z:row>   
  </rs:data>   
</xml>   
```  
  
 Die genaue Reihenfolge der Spalten in der übergeordneten Recordset ist nicht offensichtlich, wenn sie auf diese Weise beibehalten wird. Jedes Feld in das übergeordnete Element kann ein untergeordnetes Element Recordset enthalten. Der Persistenz-Provider speichert alle Skalarspalten zuerst als Attribute und speichert dann alle untergeordneten Recordset "Spalten" als untergeordnete Elemente der übergeordneten Zeile. Die Ordnungsposition des Felds in der übergeordneten Tabelle kann Recordset durch einen Blick auf die Schemadefinition des Recordset-Objekts abgerufen werden. Jedes Feld hat eine OLE DB-Eigenschaft Rs: Anzahl, definiert in der Recordset-Schemanamespace, der die Ordinalzahl für dieses Feld enthält.  
  
 Die Namen aller Felder in der untergeordneten Recordsets werden mit dem Namen des Felds in der übergeordneten Recordset verkettet, die dieses untergeordnete Element enthält. Dadurch wird sichergestellt, dass keine Namenskonflikte in Fällen, in dem übergeordneten und untergeordneten Recordsets, die beide ein Feld enthalten, aus zwei verschiedenen Tabellen abgerufen wird, aber heißt und trägt gleichzeitig Mitverantwortung, vorhanden sind.  
  
 Wenn hierarchische Recordsets in XML speichern möchten, sollten Sie in ADO die folgenden Einschränkungen bewusst sein:  
  
-   Ein hierarchisches Recordset mit ausstehende Updates kann nicht in XML beibehalten werden.  
  
-   Eine hierarchische Recordset-Objekt erstellt, mit einem parametrisierten Shape-Befehl kann nicht (im XML- oder ADTG-Format) beibehalten werden.  
  
-   ADO speichert derzeit die Beziehung zwischen übergeordneten und untergeordneten Recordsets als ein binary large Object (BLOB). XML-Tags zur Beschreibung dieser Beziehung wurden noch nicht im Rowsetschemanamespace definiert.  
  
-   Wenn ein hierarchisches Recordset gespeichert wird, werden alle untergeordneten Recordsets darin gespeichert. Wenn der aktuelle Recordset ein untergeordnetes Element von einem anderen Recordset, ist nicht seinem übergeordneten Element gespeichert. Alle untergeordneten Recordsets, die die Teilstruktur des aktuellen Recordset bilden gespeichert.  
  
 Wenn ein hierarchisches Recordset aus dem persistent gespeicherte XML-Format wieder geöffnet wird Ihnen die folgenden Einschränkungen bewusst sein müssen:  
  
-   Wenn der Datensatz untergeordnete Datensätze für die keine entsprechenden übergeordneten Datensätze vorhanden sind enthält, werden diese Zeilen nicht in der XML-Darstellung des hierarchischen Recordsets geschrieben. Daher werden diese Zeilen verloren gehen beim erneuten des Recordsets Speicherort öffnen.  
  
-   Wenn ein untergeordneter Datensatz Verweise auf mehr als einen übergeordneten Datensatz verfügt, klicken Sie dann beim erneuten Öffnen des Recordsets untergeordneten Recordset doppelte enthält möglicherweise Datensätze. Allerdings werden diese Duplikate nur sichtbar, wenn der Benutzer direkt mit dem zugrunde liegenden untergeordneten Rowset arbeitet. Wenn einem Kapitel untergeordneten Recordset navigieren (das ist die einzige Möglichkeit zum Navigieren durch ADO) verwendet wird, sind die Duplikate nicht sichtbar.  
  
## <a name="see-also"></a>Siehe auch  
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)
