---
title: Angeben von XPath-Variablen in XPath-Abfragen (SQLXML 4.0) | Microsoft Docs
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
- XPath queries [SQLXML], XPath variables
- XPath variables [SQLXML]
ms.assetid: c11ab816-11b8-4131-8b77-c03fe500fa10
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ebc047be45eb51208c7140e9d042278b9f96e6a6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="specifying-xpath-variables-in-xpath-queries-sqlxml-40"></a>Angeben von XPath-Variablen in XPath-Abfragen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Die folgenden Beispiele zeigen, wie XPath-Variablen in XPath-Abfragen übergeben werden. Die XPath-Abfragen in diesen Beispielen werden für das in SampleSchema1.xml enthaltene Zuordnungsschema angegeben. Informationen zu diesem Beispielschema finden Sie unter [Beispiel Annotated XSD-Schema für XPath-Beispiele &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-use-the-xpath-variables"></a>A. Verwenden der XPath-Variablen  
 Eine Beispielvorlage besteht aus zwei XPath-Abfragen. Jede der XPath-Abfragen verwendet einen Parameter. Die Vorlage gibt außerdem Standardwerte für diese Parameter an. Die Standardwerte werden verwendet, wenn keine Parameterwerte angegeben werden. Zwei Parameter mit Standardwerten werden in angegebenen  **\<SQL: Header >**.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:header>  
     <sql:param name='CustomerID'>1</sql:param>  
     <sql:param name='ContactID'>1</sql:param>   
  </sql:header>  
  <sql:xpath-query mapping-schema="SampleSchema1.xml">  
    Customer[@CustomerID=$CustomerID]   
  </sql:xpath-query >  
  <sql:xpath-query mapping-schema="SampleSchema1.xml">  
   Contact[@ContactID=$ContactID]   
  </sql:xpath-query>  
</ROOT>  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>So testen Sie die XPath-Abfrage mit dem Zuordnungsschema  
  
1.  Kopieren der [Schema Beispielcode](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) und fügen Sie ihn in eine Textdatei. Speichern Sie die Datei unter dem Dateinamen SampleSchema1.xml.  
  
2.  Erstellen Sie die folgende Vorlage (XPathVariables.xml), und speichern Sie sie im folgenden Verzeichnis:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:header>  
         <sql:param name='CustomerID'>1</sql:param>  
         <sql:param name='ContactID'>1</sql:param>   
      </sql:header>  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Customer[@CustomerID=$CustomerID]   
      </sql:xpath-query >  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
       Contact[@ContactID=$ContactID]   
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (SampleSchema1.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen. Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
> [!NOTE]  
>  In diesem Beispiel werden keine Parameter übergeben. Stattdessen werden die Standardparameterwerte verwendet.  
  
  
