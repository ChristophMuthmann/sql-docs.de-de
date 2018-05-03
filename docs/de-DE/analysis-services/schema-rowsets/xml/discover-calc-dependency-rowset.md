---
title: DISCOVER_CALC_DEPENDENCY-Rowset | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_CALC_DEPENDENCIES rowset
ms.assetid: f39dde72-fa5c-4c82-8b4e-88358aa2e422
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b4651aa538ed9eec11a98a06884f7b037342ae22
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="discovercalcdependency-rowset"></a>DISCOVER_CALC_DEPENDENCY-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Berichtet von den Abhängigkeiten zwischen Berechnungen und auf den in jenen Berechnungen verwiesenen Objekten. Sie können diese Informationen in einer Clientanwendung verwenden, um Probleme mit komplexen Formeln zu melden oder um eine Warnung auszugeben, wenn verbundene Objekte gelöscht oder verändert werden. Sie können auch die in Measures oder berechneten Spalten verwendeten DAX-Ausdrücke mithilfe des Rowsets extrahieren.  
  
 **Gilt für:** tabellarische Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_CALC_DEPENDENCY** -Rowset enthält die folgenden Spalten. Außerdem enthält die Tabelle den Datentyp sowie eine Beschreibung der einzelnen Spalten, und es ist angegeben, ob die Spalte eingeschränkt werden kann, um die zurückgegebenen Zeilen zu begrenzen.  
  
|Spaltenname|Typindikator|Einschränkung|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|ja|Gibt den Datenbanknamen an, der das Objekt enthält, für das die Abhängigkeitsanalyse angefordert wird. Bei Auslassung wird die aktuelle Datenbank verwendet.<br /><br /> Das **DISCOVER_DEPENDENCY_CALC** -Rowset kann mithilfe dieser Spalte eingeschränkt werden.|  
|**OBJECT_TYPE**|**DBTYPE_WSTR**|ja|Gibt den Typ des Objekts an, für den die Abhängigkeitsanalyse angefordert wird. Das Objekt muss einem der folgenden Typen entsprechen:<br /><br /> **ACTIVE_RELATIONSHIP**: eine aktive Beziehung<br /><br /> **CALC_COLUMN**: Berechnete Spalte<br /><br /> **HIERARCHY**: eine Hierarchie<br /><br /> **MEASURE**: ein Measure<br /><br /> **RELATIONSHIP**: eine Beziehung<br /><br /> **KPI**: eine Leistungskennzahl (KPI – Key Performance Indicator)<br /><br /> <br /><br /> Beachten Sie, dass die **DISCOVER_DEPENDENCY_CALC** Rowset kann mithilfe dieser Spalte eingeschränkt werden.|  
|**ABFRAGE**|**DBTYPE_WSTR**|ja|Für tabellarische Modelle, die in [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] erstellt wurden, kann eine DAX-Abfrage oder ein DAX-Ausdruck eingefügt werden, um das Abhängigkeitsdiagramm für diese Abfrage bzw. den Ausdruck anzuzeigen. Mithilfe der QUERY-Einschränkung können Clientanwendungen bestimmen, welche Objekte von einer DAX-Abfrage verwendet werden.<br /><br /> Die **QUERY** -Einschränkung kann in XMLA oder in der WHERE-Klausel einer DMV-Abfrage angegeben werden. Weitere Informationen finden Sie im Abschnitt mit Beispielen.|  
|**TABLE**|**DBTYPE_WSTR**||Der Name der Tabelle, die das Objekt enthält, wofür die Abhängigkeitsinformationen generiert werden.|  
|**OBJEKT**|**DBTYPE_WSTR**||Der Name des Objekts, wofür die Abhängigkeitsinformationen generiert werden. Falls es sich beim Objekt um ein Measure oder eine berechnete Spalte handelt, verwenden Sie den Namen des Measures. Falls es sich beim Objekt um eine Beziehung handelt: der Name der Tabelle (oder Cubedimension), die die Spalte enthält, die an der Beziehung beteiligt ist.|  
|**AUSDRUCK**|**DBTYPE_WSTR**||Die Formel, die das Objekt enthält, für das Abhängigkeiten gesucht werden.|  
|**REFERENCED_OBJECT_TYPE**|**DBTYPE_WSTR**||Gibt den Typ des Objekts zurück, das eine Abhängigkeit vom Objekt aufweist, auf das verwiesen wird. Die zurückgegebenen Objekte können folgenden Typen entsprechen:<br /><br /> **CALC_COLUMN**: eine berechnete Spalte<br /><br /> **COLUMN**: eine Datenspalte<br /><br /> **MEASURE**: ein Measure<br /><br /> **RELATIONSHIP**: eine Beziehung<br /><br /> **KPI**: eine Leistungskennzahl (KPI – Key Performance Indicator)|  
|**REFERENCED_TABLE**|**DBTYPE_ WSTR**||Der Name der Tabelle, die das abhängige Objekt enthält.|  
|**REFERENCED_OBJECT**|**DBTYPE_ WSTR**||Der Name des Objekts, das eine Abhängigkeit vom Objekt aufweist, auf das verwiesen wird. Für Measures und berechnete Spalten: der Name des Measures oder der Spalte. Für Beziehungen: der vollqualifizierte Name der Tabelle (oder Cubedimension), die das abhängige Objekt enthält.|  
|**REFERENCED_EXPRESSION**|**DBTYPE_WSTR**||Eine Formel, entweder in einer berechneten Spalte oder einem Measure, die vom Objekt abhängig ist, auf das verwiesen wird.|  
  
