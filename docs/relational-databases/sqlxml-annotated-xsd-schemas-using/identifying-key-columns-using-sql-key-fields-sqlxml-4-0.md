---
title: 'Identifizieren von Schlüsselspalten mithilfe von SQL: Key-Feldern (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- nesting XML results
- proper nesting in results [SQLXML]
- sql:key-fields
- XSD schemas [SQLXML], key columns
- identifying key columns [SQLXML]
- annotated XSD schemas, key columns
- key columns [SQLXML]
- relationships [SQLXML], key columns
- hierarchical relationships [SQLXML]
- key-fields annotation
ms.assetid: 1a5ad868-8602-45c4-913d-6fbb837eebb0
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9537b116415c9620b31ad98348bcea6aca7fefe2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="identifying-key-columns-using-sqlkey-fields-sqlxml-40"></a>Identifizieren von Schlüsselspalten mithilfe von sql:key-Feldern (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Wenn eine XPath-Abfrage für ein XSD-Schema angegeben wird, ist die Schlüsselinformationen in den meisten Fällen erforderlich, um richtige Schachtelung im Ergebnis zu erhalten. Angeben der **SQL: Key-Felder** Anmerkung ist, lässt sich sicherstellen, dass die entsprechende Hierarchie generiert wird.  
  
> [!NOTE]  
>  Um die richtige Schachtelung sicherzustellen, wird empfohlen, dass Sie angeben, **SQL: Key-Felder** für Elemente, die Tabellen zugeordnet. Das erzeugte XML wird durch die Anordnung des zugrunde liegenden Resultsets beeinflusst. Wenn **SQL: Key-Felder** nicht angegeben ist, wird die generierte XML-Code möglicherweise nicht ordnungsgemäß formatiert.  
  
 Der Wert der **SQL: Key-Felder** identifiziert die Spalte(n), die die Zeilen in der Beziehung eindeutig identifiziert. Wenn mehrere Spalten zur eindeutigen Identifizierung einer Zeile erforderlich sind, werden die Spaltenwerte jeweils durch ein Leerzeichen voneinander getrennt.  
  
 Verwenden Sie die **SQL: Key-Felder** Anmerkung, wenn ein Element enthält eine  **\<SQL: Relationship >** , die zwischen dem Element und einem untergeordneten Element definiert ist, jedoch bietet keinen Primärschlüssel der Tabelle, die im übergeordneten Element angegeben wird.  
  
## <a name="examples"></a>Beispiele  
 Es müssen bestimmte Anforderungen erfüllt sein, damit aus den folgenden Beispielen funktionierende Beispiele erstellt werden können. Weitere Informationen finden Sie unter [Anforderungen für die Ausführung von SQLXML-Beispielen](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-producing-the-appropriate-nesting-when-sqlrelationship-does-not-provide-sufficient-information"></a>A. Erzeugen der entsprechenden Schachtelung, wenn \<SQL: Relationship > keine ausreichenden Informationen bereitstellt  
 Dieses Beispiel zeigt, wo **SQL: Key-Felder** muss angegeben werden.  
  
 Betrachten Sie folgendes Schema. Das Schema gibt eine hierarchische Beziehung zwischen der  **\<Reihenfolge >** und  **\<Kunden >** Elemente, in denen die  **\<Reihenfolge >**Element ist das übergeordnete Element und die  **\<Kunden >** -Element untergeordnet ist.  
  
 Die  **\<SQL: Relationship >** Tag wird verwendet, um die über-/ unterordnungsbeziehung geben. In diesem Tag wird CustomerID als übergeordneter Schlüssel identifiziert, der auf die untergeordnete CustomerID-Schlüsselspalte in der Sales.Customer-Tabelle verweist. Die Informationen im  **\<SQL: Relationship >** reicht nicht aus, um Zeilen in der übergeordneten Tabelle (Sales.SalesOrderHeader) eindeutig zu identifizieren. Aus diesem Grund, ohne die **SQL: Key-Felder** Anmerkung in die Hierarchie, die generiert wird, ist ungenau.  
  
 Mit **SQL: Key-Felder** auf angegebenen  **\<Reihenfolge >**eindeutig identifiziert die Anmerkung die Zeilen in der übergeordneten Tabelle (Sales.SalesOrderHeader-Tabelle) und die untergeordneten Elemente werden unten der übergeordnete Element.  
  
 Das ist das Schema:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrdCust"  
        parent="Sales.SalesOrderHeader"  
        parent-key="CustomerID"  
        child="Sales.Customer"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
               sql:key-fields="SalesOrderID">  
   <xsd:complexType>  
     <xsd:sequence>  
     <xsd:element name="Customer" sql:relation="Sales.Customer"   
                       sql:relationship="OrdCust"  >  
       <xsd:complexType>  
         <xsd:attribute name="CustID" sql:field="CustomerID" />  
         <xsd:attribute name="SoldBy" sql:field="SalesPersonID" />  
       </xsd:complexType>  
     </xsd:element>  
     </xsd:sequence>  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name= "CustomerID" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>So erstellen Sie ein funktionstüchtiges Beispiel für dieses Schema  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen KeyFields1.xml.  
  
2.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen KeyFields1T.xml im gleichen Verzeichnis, in dem Sie KeyFields1.xml gespeichert haben. Die XPath-Abfrage in der Vorlage gibt alle dem  **\<Reihenfolge >** Elemente, deren CustomerID-Wert kleiner als 3.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="KeyFields1.xml">  
            /Order[@CustomerID < 3]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (KeyFields1.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields1.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird ein Teil des Resultsets aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
    <Order SalesOrderID="43860" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="44501" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="45283" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    .....  
</ROOT>  
```  
  
### <a name="b-specifying-sqlkey-fields-to-produce-proper-nesting-in-the-result"></a>B. Angeben der sql:key-Felder, um die richtige Schachtelung im Ergebnis zu erzeugen  
 Im folgenden Schema besteht keine durch festgelegte Hierarchie  **\<SQL: Relationship >**. Das Schema erfordert trotzdem die Angabe der **SQL: Key-Felder** Anmerkung, die Mitarbeiter in der Tabelle HumanResources.Employee eindeutig zu identifizieren.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="HumanResources.Employee" sql:key-fields="EmployeeID" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Title">  
          <xsd:complexType>  
            <xsd:simpleContent>  
              <xsd:extension base="xsd:string">  
                 <xsd:attribute name="EmployeeID" type="xsd:integer" />  
              </xsd:extension>  
            </xsd:simpleContent>  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
   </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>So erstellen Sie ein funktionstüchtiges Beispiel für dieses Schema  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen KeyFields2.xml.  
  
2.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen KeyFields2T.xml im gleichen Verzeichnis, in dem Sie KeyFields2.xml gespeichert haben. Die XPath-Abfrage in der Vorlage gibt alle dem  **\<HumanResources.Employee >** Elemente:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="KeyFields2.xml">  
        /HumanResources.Employee  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (KeyFields2.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields2.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Dies ist das Ergebnis:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <HumanResources.Employee>  
    <Title EmployeeID="1">Production Technician - WC60</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="2">Marketing Assistant</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="3">Engineering Manager</Title>   
  </HumanResources.Employee>  
  ...  
</ROOT>  
```  
  
  
