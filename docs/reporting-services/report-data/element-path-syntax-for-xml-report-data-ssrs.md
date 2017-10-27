---
title: "Syntax für Elementpfade für XML-Berichtsdaten (SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ElementPath syntax
- XML [Reporting Services], data retrieval
ms.assetid: 07bd7a4e-fd7a-4a72-9344-3258f7c286d1
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7c25d6665198e0392aa70d649ca658adec84d2de
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="element-path-syntax-for-xml-report-data-ssrs"></a>Syntax für Elementpfade für XML-Berichtsdaten (SSRS)
  Im Berichts-Designer geben Sie die Daten, die für einen Bericht aus einer XML-Datenquelle verwendet werden sollen, durch Definieren eines Elementpfades (mit Unterscheidung von Groß-/Kleinschreibung) an. Mit einem Elementpfad wird angegeben, wie die hierarchischen XML-Knoten und ihre Attribute in der XML-Datenquelle durchsucht werden können. Lassen Sie die Datasetabfrage oder den XML- **ElementPath** der XML- **Query** leer, um den Standardelementpfad zu verwenden. Wenn Daten aus der XML-Datenquelle abgerufen werden, werden Elementknoten mit Textwerten und Elementknotenattribute im Resultset zu Spalten. Die Werte der Knoten und Attribute werden beim Ausführen der Abfrage zu Zeilendaten. Die Spalten werden als Datasetfeldauflistung im Berichtsdatenbereich angezeigt. In diesem Thema wird die Syntax für Elementpfade beschrieben.  
  
> [!NOTE]  
>  Die Syntax von Elementpfaden ist nicht vom Namespace abhängig. Verwenden Sie die XML-Abfragesyntax, die ein XML-Element **ElementPath** enthält, das unter [XML-Abfragesyntax für XML-Berichtsdaten (SSRS)](../../reporting-services/report-data/xml-query-syntax-for-xml-report-data-ssrs.md) beschrieben ist, um Namespaces in einem Elementpfad zu verwenden.  
  
 In der folgenden Tabelle werden Konventionen für das Definieren eines Elementpfades beschrieben.  
  
|Konvention|Syntaxelemente|  
|----------------|--------------|  
|**Fett**|Text, der genau so geschrieben werden muss wie dargestellt.|  
|&#124; (Senkrechter Strich)|Trennt Syntaxelemente voneinander. Sie können nur eines der Elemente auswählen.|  
|`[ ]` (eckige Klammern)|Optionale Syntaxelemente. Geben Sie die eckigen Klammern nicht mit ein.|  
|**{ }** (geschweifte Klammern)|Begrenzt Parameter für Syntaxelemente.|  
|[**,**...*n*]|Gibt an, das vorherige Element kann wiederholt werden  *n*  -Mal. Die einzelnen Vorkommen werden durch Kommas voneinander getrennt.|  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Element path ::=  
    ElementNode[/Element path]  
ElementNode ::=  
    XMLName[(Encoding)][{[FieldList]}]  
XMLName ::=  
    [NamespacePrefix:]XMLLocalName  
Encoding ::=  
        HTMLEncoded | Base64Encoded  
FieldList ::=  
    Field[,FieldList]  
Field ::=  
    Attribute | Value | Element | ElementNode  
Attribute ::=  
        @XMLName[(Type)]  
Value ::=  
        @[(Type)]  
Element ::=  
    XMLName[(Type)]  
Type ::=  
        String | Integer | Boolean | Float | Decimal | Date | XML   
NamespacePrefix ::=  
    Identifier that specifies the namespace.  
XMLLocalName :: =  
    Identifier in the XML tag.   