## <a name="example"></a>Beispiel  
 **Grundlegende Syntax**  
  
 Die folgende Abfrage stellt eine einfache DMV-Abfrage dar, die Werte für alle Spalten in diesem Rowset zurückgibt und die Standarddatenbank über die aktuelle Verbindung verwendet. Sie können diese Abfrage in einem MDX-Abfrage-Fenster ausführen und seine Ergebnisse in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] anzeigen. Sie können auch über die Techniken beschrieben, die [Abfragen von Power Pivot-DMVs aus Excel](http://go.microsoft.com/fwlink/?LinkID=235146) um DMV-Abfrageergebnisse in Excel anzuzeigen.  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
```  
  
## <a name="example"></a>Beispiel  
 **Sortieren der Ergebnisse**  
  
 Fügt eine ORDER BY-Klausel hinzu, um das Rowset nach einer Tabelle oder einer anderen Spalte zu sortieren.  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY ORDER BY [TABLE] ASC  
```  
  
## <a name="example"></a>Beispiel  
 **Filtern Sie mithilfe einer WHERE-Klausel**  
  
 In der nächsten Abfrage wird gezeigt, wie eine Einschränkung mithilfe der WHERE-Klausel hinzugefügt wird. Die folgenden Spalten können als Abfragefilter in einer WHERE-Klausel verwendet werden: **Database_Name**, **Object_Type**und **Query**.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'RELATIONSHIP' OR OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
## <a name="example"></a>Beispiel  
 **Filtern Sie nach Measures und berechneten Spalten, um die zugrunde liegende DAX-Ausdrücke anzuzeigen**  
  
 In dieser Abfrage können Sie einfach nur das Measure oder die berechnete Spalte auswählen und dann den in der Berechnung verwendeten DAX-Ausdruck anzeigen. In der EXPRESSION-Spalte sind die DAX-Ausdrücke enthalten. Wenn Sie DISCOVER_CALC_DEPENDENCY verwenden, um den in diesem Modell verwendeten DAX-Ausdruck zu extrahieren, ist diese Abfrage dafür ausreichend. Sie gibt alle im Modell verwendeten Ausdrücke in aufsteigender Reihenfolge zurück.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'MEASURE' OR OBJECT_TYPE = 'CALC_COLUMN' ORDER BY [EXPRESSION] ASC  
```  
  
## <a name="example"></a>Beispiel  
 **Filtern unter Verwendung von Abfrage**  
  
 Mithilfe der QUERY-Einschränkung können Sie eine DAX-Abfrage angeben, um alle in dieser Abfrage verwendeten Objekte anzuzeigen. Als Beispiel dient eine einfache Abfrage wie 'Evaluate Customer'. Wie bereits erwähnt, gibt diese Abfrage Zeilen mit Kundendaten zurück, wobei die Zusammensetzung der Zeilen auf den Spalten in der Tabelle 'Customer' basiert. Wenn Sie nun DISCOVER_CALC_DEPENDENCY mit der QUERY-Einschränkung 'Evaluate Customer' ausführen, erhalten Sie die Spalten (oder Objekte), die in dieser Abfrage verwendet werden. In diesem Fall ist es eine Liste der Spalten in der Tabelle 'Customer'.  
  
 In den nächsten Abfragen wird die Syntax für die QUERY-Einschränkung veranschaulicht. Sie können diese Abfragen unter Verwendung von [AdventureWorks Tabular Model SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) ausführen, um das Resultset anzuzeigen.  
  
 Die erste Abfrage veranschaulicht, wie eine QUERY-Einschränkung für Objektnamen angegeben wird, die Leerzeichen enthalten. Die zweite, aus dem Artikel [Ausführen von DAX-Abfragen über OLE DB und ADOMD.NET](http://go.microsoft.com/fwlink/?LinkId=254329)entnommene Abfrage ist komplexer und umfasst Objekte aus mehreren Tabellen.  
  
> [!NOTE]  
>  Obwohl es so aussieht, als würden doppelte Anführungszeichen verwendet, weisen die Abfragen tatsächlich nur einfache Anführungszeichen auf. Umschließt ein Paar einfacher Anführungszeichen ' Evaluate \<Tablename > ", und einfache Anführungszeichen verwendet, um den Tabellennamen müssen mit Escapezeichen versehen werden durch diese sich verdoppelt. Tabellennamen müssen nur in einfache Anführungszeichen eingeschlossen werden, wenn der Tabellenname ein Leerzeichen enthält.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE ''Reseller Sales'''  
```  
  
```  
SELECT * from $system.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE CALCULATETABLE(VALUES(''Product Subcategory''[Product Subcategory Name]), ''Product Category''[Product Category Name] = "Bikes")'  
```  
  
## <a name="example"></a>Beispiel  
 **Abfragebeispiel Einschränkung anhand von XMLA**  
  
 Sie können den Discover-Befehl in XMLA verwenden, um die Abfrageobjekte in einer Tabelle zurückzugeben. Die Ergebnisse werden von XMLA als unformatierte XML-Daten zurückgegeben. Mithilfe von ADOMD.NET können Sie die Ergebnisse in einem besser lesbaren Format analysieren.  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>DISCOVER_CALC_DEPENDENCY</RequestType>  
     <Restrictions>  
        <RestrictionList>  
            <QUERY>Evaluate 'Reseller Sales'</QUERY>  
        </RestrictionList>  
    </Restrictions>  
    <Properties />  
</Discover>  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|a07ccd46-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|DependencyGraph|  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Schemarowsets](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Verwenden Sie dynamische Verwaltungssichten & #40; DMVs & #41; zum Überwachen von Analysis Services](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
