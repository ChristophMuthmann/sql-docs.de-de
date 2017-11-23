---
title: Rowset-Datentyp (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Rowset Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Rowset
- http://schemas.microsoft.com/analysisservices/2003/engine#Rowset
- Rowset
helpviewer_keywords: Rowset data type
ms.assetid: a3e6e227-2d53-4530-b369-afa8b4df0a40
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf941f9e6231174bd0288bf71aa3055570d1c74a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="rowset-data-type-xmla"></a>Rowset-Datentyp (XMLA)
  Definiert einen abgeleiteten Datentyp, der darstellt eine [Root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) Element, das tabellarische Daten durch gibt eine [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) oder [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) -Methodenaufruf.  
  
 **Namespace** Urn: Schemas-Microsoft-com: XML-Analyse: Rowset  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <!-- The following elements extend Resultset -->  
   <!-- Optional schema elements -->  
   <row>...</row>  
</root>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|[Resultset](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Zeile](../../../analysis-services/xmla/xml-elements-properties/row-element-xmla.md)|  
|Abgeleitete Elemente|[Stamm](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 XML lässt bestimmte Zeichen nicht als Element- und Attributnamen zu. Um diese benennungseinschränkung zu adressieren, XML for Analysis (XMLA) unterstützt die Codierung gemäß der Definition von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Für Spaltennamen, die XML-Namenszeichen enthalten, die nicht entsprechend der XML 1.0-Spezifikation gültig sind, verwendet XMLA die entsprechenden Hexadezimalwerte, um Unicode-Zeichen zu codieren, die nicht gültig sind. Die Hexadezimalwerte erhalten _x*HHHH*\_, wobei *HHHH* steht für den vierstelligen hexadezimalen UCS-2-Code für das Zeichen in die erste höchstwertigen Bit-Bestellung. XMLA codiert beispielsweise den Namen "Order Details" als Order_x0020_Details, wobei das Leerzeichen durch den entsprechenden Hexadezimalcode ersetzt wird.  
  
 Die Codierung kann XSL-Transformationen (Extensible Style Language) erschweren. Zur Unterstützung von eines schnellen Lookup der echten, nicht codierten Spaltennamen, fügen Sie der **SQL: field**-Attribut auf die XML-Rowsetschema für jede Spalte, wie im folgenden Beispiel gezeigt:  
  
```  
<xsd:element name="Order_x0020_Details" type="string" sql:field="Order Details" />  
```  
  
> [!NOTE]  
>  Die **SQL: field** -Attribut ist der `"urn:schemas-microsoft-com:xml-sql"` Namespace.  
  
## <a name="expressing-a-null-value"></a>Drückt einen Null-Wert aus.  
 Der NULL-Wert für eine Spalte innerhalb einer Zeile kann auf zwei Arten ausgedrückt werden:  
  
-   Ein fehlendes Column-Element deutet darauf hin, dass die Spalte NULL ist.  
  
-   Das Column-Element kann das `xsi:nil='true'` -Attribut nutzen, um auf den NULL-Wert hinzuweisen.  
  
 Beispiel: Eine Zeile enthält eine einzelne Spalte mit Namen Store_Name und der Wert der Spalte ist NULL. Der Wert der Spalte Store_Name kann als Fehlendes Spaltenelement dargestellt werden: oder der Wert der Spalte Store_Name kann dargestellt werden, mithilfe der `xsi:nil='true'` Attribut:  
  
```  
<row>  
   <Store_name xsi:nil='true'/>  
</row>  
```  
  
## <a name="example"></a>Beispiel  
  
## <a name="xmla-rowset-for-flat-data"></a>XMLA-Rowset für flache Daten  
 Bei flachen Daten werden Spaltennamen, die speziell für die Abfrage gelten, im Schema als die Elementnamen definiert. Des Weiteren umschließt ein Paar `<row>`-Tags jede Zeile.  
  
 Das folgende Beispiel zeigt das XMLA-Rowset-Format für flache Daten.  
  
```  
<return>  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   </xsd:element>  
      <xsd:complexType name="row">  
         <xsd:choice maxOccurs="unbounded" minOccurs="0">  
            <xsd:element name="CATALOG_NAME" type="xsd:string" sql:field="CATALOG_NAME"></xsd:element>  
            <xsd:element name="DESCRIPTION" type="xsd:string" sql:field="DESCRIPTION"></xsd:element>  
            <xsd:element name="ROLES" type="xsd:string" sql:field="ROLES"></xsd:element>  
            <xsd:element name="DATE_MODIFIED" type="xsd:time" sql:field="DATE_MODIFIED"></xsd:element>  
         </xsd:choice>  
      </xsd:complexType>  
   </xsd:schema>  
   <row>  
      <CATALOG_NAME>FoodMart 2000</CATALOG_NAME>  
      <DESCRIPTION></DESCRIPTION>  
      <ROLES>All Users</ROLES>  
      <DATE_MODIFIED>3/11/2001 6:49:36 PM</DATE_MODIFIED>  
   </row>  
   ...  
</root>  
```  
  
## <a name="xmla-rowset-for-hierarchical-data"></a>XMLA-Rowset für hierarchische Daten  
 Einige Rowsets enthalten hierarchische Daten (oder haben geschachtelte Rowsets). Von Data Mining-Abfragen zurückgegebene Rowsets sind hierarchisch. Bei hierarchischen Daten wird die Struktur der Zeilen nicht geändert; stattdessen definiert das datenspezifische Schema einen Elementuntertyp, der die geschachtelten Daten enthält.  
  
 Das folgende Beispiel zeigt das XMLA-Rowset-Format für hierarchische Daten. In diesem Beispiel ist der Elementuntertyp, der die geschachtelten Daten enthält, `<NODE_DISTRIBUTION>`.  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
   xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <xsd:complexType name="row">  
         <xsd:choice maxOccurs="unbounded" minOccurs="0">  
            <xsd:sequence maxOccurs="unbounded" minOccurs="0">  
               <xsd:element name="NODE_DISTRIBUTION" sql:field="NODE_DISTRIBUTION">  
                  <xsd:complexType>  
                     <xsd:choice maxOccurs="unbounded" minOccurs="0">  
                        <xsd:element name="ATTRIBUTE_NAME" type="xsd:string" sql:field="ATTRIBUTE_NAME"></xsd:element>  
                        <xsd:element name="ATTRIBUTE_VALUE" type="xsd:string" sql:field="ATTRIBUTE_VALUE"></xsd:element>  
                        <xsd:element name="SUPPORT" type="xsd:double" sql:field="SUPPORT"></xsd:element>  
                        <xsd:element name="PROBABILITY" type="xsd:double" sql:field="PROBABILITY"></xsd:element>  
                        <xsd:element name="VARIANCE" type="xsd:double" sql:field="VARIANCE"></xsd:element>  
                        <xsd:element name="VALUETYPE" type="xsd:int" sql:field="VALUETYPE"></xsd:element>  
                     </xsd:choice>  
                  </xsd:complexType>  
               </xsd:element>  
            </xsd:sequence>  
            <xsd:element name="MODEL_CATALOG" type="xsd:string" sql:field="MODEL_CATALOG"></xsd:element>  
            <xsd:element name="MODEL_SCHEMA" type="xsd:string" sql:field="MODEL_SCHEMA"></xsd:element>  
            <xsd:element name="MODEL_NAME" type="xsd:string" sql:field="MODEL_NAME"></xsd:element>  
            <xsd:element name="ATTRIBUTE_NAME" type="xsd:string" sql:field="ATTRIBUTE_NAME"></xsd:element>  
            <xsd:element name="NODE_NAME" type="xsd:string" sql:field="NODE_NAME"></xsd:element>  
            <xsd:element name="NODE_UNIQUE_NAME" type="xsd:string" sql:field="NODE_UNIQUE_NAME"></xsd:element>  
            <xsd:element name="NODE_TYPE" type="xsd:unsignedInt" sql:field="NODE_TYPE"></xsd:element>  
            <xsd:element name="NODE_GUID" type="xsd:string" sql:field="NODE_GUID"></xsd:element>  
            <xsd:element name="NODE_CAPTION" type="xsd:string" sql:field="NODE_CAPTION"></xsd:element>  
            <xsd:element name="CHILDREN_CARDINALITY" type="xsd:unsignedInt" sql:field="CHILDREN_CARDINALITY"></xsd:element>  
            <xsd:element name="PARENT_UNIQUE_NAME" type="xsd:string" sql:field="PARENT_UNIQUE_NAME"></xsd:element>  
            <xsd:element name="NODE_DESCRIPTION" type="xsd:string" sql:field="NODE_DESCRIPTION"></xsd:element>  
            <xsd:element name="NODE_RULE" type="xsd:string" sql:field="NODE_RULE"></xsd:element>  
            <xsd:element name="MARGINAL_RULE" type="xsd:string" sql:field="MARGINAL_RULE"></xsd:element>  
            <xsd:element name="NODE_PROBABILITY" type="xsd:double" sql:field="NODE_PROBABILITY"></xsd:element>  
            <xsd:element name="MARGINAL_PROBABILITY" type="xsd:double" sql:field="MARGINAL_PROBABILITY"></xsd:element>  
            <xsd:element name="NODE_SUPPORT" sql:type="xsd:double" sql:field="NODE_SUPPORT"></xsd:element>  
            <xsd:element name="MSOLAP_MODEL_COLUMN" sql:type="xsd:string" sql:field="MSOLAP_MODEL_COLUMN"></xsd:element>  
            <xsd:element name="MSOLAP_NODE_SCORE" sql:type="xsd:double" sql:field="MSOLAP_NODE_SCORE"></xsd:element>  
            <xsd:element name="MSOLAP_NODE_SHORT_CAPTION" sql:type="xsd:string" sql:field="MSOLAP_NODE_SHORT_CAPTION"></xsd:element>  
         </xsd:choice>  
      </xsd:complexType>  
   </xsd:schema>  
   <row>  
      <MODEL_CATALOG>FoodMart 2000</MODEL_CATALOG>  
      <MODEL_NAME>customer pattern discovery</MODEL_NAME>  
      <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
      <NODE_NAME>2147483652</NODE_NAME>  
      <NODE_UNIQUE_NAME>2147483652</NODE_UNIQUE_NAME>  
      <NODE_TYPE>2</NODE_TYPE>  
      <NODE_CAPTION>All</NODE_CAPTION>  
      <CHILDREN_CARDINALITY>8</CHILDREN_CARDINALITY>  
      <PARENT_UNIQUE_NAME>0</PARENT_UNIQUE_NAME>  
      <NODE_DESCRIPTION>All</NODE_DESCRIPTION>  
      <NODE_RULE></NODE_RULE>  
      <MARGINAL_RULE></MARGINAL_RULE>  
      <NODE_PROBABILITY>1</NODE_PROBABILITY>  
      <MARGINAL_PROBABILITY>1</MARGINAL_PROBABILITY>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>missing</ATTRIBUTE_VALUE>  
         <SUPPORT>0</SUPPORT>  
         <PROBABILITY>0</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>1</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>Bronze</ATTRIBUTE_VALUE>  
         <SUPPORT>3077</SUPPORT>  
         <PROBABILITY>0.551334886221107</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>4</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>Golden</ATTRIBUTE_VALUE>  
         <SUPPORT>659</SUPPORT>  
         <PROBABILITY>0.118079197276474</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>4</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>Normal</ATTRIBUTE_VALUE>  
         <SUPPORT>1332</SUPPORT>  
         <PROBABILITY>0.238666905572478</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>4</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>Silver</ATTRIBUTE_VALUE>  
         <SUPPORT>513</SUPPORT>  
         <PROBABILITY>9.19190109299409E-02</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>4</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_SUPPORT>5581</NODE_SUPPORT>  
      <MSOLAP_MODEL_COLUMN>Customers.Name.Member Card</MSOLAP_MODEL_COLUMN>  
      <MSOLAP_NODE_SCORE>1948.401692055</MSOLAP_NODE_SCORE>  
      <MSOLAP_NODE_SHORT_CAPTION>All</MSOLAP_NODE_SHORT_CAPTION>  
</row>  
</root>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Datentypen &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
