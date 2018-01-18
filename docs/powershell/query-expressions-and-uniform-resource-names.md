---
title: "Abfrageausdrücke und eindeutige Ressourcennamen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query expressions
- unique resource names
- URN
ms.assetid: e0d30dbe-7daf-47eb-8412-1b96792b6fb9
caps.latest.revision: "14"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87e90bc33f653b36eac95fd8f525d5eb235ed1ea
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2018
---
# <a name="query-expressions-and-uniform-resource-names"></a>Abfrageausdrücke und eindeutige Ressourcennamen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Die SMO-Modelle ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Object) und [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell-Snap-Ins verwenden zwei Typen von Ausdruckszeichenfolgen, die XPath-Ausdrücken ähneln. Bei Abfrageausdrücken handelt es sich um Zeichenfolgen, die eine Gruppe von Kriterien angeben, mit der ein oder mehrere Objekte in einer Objektmodellhierarchie aufgezählt werden. Ein eindeutiger Ressourcenname (Uniform Resource Name, URN) ist ein spezieller Typ einer Abfrageausdrucks-Zeichenfolge, der ein einzelnes Objekt eindeutig kennzeichnet.  

> [!NOTE]
> Es gibt zwei SQL Server PowerShell-Module: **SqlServer** und **SQLPS**. Das **SQLPS**-Modul ist zwar in der SQL Server-Installation (für die Abwärtskompatibilität) enthalten, wird jedoch nicht mehr aktualisiert. Das **SqlServer**-Modul ist das aktuellste PowerShell-Modul. Das **SqlServer**-Modul enthält aktualisierte Versionen der Cmdlets in **SQLPS** sowie neue Cmdlets zur Unterstützung der neuesten SQL-Funktionen.  
> Vorherige Versionen des **SqlServer**-Moduls *waren* in SQL Server Management Studio (SSMS) enthalten, allerdings nur in den Versionen 16.x. Das **SqlServer**-Modul muss über den PowerShell-Katalog installiert werden, damit PowerShell mit SSMS 17.0 und höher verwendet werden kann.
> Informationen zur Installation des **SqlServer**-Moduls finden Sie unter [Installieren von SQL Server PowerShell](download-sql-server-ps-module.md).

  
## <a name="syntax"></a>Syntax  
  
