---
title: Schema-Abschnitt | Microsoft Docs
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
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7614a2c23d21d88652c32fef480367df4db65be8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="schema-section"></a>Schema-Abschnitt
Der Schemaabschnitt ist erforderlich. Wie im vorherigen Beispiel wird gezeigt, schreibt ADO detaillierter Metadaten zu jeder Spalte auf die Semantik der Datenwerte für die Aktualisierung so weit wie möglich beibehalten. Um in der XML-Code zu laden, erfordert ADO jedoch nur die Namen der Spalten und das Rowset, zu dem sie gehören. Hier ist ein Beispiel für ein minimales Schema:  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 Im vorherigen Beispiel wird ADO die Daten als Zeichenfolgen mit variabler Länge behandelt, da keine Typinformationen im Schema enthalten ist.  
  
## <a name="creating-aliases-for-column-names"></a>Erstellen von Aliasen für Spaltennamen  
 Das Rs: Name-Attribut können Sie einen Alias für einen Spaltennamen zu erstellen, sodass ein Anzeigename möglicherweise, in die Spalteninformationen, die vom Rowset verfügbar gemacht angezeigt, und ein kürzerer Namen im Datenabschnitt verwendet werden dürfen. Beispielsweise kann das vorherige Schema zum Zuordnen von Firmen-Nr s1, S2, CompanyName und Smartphone, um s3 wie folgt geändert werden:  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 Anschließend wird im Datenabschnitt, die Zeile das Name-Attribut (nicht Rs: Name) mit würde auf diese Spalte verweisen:  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 Erstellen Aliase für Spaltennamen ist erforderlich, wenn ein Spaltenname kein gültiges Attribut oder in XML-Tagnamen ist. Z. B. "LastName" einen Alias besitzen muss, da Namen mit Leerzeichen ungültige Attribute sind. Die folgende Zeile wird nicht ordnungsgemäß von der XML-Parser behandelt werden, daher müssen Sie einen Alias in einen anderen Namen erstellen, die nicht über ein eingebettetes Leerzeichen verfügt.  
  
```  
<row last name="Jones"/>  
```  
  
 Der Wert, den Sie für die Name-Attribut verwenden, muss einheitlich an jeder Stelle verwendet werden, dass die Spalte in Abschnitten von Schema und Daten von XML-Dokument verwiesen wird. Das folgende Beispiel zeigt die konsistente Verwendung von s1:  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 Auf ähnliche Weise, da es ist kein Alias definiert für `CompanyName` im vorherigen Beispiel `CompanyName` muss im gesamten Dokument einheitlich verwendet werden.  
  
## <a name="data-types"></a>Datentypen  
 Sie können einen Datentyp auf eine Spalte mit dem dt: Type-Attribut anwenden. Die Dokumentation zum zulässige XML-Datentypen, finden Sie im Abschnitt "Datentypen" von der [W3C XML-Data-Spezifikation](http://www.w3.org/TR/1998/NOTE-XML-data/). Sie können einen Datentyp auf zwei Arten angeben: Geben Sie das dt: Type-Attribut direkt auf die Definition der Spalte selbst oder verwenden Sie das Konstrukt S:datatype als ein geschachteltes Element der Spaltendefinition. Beispiel:  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 ist gleich  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 Wenn Sie das dt: Type-Attribut vollständig aus der Zeilendefinition, in der Standardeinstellung weglassen, werden den Datentyp der Spalte eine Zeichenfolge variabler Länge.  
  
 Wenn Sie weitere Typinformationen als einfach den Typnamen (z. B. dt: MaxLength) haben, ist es besser lesbar, die S:datatype untergeordnete Element zu verwenden. Dies ist lediglich eine Konvention, jedoch nicht zwingend.  
  
 Die folgenden Beispiele zeigen, wie Ihr Schema Typinformationen einschließt.  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!—or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!—- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!—- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!—- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 Es ist eine geringfügige Verwendung des Rs: Fixedlength-Attributs im zweiten Beispiel. Legen Sie eine Spalte mit dem Rs: Fixedlength-Attribut auf "true" bedeutet, die die Daten die im Schema definierte Länge aufweisen müssen. In diesem Fall ist ein gültiger Wert für Title_id "123456," unverändert "123". Allerdings würde "123" nicht gültig, da seine Länge 3, nicht 6 ist. Finden Sie unter der OLE DB Programmer's Guide ausführlicher Beschreibung der Eigenschaft Fixedlength abzuschließen.  
  
## <a name="handling-nulls"></a>Behandlung von NULL-Werte  
 NULL-Werte werden durch das Attribut Rs: Maybenull verarbeitet. Wenn dieses Attribut festgelegt ist, auf "true", den Inhalt der Spalte einen null-Wert enthalten können. Darüber hinaus, wenn die Spalte in eine Zeile mit Daten nicht gefunden wird, wird der Benutzer, die Lesen von Daten aus dem Rowset wieder einen Nullstatus IRowset::GetData() bekommen. Berücksichtigen Sie die folgenden Definitionen der Spalten aus der Shippers-Tabelle.  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 Ermöglicht die Definition `CompanyName` null ist, werden jedoch `ShipperID` darf keine null-Wert enthalten. Wenn Datenabschnitt die folgende Zeile enthält, würde der Persistenz-Provider Festlegen des Status der Daten für die `CompanyName` Spalte auf die OLE DB-Status-Konstante DBSTATUS_S_ISNULL:  
  
```  
<z:row ShipperID="1"/>  
```  
  
 Wenn die Zeile wie folgt vollständig leer war, würde der Persistenz-Provider OLE DB-Status DBSTATUS_E_UNAVAILABLE für zurückgeben `ShipperID` und DBSTATUS_S_ISNULL für CompanyName.  
  
```  
<z:row/>   
```  
  
 Beachten Sie, dass eine Zeichenfolge der Länge 0 (null) nicht Null ist.  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 Für die vorangehende Zeile gibt den Persistenz-Provider OLE DB-Status DBSTATUS_S_OK für beide Spalten zurück. Die `CompanyName` in diesem Fall ist es, einfach "" (eine Zeichenfolge der Länge 0 (null)).  
  
 Weitere Informationen zu den OLE DB-zur Verwendung innerhalb des Schemas eines XML-Dokuments für OLE DB-Konstrukte, finden Sie unter der Definition von "Urn: Schemas-Microsoft-Com:rowset" und der OLE DB Programmer's Guide.  
  
## <a name="see-also"></a>Siehe auch  
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)
