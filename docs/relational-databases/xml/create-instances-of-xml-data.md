---
title: Erstellen Sie Instanzen der XML-Daten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- type casting string instances [XML in SQL Server]
- XML [SQL Server], typed
- xml data type [SQL Server], generating instances
- casting string instances [XML in SQL Server]
- typed XML
- generating XML instances [SQL Server]
- XML [SQL Server], generating instances
- white space [XML in SQL Server]
ms.assetid: dbd6c06f-db6e-44a7-855a-6a55bf374907
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54afef1467ec06d3ca695db00aa829fa387f6292
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-instances-of-xml-data"></a>Erstellen von Instanzen der XML-Daten
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie XML-Instanzen generiert werden.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gibt es folgende Möglichkeiten, XML-Instanzen zu generieren:  
  
-   Typumwandlung von Zeichenfolgeninstanzen  
  
-   Verwenden der SELECT-Anweisung mit der FOR XML-Klausel  
  
-   Verwenden von Konstantenzuweisungen  
  
-   Verwenden von Massenladen  
  
## <a name="type-casting-string-and-binary-instances"></a>Typumwandlung von Zeichenfolgen und Binärinstanzen  
 Sie können alle Zeichenfolgen-Datentypen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , z.B. [**n**][**var**]**char**, **[n]text**, **varbinary**und **image**, im **xml** -Datentyp analysieren, indem Sie die Zeichenfolge in den **xml** -Datentyp umwandeln (CAST) oder konvertieren (CONVERT). Nicht typisiertes XML wird überprüft, um die Wohlgeformtheit zu bestätigen. Wenn dem **xml** -Datentyp ein Schema zugeordnet ist, wird ebenfalls eine Überprüfung ausgeführt. Weitere Informationen finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
 XML-Dokumente können unterschiedlich codiert werden (z. B.: UTF-8, UTF-16, Windows-1252). Im Folgenden werden die Regeln erläutert, nach denen Zeichenfolgen- und Binärtypen mit der Codierung des XML-Dokuments interagieren und die das Verhalten des Parsers steuern.  
  
 Da **nvarchar** eine Doppelbyte-Unicode-Codierung wie UTF-16 oder UCS-2 annimmt, behandelt der XML-Parser den Zeichenfolgenwert als Doppelbyte-Unicode-codiertes XML-Dokument oder -Fragment. Dies bedeutet, dass auch das XML-Dokument in Doppelbyte-Unicode codiert sein muss, um mit dem Quelldatentyp kompatibel zu sein. Ein UTF-16-codiertes XML-Dokument kann eine UTF-16-Bytereihenfolgemarke (BOM, Byte Order Mark) besitzen, benötigt diese aber nicht, da der Kontext des Quelltyps deutlich macht, dass es sich nur um ein Doppelbyte-Unicode-Dokument handeln kann.  
  
 Der Inhalt einer **varchar** -Zeichenfolge wird vom XML-Parser als Einzelbyte-XML-Dokument/-Fragment behandelt. Da der Quellzeichenfolge **varchar** eine Codepage zugeordnet ist, verwendet der Parser diese Codepage für die Codierung, wenn im XML-Code keine explizite Codierung angegeben ist. Wenn eine XML-Instanz eine BOM- oder eine Codierungsdeklaration besitzt, muss diese zur Codepage passen. Andernfalls gibt der Parser einen Fehler aus.  
  
 Der Inhalt von **varbinary** wird als Codepointdatenstrom behandelt, der direkt an den XML-Parser übergeben wird. Daher muss das XML-Dokument oder -Fragment die BOM- oder eine andere Codierungsangabe inline enthalten. Der Parser bestimmt die Codierung ausschließlich anhand des Datenstroms. Dies bedeutet, dass UTF-16-codiertes XML die UTF-16-BOM enthalten muss, und dass eine Instanz ohne BOM und ohne Deklaration als UTF-8 interpretiert wird.  
  
 Wenn die Codierung des XML-Dokuments im Vorfeld nicht bekannt ist und die Daten vor der Konvertierung in XML als Zeichenfolgen- oder als Binärdaten übergeben werden, sollten die Daten als **varbinary**behandelt werden. Wenn z.B. Daten aus einer XML-Datei mit OpenRowset() gelesen werden, sollten die zu lesenden Daten als **varbinary(max)** -Wert festgelegt sein:  
  
