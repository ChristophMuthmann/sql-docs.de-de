---
title: XML-Format die Persistenz | Microsoft Docs
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
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09baccad7dbe8d8f6d5363c177eb5242d9a1bc42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xml-persistence-format"></a>XML-Format die Persistenz
ADO verwendet UTF-8-Codierung für die XML-Datenstrom.  
  
 Das ADO-XML-Format wird in zwei Abschnitten, einen Schemaabschnitt gefolgt von den Datenabschnitt unterteilt. Im folgenden ist eine XML-Beispieldatei für die Shippers-Tabelle aus der Northwind-Datenbank. Verschiedene Teile des XML werden folgende das Beispiel erläutert.  
  
## <a name="remarks"></a>Hinweise  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"   
xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"   
xmlns:rs="urn:schemas-microsoft-com:rowset"   
xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="ShipperID" rs:number="1"   
        rs:basetable="shippers" rs:basecolumn="ShipperID"  
        rs:keycolumn="true">   
        <s:datatype dt:type="int" dt:maxLength="4" rs:precision="10"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="CompanyName" rs:number="2"   
        rs:nullable="true" rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="CompanyName">   
        <s:datatype dt:type="string" dt:maxLength="40" />   
      </s:AttributeType>   
      <s:AttributeType name="Phone" rs:number="3" rs:nullable="true"   
        rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="Phone">   
        <s:datatype dt:type="string" dt:maxLength="24"/>   
      </s:AttributeType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  
  <rs:data>   
    <z:row ShipperID="1" CompanyName="Speedy Express"   
      Phone="(503) 555-9831"/>   
    <z:row ShipperID="2" CompanyName="United Package"   
      Phone="(503) 555-3199"/>   
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>   
  </rs:data>   
</xml>  
```  
  
 Das Schema zeigt die Deklarationen des Namespaces, Schemaabschnitt und im Datenabschnitt. Der Schemaabschnitt enthält Definitionen für die Zeile, Firmen-Nr, CompanyName und Telefonnummer.  
  
 Schemadefinitionen entsprechen den [W3C XML-Data-Spezifikation](http://www.w3.org/TR/1998/NOTE-XML-data/) und können vollständig überprüft werden, (obwohl die Überprüfung nicht im Internet Explorer 5 erfolgt). XML-Daten ist derzeit das einzige unterstützte Schemaformat für den Recordset permanenten Speicher.  
  
 Der Datenabschnitt enthält drei Zeilen, die mit Informationen zu Lieferanten. Für ein leeres Rowset Datenabschnitt möglicherweise leer, aber die \<Rs: Data >-Tags müssen vorhanden sein. Ohne Daten das Tag die Kurzform so weit geschrieben \<Rs: Data / >. Alle Tags, die mit dem Präfix "Rs" gibt an, dass er den Namespace Urn: Schemas definiert wird – Microsoft-Com:rowset.  
  
## <a name="see-also"></a>Siehe auch  
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)
