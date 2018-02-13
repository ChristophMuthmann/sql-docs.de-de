---
title: Angeben von expliziten Konvertierungsfunktionen in XPath-Abfragen (SQLXML 4.0) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- explicit conversion functions [SQLXML]
- string function
- number function
- XPath queries [SQLXML], explicit conversion functions
ms.assetid: 1111cb5d-2bd9-4bdb-8de2-dc0e47452dd6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bd554000ca2982ad265cdd0e45856baa592d2be0
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-40"></a>Angeben von expliziten Konvertierungsfunktionen in XPath-Abfragen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
In den folgenden Beispielen wird gezeigt, wie explizite Konvertierungsfunktionen in XPath-Abfragen angegeben werden. Die XPath-Abfragen in diesen Beispielen werden für das in SampleSchema1.xml enthaltene Zuordnungsschema angegeben. Informationen zu diesem Beispielschema finden Sie unter [Beispiel Annotated XSD-Schema für XPath-Beispiele &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-use-the-number-explicit-conversion-function"></a>A. Verwenden der expliziten Konvertierungsfunktion number()  
 Die **number()** -Funktion konvertiert ein Argument in eine Zahl.  
  
 Wenn den Wert der **ContactID** ist nicht numerisch, die folgende Abfrage konvertiert **ContactID** in eine Zahl und vergleicht ihn mit dem Wert 4. Die Abfrage gibt dann alle  **\<Mitarbeiter >** untergeordneten-Elemente des Kontextknotens mit der **ContactID** -Attribut den numerischen Wert 4 aufweist:  
  
```  
/child::Contact[number(attribute::ContactID)= 4]  
```  
  
 Eine Verknüpfung zu den **Attribut** Achse (@) angegeben werden können, und da die **untergeordneten** -Achse die Standardachse ist, können Sie in der Abfrage ausgelassen werden:  
  
```  
/Contact[number(@ContactID) = 4]  
```  
  
 Anders ausgedrückt, gibt die Abfrage einen Mitarbeiter mit einem **ContactID** 4.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>So testen Sie die XPath-Abfrage mit dem Zuordnungsschema  
  
1.  Kopieren der [Schema Beispielcode](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) und fügen Sie ihn in eine Textdatei. Speichern Sie die Datei unter dem Dateinamen SampleSchema1.xml.  
  
2.  Erstellen Sie die folgende Vorlage (ExplicitConversionA.xml), und speichern Sie sie in dem Verzeichnis, in dem SampleSchema1.xml gespeichert wurde.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Contact[number(@ContactID)=4]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (SampleSchema1.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Das Resultset für diese Vorlagenausführung sieht so aus:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
### <a name="b-use-the-string-explicit-conversion-function"></a>B. Verwenden der expliziten Konvertierungsfunktion string()  
 Die **string()** -Funktion konvertiert ein Argument in eine Zeichenfolge.  
  
 Die folgende Abfrage konvertiert **ContactID** zu einer Zeichenfolge und vergleicht Wert mit dem Zeichenfolgenwert "4". Die Abfrage gibt alle  **\<Mitarbeiter >** untergeordneten-Elemente des Kontextknotens mit einem **ContactID** mit einem Zeichenfolgenwert "4":  
  
```  
/child::Contact[string(attribute::ContactID)="4"]  
```  
  
 Eine Verknüpfung zu den **Attribut** Achse (@) angegeben werden können, und da die **untergeordneten** -Achse die Standardachse ist, können Sie in der Abfrage ausgelassen werden:  
  
```  
/Contact[string(@ContactID)="4"]  
```  
  
 Diese Abfrage gibt praktisch die gleichen Ergebnisse wie das vorherige Abfragebeispiel zurück, obwohl hier der Zeichenfolgenwert und nicht der numerische Wert (d. h. die Zahl 4) ausgewertet wird.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>So testen Sie die XPath-Abfrage mit dem Zuordnungsschema  
  
1.  Kopieren der [Schema Beispielcode](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) und fügen Sie ihn in eine Textdatei. Speichern Sie die Datei unter dem Dateinamen SampleSchema1.xml.  
  
2.  Erstellen Sie die folgende Vorlage (ExplicitConversionB.xml), und speichern Sie sie in dem Verzeichnis, in dem SampleSchema1.xml gespeichert wurde.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Contact[string(@ContactID)="4"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (SampleSchema1.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden finden Sie das Resultset der Vorlagenausführung:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
  
