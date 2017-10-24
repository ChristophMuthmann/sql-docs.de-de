---
title: Typumwandlungsregeln in XQuery | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- XQuery, type casting
- casting rules [XML in SQL Server]
- explicit casting [SQL Server]
- type casting rules [XML in SQL Server]
- cast as operator
- implicit casting
ms.assetid: f2e91306-2b1b-4e1c-b6d8-a34fb9980057
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b3fc531210c575742ab4af7670bb122bb7473ca3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="type-casting-rules-in-xquery"></a>Typumwandlungsregeln in XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Das folgende Spezifikationsdiagramm für Funktionen und Operatoren von W3C XQuery 1.0 und XPath 2.0 zeigt die integrierten Datentypen. Dies umfasst die integrierten Grundtypen und abgeleiteten Typen.  
  
 ![XQuery 1.0-Typhierarchie](../xquery/media/xquery-typing-rules.gif "XQuery 1.0-Typhierarchie")  
  
 In diesem Thema werden die Regeln für die Typumwandlung beschrieben, die beim Umwandeln von einem Typ in einen anderen mithilfe der folgenden Methoden angewendet werden:  
  
-   Explizite Umwandlung, die Sie verwenden Sie **umgewandelt als** oder die typenkonstruktorfunktionen (z. B. `xs:integer("5")`).  
  
-   Implizite Umwandlung, die während der Typhöherstufung auftritt  
  
## <a name="explicit-casting"></a>Explizite Umwandlung  
 Die folgende Tabelle erläutert die zulässige Typumwandlung zwischen den integrierten Grundtypen.  
  
 ![Umwandlungsregeln für XQuery. ] (../xquery/media/casting-builtin-types.gif "Umwandlungsregeln für XQuery.")  
  
-   Ein integrierter Grundtyp kann basierend auf den in der Tabelle aufgeführten Regeln in einen anderen integrierten Grundtyp umgewandelt werden.  
  
-   Ein Grundtyp kann in jeden beliebigen Typ umgewandelt werden, der von diesem betreffenden Grundtyp abgeleitet ist. Sie können z. B. Typumwandlung aus **xs: decimal** auf **xs: Integer**, oder von **xs: decimal** auf **xs: Long**.  
  
-   Ein abgeleiteter Typ kann in einen beliebigen Typ umgewandelt werden, der sein Vorgänger in der Typhierarchie ist (bis hinauf zu seinem integrierten Grundtyp). Sie können z. B. Typumwandlung aus **xs: Token** auf **normalizedString** oder **xs: String**.  
  
-   Ein abgeleiteter Typ kann in einen Grundtyp umgewandelt werden, wenn sein primitiver Vorgänger in den Zieltyp umgewandelt werden kann. Sie können z. B. eine Typumwandlung **xs: Integer**, einen abgeleiteten Typ, in eine **xs: String**', ' primitive eingeben, da **xs: decimal**, **xs: Integer**des Primitive Vorgänger umgewandelt werden kann, um **xs: String**.  
  
-   Ein abgeleiteter Typ kann in einen anderen abgeleiteten Typ umgewandelt werden, wenn der primitive Vorgänger des Quelltyps in den primitiven Vorgänger des Zieltyps umgewandelt werden kann. Sie können z. B. Typumwandlung aus **xs: Integer** auf **xs: Token**, da umgewandelt werden kann **xs: decimal** auf **xs: String**.  
  
-   Die Regeln zum Umwandeln benutzerdefinierter Typen in integrierte Typen sind die gleichen wie für die integrierten Datentypen. Beispielsweise können Sie definieren eine **MyInteger** von abgeleiteten Typ **xs: Integer** Typ. Klicken Sie dann **MyInteger** umgewandelt werden kann, um **xs: Token**, da **xs: decimal** umgewandelt werden kann, um **xs: String**.  
  
 Die folgenden Datentypumwandlungsarten werden nicht unterstützt:  
  
-   Die Typumwandlung in oder aus Listentypen ist nicht zulässig. Dies schließt sowohl benutzerdefinierte Listentypen und integrierte Listentypen wie z. B. **xs: IDREFS**, **xs: Entities**, und **xs: NMTOKENS**.  
  
-   Typumwandlung in oder aus **xs: QName** wird nicht unterstützt.  
  
-   **xs: Notation** und die vollständig geordneten Untertypen von Duration **xdt: yearmonthduration** und **dayTimeDuration**, werden nicht unterstützt. Daher ist auch die Typumwandlung in oder aus diese(n) Datentypen nicht zulässig.  
  
 Die folgenden Beispiele veranschaulichen die explizite Typumwandlung.  
  
### <a name="example-a"></a>Beispiel A  
 Das folgende Beispiel fragt eine Variable vom Typ xml ab. Die Abfrage gibt eine Sequenz eines Werts vom simple-Typ zurück, der als xs:string typisiert ist.  
  
```  
declare @x xml  
set @x = '<e>1</e><e>2</e>'  
select @x.query('/e[1] cast as xs:string?')  
go  
```  
  