```  
select CAST(x as XML)   
from OpenRowset(BULK 'filename.xml', SINGLE_BLOB) R(x)  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt XML intern in einer effizienten Binärdarstellung dar, die UTF-16-Codierung verwendet. Vom Benutzer bereitgestellte Codierung wird nicht beibehalten, während des Analysevorgangs jedoch berücksichtigt.  
  
### <a name="type-casting-clr-user-defined-types"></a>Typumwandlung benutzerdefinierter CLR-Typen  
 Wenn ein benutzerdefinierter CLR-Typ eine XML-Serialisierung besitzt, können Instanzen dieses Typs explizit in einen XML-Datentyp umgewandelt werden. Weitere Einzelheiten zur XML-Serialisierung von benutzerdefinierten CLR-Typen finden Sie unter [XML-Serialisierung auf Grundlage von CLR-Datenbankobjekten](http://msdn.microsoft.com/library/ac84339b-9384-4710-bebc-01607864a344).  
  
### <a name="white-space-handling-in-typed-xml"></a>Leerzeichenbehandlung in typisiertem XML  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Leerzeichen in Elementinhalten als unbedeutend betrachtet, wenn diese in einer Sequenz von Nur-Leerzeichen-Zeichendaten auftreten, die durch ein Markup wie z. B. Begin- oder End-Tags getrennt und nicht in Entitäten geändert werden. (CDATA-Abschnitte werden ignoriert). Diese Behandlung von Leerzeichen unterscheidet sich von der Beschreibung von Leerzeichen in der XML 1.0-Spezifikation, die vom W3C (World Wide Web Consortium) veröffentlicht wird. Die Ursache ist darin zu suchen, dass der XML-Parser in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nur eine beschränkte Anzahl der in XML 1.0 definierten DTD-Teilmengen erkennt. Weitere Informationen zu den beschränkten DTD-Teilmengen, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt werden, finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 Standardmäßig verwirft der XML-Parser insignifikante Leerzeichen, wenn Zeichenfolgendaten in XML konvertiert werden, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Das `xml:space`-Attribut ist nicht für ein Element oder seine Vorgängerelemente definiert.  
  
-   Das `xml:space` -Attribut für ein Element oder eines seiner Vorgängerelemente weist den Standardwert auf.  
  
 Zum Beispiel:  
  
```  
declare @x xml  
set @x = '<root>      <child/>     </root>'  
select @x   
```  
  
 Dies ist das Ergebnis:  
  
```  
<root><child/></root>  
```  
  
 Sie können dieses Verhalten jedoch ändern. Um Leerzeichen für eine xml DT-Instanz beizubehalten, verwenden Sie den CONVERT-Operator und seinen optionalen *style* -Parameter, um einen Wert von 1 festzulegen. Zum Beispiel:  
  
```  
SELECT CONVERT(xml, N'<root>      <child/>     </root>', 1)  
```  
  
 Wenn der *style* -Parameter nicht verwendet oder sein Wert auf 0 festgelegt wird, werden insignifikante Leerzeichen für die Konvertierung der xml DT-Instanz nicht beibehalten. Weitere Informationen zum Verwenden des CONVERT-Operators und seines *style*-Parameters beim Konvertieren von Zeichenfolgendaten in XML DT-Instanzen finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
### <a name="example-cast-a-string-value-to-typed-xml-and-assign-it-to-a-column"></a>Beispiel: Umwandeln eines Zeichenfolgenwertes in typisiertes XML und Zuweisen des Wertes zu einer Spalte  
 Das folgende Beispiel wandelt eine Zeichenfolgenvariable, die ein XML-Fragment enthält, in den **xml** -Datentyp um und speichert diesen dann in der Spalte vom Typ **xml** :  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
go  
DECLARE  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
```  
  
 Der folgende insert-Vorgang wandelt eine Zeichenfolge implizit in den **xml** -Typ um:  
  
```  
INSERT INTO T VALUES (3, @s)   
```  
  
 Mithilfe von cast() können Sie die Zeichenfolge explizit in den **xml** -Datentyp umwandeln:  
  
```  
INSERT INTO T VALUES (3, cast (@s as xml))  
```  
  
 Sie können auch convert() wie im folgenden Beispiel gezeigt verwenden:  
  
```  
INSERT INTO T VALUES (3, convert (xml, @s))   
```  
  
### <a name="example-convert-a-string-to-typed-xml-and-assign-it-to-a-variable"></a>Beispiel: Konvertieren einer Zeichenfolge in typisiertes XML und Zuweisen der Zeichenfolge zu einer Spalte  
 Im folgenden Beispiel wird eine Zeichenfolge in den **xml** -Typ konvertiert und dann einer Variablen des **xml** -Datentyps zugewiesen.  
  
```  
declare @x xml  
declare  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
set @x =convert (xml, @s)  
select @x  
```  
  
