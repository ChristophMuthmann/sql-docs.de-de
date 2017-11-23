---
title: Explizite Zuordnung XSD-Elementen und-Attributen zu Tabellen und Spalten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- explicit schema mapping [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- sql:field
- row mapping [SQLXML]
- attribute mapping [SQLXML], explicit mapping
- field annotation
- XSD schemas [SQLXML], mapping attributes and elements
- names [SQLXML]
- relation annotation
- table/view mapping [SQLXML], explicit mapping
- sql:relation
- mapping schema [SQLXML], explicit mapping
- annotated XSD schemas, mapping attributes and elements
- column mapping [SQLXML]
- element mapping [SQLXML], explicit mapping
- table mapping [SQLXML], explicit mapping
- element/attribute mapping [SQLXML]
ms.assetid: 7a5ebeb6-7322-4141-a307-ebcf95976146
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a83de0653a25fa2bf055c003a13600a67e37bb9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns"></a>Explizite Zuordnung XSD-Elementen und-Attributen zu Tabellen und Spalten
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Wenn ein XSD-Schema verwenden, um eine XML-Sicht der relationalen Datenbank zu ermöglichen, müssen die Elemente und Attribute des Schemas, Tabellen und Spalten der Datenbank zugeordnet werden. Die Zeilen in der Datenbanktabelle/-sicht werden den Elementen im XML-Dokument zugeordnet. Die Spaltenwerte in der Datenbank werden Attributen oder Elementen zugeordnet.  
  
 Wenn Xpath-Abfragen für das mit Anmerkungen versehene XSD-Schema angegeben werden, werden die Daten für die Elemente und Attribute im Schema aus den Tabellen und Spalten abgerufen, denen sie zugeordnet sind. Um einen einzelnen Wert aus der Datenbank abrufen zu können, muss die im XSD-Schema angegebene Zuordnung sowohl über eine Beziehungs- als auch eine Feldangabe verfügen. Ist der Name des Elements/Attributs nicht den gleichen Namen wie die Tabelle/Sicht oder Spalte, der sie zugeordnet, die **SQL: Relation** und **SQL: field** Anmerkungen werden verwendet, um die Zuordnung zwischen einem Element anzugeben oder Das Attribut in einem XML-Dokument und die Tabelle (Sicht) oder die Spalte in einer Datenbank.  
  
## <a name="sql-relation"></a>sql-Beziehung  
 Die **SQL: Relation** -Anmerkung wird hinzugefügt, um eine XML-Knoten in der XSD-Schema einer Datenbanktabelle zuzuordnen. Der Name einer Tabelle (Sicht) wird angegeben, als Wert für die **SQL: Relation** Anmerkung.  
  
 Wenn **SQL: Relation** ist für ein Element angegeben, gilt der Bereich dieser Anmerkung für alle Attribute und untergeordneten Elementen, die in der komplexen Typdefinition des jeweiligen Elements, dadurch wird eine Verknüpfung im Schreiben von beschriebenen Anmerkungen.  
  
 Die **SQL: Relation** Anmerkung ist auch nützlich, wenn Bezeichner in gültig sind [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind in XML nicht gültig. Zum Beispiel ist "Order Details" ein gültiger Tabellenname in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], jedoch nicht in XML. In solchen Fällen das **SQL: Relation** Anmerkung kann z. B. an der Zuordnung verwendet werden:  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-Feld  
 Die **Sql-Feld** -Anmerkung ordnet ein Element oder Attribut einer Datenbankspalte. Die **SQL: field** -Anmerkung wird hinzugefügt, um eine XML-Knoten im Schema einer Datenbankspalte zuzuordnen. Sie können keine angeben **SQL: field** auf ein Element ohne Inhalt.  
  
## <a name="examples"></a>Beispiele  
 Es müssen bestimmte Anforderungen erfüllt sein, damit aus den folgenden Beispielen funktionierende Beispiele erstellt werden können. Weitere Informationen finden Sie unter [Anforderungen für die Ausführung von SQLXML-Beispielen](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. Angeben der Anmerkungen sql:relation und sql:field  
 In diesem Beispiel besteht das XSD-Schema eine  **\<Kontakt >** -Element komplexen Typs mit  **\<FName >** und  **\<LName >** untergeordnete Elemente und die **ContactID** Attribut.  
  
 Die **SQL: Relation** -Anmerkung ordnet das  **\<Kontakt >** -Element der Person.Contact-Tabelle in der AdventureWorks-Datenbank. Die **SQL: field** -Anmerkung ordnet das  **\<FName >** -Element der FirstName-Spalte und die  **\<LName >** -Element der LastName die Spalte.  
  
 Wird keine Anmerkung angegeben, für die **ContactID** Attribut. Dies führt zu einer Standardzuordnung des Attributs zur Spalte mit dem gleichen Namen.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>So testen Sie eine Beispiel-XPath-Abfrage anhand des Schemas  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen MySchema-annotated.xml.  
  
2.  Kopieren Sie die unten stehende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen MySchema-annotatedT.xml im gleichen Verzeichnis, in dem Sie MySchema-annotated.xml gespeichert haben.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="MySchema-annotated.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (MySchema-annotated.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema-annotated.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [mithilfe von ADO zum Ausführen von SQLXML-Abfragen](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird ein Teil des Resultsets aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
 <Contact ContactID="1">   
    <FName>Gustavo</FName>   
    <LName>Achong</LName>   
 </Contact>   
  .....  
</ROOT>  
```  
  
  