### <a name="example-b"></a>Beispiel B  
 Das folgende Beispiel fragt eine typisierte xml-Variable ab. Das Beispiel erstellt zuerst eine XML-Schemaauflistung. Anschließend wird die XML-Schemaauflistung zum Erstellen einer typisierten xml-Variablen verwendet. Das Schema stellt die Typisierungsinformationen für die XML-Instanz bereit, die der Variablen zugeordnet ist. Anschließend werden Abfragen für die Variable angegeben.  
  
```  
create xml schema collection myCollection as N'  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">  
      <xs:element name="root">  
            <xs:complexType>  
                  <xs:sequence>  
                        <xs:element name="A" type="xs:string"/>  
                        <xs:element name="B" type="xs:string"/>  
                        <xs:element name="C" type="xs:string"/>  
                  </xs:sequence>  
            </xs:complexType>  
      </xs:element>  
</xs:schema>'  
go  
```  
  
 Die folgende Abfrage gibt einen statischen Fehler zurück, da nicht bekannt ist, wie viele <`root`>-Elemente der obersten Ebene in der Dokumentinstanz vorhanden sind.  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
          <root><A>4</A><B>5</B><C>6</baz></C>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
 Die Abfrage ist erfolgreich, wenn ein <`root`>-Singleton-Element im Ausdruck angegeben wird. Die Abfrage gibt eine Sequenz eines Werts vom simple-Typ zurück, der als xs:string typisiert ist.  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
select @x.query('/root[1]/A cast as xs:string?')  
go  
```  
  
 Im folgenden Beispiel enthält die Variable vom Typ xml ein document-Schlüsselwort, das die XML-Schemaauflistung angibt. Dies zeigt an, dass es sich bei der XML-Instanz um ein Dokument handeln muss, das ein einziges Element der obersten Ebene besitzt. Wenn Sie zwei <`root`>-Elemente in der XML-Instanz erstellen, wird ein Fehler zurückgegeben.  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
go  
```  
  
 Sie können die Instanz so ändern, dass nur ein Element der obersten Ebene eingeschlossen wird. Die Abfrage funktioniert dann. Die Abfrage gibt erneut eine Sequenz eines Werts vom simple-Typ zurück, der als xs:string typisiert ist.  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
## <a name="implicit-casting"></a>Implizite Typumwandlung  
 Implizite Typumwandlung ist nur für numerische Datentypen und nicht typisierte atomare Datentypen zulässig. Beispielsweise die folgenden **min()** -Funktion gibt das Minimum der beiden Werte zurück:  
  
```  
min(xs:integer("1"), xs:double("1.1"))  
```  
  
 In diesem Beispiel die beiden Werte übergeben, an die XQuery **min()** Funktion weisen unterschiedliche Datentypen. Aus diesem Grund wird implizite Konvertierung durchgeführt, in denen **Ganzzahl** Typ wird zu höher gestuft **doppelte** und die beiden **doppelte** Werte verglichen werden.  
  
 Die Typhöherstufung, die in diesem Beispiel gezeigt wurde, unterliegt den folgenden Regeln:  
  
-   Ein integrierter abgeleiteter numerischer Datentyp kann auf seinen Basistyp heraufgestuft werden. Beispielsweise **Ganzzahl** auf heraufgestuft werden **decimal**.  
  
-   Ein **decimal** auf heraufgestuft werden **"float",** und ein **"float"** auf heraufgestuft werden **doppelte**.  
  
 Da implizite Typumwandlung nur für numerische Datentypen zulässig ist, sind die folgenden Vorgänge nicht zulässig.  
  
-   Die implizite Typumwandlung für Zeichenfolgen-Datentypen ist nicht zulässig. Angenommen, zwei **Zeichenfolge** -Datentypen erwartet werden, und übergeben Sie eine **Zeichenfolge** und ein **token**, tritt keine implizite Typumwandlung auf, und ein Fehler zurückgegeben.  
  
-   Die implizite Typumwandlung aus numerischen Datentypen in Zeichenfolgen-Datentypen ist nicht zulässig. Wenn Sie z. B. einen Wert vom Typ integer an eine Funktion übergeben, die einen Parameter vom string-Typ erwartet, tritt keine implizite Typumwandlung auf, und es wird ein Fehler zurückgegeben.  
  
## <a name="casting-values"></a>Typumwandlung von Werten  
 Wenn eine Umwandlung von einem Datentyp in einen anderen erfolgt, werden die Istwerte aus dem Wertebereich des Quelltyps in den Wertebereich des Zieltyps transformiert. Die Typumwandlung aus einem xs:decimal- in einen xs:double-Typ transformiert z. B. den decimal-Wert in einen double-Wert.  
  
 Im Folgenden finden Sie einige der Transformationsregeln.  
  
##### <a name="casting-a-value-from-a-string-or-untypedatomic-type"></a>Umwandeln eines Werts aus einem string- oder untypedAtomic-Typ  
 Der Wert, der in einen string- oder untypedAtomic-Typ umgewandelt wird, wird auf die gleiche Weise wie beim Überprüfen des Werts basierend auf den Regeln des Zieltyps transformiert. Dies schließt ggf. Muster- und Leerzeichenverarbeitungsregeln ein. Die folgende Umwandlung ist z. B. erfolgreich und generiert einen double-Wert (1.1e0):  
  
 `xs:double("1.1")`  
  
 Bei der Umwandlung in binäre Typen wie z. B. xs:base64Binary oder xs:hexBinary aus einem string- oder untypedAtomic-Typ müssen die Eingabewerte base64- bzw. hexadezimal codiert sein.  
  