```  
  
## <a name="remarks"></a>Hinweise  
 In der folgenden Tabelle sind Begriffe für Pfadelemente zusammengefasst. Die Beispiele in der Tabelle beziehen sich auf das XML-Beispieldokument Customers.xml, das im Abschnitt mit Beispielen in diesem Thema enthalten ist.  
  
> [!NOTE]  
>  Bei XML-Tags wird zwischen Groß- und Kleinschreibung unterschieden. Wenn Sie im Elementpfad einen Elementknoten (ElementNode) angeben, müssen die XML-Tags in der Datenquelle genau übereinstimmen.  
  
|Begriff|Definition|  
|----------|----------------|  
|Elementpfad|Definiert die zu durchsuchende Sequenz von Knoten im XML-Dokument, um Felddaten für ein Dataset mit einer XML-Datenquelle abzurufen.|  
|**ElementNode**|Der XML-Knoten im XML-Dokument. Knoten werden durch Tags gekennzeichnet und sind in einer hierarchischen Beziehung mit anderen Knoten vorhanden. Bei <Kunden\< handelt es sich beispielsweise um den Stammknoten des Elements. <Kunde\< ist ein untergeordnetes Element von <Kunden\<.|  
|**XMLName**|Der Name des Knotens. Der Name des Knotens Customers ist beispielsweise Customers. Für **XMLName** kann ein Namespacebezeichner als Präfix verwendet werden, um jeden Knoten eindeutig zu benennen.|  
|**Codierung**|Gibt an, dass der **Value** für dieses Element codiertes XML darstellt und decodiert werden sowie als untergeordnetes Element dieses Elements aufgenommen muss.|  
|**FieldList**|Definiert eine Gruppe von Elementen und Attributen, die zum Abrufen von Daten verwendet werden.<br /><br /> Wenn dieses Element nicht angegeben wird, werden alle Attribute und untergeordneten Elemente als Felder verwendet. Wenn die leere Feldliste angegeben wird (**{}**), werden keine Felder von diesem Knoten verwendet.<br /><br /> Eine **FieldList** kann nicht gleichzeitig einen **Value** und ein **Element** oder einen **ElementNode**enthalten.|  
|**Feld**|Gibt die Daten an, die als Datasetfeld abgerufen werden.|  
|**Attribut**|Ein Name/Wert-Paar innerhalb von **ElementNode**. Beispielsweise handelt es sich bei **ID** im Elementknoten \<Customer ID="1"> um ein Attribut, und **@ID(Integer)** gibt „1“ als Integer-Typ im entsprechenden Datenfeld **ID** zurück.|  
|**Wert**|Der Wert des Elements. **Value** kann nur für den letzten **ElementNode** im Elementpfad verwendet werden. Da es sich beispielsweise bei \<Return> um einen Blattknoten handelt, ist der Wert von **Return {@}** **Chair**.|  
|**Element**|Der Wert des benannten untergeordneten Elements. Beispielsweise werden mithilfe von Customers {}/Customer {}/LastName nur Werte für das LastName-Element abgerufen.|  
|**Typ**|Der optionale Datentyp, der für das aus diesem Element erstellte Feld zu verwenden ist.|  
|**NamespacePrefix**|**NamespacePrefix** wird im XML-Abfrageelement definiert. Wenn kein XML-Abfrageelement vorhanden ist, werden Namespaces im XML- **ElementPath** ignoriert. Wenn ein XML-Abfrageelement vorhanden ist, verfügt der XML- **ElementPath** über das optionale Attribut **IgnoreNamespaces**. Wenn IgnoreNamespaces **TRUE**ist, werden Namespaces in XML- **ElementPath** und im XML-Dokument ignoriert. Weitere Informationen finden Sie unter [XML-Abfragesyntax für XML-Berichtsdaten (SSRS)](../../reporting-services/report-data/xml-query-syntax-for-xml-report-data-ssrs.md).|  
  
## <a name="example---no-namespaces"></a>Beispiel – Keine Namespaces  
 In den folgenden Beispiele wird das XML-Dokument "Customers.xml" verwendet. Diese Tabelle zeigt Beispiele zur Syntax von Elementpfaden und die Ergebnisse beim Verwenden des Elementpfades in einer Abfrage an, die ein Dataset anhand eines als Datenquelle dienenden XML-Dokuments definiert.  
  
> [!NOTE]  
>  Wenn der Elementpfad leer ist, wird für die Abfrage der Standardelementpfad verwendet: der erste Pfad zur Blattknotenauflistung. Im ersten Beispiel entspricht das Leerlassen des Elementpfades dem Angeben des Elementpfades /Customers/Customer/Orders/Order. Alle Knotenwerte und -attribute entlang dieses Pfades werden im Resultset zurückgegeben, und die Knotennamen und -attribute werden als Datasetfelder angezeigt.  
  
 **Beispiel 1**: *Leer*  
  
|Order|Qty|im Elementknoten <Customer ID="1"|FirstName|LastName|Customer.ID|xmlns|  
|-----------|---------|--------|---------------|--------------|-----------------|-----------|  
|Chair|6|1|Bobby|Moore|11|http://www.adventure-works.com|  
|Tabelle|1|2|Bobby|Moore|11|http://www.adventure-works.com|  
|Sofa|2|8|Crystal|Hu|20|http://www.adventure-works.com|  
|EndTables|2|15|Wyatt|Diaz|33|http://www.adventure-works.com|  
  
 **Beispiel 2**: `Customers {}/Customer`  
  
|FirstName|LastName|im Elementknoten <Customer ID="1"|  
|---------------|--------------|--------|  
|Bobby|Moore|11|  
|Crystal|Hu|20|  
|Wyatt|Diaz|33|  
  
 **Beispiel 3**: `Customers {}/Customer {}/LastName`  
  
|LastName|  
|--------------|  
|Moore|  
|Hu|  
|Diaz|  
  
 **Beispiel 4**: `Customers {}/Customer {}/Orders/Order {@,@Qty}`  
  
|Order|Qty|  
|-----------|---------|  
|Chair|6|  
|Tabelle|1|  
|Sofa|2|  
|EndTables|2|  
  
 **Beispiel 5**: `Customers {}/Customer/Orders/Order{ @ID(Integer)}`  
  
|Order.ID|FirstName|LastName|im Elementknoten <Customer ID="1"|  
|--------------|---------------|--------------|--------|  
|1|Bobby|Moore|11|  
|2|Bobby|Moore|11|  
|8|Crystal|Hu|20|  
|15|Wyatt|Diaz|33|  
  
#### <a name="xml-document-customersxml"></a>XML-Dokument: Customers.xml  
 Um die Elementpfadbeispiele im vorherigen Abschnitt auszuprobieren, können Sie dieses XML-Dokument kopieren und unter einer URL speichern, auf die der Berichts-Designer zugreifen kann. Anschließend können Sie das XML-Dokument als XML-Datenquelle verwenden: z. B. `http://localhost/Customers.xml`  
  
