---
title: Sp_xml_preparedocument (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_xml_preparedocument_TSQL
- sp_xml_preparedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_preparedocument
ms.assetid: 95f41cff-c52a-4182-8ac6-bf49369d214c
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 040d5a0490457d9edd0ce9cc0e6674fcfc45e7b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spxmlpreparedocument-transact-sql"></a>sp_xml_preparedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Liest den als Eingabe bereitgestellten XML-Text, analysiert diesen mit dem MSXML-Parser (Msxmlsql.dll) und stellt das analysierte Dokument für die Verwendung bereit. Das analysierte Dokument ist eine strukturierte Darstellung der verschiedenen Knoten im XML-Dokument: Elemente, Attribute, Text, Kommentare usw.  
  
 **Sp_xml_preparedocument** gibt ein Handle, das verwendet werden kann, auf die neu erstellte interne Darstellung des XML-Dokuments zurück. Dieses Handle ungültig ist, für die Dauer der Sitzung oder bis das Handle, durch das Ausführen ungültig ist **Sp_xml_removedocument**.  
  
> [!NOTE]  
>  Ein analysiertes Dokument wird im internen Cache von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert. Der MSXML-Parser verwendet ein Achtel des gesamten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbaren Arbeitsspeichers. Führen Sie zur Vermeidung der Arbeitsspeicher knapp **Sp_xml_removedocument** , um Speicher freizugeben.  
  
> [!NOTE]  
>  Für Abwärtskompatibilität-Kompatibilität **Sp_xml_preparedocument** reduziert die CR ((char(13))- und LF (char(10)) Zeichen in Attributen auch dann, wenn diese Zeichen in Entitäten geändert wurden.  
  
> [!NOTE]  
>  Der XML-Parser aufgerufen, indem **Sp_xml_preparedocument** interner DTDs und Entitätsdeklarationen analysieren können. Weil in böswilliger Absicht DTDs und konstruiert Deklarationen verwendet werden können, um einen DoS-Angriff ausführen, es wird dringend empfohlen, dass Benutzer nicht direkt auf XML-Dokumente aus nicht vertrauenswürdigen Quellen zu passieren **Sp_xml_preparedocument**.  
>   
>  Zur Abschwächung von rekursiven Entität Erweiterung Angriffen **Sp_xml_preparedocument** auf 10.000 begrenzt die Anzahl der Entitäten, die sich unterhalb einer einzelnen Entität auf der obersten Ebene eines Dokuments erweitert werden können. Diese Grenze gilt nicht für Zeichen- oder numerische Entitäten. Die Grenze ermöglicht die Speicherung von Dokumenten mit zahlreichen Entitätsverweisen, verhindert jedoch die rekursive Erweiterung einer Entität in eine Kette von mehr als 10.000 Erweiterungen.  
  
> [!NOTE]  
>  **Sp_xml_preparedocument** begrenzt die Anzahl der Elemente, die auf 256 gleichzeitig geöffnet sein können.  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_xml_preparedocument  
hdoc   
OUTPUT  
[ , xmltext ]  
[ , xpath_namespaces ]   
```  
  
## <a name="arguments"></a>Argumente  
 *hdoc*  
 Das Handle für das gerade erstellte Dokument. *Hdoc* ist eine ganze Zahl.  
  
 [ *Xmltext* ]  
 Das ursprüngliche XML-Dokument. Der MSXML-Parser analysiert dieses XML-Dokument. *XmlText* ist ein Textparameter: **Char**, **Nchar**, **Varchar**, **Nvarchar**, **Text**, **Ntext** oder **Xml**. Der Standardwert ist NULL; in diesem Fall wird eine interne Darstellung eines leeren XML-Dokuments erstellt.  
  
> [!NOTE]  
>  **Sp_xml_preparedocument** kann nur Text oder nicht typisiertes XML verarbeitet. Falls ein Instanzwert, der als Eingabewert verwendet werden soll, bereits ein typisierter XML-Wert ist, müssen Sie ihn zunächst in eine neue nicht typisierte XML-Instanz oder eine Zeichenfolge konvertieren und anschließend diesen Wert als Eingabewert übergeben. Weitere Informationen finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
 [ *Xpath_namespaces* ]  
 Gibt die Namespacedeklarationen an, die in XPATH-Ausdrücken für Zeilen und Spalten in OPENXML verwendet werden. *Xpath_namespaces* ist ein Textparameter: **Char**, **Nchar**, **Varchar**, **Nvarchar**, **Text**, **Ntext** oder **Xml**.  
  
 Der Standardwert ist  **\<root Xmlns:mp = "Urn: Schemas-Microsoft-com: xml-Metaprop" >**. *Xpath_namespaces* stellt die Namespace-URIs für die Präfixe, die in den XPath-Ausdrücken in OPENXML mittels ein wohlgeformtes XML-Dokument verwendet. *Xpath_namespaces* deklariert das Präfix, das verwendet werden muss, um auf den Namespace verweisen **Urn: Schemas-Microsoft-com: xml-Metaprop**; Hier werden Metadaten zu den analysierten XML-Elementen. Obwohl Sie das Namespacepräfix für den Namespace der Metaeigenschaften mit diesem Verfahren neu definieren können, geht dieser Namespace nicht verloren. Das Präfix **mp** ist noch gültig für **Urn: Schemas-Microsoft-com: xml-Metaprop** selbst wenn *Xpath_namespaces* keine derartige Deklaration enthält.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder >0 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-preparing-an-internal-representation-for-a-well-formed-xml-document"></a>A. Erstellen einer internen Darstellung für ein wohlgeformtes XML-Dokument  
 Im folgenden Beispiel wird ein Handle für die neu erstellte interne Darstellung des als Eingabe bereitgestellten XML-Dokuments zurückgegeben. Im Aufruf von `sp_xml_preparedocument` wird die Standardzuordnung für das Namespacepräfix verwendet.  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
-- Remove the internal representation.  
exec sp_xml_removedocument @hdoc;  
```  
  
### <a name="b-preparing-an-internal-representation-for-a-well-formed-xml-document-with-a-dtd"></a>B. Erstellen einer internen Darstellung für ein wohlgeformtes XML-Dokument mit einer DTD  
 Im folgenden Beispiel wird ein Handle für die neu erstellte interne Darstellung des als Eingabe bereitgestellten XML-Dokuments zurückgegeben. Die gespeicherte Prozedur überprüft das geladene Dokument in Bezug auf die im Dokument enthaltene DTD. Im Aufruf von `sp_xml_preparedocument` wird die Standardzuordnung für das Namespacepräfix verwendet.  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(2000);  
SET @doc = '  
<?xml version="1.0" encoding="UTF-8" ?>   
<!DOCTYPE root   
[<!ELEMENT root (Customers)*>  
<!ELEMENT Customers EMPTY>  
<!ATTLIST Customers CustomerID CDATA #IMPLIED ContactName CDATA #IMPLIED>]>  
<root>  
<Customers CustomerID="ALFKI" ContactName="Maria Anders"/>  
</root>';  
  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
```  
  
### <a name="c-specifying-a-namespace-uri"></a>C. Angeben eines Namespace-URI  
 Im folgenden Beispiel wird ein Handle für die neu erstellte interne Darstellung des als Eingabe bereitgestellten XML-Dokuments zurückgegeben. Der Aufruf von `sp_xml_preparedocument` behält die `mp` als Präfix für die Namespacezuordnung der Metaeigenschaften und fügt die `xyz` Zuordnungspräfix für den Namespace `urn:MyNamespace`.  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc, '<ROOT xmlns:xyz="urn:MyNamespace"/>';  
```  
  
## <a name="see-also"></a>Siehe auch  
 <br>[Gespeicherte XML-Procedures(Transact-SQL)](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[Gespeicherte Procedures(Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[OPENXML(Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
 <br>[dm_exec_xml_handles (Transact-SQL)](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[Sp_xml_removedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)
  
  
