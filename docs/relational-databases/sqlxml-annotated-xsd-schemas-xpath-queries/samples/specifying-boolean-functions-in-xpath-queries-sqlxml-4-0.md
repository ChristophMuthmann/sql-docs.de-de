---
title: Angeben von booleschen Funktionen in XPath-Abfragen (SQLXML 4.0) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
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
- XPath queries [SQLXML], Boolean functions
- false function
- not function [SQLXML]
- true function
- Boolean functions
ms.assetid: c72cd333-9294-4d41-84f2-1748bf20e3eb
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6fa92aee30c401bc0a244a46f7e5f944c5bf8c80
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="specifying-boolean-functions-in-xpath-queries-sqlxml-40"></a>Angeben von booleschen Funktionen in XPath-Abfragen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Die folgenden Beispiele zeigen, wie boolesche Funktionen in XPath-Abfragen angegeben werden. Die XPath-Abfragen in diesen Beispielen werden für das in SampleSchema1.xml enthaltene Zuordnungsschema angegeben. Informationen zu diesem Beispielschema finden Sie unter [Beispiel Annotated XSD-Schema für XPath-Beispiele &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Beispiele  
  
## <a name="a-specify-the-not-boolean-function"></a>A. Angeben der booleschen Funktion "not()"  
 Diese Abfrage gibt alle dem  **\<Kunden >** untergeordnete Elemente des Kontextknotens, auf denen kein  **\<Reihenfolge >** Unterelemente:  
  
```  
/child::Customer[not(child::Order)]  
```  
  
 Die **untergeordneten** -Achse die Standardachse ist. Daher kann die Abfrage wie folgt angegeben werden:  
  
```  
/Customer[not(Order)]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>So testen Sie die XPath-Abfrage mit dem Zuordnungsschema  
  
1.  Kopieren der [Schema Beispielcode](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) und fügen Sie ihn in eine Textdatei. Speichern Sie die Datei unter dem Dateinamen SampleSchema1.xml.  
  
2.  Erstellen Sie die folgende Vorlage (BooleanFunctionsA.xml), und speichern Sie sie in dem Verzeichnis, in dem SampleSchema1.xml gespeichert ist.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Customer[not(Order)]  
    </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (SampleSchema1.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden finden Sie einen Auszug aus dem Resultset der Vorlagenausführung:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
## <a name="b-specify-the-true-and-false-boolean-functions"></a>B. Angeben der booleschen Funktionen "true()" und "false()"  
 Diese Abfrage gibt alle  **\<Kunden >** -Elemente des Kontextknotens, auf denen kein  **\<Reihenfolge >** untergeordnete Elemente. In relationalem Sinn gibt diese Abfrage alle Kunden zurück, die keine Bestellungen aufgegeben haben.  
  
```  
/child::Customer[child::Order=false()]  
```  
  
 Die **untergeordneten** -Achse die Standardachse ist. Daher kann die Abfrage wie folgt angegeben werden:  
  
```  
/Customer[Order=false()]  
```  
  
 Diese Abfrage ist äquivalent zu folgendem:  
  
```  
/Customer[not(Order)]  
```  
  
 Die folgende Abfrage gibt alle Kunden zurück, die mindestens eine Bestellung aufgegeben haben:  
  
```  
/Customer[Order=true()]  
```  
  
 Diese Abfrage hat die folgende Entsprechung:  
  
```  
/Customer[Order]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>So testen Sie die XPath-Abfrage mit dem Zuordnungsschema  
  
1.  Kopieren der [Schema Beispielcode](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) und fügen Sie ihn in eine Textdatei. Speichern Sie die Datei unter dem Dateinamen SampleSchema1.xml.  
  
2.  Erstellen Sie die folgende Vorlage (BooleanFunctionsB.xml), und speichern Sie sie in dem Verzeichnis, in dem SampleSchema1.xml gespeichert ist.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[Order=false()]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (SampleSchema1.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden finden Sie einen Auszug aus dem Resultset der Vorlagenausführung:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
  
