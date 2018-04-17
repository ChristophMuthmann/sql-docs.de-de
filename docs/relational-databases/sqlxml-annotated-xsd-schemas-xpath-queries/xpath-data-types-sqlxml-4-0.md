---
title: XPath-Datentypen (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- mapping XDR types to XPath types [SQLXML]
- data types [XPath]
- arithmetic operators
- mapping data types [SQLXML]
- relational operators [SQLXML]
- node-set [SQLXML]
- data types [SQLXML], XPath
- XPath operators [SQLXML]
- XDR data type [SQLXML]
- equality operators [SQLXML]
- XPath conversions [SQLXML]
- converting data types [SQLXML]
- Boolean operators
- XPath queries [SQLXML], data types
- XPath data types [SQLXML]
- operators [SQLXML]
ms.assetid: a90374bf-406f-4384-ba81-59478017db68
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2d52d84c175b7f7f3975645c385934a3c89be0d8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath-Datentypen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-, XPath- und XML-Schemas (XSD) verfügen über sehr unterschiedliche Datentypen. Zum Beispiel verfügt XPath nicht über Ganzzahl- oder Datumsdatentypen, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und XSD hingegen über mehrere. XSD gibt Zeitwerte auf die Nanosekunde genau an, während die Genauigkeit von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] höchstens 1/300 Sekunde beträgt. Einen Datentyp einem anderen zuzuordnen ist deshalb nicht immer möglich. Weitere Informationen zur Zuordnung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen und XSD-Datentypen, finden Sie unter [Datentypumwandlungen und die SQL: DataType-Anmerkung &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XPath verfügt über drei Datentypen: **Zeichenfolge**, **Anzahl**, und **booleschen**. Die **Anzahl** -Datentyp ist immer eine IEEE 754 Double Gleitkommazahlen mit doppelter Genauigkeit. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float(53)** -Datentyp kommt XPath **Anzahl**. Allerdings **float(53)** IEEE 754 nicht genau ist. Zum Beispiel wird weder NaN (Not-a-Number) noch Unendlichkeit verwendet. Es wird versucht, eine nicht numerische Zeichenfolge zu konvertieren **Anzahl** und der Versuch, eine Division durch 0 (null) führt zu einem Fehler.  
  
## <a name="xpath-conversions"></a>XPath-Konvertierungen  
 Wenn Sie eine XPath-Abfrage wie `OrderDetail[@UnitPrice > "10.0"]` verwenden, können implizite und explizite Datentypkonvertierungen den Sinn der Abfrage leicht verändern. Deshalb sollte nachvollzogen werden können, wie XPath-Datentypen implementiert werden. Der XPath-Sprachspezifikation, XML Path Language (XPath) Version 1.0 W3C vorgeschlagenen Empfehlung 8. Oktober 1999, finden Sie unter der W3C-Website unter http://www.w3.org/TR/1999/PR-xpath-19991008.html.  
  
 XPath-Operatoren werden in vier Kategorien unterteilt:  
  
-   Boolesche Operatoren (AND, OR)  
  
-   Relationale Operatoren (\<, >, \<=, > =)  
  
-   Gleichheitsoperatoren (=, !=)  
  
-   Arithmetische Operatoren (+, -, *, DIV, MOD)  
  
 Bei jeder Operatorkategorie werden die Operanden auf andere Art und Weise konvertiert. XPath-Operatoren konvertieren ihre Operanden gegebenenfalls implizit. Arithmetische Operatoren konvertieren ihre Operanden **Anzahl**, und das Ergebnis in einen numerischen Wert. Boolesche Operatoren konvertieren ihre Operanden **booleschen**, und das Ergebnis in einen booleschen Wert. Relationale Operatoren und Gleichheitsoperatoren geben einen booleschen Wert aus. Allerdings verfügen sie, je nach dem ursprünglichen Datentyp ihrer Operanden, über unterschiedliche Konvertierungsregeln (siehe Tabelle).  
  
|Operand|Relationaler Operator|Gleichheitsoperator|  
|-------------|-------------------------|-----------------------|  
|Beide Operanden sind Knotensätze.|"True", wenn ein Knoten in einem Satz vorhanden ist und ein Knoten in der zweiten Satz befindet, sodass diese beim Vergleich von ihren **Zeichenfolge** Werte sind "true".|Identisch.|  
|Eine einen Knotensatz, der andere ist eine **Zeichenfolge**.|TRUE, wenn ein Knoten im Knotensatz vorhanden ist, dass bei der Konvertierung in **Anzahl**, im Vergleich mit der **Zeichenfolge** konvertiert **Anzahl** ist "true".|TRUE, wenn ein Knoten im Knotensatz vorhanden ist, dass bei der Konvertierung in **Zeichenfolge**, im Vergleich mit der **Zeichenfolge** ist "true".|  
|Eine einen Knotensatz, der andere ist eine **Anzahl**.|TRUE, wenn ein Knoten im Knotensatz vorhanden ist, dass bei der Konvertierung in **Anzahl**, im Vergleich mit der **Anzahl** ist "true".|Identisch.|  
|Eine einen Knotensatz, der andere ist eine **booleschen**.|TRUE, wenn ein Knoten im Knotensatz vorhanden ist, dass bei der Konvertierung in **booleschen** , und klicken Sie dann auf **Anzahl**, im Vergleich mit der **booleschen** konvertiert**Anzahl** ist "true".|TRUE, wenn ein Knoten im Knotensatz vorhanden ist, dass bei der Konvertierung in **booleschen**, im Vergleich mit der **booleschen** ist "true".|  
|In beiden Fällen handelt es sich nicht um einen Knotensatz.|Konvertieren Sie beide Operanden **Anzahl** und vergleichen.|Konvertieren Sie beide Operanden in einen gängigen Typ , und führen Sie dann einen Vergleich durch. Konvertieren in **booleschen** ist entweder **booleschen**, **Anzahl** ist entweder **Anzahl**ist, andernfalls konvertieren in **Zeichenfolge**.|  
  
> [!NOTE]  
>  Da relationale XPath-Operatoren ihre Operanden stets konvertiert **Anzahl**, **Zeichenfolge** Vergleiche sind nicht möglich. Um Datenvergleiche, SQL Server 2000 bietet diese Variante der XPath-Spezifikation: Wenn ein relationaler Operator vergleicht eine **Zeichenfolge** auf eine **Zeichenfolge**ein Node-Set eine **Zeichenfolge**, oder eine Zeichenfolge ausgewertet Node-Set einen Zeichenfolgenwerten Knotensatz, eine **Zeichenfolge** Vergleich (keine **Anzahl** Vergleich) ausgeführt wird.  
  
## <a name="node-set-conversions"></a>Konvertierungen von Knotensätzen  
 Konvertierungen von Knotensätzen sind nicht immer intuitiv. Eine Knotengruppe konvertiert eine **Zeichenfolge** ergreifen Sie hierzu den Zeichenfolgenwert des ersten Knotens in der Menge. Eine Knotengruppe konvertiert **Anzahl** durch Konvertierung in **Zeichenfolge**, und klicken Sie dann zum Konvertieren von **Zeichenfolge** auf **Anzahl**. Eine Knotengruppe konvertiert **booleschen** durch sein Vorhandensein überprüft.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] führt bei Knotensätzen keine Positionalauswahl durch: Die XPath-Abfrage `Customer[3]` beispielsweise bezieht sich auf den dritten Kunden; eine solche Positionalauswahl wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht unterstützt. Daher den Knoten-festgelegt-zu-**Zeichenfolge** oder Knoten-festgelegt-zu-**Anzahl** Konvertierungen wie XPath-Spezifikation beschrieben wird, nicht implementiert. Die Semantik von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bezieht sich auf "ein" Vorkommnis, während die XPath-Spezifikation "das erste" Vorkommnis bezeichnet. Zum Beispiel basiert auf der W3C-XPath-Spezifikation die XPath-Abfrage `Order[OrderDetail/@UnitPrice > 10.0]` wählt diese Aufträge mit dem ersten **OrderDetail** , besitzt eine **UnitPrice** größer als 10.0. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], diese XPath-Abfrage wählt diese Aufträge mit **OrderDetail** , besitzt eine **UnitPrice** größer als 10.0.  
  
 Konvertierung in **booleschen** wird das Vorhandensein überprüft Test daher den XPath-Abfrage `Products[@Discontinued=true()]` ist gleichbedeutend mit der SQL-Ausdruck "Products.Discontinued is not null", nicht in der SQL-Ausdruck "Products.Discontinued = 1". Um die Abfrage entspricht dem zweiten SQL-Ausdruck machen, konvertieren Sie zuerst die Knotengruppe nicht**booleschen** eingeben, z. B. **Anzahl**. Beispiel: `Products[number(@Discontinued) = true()]`.  
  
 Da die meisten Operatoren gemäß Definition als TRUE gelten, wenn sie für einen beliebigen oder einen einzigen der Knoten im Knotensatz TRUE sind, ergeben diese Operationen stets FALSE, wenn der Knotensatz leer ist. Wenn also A leer ist, gilt sowohl für `A = B` als auch `A != B` FALSE, für `not(A=B)` und `not(A!=B)` hingegen gilt TRUE.  
  
 In der Regel ein Attribut oder Element, das eine Spalte zugeordnet, ist vorhanden, wenn der Wert dieser Spalte in der Datenbank nicht **null**. Elemente, die auf Zeilen verweisen, sind vorhanden, sobald untergeordnete Elemente vorhanden sind.  
  
