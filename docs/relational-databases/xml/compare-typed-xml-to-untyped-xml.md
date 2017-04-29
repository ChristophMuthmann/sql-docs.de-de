---
title: Vergleichen von typisiertem XML mit nicht typisiertem XML | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xml data type [SQL Server], variables
- parameters [XML in SQL Server]
- facets [XML in SQL Server]
- xml data type [SQL Server], columns
- untyped XML
- xml data type [SQL Server], typed xml
- XML [SQL Server], typed
- variables [XML in SQL Server], creating
- xml data type [SQL Server], untyped xml
- columns [XML in SQL Server], creating
- typed XML
- document mode processing [SQL Server]
- XML [SQL Server], untyped
- xml data type [SQL Server], parameters
ms.assetid: 4bc50af9-2f7d-49df-bb01-854d080c72c7
caps.latest.revision: 57
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 27533bcc63a8df64597db4529b16a26f1fb5a009
ms.lasthandoff: 04/11/2017

---
# <a name="compare-typed-xml-to-untyped-xml"></a>Vergleichen von typisiertem XML mit nicht typisiertem XML
  Sie können Variablen, Parameter und Spalten des **xml** -Datentyps erstellen. Optional können Sie eine Auflistung von XML-Schemas mit einer Variablen, einem Parameter oder einer Spalte vom Typ **xml** verknüpfen. In diesem Fall wird die Instanz des **xml** -Datentyps als *typisiert*bezeichnet. Anderenfalls wird die XML-Instanz als *nicht typisiert*bezeichnet.  
  
## <a name="well-formed-xml-and-the-xml-data-type"></a>Wohlgeformtes XML und der xml-Datentyp  
 Der **xml** -Datentyp implementiert den im ISO-Standard definierten **xml** -Datentyp. Deshalb ermöglicht er das Speichern sowohl von wohlgeformten XML-Dokumenten der Version 1.0 als auch von so genannten XML-Inhaltsfragmenten mit Textknoten und einer beliebigen Anzahl von Elementen auf der obersten Ebene in einer nicht typisierten XML-Spalte. Das System überprüft, ob die Daten wohlgeformt sind (wobei es nicht erforderlich ist, dass die Spalte an XML-Schemas gebunden ist) und weist alle Daten zurück, die in diesem erweiterten Sinne nicht wohlgeformt sind. Dies gilt auch für nicht typisierte XML-Variablen und -Parameter.  
  
## <a name="xml-schemas"></a>XML-Schemas  
 Ein XML-Schema stellt Folgendes bereit:  
  
-   **Überprüfungseinschränkungen.** Bei jeder Zuweisung oder Änderung einer typisierten xml-Instanz überprüft SQL Server die Instanz.  
  
-   **Datentypinformationen.** Schemas stellen Informationen zu den Typen von Attributen und Elementen in der **xml** -Datentypinstanz bereit. Die Typinformationen stellen den in der Instanz enthaltenen Werten genauere operationale Semantik zur Verfügung als dies bei untypisiertem **xml**möglich ist. Dezimale arithmetische Operationen können z. B. für einen Dezimalwert, nicht jedoch für einen Zeichenfolgenwert ausgeführt werden. Aus diesem Grund ist die Speicherung typisierten XMLs erheblich kompakter als bei nicht typisiertem XML.  
  
## <a name="choosing-typed-or-untyped-xml"></a>Auswählen zwischen typisiertem oder nicht typisiertem XML  
 Verwenden Sie den nicht typisierten **xml** -Datentyp in den folgenden Situationen:  
  
-   Sie verfügen über kein Schema für Ihre XML-Daten.  
  
-   Sie verfügen zwar über Schemas, wollen jedoch die Gültigkeit der Daten nicht durch den Server überprüfen lassen. Dies ist manchmal der Fall, wenn eine Anwendung eine clientseitige Gültigkeitsprüfung vor dem Speichern der Daten auf dem Server durchführt oder gemäß dem Schema ungültige XML-Daten temporär speichert oder Schemakomponenten verwendet, die vom Server nicht unterstützt werden.  
  
 Verwenden Sie den typisierten **xml** -Datentyp in den folgenden Situationen:  
  
-   Sie verfügen über Schemas für Ihre XML-Daten und wollen, dass der Server anhand der XML-Schemas die Gültigkeit Ihrer XML-Daten überprüft.  
  
-   Sie möchten Speicherungs- und Abfrageoptimierungen nutzen, die auf den Typinformationen basieren.  
  
