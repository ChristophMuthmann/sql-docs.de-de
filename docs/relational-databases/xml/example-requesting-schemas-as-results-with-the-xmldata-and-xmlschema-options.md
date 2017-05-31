---
title: 'Beispiel: Anfordern von Schemas als Ergebnisse mithilfe der Optionen XMLDATA und XMLSCHEMA | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RAW mode, requesting schema example
- RAW mode, with XMLDATA and XMLSCHEMA
ms.assetid: 3504ca38-be66-42b2-8dab-f499c9584840
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bca71096e7e34aa6a72c84f065fd7df76eb6462f
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options"></a>Beispiel: Anfordern von Schemas als Ergebnisse mithilfe der Optionen XMLDATA und XMLSCHEMA
  Die folgende Abfrage gibt das XML-Datenschema zurück, das die Dokumentstruktur beschreibt.  
  
## <a name="example"></a>Beispiel  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, XMLDATA  
GO  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Schema name="Schema1" xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="row" content="empty" model="closed">  
    <AttributeType name="ProductModelID" dt:type="i4" />  
    <AttributeType name="Name" dt:type="string" />  
    <attribute type="ProductModelID" />  
    <attribute type="Name" />  
  </ElementType>  
</Schema>  
<row xmlns="x-schema:#Schema1" ProductModelID="122" Name="All-Purpose Bike Stand" />  
<row xmlns="x-schema:#Schema1" ProductModelID="119" Name="Bike Wash" />  
```  
  
> [!NOTE]  
>  Das <`Schema`> ist als Namespace deklariert. Damit Namespacekonflikte vermieden werden, wenn mehrere XML-Datenschemas in verschiedenen FOR XML-Abfragen angefordert werden, wird der Namespacebezeichner – in diesem Beispiel `Schema1` – bei jeder Abfrageausführung geändert. Der Namespacebezeichner setzt sich aus **Schema*n*zusammen, wobei ***n*** eine ganze Zahl ist.  
  
 Durch Angeben der Option `XMLSCHEMA` können Sie das XSD-Schema für das Ergebnis anfordern.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, XMLSCHEMA  
GO  
```  
  
 Dies ist das Ergebnis:  
  
```  
<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="row">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="122" Name="All-Purpose Bike Stand" />  
<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="119" Name="Bike Wash" />  
  
```  
  
 Sie können den Zielnamespace-URI als optionales Argument für XMLSCHEMA in FOR XML angeben. Auf diese Weise wird der angegebene Zielnamespace im Schema zurückgegeben. Dieser Zielnamespace bleibt bei jeder Ausführung der Abfrage gleich. Die folgende geänderte Version der vorherigen Abfrage enthält z. B. den Namespace-URI `'urn:example.com'`als Argument.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, XMLSCHEMA ('urn:example.com')  
GO  
```  
  
 Dies ist das Ergebnis:  
  
```  
<xsd:schema targetNamespace="urn:example.com" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="row">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<row xmlns="urn:example.com" ProductModelID="122" Name="All-Purpose Bike Stand" />  
<row xmlns="urn:example.com" ProductModelID="119" Name="Bike Wash" />  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
