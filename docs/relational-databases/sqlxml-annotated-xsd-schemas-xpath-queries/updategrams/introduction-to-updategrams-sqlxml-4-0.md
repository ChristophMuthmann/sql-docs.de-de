---
title: Einführung in Updategrams (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
- explicit schema mapping [SQLXML]
- updategrams [SQLXML], mapping schema specifying
- namespaces [SQLXML]
- updategrams [SQLXML], about updategrams
- attribute-centric mapping
- invalid characters [SQLXML]
- element-centric mapping [SQLXML]
- mapping schema [SQLXML], updategrams
- namespaces [SQLXML], updategrams
- executing updategrams [SQLXML]
- implicit schema mapping
ms.assetid: cfe24e82-a645-4f93-ab16-39c21f90cce6
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 387646968ef4e44a43ec9ee2c50a06d4ba4b6e6c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="introduction-to-updategrams-sqlxml-40"></a>Einführung in Updategrams (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Sie können ändern (einfügen, aktualisieren oder löschen) eine Datenbank in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aus einem vorhandenen XML-Dokument mithilfe eines Updategrams oder der OPENXML- [!INCLUDE[tsql](../../../includes/tsql-md.md)] Funktion.  
  
 Die OPENXML-Funktion ändert eine Datenbank durch Aufteilen des vorhandenen XML-Dokuments und Bereitstellen eines Rowsets, das an eine INSERT-, UPDATE- oder DELETE-Anweisung übergeben werden kann. Mit OPENXML werden Operationen direkt für die Datenbanktabellen ausgeführt. Daher eignet sich OPENXML besonders gut, wenn Rowsetanbieter, wie Tabellen, als Quelle auftreten können.  
  
 Wie mit OPENXML können Sie mit einem Updategram Daten in der Datenbank einfügen, aktualisieren oder löschen. Ein Updategram wird jedoch für die XML-Sichten verwendet, die vom XSD-Schema (oder einem XDR-Schema) bereitgestellt werden. So werden beispielsweise die Updates auf die vom Zuordnungsschema bereitgestellte XML-Sicht angewendet. Das Zuordnungsschema enthält die erforderlichen Informationen zum Zuordnen von XML-Elementen und -Attributen zu den entsprechenden Datenbanktabellen und -spalten. Das Updategram verwendet diese Zuordnungsinformationen zum Aktualisieren der Datenbanktabellen und -spalten.  
  
> [!NOTE]  
>  Diese Dokumentation setzt voraus, dass Sie mit Vorlagen und der Unterstützung von Zuordnungsschemas in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vertraut sind. Weitere Informationen finden Sie unter [Einführung in XSD-Schemas mit Anmerkungen versehen & #40; SQLXML 4.0 & #41; ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Ältere Anwendungen, die XDR verwenden, finden Sie unter [XDR-Schemas mit Anmerkungen versehen &#40;in SQLXML 4.0 veraltet&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="required-namespaces-in-the-updategram"></a>Erforderliche Namespaces im Updategram  
 Die Schlüsselwörter in einem Updategram, wie z. B.  **\<Sync >**,  **\<vor >**, und  **\<nach >**, vorhanden sind, in der **Urn: Schemas-Microsoft-com: XML-Updategrams** Namespace. Sie können ein beliebiges Namespacepräfix verwenden. In dieser Dokumentation wird die **Updg** Präfix kennzeichnet die **Updategram** Namespace.  
  
## <a name="reviewing-syntax"></a>Überprüfen der Syntax  
 Ein Updategram ist eine Vorlage mit  **\<Sync >**,  **\<vor >**, und  **\<nach >** Blöcke, die die Syntax der bilden die Updategram. Der folgende Code zeigt diese Syntax in ihrer einfachsten Form:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema= "AnnotatedSchemaFile.xml"] >  
    <updg:before>  
        ...  
    </updg:before>  
    <updg:after>  
        ...  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 In den folgenden Definitionen werden die Rollen der einzelnen Blöcke beschrieben:  
  
 **\<before>**  
 Identifiziert den vorhandenen Status (auch als "Vorher-Status" bezeichnet) der Datensatzinstanz.  
  
 **\<after>**  
 Identifiziert den neuen Status, in den Daten geändert werden sollen.  
  
 **\<sync>**  
 Enthält die  **\<vor >** und  **\<nach >** blockiert. Ein  **\<Sync >** Block darf maximal einen Satz von  **\<vor >** und  **\<nach >** blockiert. Es ist mehr als ein Satz von  **\<vor >** und  **\<nach >** Blöcke, diese Blöcke (selbst wenn sie leer sind) müssen paarweise angegeben werden. Darüber hinaus ein Updategram kann mehr als einen haben  **\<Sync >** Block. Jede  **\<Sync >** Block ist eine Transaktionseinheit (was bedeutet, dass entweder der gesamte der  **\<Sync >** -Block oder nichts ausgeführt). Bei Angabe mehrerer  **\<Sync >** -Blöcke in einem Updategram, die Fehler in einer  **\<Sync >** Block hat keinen Einfluss auf die andere  **\<Sync >** blockiert.  
  
 Gibt an, ob ein Updategram löscht, einfügt oder aktualisiert eine Datensatzinstanz hängt vom Inhalt des der  **\<vor >** und  **\<nach >** blockiert:  
  
-   Kommt eine nur in Datensatzinstanz der  **\<vor >** -Block ohne entsprechende Instanz in der  **\<nach >** das Updategram-Block führt einen Löschvorgang an.  
  
-   Kommt eine nur im Datensatzinstanz die  **\<nach >** -Block ohne entsprechende Instanz in der  **\<vor >** Block, es wird ein Einfügevorgang durchgeführt.  
  
-   Kommt eine im Datensatzinstanz die  **\<vor >** blockieren und verfügt über eine entsprechende Instanz der  **\<nach >** Block, es wird ein Updatevorgang. In diesem Fall das Updategram die Datensatzinstanz, die Werte, die im angegebenen aktualisiert die  **\<nach >** Block.  
  
## <a name="specifying-a-mapping-schema-in-the-updategram"></a>Angeben eines Zuordnungsschemas im Updategram  
 In einem Updategram kann die von einem Zuordnungsschema (sowohl XSD- als auch XDR-Schemas werden unterstützt) bereitgestellte XML-Abstraktion implizit oder explizit sein (d. h., ein Updategram kann mit angegebenem Zuordnungsschema oder ohne angegebenes Zuordnungsschema verwendet werden). Wenn Sie kein Zuordnungsschema angeben, geht das Updategram eine implizite Zuordnung (standardzuordnung), wobei jedes Element in der  **\<vor >** Block oder  **\<nach >** Block ordnet eine Tabelle und jedes Element untergeordnetes Element oder Attribut an eine Spalte in der Datenbank zugeordnet. Wenn Sie ausdrücklich ein Zuordnungsschema angeben, müssen die Elemente und Attribute im Updategram mit den Elementen und Attributen im Zuordnungsschema übereinstimmen.  
  
### <a name="implicit-default-mapping"></a>Implizite Zuordnung (Standardzuordnung)  
 Ein Updategram, das einfache Updates durchführt, benötigt in der Regel kein Zuordnungsschema. In diesem Fall verwendet das Updategram das Standardzuordnungsschema.  
  
 Das folgende Updategram zeigt eine implizite Zuordnung. In diesem Beispiel fügt das Updategram einen neuen Kunden in die Sales.Customer-Tabelle ein. Da in diesem Updategram eine implizite Zuordnung verwendet das \<Sales.Customer >-Element der Sales.Customer-Tabelle zugeordnet, und ordnen Sie die Attribute CustomerID und SalesPersonID den entsprechenden Spalten in der Sales.Customer-Tabelle.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
</updg:before>  
<updg:after>  
    <Sales.Customer CustomerID="1" SalesPersonID="277" />  
    </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="explicit-mapping"></a>Explizite Zuordnung  
 Wenn Sie ein Zuordnungsschema angeben (XSD oder XDR) verwendet das Updategram das Schema um zu bestimmen, welche Datenbanktabellen und -spalten aktualisiert werden sollen.  
  
 Wenn das Updategram ein komplexes Update (z. B. Einfügen von Datensätzen in mehreren Tabellen auf der Basis der über-/ unterordnungsbeziehung, die im Zuordnungsschema angegeben ist) ausführt, müssen Sie das Zuordnungsschema explizit angeben, mit der  **Zuordnungsschema** Attribut, für das das Updategram ausgeführt wird.  
  
 Da ein Updategram eine Vorlage ist, ist der für das Zuordnungsschema im Updategram angegebene Pfad bezieht sich auf den Speicherort der Vorlagendatei (relativ zum Speicherort des Updategrams). Weitere Informationen finden Sie unter [angeben eines Zuordnungsschemas in einem Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="element-centric-and-attribute-centric-mapping-in-updategrams"></a>Elementzentrierte und attributzentrierte Zuordnung in Updategrams  
 Bei der Standardzuordnung (wenn im Updategram kein Zuordnungsschema angegeben ist) werden die Updategramelemente Tabellen und die untergeordneten Elemente (bei der elementzentrierten Zuordnung) und die Attribute (bei der attributzentrierten Zuordnung) Spalten zugeordnet.  
  
### <a name="element-centric-mapping"></a>Elementzentrierte Zuordnung  
 Ein Element in einem elementzentrierten Updategram enthält untergeordnete Elemente, die die Eigenschaften des Elements angeben. Ein Beispiel finden Sie im folgenden Updategram. Die  **\<Person.Contact >** Element enthält die  **\<FirstName >**und  **\<LastName >** untergeordnete Elemente. Diese untergeordneten Elemente sind Eigenschaften von der  **\<Person.Contact >** Element.  
  
 Da dieses Updategram kein Zuordnungsschema angegeben ist, verwendet das Updategram die implizite Zuordnung, in dem die  **\<Person.Contact >** Element wird der Person.Contact-Tabelle zugeordnet und seinen untergeordneten Elementen zuordnen der FirstName und LastName-Spalten.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:after>  
    <Person.Contact>  
       <FirstName>Catherine</FirstName>  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="attribute-centric-mapping"></a>Attributzentrierte Zuordnung  
 Die Elemente in einer attributzentrierten Zuordnung verfügen über Attribute. Im folgenden Updategram wird die attributzentrierte Zuordnung verwendet. In diesem Beispiel wird die  **\<Person.Contact >** Element besteht aus den **FirstName** und **LastName** Attribute. Diese Attribute sind die Eigenschaften der  **\<Person.Contact >** Element. Wie im vorherigen Beispiel in diesem Updategram kein Zuordnungsschema angegeben, daher werden auf die implizite Zuordnung zum Zuordnen der  **\<Person.Contact >** -Element der Person.Contact-Tabelle und die Attribute des Elements der entsprechende Spalten in der Tabelle.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" LastName="Abel" />  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
### <a name="using-both-element-centric-and-attribute-centric-mapping"></a>Verwenden der elementzentrierten und der attributzentrierten Zuordnung  
 Sie können eine Mischung elementzentrierter und attributzentrierter Zuordnung angeben, wie im folgenden Updategram dargestellt. Beachten Sie, dass die  **\<Person.Contact >** -Element enthält sowohl ein Attribut als auch ein untergeordnetes Element. Für dieses Updategram wird die implizite Zuordnung verwendet. Daher die **FirstName** Attribut und der  **\<LastName >** untergeordneten Element entsprechenden Spalten in der Person.Contact-Tabelle zugeordnet.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
    <Person.Contact FirstName="Catherine" >  
       <LastName>Abel</LastName>  
    </Person.Contact>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="working-with-characters-valid-in-sql-server-but-not-valid-in-xml"></a>Verwenden von Zeichen, die in SQL Server gültig sind, in XML jedoch nicht  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dürfen Tabellennamen Leerzeichen enthalten. Dieser Tabellennamentyp ist in XML jedoch nicht gültig.  
  
 Um Zeichen zu codieren, die gültig sind [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Bezeichner, sind jedoch keine gültigen XML-Bezeichner, verwenden Sie "__xHHHH\_\_' als Codierungswert, wobei HHHH für den vierstelligen hexadezimalen UCS-2-Code für das Zeichen in den meisten steht bedeutende Bitfolge. Verwenden dieses Codierungsschema verwenden, ruft ein Leerzeichen mit X0020 (die vierstellige hexadezimale Code für ein Leerzeichen); ersetzt. daher den Tabellennamen [Order Details] in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] wird _x005B_Order_x0020_Details_x005D\_ im XML-Format.  
  
 Auf ähnliche Weise müssen möglicherweise Geben Sie dreiteilige Elementnamen, wie z. B. \<[Database]. [ Owner]. [Table] >. Da die Klammern ([ und ]) in XML nicht gültig sind, müssen Sie dies als angeben \<_x005B_database_x005D\_._x005B_owner_x005D\_._x005B_table_x005D\_>, wobei _x005B\_ ist die Codierung für die öffnende Klammer ([) und _x005D\_ ist die Codierung für die Rechte Klammer (]).  
  
## <a name="executing-updategrams"></a>Ausführen von Updategrams  
 Da ein Updategram eine Vorlage ist, gelten alle Verarbeitungsmechanismen einer Vorlage auch für ein Updategram. Zum Ausführen eines Updategrams in SQLXML 4.0 können Sie eine der beiden folgenden Möglichkeiten verwenden:  
  
-   Senden des Updategrams in einem ADO-Befehl  
  
-   Senden des Updategrams in einem OLE DB-Befehl  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitsüberlegungen zu Updategrams &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