-   Sie möchten beim Kompilieren Ihrer Abfragen einen größeren Nutzen aus den Typinformationen ziehen.  
  
 Typisierte XML-Spalten, -Parameter und -Variablen können XML-Dokumente oder -Inhalte speichern. Allerdings müssen Sie zum Zeitpunkt der Deklaration durch ein Flag angeben, ob Sie ein Dokument oder einen Inhalt speichern. Außerdem müssen Sie die Auflistung der XML-Schemas bereitstellen. Geben Sie DOCUMENT an, wenn jede XML-Instanz genau ein Element auf der obersten Ebene aufweist. Verwenden Sie ansonsten CONTENT. Der Abfragecompiler verwendet das DOCUMENT-Flag bei den Typüberprüfungen während der Abfragekompilierung, um Singleton-Elemente auf der obersten Ebene abzuleiten.  
  
## <a name="creating-typed-xml"></a>Erstellen von typisiertem XML  
 Bevor Sie typisierte **xml**-Variablen, -Parameter oder -Spalten erstellen können, müssen Sie die XML-Schemaauflistung zuerst mithilfe von [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md). erstellen. Anschließend können Sie der XML-Schemaauflistung Variablen, Parameter oder Spalten des **xml** -Datentyps zuordnen.  
  
 Im folgenden Beispiel wird eine zweiteilige Benennungskonvention zum Angeben des Namens der XML-Schemaauflistung verwendet. Der erste Teil ist der Schemaname, der zweite Teil der Name der XML-Schemaauflistung.  
  
### <a name="example-associating-a-schema-collection-with-an-xml-type-variable"></a>Beispiel: Verknüpfen einer Schemaauflistung mit einer Variablen vom Typ xml  
 Im folgenden Beispiel wird eine Variable vom Typ**xml** erstellt und eine Schemaauflistung mit dieser verknüpft. Die im Beispiel angegebene Schemaauflistung wurde bereits in die **AdventureWorks** -Datenbank importiert.  
  
```  
DECLARE @x xml (Production.ProductDescriptionSchemaCollection);   
```  
  
### <a name="example-specifying-a-schema-for-an-xml-type-column"></a>Beispiel: Angeben eines Schemas für eine Spalte vom Typ xml  
 Im folgenden Beispiel wird eine Tabelle mit einer Spalte vom Typ **xml** erstellt und ein Schema für die Spalte angegeben:  
  
```  
CREATE TABLE T1(  
 Col1 int,   
 Col2 xml (Production.ProductDescriptionSchemaCollection)) ;  
```  
  
### <a name="example-passing-an-xml-type-parameter-to-a-stored-procedure"></a>Beispiel: Übergeben eines Parameters vom Typ xml an eine gespeicherte Prozedur  
 Im folgenden Beispiel wird ein Parameter vom Typ **xml** an eine gespeicherte Prozedur übergeben und ein Schema für die Variable angegeben:  
  
```  
CREATE PROCEDURE SampleProc   
  @ProdDescription xml (Production.ProductDescriptionSchemaCollection)   
AS   
...  
```  
  
 Beachten Sie hinsichtlich der XML-Schemaauflistung Folgendes:  
  
-   Eine XML-Schemaauflistung ist nur in der Datenbank verfügbar, in der sie mit [Erstellen einer XML-Schemaauflistung](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)registriert wurde.  
  
-   Wenn Sie die Umwandlung aus einer Zeichenfolge in einen typisierten **xml** -Datentyp vornehmen, führt die Analyse außerdem die Überprüfung und Typisierung basierend auf den XML-Schemanamespaces in der angegebenen Auflistung aus.  
  
-   Sie können einen typisierten **xml** -Datentyp in einen nicht typisierten **xml** -Datentyp umwandeln und umgekehrt.  
  
 Weitere Informationen zu anderen Methoden zum Generieren von XML in SQL Server finden Sie unter [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md). Nachdem das XML generiert wurde, kann es einer Variablen vom Datentyp **xml** zugewiesen oder in Spalten vom Typ **xml** für die weitere Verarbeitung gespeichert werden.  
  
 In der Datentyphierarchie nimmt der **xml** -Datentyp einen Platz unter **sql_variant** und benutzerdefinierten Typen ein, steht jedoch über allen integrierten Typen.  
  
### <a name="example-specifying-facets-to-constrain-a-typed-xml-column"></a>Beispiel: Angeben von Facets zum Einschränken einer typisierten xml-Spalte  
 Typisierte **xml** -Spalten können so eingeschränkt werden, dass nur einzelne Elemente der obersten Ebene für jede darin gespeicherte Instanz zulässig sind. Sie geben zu diesem Zweck beim Erstellen der Tabelle den optionalen `DOCUMENT` -Facet an, wie das folgende Beispiel zeigt:  
  
