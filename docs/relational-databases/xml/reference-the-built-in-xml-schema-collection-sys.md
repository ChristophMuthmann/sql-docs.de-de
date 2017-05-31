---
title: Verweisen auf die integrierte XML-Schemaauflistung (sys) | Microsoft-Dokumentation
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
- sys XML schema collections [SQL Server]
- schema collections [SQL Server], predefined
- predefined XML schema collections [SQL Server]
- XML schema collections [SQL Server], predefined
- built-in XML schema collections [SQL Server]
ms.assetid: 1e118303-5df0-4ee4-bd8d-14ced7544144
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fa2b103a4c846e52c9af999980bb3c8080a4f6d5
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="reference-the-built-in-xml-schema-collection-sys"></a>Verweisen auf die integrierte XML-Schemaauflistung (sys)
  Jede Datenbank, die Sie erstellen, besitzt eine vordefinierte **sys** -XML-Schemaauflistung im relationalen **sys** -Schema. Es reserviert diese vordefinierten Schemas, und der Zugriff darauf kann aus einer beliebigen, von einem Benutzer erstellten XML-Schemaauflistung erfolgen. Die in diesen vordefinierten Schemas verwendeten Präfixe sind in XQuery von Bedeutung. Nur **xml** ist ein reserviertes Präfix.  
  
```  
xml = http://www.w3.org/XML/1998/namespace  
xs = http://www.w3.org/2001/XMLSchema  
xsi = http://www.w3.org/2001/XMLSchema-instance  
fn = http://www.w3.org/2004/07/xpath-functions  
sqltypes = http://schemas.microsoft.com/sqlserver/2004/sqltypes  
xdt = http://www.w3.org/2004/07/xpath-datatypes  
(no prefix) = urn:schemas-microsoft-com:xml-sql  
(no prefix) = http://schemas.microsoft.com/sqlserver/2004/SOAP  
```  
  
 Beachten Sie, dass der **sqltypes** -Namespace Komponenten enthält, auf die aus jeder beliebigen, von einem Benutzer erstellten XML-Schemaauflistung verwiesen werden kann. Sie können das **sqltypes** -Schema von dieser [Microsoft-Website](http://go.microsoft.com/fwlink/?linkid=31850)herunterladen. Die folgenden Komponenten sind z. B. integriert:  
  
-   XSD-Typen  
  
-   Die XML-Attribute **lang**, **base**und **space**  
  
-   Komponenten des **sqltypes** -Namespace  
  
 Die folgende Abfrage gibt integrierte Komponenten zurück, auf die aus einer von einem Benutzer erstellten XML-Schemaauflistung verwiesen werden kann:  
  
```  
SELECT C.name, N.name, C.symbol_space_desc from sys.xml_schema_components C join sys.xml_schema_namespaces N  
on ((C.xml_namespace_id = N.xml_namespace_id) AND (C.xml_collection_id = N.xml_collection_id))  
join sys.xml_schema_collections SC  
on SC.xml_collection_id = C.xml_collection_id  
where ((C.xml_collection_id = 1) AND (C.name is not null) AND (C.scoping_xml_component_id is null)   
AND (SC.schema_id = 4))  
GO  
```  
  
 Im folgenden Beispiel wird veranschaulicht, wie auf diese Komponenten in einem Benutzerschema verwiesen wird. `CREATE XML SCHEMA COLLECTION` erstellt eine XML-Schemasammlung, die auf den im `varchar` -Namespace definierten `sqltypes` -Typ verweist. Das Beispiel verweist außerdem auf das `lang` -Attribut, das im `xml` -Namespace definiert wurde.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema   
   xmlns="http://www.w3.org/2001/XMLSchema"   
   targetNamespace="myNS"  
   xmlns:ns="myNS"  
   xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
   <import namespace="http://www.w3.org/XML/1998/namespace"/>  
   <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
   <element name="root">  
      <complexType>  
          <sequence>  
             <element name="a" type="string"/>  
             <element name="b" type="string"/>  
             <!-- varchar type is defined in the sys.sys collection and   
                  can be referenced in any user-defined schema -->  
             <element name="c" type="s:varchar"/>  
          </sequence>  
          <attribute name="att" type="int"/>  
          <!-- xml:lang attribute is defined in the sys.sys collection   
               and can be referenced in any user-defined schema -->  
          <attribute ref="xml:lang"/>  
      </complexType>  
    </element>  
 </schema>'  
GO  
 -- Cleanup  
DROP xml schema collection SC   
GO  
```  
  
 Beachten Sie Folgendes:  
  
-   Sie können keine XML-Schemas mit diesen Namespaces in benutzerdefinierten XML-Schemaauflistungen ändern. Die folgende XML-Schemaauflistung verursacht einen Fehler, weil dem geschützten Namespace `sqltypes` eine Komponente hinzugefügt wird:  
  
    ```  
    CREATE XML SCHEMA COLLECTION SC AS '  
    <schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace    
        ="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
          <element name="root" type="string"/>  
    </schema>'  
    GO  
    ```  
  
-   Sie können die XML-Schemaauflistung `sys` nicht zum Typisieren von Spalten, Variablen oder Parametern von `xml` verwenden. So gibt z. B. der folgende Code einen Fehler zurück:  
  
    ```  
    DECLARE @x xml (sys.sys)  
    ```  
  
-   Die Serialisierung dieser integrierten Schemas wird nicht unterstützt. So gibt z. B. der folgende Code einen Fehler zurück:  
  
    ```  
    SELECT XML_SCHEMA_NAMESPACE(N'sys',N'sys')  
    GO  
    ```  
  
 Auch mit dem Code im folgenden Beispiel wird eine XML-Schemaauflistung erstellt, die den `varchar`-Datentyp verwendet, der im `sqltypes`-Namespace definiert wurde:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="myNS" xmlns:ns="myNS"  
        xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
   <import     
     namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
            <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
go  
```  
  
 Wie das folgende Beispiel zeigt, können Sie eine typisierte `XML`-Variable erstellen, dieser eine XML-Instanz zuweisen und dann überprüfen, ob der Wert des <`root`>-Elementtyps vom Typ `varchar` ist.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
GO  
```  
  
 Der Ausdruck `instance of sqltypes:varchar?`gibt TRUE zurück, weil der Wert des Elements <`root`> einem Typ entspricht, der gemäß dem Schema, das der `@var`-Variablen zugeordnet ist, von **varchar** abgeleitet wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