```  
  
Object1[<FilterExpression1>]/ ... /ObjectN[<FilterExpressionN>]  
  
<FilterExpression>::=  
<PropertyExpression> [and <PropertyExpression>][...n]  
  
<PropertyExpression>::=  
      @BooleanPropertyName=true()  
 | @BooleanPropertyName=false()  
 | contains(@StringPropertyName, 'PatternString')  
  | @StringPropertyName='String'  
 | @DatePropertyName=datetime('DateString')  
 | is_null(@PropertyName)  
 | not(<PropertyExpression>)  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Objekt*  
 Gibt den Typ des Objekts an, der an diesem Knoten der Ausdruckszeichenfolge dargestellt wird. Jedes Objekt stellt eine Auflistungsklasse von diesen SMO-Objektmodellnamespaces dar:  
  
 <xref:Microsoft.SqlServer.Management.Smo>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Agent>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Mail>  
  
 <xref:Microsoft.SqlServer.Management.Dmf>  
  
 <xref:Microsoft.SqlServer.Management.Facets>  
  
 <xref:Microsoft.SqlServer.Management.RegisteredServers>  
  
 <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>  
  
 Geben Sie z.B. „Server“ für die **ServerCollection** -Klasse und „Database“ für die **DatabaseCollection** -Klasse an.  
  
 @*PropertyName*  
 Gibt den Namen einer Eigenschaft der Klasse an, die mit dem in *Object*angegebenen Objekt verknüpft ist. Dem Namen der Eigenschaft muss das Zeichen @ vorangestellt werden. Geben Sie beispielsweise @IsAnsiNull für die **Datenbank**-Klasseneigenschaft **IsAnsiNull** an.  
  
 @*BooleanPropertyName*=true()  
 Listet alle Objekte auf, bei denen die angegebene boolesche Eigenschaft auf TRUE gesetzt ist.  
  
 @*BooleanPropertyName*=false()  
 Listet alle Objekte auf, bei denen die angegebene boolesche Eigenschaft auf FALSE gesetzt ist.  
  
 contains(@*StringPropertyName*, '*PatternString*')  
 Listet alle Objekte auf, bei denen die angegebene Zeichenfolgeneigenschaft mindestens ein Vorkommen des Zeichensatzes enthält, der in '*PatternString*' angegeben ist.  
  
 @*StringPropertyName*='*PatternString*'  
 Listet alle Objekte auf, bei denen der Wert der angegebenen Zeichenfolgeneigenschaft mit dem Zeichenmuster identisch ist, das in '*PatternString*' angegeben ist.  
  
 @*DatePropertyName*= datetime('*DateString*')  
 Listet alle Objekte auf, bei denen der Wert der angegebenen Datumseigenschaft mit dem in '*DateString*' angegebenen Datum übereinstimmt. *DateString* muss dem Format „yyyy-mm-dd hh:mi:ss.mmm“ entsprechen.  
  
|||  
|-|-|  
|yyyy|Vierstellige Jahreszahl|  
|MM|Zweistellige Monatsangabe (01 bis 12)|  
|dd|Zweistellige Tagesangabe (01 bis 31)|  
|hh|Zweistellige Angabe der Stunde im 24-Stunden-Format (01 bis 23).|  
|mi|Zweistellige Minutenangabe (01 bis 59)|  
|ss|Zweistellige Sekundenangabe (01 bis 59)|  
|mmm|Anzahl der Millisekunden (001 bis 999)|  
  
 Die in diesem Format angegebenen Daten können mit einem beliebigen Datumsformat, das in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]gespeichert ist, verglichen werden.  
  
 is_null(@*PropertyName*)  
 Listet alle Objekte auf, bei denen die angegebene Eigenschaft den Wert NULL hat.  
  
 Keine (\<*PropertyExpression*>)  
 Negiert den Evaluierungswert von *PropertyExpression*und listet alle Objekte auf, die nicht der in *PropertyExpression*angegebenen Bedingung entsprechen. Zum Beispiel listet not(contains(@Name, 'xyz')) alle Objekte auf, deren Name nicht die Zeichenfolge xyz aufweist.  
  
## <a name="remarks"></a>Remarks  
 Abfrageausdrücke sind Zeichenfolgen, die die Knoten in einer SMO-Modellhierarchie auflisten. Jeder Knoten besitzt einen Filterausdruck, der die Kriterien angibt, mit denen bestimmt werden kann, welche Objekte an diesem Knoten aufgelistet sind. Abfrageausdrücke werden anhand der XPath-Ausdruckssprache modelliert. Abfrageausdrücke implementieren eine kleine Teilmenge von Ausdrücken, die von XPath unterstützt werden, und weisen zudem einige Erweiterungen auf, die nicht in XPath zu finden sind. Bei XPath-Ausdrücken handelt es sich um Zeichenfolgen, die eine Gruppe von Kriterien angeben, mit der ein oder mehrere Tags in einem XML-Dokument aufgezählt werden. Weitere Informationen zu XPath finden Sie unter [W3C XPath Language](http://www.w3.org/TR/xpath20/).  
  
 Abfrageausdrücke müssen mit einem absoluten Verweis auf das Serverobjekt beginnen. Relative Ausdrücke mit einem vorangestellten Schrägstrich (/) sind nicht zulässig. Die Sequenz der Objekte, die in einem Abfrageausdruck angegeben sind, muss der Hierarchie der Auflistungsobjekte im zugeordneten Objektmodell entsprechen. Ein Abfrageausdruck beispielsweise, der auf Objekte im Microsoft.SqlServer.Management.Smo-Namespace verweist, muss mit einem Serverknoten beginnen, gefolgt von einem Datenbankknoten usw.  
  
 Wenn für ein Objekt kein Wert für *\<<FilterExpression* angegeben wird, werden alle Objekte an diesem Knoten aufgelistet.  
  
## <a name="uniform-resource-names-urn"></a>Uniform Resource Name (URN)  
 URNs sind eine Teilmenge von Abfrageausdrücken. Jeder URN bildet einen voll qualifizierten Verweis auf ein einzelnes Objekt. Ein typischer URN verwendet die Eigenschaft Name, um ein einzelnes Objekt an jedem Knoten zu identifizieren. Zum Beispiel verweist dieser URN auf eine bestimmte Spalte:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[@Name='SalesPerson' and @Schema='Sales']/Column[@Name='SalesPersonID']  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-enumerating-objects-using-false"></a>A. Auflisten von Objekten mit „false()“  
 Dieser Abfrageausdruck listet alle Datenbanken auf, für die das Attribut **AutoClose** in der Standardinstanz unter **MyComputer**auf "false" gesetzt wurde.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@AutoClose=false()]  
```  
  
### <a name="b-enumerating-objects-using-contains"></a>B. Auflisten von Objekten mit „contains“  
 Dieser Abfrageausdruck listet alle Datenbanken auf, bei denen die Groß-/Kleinschreibung nicht beachtet werden muss und deren Namen den Buchstaben „m“ enthalten.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@CaseSensitive=false() and contains(@Name, 'm')]   
```  
  
### <a name="c-enumerating-objects-using-not"></a>C. Auflisten von Objekten mit „not“  
 Dieser Abfrageausdruck listet alle [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Tabellen auf, die nicht Bestandteil des **Production** -Schemas sind und deren Name das Wort „History“ enthält:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[not(@Schema='Production') and contains(@Name, 'History')]  
```  
  
### <a name="d-not-supplying-a-filter-expression-for-the-final-node"></a>D. Keine Angabe eines Filterausdrucks für den abschließenden Knoten  
 Dieser Abfrageausdruck listet alle Spalten in der **AdventureWorks2012.Sales.SalesPerson** -Tabelle auf:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@Schema='Sales' and @Name='SalesPerson']/Columns  
```  
  
### <a name="e-enumerating-objects-using-datetime"></a>E. Auflisten von Objekten mit „datetime“  
 Dieser Abfrageausdruck listet alle Tabellen auf, die in der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank zu einem bestimmten Zeitpunkt erstellt wurden:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@CreateDate=datetime('2008-03-21 19:49:32.647')]  
```  
  
### <a name="f-enumerating-objects-using-isnull"></a>F. Auflisten von Objekten mit „is_null“  
 Dieser Abfrageausdruck listet alle Tabellen in der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank auf, deren Eigenschaft für das Datum der letzten Änderung nicht NULL ist:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[Not(is_null(@DateLastModified))]  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Invoke-PolicyEvaluation-Cmdlet](invoke-policyevaluation-cmdlet.md)   
 [SQL Server Audit &#40;Datenbankmodul&#41;](../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  
