---
title: "XML-Abfragesyntax f&#252;r XML-Berichtsdaten (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Namespaces [Reporting Services]"
  - "Datenverarbeitungserweiterungen [Reporting Services], Datenquellen"
  - "xmldp [Reporting Services]"
  - "XML [Reporting Services], Datenabruf"
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
caps.latest.revision: 49
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 49
---
# XML-Abfragesyntax f&#252;r XML-Berichtsdaten (SSRS)
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]können Sie Datasets für XML-Datenquellen erstellen. Wenn Sie eine Datenquelle definiert haben, erstellen Sie eine Abfrage für das Dataset. Je nach Typ der XML-Daten, auf die die Datenquelle zeigt, können Sie die Datasetabfrage erstellen, indem Sie eine XML- **Query** oder einen Elementpfad einfügen. Eine XML-**Query** beginnt mit einem **\<Query>**-Tag und enthält Namespaces und XML-Elemente, die je nach Datenquelle variieren. Ein Elementpfad ist von Namespaces unabhängig und gibt die Knoten und Knotenattribute in den zugrunde liegenden XML-Daten an, die mit der XPath-ähnlichen Syntax verwendet werden sollen. Weitere Informationen zu Elementpfaden finden Sie unter [Syntax für Elementpfade für XML-Berichtsdaten &#40;SSRS&#41;](../../reporting-services/report-data/element-path-syntax-for-xml-report-data-ssrs.md).  
  
 Sie können eine XML-Datenquelle für die folgenden Typen von XML-Daten erstellen:  
  
-   XML-Dokumente, auf die eine URL über HTTP zeigt  
  
-   Webdienst-Endpunkte, die XML-Daten zurückgeben  
  
-   Eingebettete XML-Daten  
  
 Die Art, wie Sie eine XML- **Query** oder einen Elementpfad angeben, ist vom Typ der XML-Daten abhängig.  
  
 Bei einem XML-Dokument ist die XML- **Query** optional. Wenn sie eingeschlossen wird, kann sie einen optionalen XML- **ElementPath**enthalten. Der Wert des XML- **ElementPath** verwendet die Syntax des Elementpfades. Sie schließen die XML- **Query** und den XML- **ElementPath** ein, um Namespaces ordnungsgemäß zu verarbeiten, wenn diese von den XML-Daten in der Datenquelle benötigt werden.  
  
 Für einen Webdienst-Endpunkt, auf den eine Verbindungszeichenfolgen-URL zeigt, definiert die XML- **Query** die Webdienstmethode, die SOAP-Aktion oder beide. Der XML-Datenanbieter erstellt eine Webdienstanforderung, mit der XML-Daten abgerufen werden, die im Bericht verwendet werden sollen.  
  
> [!NOTE]  
>  Wenn ein Webdienst-Namespace einen Schrägstrich (**/**) enthält, fügen Sie die Webdienstmethode und die SOAP-Aktion ein, sodass die XML-Datenverarbeitungserweiterung den Namespace fehlerfrei ableiten kann.  
  
 Für ein eingebettetes XML-Dokument definiert die XML- **Query** die zu verwendenden eingebetteten XML-Daten, außerdem enthält sie optionale Namespaces und einen optionalen XML- **ElementPath**.  
  
## Angeben von Abfrageparametern für XML-Daten  
 Sie können Abfrageparameter für XML-Dokumente angeben.  
  
-   Bei URL-Anforderungen sind die Abfrageparameter als URL-Standardparameter enthalten.  
  
-   Bei Webdienstanforderungen werden Abfrageparameter an die Webdienstmethode übergeben. Verwenden Sie zum Definieren eines Abfrageparameters im Dialogfeld **Dataseteigenschaften** die Seite **Parameter** . Weitere Informationen finden Sie unter [Dataseteigenschaften (Dialogfeld), Parameter](../../reporting-services/report-data/dataset-properties-dialog-box-parameters.md).  
  
### Beispiel  
 Die Beispiele in der folgenden Tabelle veranschaulichen das Abrufen von Daten vom Berichtsserver-Webdienst, einem XML-Dokument und eingebetteten XML-Daten.  
  
|XML-Datenquelle|Abfragebeispiel|  
|---------------------|-------------------|  
|Webdienst-XML-Daten aus der <xref:ReportService2010.ReportingService2010.ListChildren%2A>-Methode|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="http://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|Webdienst-XML-Daten von SoapAction.|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>http://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|XML-Dokument oder eingebettete XML-Daten, die Namespaces verwenden.<br /><br /> Abfrageelement, das Namespaces für einen Elementpfad angibt.|`<Query xmlns:es="http://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|Eingebettetes XML-Dokument.|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|XML-Dokument, das Standardwerte verwendet.|*No query*.<br /><br /> Der Elementpfad wird vom XML-Dokument selbst abgeleitet und ist von Namespaces unabhängig.|  
  
> [!NOTE]  
>  Im ersten Webdienstbeispiel wird der Inhalt des Berichtsservers aufgeführt, der die <xref:ReportService2006.ReportingService2006.ListChildren%2A>-Methode verwendet. Diese Abfrage können Sie ausführen, indem Sie eine neue Datenquelle erstellen und die Verbindungszeichenfolge auf "http://localhost/reportserver/reportservice2006.asmx" festlegen. Die <xref:ReportService2006.ReportingService2006.ListChildren%2A>-Methode akzeptiert zwei Parameter: **Item** und **Recursive**. Legen Sie den Standardwert für **Item** auf **/** und für **Recursive** auf **1** fest.  
  
## Angeben von Namespaces  
 Verwenden Sie das XML- **Query** -Element zum Angeben der in den XML-Daten der Datenquelle verwendeten Namespaces. In der folgenden XML-Abfrage wird der Namespace **sales**verwendet. Die XML-**ElementPath**-Knoten für `sales:LineItems` und `sales:LineItem` verwenden den Namespace **sales**.  
  
```  
<Query xmlns:sales=  
"http://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      http://schemas.microsoft.com/SalesWebService/ListOrders   
   </SoapAction>  
   <ElementPath>  
      Customers/Customer/Orders/Order/sales:LineItems/sales:LineItem  
   </ElementPath>  
</Query>  
```  
  
 Wenn Sie den Namespace des Datenanbieters so angeben möchten, dass der Standardnamespace leer bleibt, verwenden Sie **xmldp**. Dies wird im folgenden Beispiel gezeigt.  
  
### Beispiel  
 Im folgenden Beispiel wird das XML-Dokument DPNamespace.xml verwendet, das zur Veranschaulichung unter der Tabelle bereitgestellt ist. In dieser Tabelle sind zwei Beispiele für XML-ElementPath-Syntax angegeben, die Namespacepräfixe enthalten.  
  
|XML-Abfrageelement|Resultierende Felder im Dataset|  
|-----------------------|-------------------------------------|  
|\<Query/>|Value A: http://schemas.microsoft.com/...<br /><br /> Value B: http://schemas.microsoft.com/...<br /><br /> Value C: http://schemas.microsoft.com/...|  
|`<xmldp:Query xmlns:xmldp="http://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery" xmlns:ns="http://schemas.microsoft.com/...">`<br /><br /> `<xmldp:ElementPath>Root {}/ns:Element2/Node</xmldp:ElementPath>`<br /><br /> `</xmldp:Query>`|Value D<br /><br /> Value E<br /><br /> Value F|  
  
#### XML-Dokument: DPNamespace.xml  
 Sie können dieses XML-Dokument kopieren und unter einer URL speichern, auf den der Berichts-Designer zugreifen kann, um es als XML-Datenquelle zu verwenden: z. B. http://localhost/DPNamespace.xml.  
  
```  
<Root xmlns:ns="http://schemas.microsoft.com/...">  
   <ns:Element1>  
      <Node>Value A</Node>  
      <Node>Value B</Node>  
      <Node>Value C</Node>  
   </ns:Element1>  
   <ns:Element2>  
      <Node>Value D</Node>  
      <Node>Value E</Node>  
      <Node>Value F</Node>  
   </ns:Element2>  
</Root>  
```  
  
## Siehe auch  
 [XML-Verbindungstyp &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Reporting Services-Tutorials &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  