##### <a name="casting-a-value-to-a-string-or-untypedatomic-type"></a>Umwandeln eines Werts in einen string- oder untypedAtomic-Typ  
 Bei der Umwandlung eines string- oder untypedAtomic-Typs wird der Wert in die kanonische lexikalische Darstellung von XQuery transformiert. Dies kann insbesondere bedeuten, dass ein Wert, der während der Eingabe einem bestimmten Muster oder einer anderen Einschränkung unterworfen war, nicht gemäß dieser Einschränkung dargestellt wird.  Informieren Sie Benutzer dazu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Typen, in denen kann Einschränkung des Typs ein Problem werden, indem Sie eine Warnung bereitgestellt wird, wenn diese Typen in die schemaauflistung geladen werden.  
  
 Wenn ein Wert vom Typ xs:float oder xs:double oder einer ihrer Untertypen in einen string- oder untypedAtomic-Typ umgewandelt wird, wird der Wert in wissenschaftlicher Schreibweise dargestellt. Dies geschieht nur, wenn der Absolutwert des Werts kleiner als 1.0E-6 oder größer oder gleich 1.0E6 ist. Dies bedeutet, dass 0 in wissenschaftlicher Schreibweise zu 0.0E0 serialisiert wird.  
  
 Beispielsweise gibt `xs:string(1.11e1)` den Zeichenfolgenwert `"11.1"` zurück, während `xs:string(-0.00000000002e0)` den Zeichenfolgenwert `"-2.0E-11"` zurückgibt.  
  
 Bei der Umwandlung binärer Typen wie z. B. xs:base64Binary oder xs:hexBinary in einen string- oder untypedAtomic-Typ werden die Binärwerte in base64- bzw. hexadezimal codierter Form dargestellt.  
  
##### <a name="casting-a-value-to-a-numeric-type"></a>Umwandeln eines Werts in einen numeric-Typ  
 Wenn ein Wert eines numeric-Typs in einen Wert eines anderen numeric-Typs umgewandelt wird, wird der Wert aus einem Wertebereich dem anderen Wertebereich zugeordnet, ohne die Zeichenfolgenserialisierung zu durchlaufen. Wenn der Wert nicht der Einschränkung eines Zieltyps genügt, gelten die folgenden Regeln:  
  
-   Wenn der Quellwert bereits vom Typ numeric und der Zieltyp xs:float oder ein Untertyp davon ist, der -INF- oder INF-Werte zulässt, und die Typumwandlung des numeric-Quellwerts zu einem Überlauf führen würde, wird der Wert INF zugeordnet, wenn er positiv ist, oder -INF, wenn der Wert negativ ist. Wenn der Zieltyp keine INF- oder -INF-Werte zulässt und ein Überlauf auftreten würde, schlägt die Typumwandlung fehl. Das Ergebnis ist in dieser Version von SQL Server die leere Sequenz.  
  
-   Wenn der Quellwert bereits vom Typ numeric und der Zieltyp ein numeric-Typ ist, der 0, -0e0 oder 0e0 im zulässigen Wertebereich enthält, und die Typumwandlung des numeric-Quellwerts einen Unterlauf verursachen würde, wird der Wert auf die folgende Weise zugeordnet:  
  
    -   Der Wert wird für einen decimal-Zieltyp 0 zugeordnet.  
  
    -   Der Wert wird -0e0 zugeordnet, wenn der Wert einen negativen Unterlauf verursacht.  
  
    -   Der Wert wird 0e0 zugeordnet, wenn der Wert einen negativen Unterlauf für einen float- oder double-Zieltyp verursacht.  
  
     Die Typumwandlung schlägt fehl, wenn der Zieltyp nicht Null in seinem Wertebereich enthält; das Ergebnis ist die leere Sequenz.  
  
     Beachten Sie, dass durch die Umwandlung eines Werts in einen binären Gleitkommawert wie z. B. xs:float, xs:double oder einen der jeweiligen Untertypen die Genauigkeit beeinträchtigt werden kann.  
  
## <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Der Gleitkommawert NaN wird nicht unterstützt.  
  
-   Umwandelbare Werte werden durch die Implementierungsbeschränkungen der Zieltypen eingeschränkt. Sie können nicht mit einem negativen Jahr in eine Datumszeichenfolge z. B. eine Typumwandlung **xs: Date**. Solche Umwandlungen führen zu einer leeren Sequenz, wenn der Wert zur Laufzeit bereitgestellt wird (statt einen Laufzeitfehler auszulösen).  
  
## <a name="see-also"></a>Siehe auch  
 [Definieren der Serialisierung von XML-Daten](../relational-databases/xml/define-the-serialization-of-xml-data.md)  
  
  