## <a name="using-the-select-statement-with-a-for-xml-clause"></a>Verwenden der SELECT-Anweisung mit einer FOR XML-Klausel  
 Sie können die FOR XML-Klausel in einer SELECT-Anweisung verwenden, um Ergebnisse als XML zurückzugeben. Zum Beispiel:  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = (SELECT Column1, Column2  
               FROM   Table1, Table2  
               WHERE   Some condition  
               FOR XML AUTO)  
 ...  
```  
  
 Die SELECT-Anweisung gibt ein XML-Textfragment zurück, das dann während der Zuweisung zur Variablen des **xml** -Datentyps analysiert wird.  
  
 Sie können auch die [TYPE-Direktive](../../relational-databases/xml/type-directive-in-for-xml-queries.md) in der FOR XML-Klausel verwenden, die direkt ein FOR XML-Abfrageergebnis als **xml** -Datentyp zurückgibt:  
  
```  
Declare @xmlDoc xml  
SET @xmlDoc = (SELECT ProductModelID, Name  
               FROM   Production.ProductModel  
               WHERE  ProductModelID=19  
               FOR XML AUTO, TYPE)  
SELECT @xmlDoc  
```  
  
 Dies ist das Ergebnis:  
  
```  
<Production.ProductModel ProductModelID="19" Name="Mountain-100" />...  
```  
  
 Im folgenden Beispiel wird das typisierte **xml** -Ergebnis einer FOR XML-Abfrage in eine Spalte vom Typ **xml** eingefügt:  
  
```  
CREATE TABLE T1 (c1 int, c2 xml)  
go  
INSERT T1(c1, c2)  
SELECT 1, (SELECT ProductModelID, Name  
           FROM Production.ProductModel  
           WHERE ProductModelID=19  
           FOR XML AUTO, TYPE)  
SELECT * FROM T1  
go  
```  
  
 Weitere Informationen zu FOR XML finden Sie unter [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden **xml** -Datentypinstanzen an den Client zurückgegeben, die das Ergebnis unterschiedlicher Serverkonstrukte sind (z. B. FOR XML-Abfragen, für die die TYPE-Direktive verwendet wird, oder bei denen der **xml** -Datentyp verwendet wird, um XML aus SQL-Spalten, -Variablen und -Ausgabeparametern zurückzugeben). Im Clientanwendungscode wird vom ADO.NET-Anbieter angefordert, dass diese **xml** -Datentypinformationen als Binärcode vom Server gesendet werden. Wenn Sie FOR XML jedoch ohne die TYPE-Direktive verwenden, werden die XML-Daten als Zeichenfolgentyp zurückgegeben. Der Clientanbieter ist in jedem Fall fähig, beide XML-Formate zu verarbeiten.  
  
## <a name="using-constant-assignments"></a>Verwenden von Konstantenzuweisungen  
 Eine Zeichenfolgenkonstante kann dort verwendet werden, wo eine Instanz des **xml** -Datentyps erwartet wird. Dies entspricht einer impliziten CAST-Anweisung für die Zeichenfolge in XML. Zum Beispiel:  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
-- Or  
SET @xmlDoc = N'<?xml version="1.0" encoding="ucs-2"?><doc/>'  
```  
  
 Im vorherigen Beispiel wurde die Zeichenfolge implizit in den **xml** -Datentyp konvertiert und dann einer Variablen des **xml** -Datentyps zugewiesen.  
  
 Das folgende Beispiel fügt eine Konstantenzeichenfolge in eine Spalte vom Typ **xml** ein:  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
INSERT INTO T VALUES (3, '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>')   
```  
  
> [!NOTE]  
>  Für typisiertes XML wird das XML für das angegebene Schema überprüft. Weitere Informationen finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="using-bulk-load"></a>Verwenden von Massenkopieren  
 Die verbesserten [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md) -Funktionen ermöglichen das Massenkopieren von XML-Dokumenten in der Datenbank. Sie können XML-Instanzen aus Dateien in Spalten vom Typ **xml** in der Datenbank mit einem Massenkopiervorgang kopieren. Funktionierende Beispiele finden Sie unter [Beispiele für den Massenimport und -export von XML-Dokumenten &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md). Weitere Informationen über das Laden von XML-Dokumenten finden Sie unter [Laden von XML-Daten](../../relational-databases/xml/load-xml-data.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Abrufen und Abfragen von XML-Daten](../../relational-databases/xml/retrieve-and-query-xml-data.md)|Beschreibt die Teile von XML-Instanzen, die nicht beibehalten werden, wenn sie in Datenbanken gespeichert werden.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [xml-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;Data Modification Language&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)   
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
