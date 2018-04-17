---
title: 'Erstellen von CDATA-Abschnitten mithilfe von SQL: use-Cdata (SQLXML 4.0) | Microsoft Docs'
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
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 614f9f5c014b8f762992110108c6eccd2ac1f4e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Erstellen von CDATA-Abschnitten mit sql:use-cdata (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In XML werden Textblöcke, die Zeichen enthalten, die andernfalls als Markup erkannt würden, mit CDATA-Abschnitten in Escapezeichen umgewandelt.  
  
 Eine Datenbank in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann manchmal Zeichen enthalten, die vom XML-Parser als Markupzeichen behandelt werden. Zum Beispiel werden spitze Klammern (< und >), das Symbol "kleiner als oder gleich" (<=) und das kaufmännische Und-Zeichen (&) als Markupzeichen behandelt. Sie können diese Sonderzeichen in einem CDATA-Abschnitt jedoch umschließen, um zu verhindern, dass sie als Markupzeichen behandelt werden. Der Text innerhalb des CDATA-Abschnitts wird vom XML-Parser als Nur-Text behandelt.  
  
 Die **SQL: use-Cdata** -Anmerkung verwendet, um anzugeben, dass die Daten durch zurückgegeben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollte in einem CDATA-Abschnitt eingeschlossen werden (d. h. er gibt an, ob der Wert aus einer Spalte, die vom angegebenen **SQL: field** in einem CDATA-Abschnitt eingeschlossen werden soll). Die **SQL: use-Cdata** -Anmerkung kann nur für Elemente, die einer Datenbankspalte zugeordnet.  
  
 Die **SQL: use-Cdata** -Anmerkung akzeptiert einen booleschen Wert (0 = False, 1 = "true"). Zulässig sind die Werte 0, 1, true und false.  
  
 Diese Anmerkung kann nicht verwendet werden, mit **SQL: URL-codieren** oder für die ID, IDREF, IDREFS, NMTOKEN und NMTOKENS Attributtypen.  
  
## <a name="examples"></a>Beispiele  
 Es müssen bestimmte Anforderungen erfüllt sein, damit aus den folgenden Beispielen funktionierende Beispiele erstellt werden können. Weitere Informationen finden Sie unter [Anforderungen für die Ausführung von SQLXML-Beispielen](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. Angeben von sql:use-cdata für ein Element  
 Im folgenden Schema **SQL: use-Cdata** auf 1 (True) festgelegt ist, für die  **\<AddressLine1 >** innerhalb der  **\<Adresse >** Element. Daraufhin werden die Daten in einem CDATA-Abschnitt zurückgegeben.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>So testen Sie eine Beispiel-XPath-Abfrage anhand des Schemas  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen UseCData.xml.  
  
2.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen UseCDataT.xml im gleichen Verzeichnis, in dem Sie UseCData.xml gespeichert haben.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungschema (UseCData.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird ein Teil des Resultsets aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