> [!NOTE]  
>  Elemente mit versehen **ist Konstante** immer vorhanden sein. Folglich können nicht XPath-Prädikate verwendet werden, auf **ist Konstante** Elemente.  
  
 Wenn eine Knotengruppe konvertiert wird, wird **Zeichenfolge** oder **Anzahl**, wird sein XDR-Typ (sofern vorhanden) im mit Anmerkungen versehenen Schema überprüft wird, und dieses Typs wird verwendet, um die Konvertierung zu bestimmen, die erforderlich ist.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Zuordnung von XDR-Datentypen und XPath-Datentypen  
 Der XPath-Datentyp eines Knotens wird vom XDR-Datentyp im Schema abgeleitet, wie in der folgenden Tabelle dargestellt (der Knoten **EmployeeID** wird zur Veranschaulichung verwendet).  
  
|XDR-Datentyp|Entsprechung<br /><br /> XPath-Datentyp|Verwendete SQL Server-Konvertierung|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|–|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|number|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|Zeichenfolge|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|– (es gibt keinen Datentyp in XPath, der dem fixed14.4 XDR-Datentyp entspricht)|CONVERT(money, EmployeeID)|  
|Datum|Zeichenfolge|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|Uhrzeit<br /><br /> time.tz|Zeichenfolge|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 Das Datum und Uhrzeit-Konvertierungen sind für die Verwendung konzipiert, ob der Wert in der Datenbank gespeichert ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"DateTime"** -Datentyp oder einen **Zeichenfolge**. Beachten Sie, dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"DateTime"** -Datentyp nicht verwendet **Timezone** und eine geringere Genauigkeit als der XML-Code hat **Zeit** -Datentyp. Enthalten die **Zeitzone** -Datentyp oder höhere Genauigkeit zu gewährleisten, speichern Sie die Daten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit einer **Zeichenfolge** Typ.  
  
 Wenn ein Knoten vom XDR-Datentyp in den XPath-Datentyp konvertiert wird, müssen mitunter weitere Konvertierungen vorgenommen werden (von einem XPath-Datentyp in einen anderen XPath-Datentyp). Ein Beispiel ist die folgende XPath-Abfrage:  
  
