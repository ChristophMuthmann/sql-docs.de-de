---
title: 'Angeben von Beziehungen mithilfe von SQL: Relationship (SQLXML 4.0) | Microsoft Docs'
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- parent attribute [SQLXML]
- element relationships [SQLXML]
- multiple element relationships
- attribute relationships [SQLXML]
- sql:relationship
- relationship chains [SQLXML]
- IDREF relationships [SQLXML]
- parent-child relationships [SQLXML]
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- relationships [SQLXML], specifying
- unnamed relationships
- ID relationships [SQLXML]
- hierarchical relationships [SQLXML]
- named relationships [SQLXML]
ms.assetid: 98820afa-74e1-4e62-b336-6111a3dede4c
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce5968efc9238e44be3d66b2533da8951e28c907
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="specifying-relationships-using-sqlrelationship-sqlxml-40"></a>Angeben von Beziehungen mit 'sql:relationship' (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Die Elemente in einem XML-Dokument können verknüpft werden. Die Elemente können hierarchisch geschachtelt sein, und es können ID-, IDREF- oder IDREFS-Beziehungen zwischen den Elementen angegeben werden.  
  
 In einem XSD-Schema, z. B. eine  **\<Kunden >** Element enthält  **\<Reihenfolge >** untergeordnete Elemente. Wenn das Schema der AdventureWorks-Datenbank zugeordnet ist die  **\<Kunden >** -Element der Sales.Customer-Tabelle zugeordnet und die  **\<Reihenfolge >** -Element ordnet die Sales.SalesOrderHeader-Tabelle. Da Kunden Bestellungen aufgeben, stehen die zugrunde liegenden Tabellen Sales.Customer und Sales.SalesOrderHeader in Beziehung,. CustomerID in der Sales.SalesOrderHeader-Tabelle ist ein Fremdschlüssel, der auf den Primärschlüssel CustomerID in der Sales.Customer-Tabelle verweist. Sie können diese Beziehungen unter Elementen dieses Zuordnungsschemas mit Einrichten der **SQL: Relationship** Anmerkung.  
  
 In der XSD-Schema mit Anmerkungen die **SQL: Relationship** -Anmerkung verwendet, um die Elemente des Schemas hierarchisch zu schachteln, basierend auf Primärschlüssel und Fremdschlüssel-Beziehungen zwischen den zugrunde liegenden Tabellen, denen die Elemente zugeordnet. Bei Angabe der **SQL: Relationship** Anmerkung, müssen Sie Folgendes bestimmen:  
  
-   Die übergeordnete Tabelle (Sales.Customer) und die untergeordnete Tabelle (Sales.SalesOrderHeader).  
  
-   Die Spalte oder Spalten, die das Verhältnis zwischen übergeordneten und untergeordneten Tabellen festlegen. Beispiel: die Spalte CustomerID, die sowohl in übergeordneten als auch in untergeordneten Tabellen angezeigt wird.  
  
 Diese Informationen dienen dazu, die richtige Hierarchie zu erstellen.  
  
 Um die Tabellenamen und die erforderlichen joininformationen zu gewährleisten, werden die folgenden Attribute angegeben, auf die **SQL: Relationship** Anmerkung. Diese Attribute gelten nur für die  **\<SQL: Relationship >** Element:  
  
 **Name**  
 Gibt den eindeutigen Namen der Beziehung an.  
  
 **Parent**  
 Gibt die übergeordnete Beziehung (Tabelle) an. Dieses Attribut ist optional. Wird es nicht angegeben, wird der Name der übergeordneten Tabelle aus den Informationen in der untergeordneten Hierarchie des Dokuments abgerufen. Wenn das Schema zwei über-/ unterordnungshierarchien angibt, die die gleiche  **\<SQL: Relationship >** aber unterschiedliche übergeordnete Elemente verwenden, Sie nicht das übergeordnete Attribut in angeben  **\<Sql: Beziehung >**. Diese Informationen werden aus der Hierarchie im Schema abgerufen.  
  
 **übergeordneten Schlüssel**  
 Gibt den übergeordneten Schlüssel des übergeordneten Elements an. Wenn der übergeordnete Schlüssel aus mehreren Spalten besteht, werden Werte mit einer Leerstelle angegeben. Es besteht eine positionelle Zuordnung zwischen den Werten, die für den mehrspaltigen Schlüssel und für den entsprechenden untergeordneten Schlüssel festgelegt wurden.  
  
 **Untergeordnetes Element**  
 Gibt die untergeordnete Beziehung (Tabelle) an.  
  
 **untergeordneten Schlüssel**  
 Gibt den untergeordneten Schlüssel im untergeordneten Element an, das im übergeordnetem Element auf den übergeordneten Schlüssel verweist. Wenn der untergeordnete Schlüssel aus mehreren Attributen (Spalten) besteht, werden Werte des untergeordneten Schlüssels mit einer Leerstelle angegeben. Es besteht eine positionelle Zuordnung zwischen den Werten, die für den mehrspaltigen Schlüssel und für den entsprechenden übergeordneten Schlüssel festgelegt wurden.  
  
 **Inverse**  
 Dieses in angegebene Attribut  **\<SQL: Relationship >** wird von Updategrams verwendet. Weitere Informationen finden Sie unter [angeben des SQL: Inverse-Attribut für SQL: Relationship](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md).  
  
 Die **SQL: Key-Felder** -Anmerkung muss in einem Element, das ein untergeordnetes Element verfügt über eine  **\<SQL: Relationship >** zwischen dem Element und dem untergeordneten Element definiert und ausführt nicht den Primärschlüssel der im übergeordneten Element angegebenen Tabelle bereitstellt. Selbst wenn das Schema keine-Beziehung angibt  **\<SQL: Relationship >**, müssen Sie angeben, **SQL: Key-Felder** um die richtige Hierarchie zu erzeugen. Weitere Informationen finden Sie unter [Identifizieren von Schlüsselspalten mit SQL: Key-Felder](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md).  
  
 Um die richtige Schachtelung im Ergebnis zu erzeugen, es wird empfohlen, **SQL: Key-Felder** in allen Schemas angegeben werden.  
  
## <a name="examples"></a>Beispiele  
 Es müssen bestimmte Anforderungen erfüllt sein, damit aus den folgenden Beispielen funktionierende Beispiele erstellt werden können. Weitere Informationen finden Sie unter [Anforderungen für die Ausführung von SQLXML-Beispielen](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlrelationship-annotation-on-an-element"></a>A. Angeben der sql:relationship-Anmerkung für ein Element  
 Das folgende mit Anmerkungen versehene XSD-Schema enthält  **\<Kunden >** und  **\<Reihenfolge >** Elemente. Die  **\<Reihenfolge >** Element ist ein untergeordnetes Element von der  **\<Kunden >** Element.  
  
 Im Schema der **SQL: Relationship** -Anmerkung für das  **\<Reihenfolge >** untergeordnetes Element. Die Beziehung selbst wird definiert, der  **\<xsd: AppInfo >** Element.  
  
 Die  **\<Beziehung >** -Element bezeichnet CustomerID in der Sales.SalesOrderHeader-Tabelle als Fremdschlüssel, der auf den Primärschlüssel CustomerID in der Sales.Customer-Tabelle verweist. Bestellungen eines Kunden als untergeordnetes Element dieses daher so scheinen  **\<Kunden >** Element.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                    sql:relationship="CustOrders" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 Das vorherige Schema verwendet eine benannte Beziehung. Sie können auch eine unbenannte Beziehung angeben. Das Ergebnis ist dasselbe.  
  
 Dies ist das überarbeitete Schema, in dem eine unbenannte Beziehung angegeben wird:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer"  type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader">  
           <xsd:annotation>  
            <xsd:appinfo>  
              <sql:relationship   
                parent="Sales.Customer"  
                parent-key="CustomerID"  
                child="Sales.SalesOrderHeader"  
                child-key="CustomerID" />  
            </xsd:appinfo>  
           </xsd:annotation>  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>So testen Sie eine Beispiel-XPath-Abfrage anhand des Schemas  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen sql-relationship.xml.  
  
2.  Kopieren Sie die unten stehende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen sql-relationshipT.xml im gleichen Verzeichnis, in dem Sie sql-relationship.xml gespeichert haben.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-relationship.xml">  
            /Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungschema (sql-relationship.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\sql-relationship.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer CustomerID="1">   
    <Order OrderID="43860" CustomerID="1" />   
    <Order OrderID="44501" CustomerID="1" />   
    <Order OrderID="45283" CustomerID="1" />   
    <Order OrderID="46042" CustomerID="1" />   
  </Customer>   
</ROOT>  
```  
  
### <a name="b-specifying-a-relationship-chain"></a>B. Angeben einer Beziehungskette  
 Angenommen, Sie verwenden das folgende XML-Dokument zur Abfrage von Daten aus der AdventureWorks-Datenbank:  
  
```  
<Order SalesOrderID="43659">  
  <Product Name="Mountain Bike Socks, M"/>   
  <Product Name="Sport-100 Helmet, Blue"/>  
  ...  
</Order>  
...  
```  
  
 Für jede Bestellung in der Sales.SalesOrderHeader-Tabelle, die XML-Dokument verfügt über einen  **\<Reihenfolge >** Element. Und jede  **\<Reihenfolge >** Element enthält eine Liste der  **\<Product >** untergeordnete Elemente, jeweils eines für jedes in der Bestellung aufgeführte Produkt.  
  
 Zur Angabe eines XSD-Schemas, das diese Hierarchie erzeugt, müssen Sie zwei Beziehungen angeben: OrderOD und ODProduct. Die OrderOD-Beziehung gibt die Über-/Unterordnungsbeziehung zwischen den Tabellen Sales.SalesOrderHeader und Sales.SalesOrderDetail an. Die ODProduct-Beziehung gibt die Beziehung zwischen den Tabellen Sales.SalesOrderDetail und Production.Product an.  
  
 Im folgenden Schema die **msdata: Relationship** Anmerkung für die  **\<Product >** Element gibt zwei Werte an: OrderOD und ODProduct. Die Reihenfolge, in der diese Werte angegeben werden, spielt eine wichtige Rolle.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <msdata:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  
    <msdata:relationship name="ODProduct"  
          parent="Sales.SalesOrderDetail"  
          parent-key="ProductID"  
          child="Production.Product"  
          child-key="ProductID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID"  
                     msdata:relationship="OrderOD ODProduct">  
          <xsd:complexType>  
             <xsd:attribute name="Name" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
    </xsd:complexType>  
</xsd:schema>  
```  
  
 Statt eine benannte Beziehung anzugeben, können Sie eine anonyme Beziehung angeben. In diesem Fall wird der gesamte Inhalt des  **\<Annotation >**...  **\</annotation >**, der die beiden Beziehungen beschreibt, werden als ein untergeordnetes Element des  **\<Product >**.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID" >  
         <xsd:annotation>  
          <xsd:appinfo>  
           <msdata:relationship   
               parent="Sales.SalesOrderHeader"  
               parent-key="SalesOrderID"  
               child="Sales.SalesOrderDetail"  
               child-key="SalesOrderID" />  
  
           <msdata:relationship   
               parent="Sales.SalesOrderDetail"  
               parent-key="ProductID"  
               child="Production.Product"  
               child-key="ProductID" />  
         </xsd:appinfo>  
       </xsd:annotation>  
       <xsd:complexType>  
          <xsd:attribute name="Name" type="xsd:string" />  
       </xsd:complexType>  
     </xsd:element>  
   </xsd:sequence>  
   <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
  </xsd:complexType>  
 </xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>So testen Sie eine Beispiel-XPath-Abfrage anhand des Schemas  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen relationshipChain.xml.  
  
2.  Kopieren Sie die unten stehende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen relationshipChainT.xml im gleichen Verzeichnis, in dem Sie relationshipChain.xml gespeichert haben.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationshipChain.xml">  
            /Order  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungschema (relationshipChain.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\relationshipChain.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Order SalesOrderID="43659">  
    <Product Name="Mountain Bike Socks, M" />   
    <Product Name="Sport-100 Helmet, Blue" />   
    <Product Name="AWC Logo Cap" />   
    <Product Name="Long-Sleeve Logo Jersey, M" />   
    <Product Name="Long-Sleeve Logo Jersey, XL" />   
    ...  
  </Order>  
  ...  
</ROOT>  
```  
  
### <a name="c-specifying-the-relationship-annotation-on-an-attribute"></a>C. Angeben der "relationship"-Anmerkung für ein Attribut  
 Das Schema in diesem Beispiel enthält eine \<Customer > Element mit einer \<CustomerID > untergeordnetes Element und einem OrderIDList-Attribut des IDREFS-Typ. Die \<Customer >-Element der Sales.Customer-Tabelle in der AdventureWorks-Datenbank zugeordnet. Standardmäßig der Bereich dieser Zuordnung gilt für alle untergeordneten Elemente oder Attribute, es sei denn, **SQL: Relation** für angegeben wird das untergeordnete Element oder Attribut in diesem Fall muss die entsprechende primäre-Schlüssel/Fremdschlüssel-Beziehung definiert die \<Beziehung > Element. Und das untergeordnete Element oder ein Attribut, der angibt, die andere Tabelle mit den **Beziehung** Anmerkung, müssen auch angeben, die **Beziehung** Anmerkung.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="CustomerID"   type="xsd:string" />   
     </xsd:sequence>  
     <xsd:attribute name="OrderIDList"   
                     type="xsd:IDREFS"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:field="SalesOrderID"  
                     sql:relationship="CustOrders" >  
        </xsd:attribute>  
    </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>So testen Sie eine Beispiel-XPath-Abfrage anhand des Schemas  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen relationship-on-attribute.xml.  
  
2.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Datei ein. Speichern Sie die Datei unter dem Namen relationship-on-attributeT.xml im gleichen Verzeichnis, in dem Sie relationship-on-attribute.xml gespeichert haben. Die Abfrage in der Vorlage wählt einen Kunden mit der CustomerID des Werts 1 aus.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-on-attribute.xml">  
        /Customer[CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungschema (relationship-on-attribute.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\relationship-on-attribute.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer OrderIDList="43860 44501 45283 46042">  
    <CustomerID>1</CustomerID>   
  </Customer>  
</ROOT>  
```  
  
### <a name="d-specifying-sqlrelationship-on-multiple-elements"></a>D. Angeben von "sql:relationship" für mehrere Elemente  
 In diesem Beispiel, das mit Anmerkungen versehene XSD-Schema enthält die  **\<Kunden >**,  **\<Reihenfolge >**, und  **\<OrderDetail >** Elemente.  
  
 Die  **\<Reihenfolge >** Element ist ein untergeordnetes Element von der  **\<Kunden >** Element. **\<SQL: Relationship >** angegeben ist, auf die  **\<Reihenfolge >** untergeordnetes Element; daher werden Bestellungen eines Kunden als untergeordnete Elemente des angezeigt  **\<Kunden >** .  
  
 Die  **\<Reihenfolge >** Element enthält die  **\<OrderDetail >** untergeordnetes Element. **\<SQL: Relationship >** angegeben  **\<OrderDetail >** untergeordnetes Element, sodass die Details einer Bestellung als untergeordnete Elemente dieses angezeigt  **\<Reihenfolge >** Element.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
        parent="Sales.Customer"  
        parent-key="CustomerID"  
        child="Sales.SalesOrderHeader"  
        child-key="CustomerID" />  
  
    <sql:relationship name="OrderOrderDetail"  
        parent="Sales.SalesOrderHeader"  
        parent-key="SalesOrderID"  
        child="Sales.SalesOrderDetail"  
        child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
              sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                             sql:relationship="OrderOrderDetail"   
                             maxOccurs="unbounded" >  
                  <xsd:complexType>  
                    <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                    <xsd:attribute name="ProductID" type="xsd:string" />  
                    <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>So testen Sie eine Beispiel-XPath-Abfrage anhand des Schemas  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen relationship-multiple-elements.xml.  
  
2.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen relationship-multiple-elementsT.xml im gleichen Verzeichnis, in dem Sie relationship-multiple-elements gespeichert haben. Die Abfrage in der Vorlage gibt die Bestellinformationen für einen Kunden mit der CustomerID des Werts 1 und der SalesOrderID des Werts 43860 zurück.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-multiple-elements.xml">  
        /Customer[@CustomerID=1]/Order[@SalesOrderID=43860]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungschema (relationship-multiple-elements.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\relationship-multiple-elements.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1">  
     <OrderDetail SalesOrderID="43860" ProductID="761" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="770" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="758" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="765" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="762" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="768" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="763" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="756" OrderQty="1" />   
  </Order>  
</ROOT>  
```  
  
### <a name="e-specifying-the-sqlrelationship-without-the-parent-attribute"></a>E. Angeben der \<SQL: Relationship > ohne das übergeordnete Attribut  
 Dieses Beispiel veranschaulicht das Angeben der  **\<SQL: Relationship >** ohne die **übergeordneten** Attribut. Angenommen, es sind die folgenden Mitarbeitertabellen vorhanden:  
  
```  
Emp1(SalesPersonID, FirstName, LastName, ReportsTo)  
Emp2(SalesPersonID, FirstName, LastName, ReportsTo)  
```  
  
 Die folgenden XML-Sicht sind die  **\<Emp1 >** und  **\<Emp2 >** Elemente, die Zuordnung von Tabellen Sales. emp1 und Sales. emp2 zugeordnet:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="EmpOrders"  
          parent-key="SalesPersonID"  
          child="Sales.SalesOrderHeader"  
          child-key="SalesPersonID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Emp1" sql:relation="Sales.Emp1" type="EmpType" />  
  <xsd:element name="Emp2" sql:relation="Sales.Emp2" type="EmpType" />  
   <xsd:complexType name="EmpType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:relationship="EmpOrders" >  
          <xsd:complexType>  
             <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesPersonID"   type="xsd:integer" />   
        <xsd:attribute name="LastName"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 Im Schema sind sowohl der  **\<Emp1 >** Element und  **\<Emp2 >** Element sind vom Typ **EmpType**. Der Typ **EmpType** beschreibt ein  **\<Reihenfolge >** untergeordnetes Element und dem entsprechenden  **\<SQL: Relationship >**. In diesem Fall gibt es kein einzelnes übergeordnetes Element, das in identifiziert werden kann, ist  **\<SQL: Relationship >** mithilfe der **übergeordneten** Attribut. In diesem Fall geben Sie die **übergeordneten** Attribut in  **\<SQL: Relationship >**; das **übergeordneten** Attributinformationen abgerufenes der Hierarchie im Schema.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>So testen Sie eine Beispiel-XPath-Abfrage anhand des Schemas  
  
1.  Erstellen Sie diese Tabellen in der AdventureWorks-Datenbank:  
  
    ```  
    USE AdventureWorks  
    CREATE TABLE Sales.Emp1 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    CREATE TABLE Sales.Emp2 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    ```  
  
2.  Fügen Sie den Tabellen diese Beispieldaten hinzu:  
  
    ```  
    INSERT INTO Sales.Emp1 values (279, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Sales.Emp1 values (282, 'Andrew', 'Fuller',1)  
    INSERT INTO Sales.Emp1 values (276, 'Janet', 'Leverling',1)  
    INSERT INTO Sales.Emp2 values (277, 'Margaret', 'Peacock',3)  
    INSERT INTO Sales.Emp2 values (283, 'Steven', 'Devolio',4)  
    INSERT INTO Sales.Emp2 values (275, 'Nancy', 'Buchanan',5)  
    INSERT INTO Sales.Emp2 values (281, 'Michael', 'Suyama',6)  
    ```  
  
3.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen relationship-noparent.xml.  
  
4.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen relationship-noparentT im gleichen Verzeichnis, in dem Sie relationship-noparent.xml gespeichert haben. Die Abfrage in der Vorlage wählt alle dem \<Emp1 > Elemente (daher, die das übergeordnete Element Emp1 ist).  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationship-noparent.xml">  
            /Emp1  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungschema (relationship-noparent.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\relationship-noparent.xml"  
    ```  
  
5.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Hier ist ein Teilergebnis-Satz:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<Emp1 SalesPersonID="276" LastName="Leverling">  
  <Order SalesOrderID="43663" CustomerID="510" />   
  <Order SalesOrderID="43666" CustomerID="511" />   
  <Order SalesOrderID="43859" CustomerID="259" />  
  ...  
</Emp1>  
```  
  
  