```  
<?xml version="1.0"?>  
<Customers xmlns="http://www.adventure-works.com">  
   <Customer ID="11">  
      <FirstName>Bobby</FirstName>  
      <LastName>Moore</LastName>  
      <Orders>  
         <Order ID="1" Qty="6">Chair</Order>  
         <Order ID="2" Qty="1">Table</Order>  
      </Orders>  
      <Returns>  
         <Return ID="1" Qty="2">Chair</Return>  
      </Returns>  
   </Customer>  
   <Customer ID="20">  
      <FirstName>Crystal</FirstName>  
      <LastName>Hu</LastName>  
      <Orders>  
         <Order ID="8" Qty="2">Sofa</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
   <Customer ID="33">  
      <FirstName>Wyatt</FirstName>  
      <LastName>Diaz</LastName>  
      <Orders>  
         <Order ID="15" Qty="2">EndTables</Order>  
      </Orders>  
      <Returns/>  
   </Customer>  
</Customers>  
```  
  
 Sie können auch eine XML-Datenquelle ohne Verbindungszeichenfolge erstellen und Customers.XML in die Abfrage einbetten. Gehen Sie dazu wie folgt vor:  
  
###### <a name="to-embed-customersxml-in-a-query"></a>So betten Sie Customers.XML in einer Abfrage ein  
  
1.  Erstellen Sie eine XML-Datenquelle mit einer leeren Verbindungszeichenfolge.  
  
2.  Erstellen Sie ein neues Dataset für die XML-Datenquelle.  
  
3.  Klicken Sie im Dialogfeld **Dataseteigenschaften** auf **Abfrage-Designer**. Das textbasierte Dialogfeld des Abfrage-Designers wird geöffnet.  
  
4.  Geben Sie die folgenden Zeilen im Abfragebereich ein:  
  
     `<Query>`  
  
     `<XmlData>`  
  
5.  Kopieren Sie die Datei Customers.XML, und fügen Sie den Text im Abfragebereich nach der Zeile `<XmlData>`ein.  
  
6.  Löschen Sie im Abfragebereich die erste Zeile, die Sie aus der Datei Customers.XML kopiert haben: `<?xml version="1.0"?>`  
  
7.  Fügen Sie am Ende der Abfrage die beiden folgenden Zeilen hinzu:  
  
     `<XmlData>`  
  
     `<Query>`  
  
8.  Klicken Sie auf **Abfrage ausführen** (!).  
  
     Das Resultset zeigt vier Datenzeilen mit den folgenden Spalten an: `xmlns`, `Customer.ID`, `FirstName`, `LastName`, `ID`, `Qty`, `Order`  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Verbindungstyp &#40; SSRS &#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Reporting Services-Lernprogramme &#40; SSRS &#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Hinzufügen, bearbeiten und Aktualisieren von Feldern im Fenster ' Berichtsdaten ' &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
  