```  
(@m + 3) = 4  
```  
  
 Wenn @m wird von der **fixed14. 4** XDR-Datentyp, die Konvertierung von XDR-Datentyp in XPath-Datentyp erfolgt über:  
  
```  
CONVERT(money, m)  
```  
  
 Bei dieser Konvertierung wird der Knoten `m` von konvertiert **fixed14. 4** auf **Money**. Um den Wert 3 hinzuzufügen, ist jedoch eine zusätzliche Konvertierung erforderlich:  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 Der XPath-Ausdruck wird wie folgt ausgewertet:  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 Wie in der folgenden Tabelle dargestellt, handelt es sich hierbei um die gleiche Konvertierung wie bei anderen XPath-Ausdrücken (etwa Literalausdrücken oder zusammengesetzten Ausdrücken).  
  
||||||  
|-|-|-|-|-|  
||X ist unbekannt|X ist **Zeichenfolge**|X ist **Anzahl**|X ist **boolean**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. Konvertieren Sie einen Datentyp in einer XPath-Abfrage  
 In der folgenden XPath-Abfrage für ein mit Anmerkungen versehene XSD-Schema angegeben, die Abfrage wählt alle **Mitarbeiter** Knoten mit der **EmployeeID** -Attributwert E-1, wobei "E-" das Präfix angegeben ist, mit der **SQL: ID-Präfix** Anmerkung.  
  
 `Employee[@EmployeeID="E-1"]`  
  
 Das Prädikat in der Abfrage entspricht dem folgenden SQL-Ausdruck:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Da **EmployeeID** ist eines der **Id** (**Idref**, **Idrefs**, **Nmtoken**,  **NMTOKENS**usw.) Datentyp der Werte in der XSD-Schema **EmployeeID** konvertiert die **Zeichenfolge** XPath-Datentyp mithilfe der zuvor beschriebenen Konvertierungsregeln.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 Der Zeichenfolge wird das Präfix "E-" hinzugefügt, und das Ergebnis wird dann mit `N'E-1'` verglichen.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Führen Sie mehrere Datentypkonvertierungen in einer XPath-Abfrage aus  
 Betrachten Sie die folgende, für ein mit Anmerkungen versehenes XSD-Schema angegebene XPath-Abfrage: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Diese XPath-Abfrage gibt alle dem  **\<OrderDetail >** Elemente das Prädikat erfüllen `@UnitPrice * @OrderQty > 98`. Wenn die **UnitPrice** mit versehen ist ein **fixed14. 4** -Datentyp, in dem Schema mit Anmerkungen dieses Prädikat ist gleichbedeutend mit der SQL-Ausdruck:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Beim Konvertieren der Werte in der XPath-Abfrage wird zunächst der XDR-Datentyp in den XPath-Datentyp konvertiert. Da der XSD-Datentyp **UnitPrice** ist **fixed14. 4**, wie in der obigen Tabelle beschrieben wird, ist dies die erste Konvertierung, die verwendet wird:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Da die arithmetischen Operatoren ihre Operanden konvertiert die **Anzahl** XPath-Datentyp, die zweite Konvertierung (von einem XPath-Datentyp in einen anderen XPath-Datentyp) wird angewendet, in dem der Wert wird in **float(53)**  (**float(53)** liegt nahe bei den XPath **Anzahl** -Datentyp):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Vorausgesetzt, die **OrderQty** Attribut hat keine XSD-Datentyp **OrderQty** konvertiert eine **Anzahl** XPath-Datentyp in einer einzelkonvertierung:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 Auf ähnliche Weise wird der Wert 98 konvertiert, um die **Anzahl** XPath-Datentypen:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Wenn der im Schema verwendete XSD-Datentyp mit dem in der Datenbank zugrunde gelegten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp inkompatibel ist oder eine nicht mögliche XPath-Datentypkonvertierung durchgeführt werden soll, sollte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler melden. Z. B. wenn die **EmployeeID** mit dem Attribut versehen ist **Id-Präfix** Anmerkung XPath `Employee[@EmployeeID=1]` generiert einen Fehler, da **EmployeeID** hat die **Id-Präfix** Anmerkung und kann nicht konvertiert werden, um **Anzahl**.  
  
  