```  
CREATE TABLE T(Col1 xml   
   (DOCUMENT Production.ProductDescriptionSchemaCollection));  
GO  
DROP TABLE T;  
GO  
```  
  
 Standardmäßig werden Instanzen, die in der typisierten **xml** -Spalte gespeichert werden, als XML-Inhalt und nicht als XML-Dokumente gespeichert. Folgendes wird auf diese Weise ermöglicht:  
  
-   Null oder zahlreiche Elemente der obersten Ebene  
  
-   Textknoten in Elementen der obersten Ebene  
  
 Sie können dieses Verhalten auch explizit festlegen, indem Sie, wie im folgenden Beispiel dargestellt, das `CONTENT` -Facet hinzufügen:  
  
```  
CREATE TABLE T(Col1 xml(CONTENT Production.ProductDescriptionSchemaCollection));  
GO -- Default  
```  
  
 Beachten Sie, dass Sie die optionalen DOCUMENT/CONTENT-Facets immer angeben können, wenn Sie den **xml** -Typ definieren (typisiertes xml). Wenn Sie eine typisierte **xml** -Variable erstellen, können Sie z.B. das DOCUMENT/CONTENT-Facet, wie im folgenden Beispiel gezeigt, hinzufügen:  
  
```  
declare @x xml (DOCUMENT Production.ProductDescriptionSchemaCollection);  
```  
  
## <a name="document-type-definition-dtd"></a>Dokumenttypdefinition (DTD)  
 Die Spalten, Variablen und Parameter des **xml** -Datentyps können mithilfe eines XML-Schemas typisiert werden, jedoch nicht mithilfe von DTD. Allerdings kann Inline-DTD sowohl für nicht typisiertes als auch für typisiertes XML verwendet werden, um Standardwerte bereitzustellen und um Entitätsverweise durch ihre erweiterte Form zu ersetzen.  
  
 Mithilfe von Drittanbieter-Tools können Sie DTDs in XML-Schemadokumente konvertieren und die XML-Schemas in die Datenbank laden.  
  
## <a name="upgrading-typed-xml-from-sql-server-2005"></a>Aktualisieren von typisiertem XML aus SQL Server 2005  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] wurde die XML-Schemaunterstützung erweitert, beispielsweise um die Unterstützung für die lax-Überprüfung, verbesserte Behundlung von Instanzdaten des Typs **xs:date**, **xs:time** und **xs:dateTime** instance data, und added support for list und union types. In den meisten Fällen beeinflussen die Änderungen die Aktualisierung nicht. Wenn Sie jedoch eine XML-Schemaauflistung in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] verwendeten, die Werte des Typs **xs:date**, **xs:time**oder **xs:dateTime** (oder einen Untertyp davon) zuließ, dann werden die folgenden Aktualisierungsschritte ausgeführt, wenn Sie die [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank an eine spätere Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]anfügen:  
  
1.  Für jede XML-Spalte, die mit einer XML-Schemaauflistung typisiert ist, die Elemente oder Attribute vom Typ **xs:anyType**, **xs:anySimpleType**, **xs:date** oder eines Untertyps davon, **xs:time** oder eines Untertyps davon oder **xs:dateTime** oder eines Untertyps davon enthält bzw. Elemente oder Attribute vom Typ union oder list sind, die einen dieser Typen enthalten, wird folgender Vorgang ausgeführt:  
  
    1.  Alle XML-Indizes der Spalte werden deaktiviert.  
  
    2.  Alle [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Werte werden weiterhin in der Z-Zeitzone dargestellt, weil sie in die Z-Zeitzone normalisiert wurden.  
  
    3.  Alle Werte des Typs **xs:date** oder **xs:dateTime** , die kleiner sind als der 1. Januar im Jahr 1, führen zu einem Laufzeitfehler, wenn der Index erneut erstellt wird oder wenn eine XQuery-Anweisung oder eine XML-DML-Anweisung für den XML-Datentyp ausgeführt wird, der diesen Wert enthält.  
  
2.  Alle negativen Jahresangaben in **xs:date** - oder **xs:dateTime** -Facets oder in Standardwerten einer XML-Schemaauflistung werden automatisch durch den kleinsten für den Basistyp **xs:date** oder **xs:dateTime** zulässigen Wert ersetzt (beispielsweise 0001-01-01T00:00:00.0000000Z für **xs:dateTime**).  
  
 Beachten Sie, dass Sie den gesamten XML-Datentyp weiterhin mit einer einfachen SQL-SELECT-Anweisung abrufen können, selbst wenn er negative Jahresangaben enthält. Es wird empfohlen, dass Sie die negativen Jahresangaben durch eine Jahresangabe ersetzen, die im neuen unterstützten Bereich liegt, oder den Typ des Elements oder Attributs in **xs:string**ändern.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;Data Modification Language&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)   
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
