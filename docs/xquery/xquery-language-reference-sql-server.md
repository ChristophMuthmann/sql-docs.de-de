---
title: XQuery-Sprachreferenz (SQLServer) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XQuery
- XQuery, about XQuery
- xml data type [SQL Server], XQuery
- XML [SQL Server], XQuery
- queries [XML in SQL Server], XQuery
ms.assetid: 8a69344f-2990-4357-8160-cb26aac95b91
caps.latest.revision: 51
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 54ce6897762f6d23632ee4bdf45be7103a89cf16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xquery-language-reference-sql-server"></a>XQuery-Sprachreferenz (SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../includes/tsql-md.md)] unterstützt eine Teilmenge der XQuery-Sprache, die für die Abfrage verwendet, wird die **Xml** -Datentyp. Diese XQuery-Implementierung orientiert sich am Arbeitsentwurf für XQuery (Juli 2004). Diese Sprache wird zurzeit vom W3C (World Wide Web Consortium) unter Mitwirkung aller großen Datenbankhersteller und Microsoft entwickelt. Da die W3C-Spezifikationen möglicherweise überarbeitet werden, bevor eine W3C-Empfehlung ausgesprochen wird, kann sich diese Implementierung von der endgültigen Empfehlung unterscheiden. Dieses Thema beschreibt die Semantik und Syntax der Teilmenge von XQuery, die in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt wird.  
  
 Weitere Informationen finden Sie unter der [W3C XQuery 1.0-Sprachspezifikation](http://go.microsoft.com/fwlink/?LinkId=48846).  
  
 XQuery ist eine Sprache, die strukturierte oder halbstrukturierte XML-Daten abfragen kann. Mit der **Xml** -Datentyp-Unterstützung der [!INCLUDE[ssDE](../includes/ssde-md.md)], Dokumente in einer Datenbank gespeichert und dann mithilfe von XQuery abgefragt werden können.  
  
 XQuery basiert auf der vorhandenen XPath-Abfragesprache. Dieser wurde Unterstützung für bessere Iteration, bessere Sortierergebnisse und eine Funktion zum Erstellen des erforderlichen XML hinzugefügt. XQuery wird auf der Grundlage des XQuery-Datenmodells ausgeführt. Dabei handelt es sich um eine Abstraktion von XML-Dokumenten und die XQuery-Ergebnisse, die typisiert oder nicht typisiert sein können. Die Typinformationen basieren auf den von der W3C XML-Schemasprache bereitgestellten Typen. Wenn keine Typisierungsinformationen verfügbar sind, behandelt XQuery die Daten so, als wären sie nicht typisiert. XPath, Version 1.0, verarbeitet XML auf ähnliche Weise.  
  
 Zum Abfragen einer XML-Instanz, die in einer Variable oder Spalte gespeicherten **Xml** , verwenden Sie die [Xml-Datentypmethoden](../t-sql/xml/xml-data-type-methods.md). Sie können z. B. eine Variable deklarieren **Xml** geben und es mithilfe von Abfragen die **query()** Methode der **Xml** -Datentyp.  
  
```  
DECLARE @x xml  
SET @x = '<ROOT><a>111</a></ROOT>'  
SELECT @x.query('/ROOT/a')  
```  
  
 Im folgenden Beispiel wird die Abfrage angegeben, für die Instructions-Spalte der **Xml** Typ in der ProductModel-Tabelle der AdventureWorks-Datenbank.  
  
```  
SELECT Instructions.query('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Die XQuery umfasst die Namespacedeklaration `declare namespace``AWMI=...`, und der Abfrageausdruck `/AWMI:root/AWMI:Location[@LocationID=10]`.  
  
 Beachten Sie, dass die XQuery, für die Instructions-Spalte der angegeben wird **Xml** Typ. Die [Query()-Methode](../t-sql/xml/query-method-xml-data-type.md) der XML-Typ zum Angeben der XQuery verwendet wird.  
  
 Die folgende Tabelle enthält die verwandten Themen, die das Verständnis der Implementierung von XQuery in [!INCLUDE[ssDE](../includes/ssde-md.md)] vertiefen sollen.  
  
|Thema|Description|  
|-----------|-----------------|  
|[XML-Daten &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)|Erläutert die Unterstützung für die **Xml**-Datentyp in der [!INCLUDE[ssDE](../includes/ssde-md.md)] und die Methoden, die Sie für diesen Datentyp verwenden können. Die **Xml** -Datentyp bildet das XQuery-Eingabedaten zu modellieren, auf die die XQuery-Ausdrücke ausgeführt werden.|  
|[XML-Schemaauflistungen &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)|Beschreibt, wie die in einer Datenbank gespeicherten XML-Instanzen typisiert werden können. Dies bedeutet, Sie können eine XML-schemaauflistung mit Zuordnen der **Xml** Typspalte. Alle in der Spalte gespeicherten Instanzen werden in der Auflistung anhand des Schemas überprüft und typisiert und stellen die Typinformationen für XQuery bereit.|  
|||  
  
> [!NOTE]  
>  Die Organisation dieses Abschnitts basiert auf der Arbeitsentwurfspezifikation für XQuery des World Wide Web Consortium (W3C). Einige der in diesem Abschnitt bereitgestellten Diagramme stammen aus dieser Spezifikation. In diesem Abschnitt wird die Microsoft XQuery-Implementierung mit der W3C-Spezifikation verglichen, es werden die Unterschiede zwischen XQuery und W3C beschrieben und die nicht unterstützten W3C-Funktionen genannt. Die W3C-Spezifikation finden Sie unter [ http://www.w3.org/TR/2004/WD-xquery-20040723 ](http://go.microsoft.com/fwlink/?LinkId=48846).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[XQuery Basics (XQuery-Grundlagen)](../xquery/xquery-basics.md)|Stellt eine grundlegende Übersicht über die XQuery-Konzepte und die Auswertung von Ausdrücken (statischer und dynamischer Kontext), die Atomarmachung, effektive boolesche Werte, das XQuery-Typsystem, Sequenztypzuordnung und Fehlerbehandlung zur Verfügung.|  
|[XQuery Expressions (XQuery-Ausdrücke)](../xquery/xquery-expressions.md)|Beschreibt primäre XQuery-Ausdrücke, path-Ausdrücke, sequence-Ausdrücke, arithmetische Vergleiche und logische Ausdrücke, die XQuery-Erstellung, FLWOR-Ausdrücke, bedingte und quantifizierte Ausdrücke sowie verschiedene Ausdrücke für Sequenztypen.|  
|[Module und Prologe &#40;XQuery&#41;](../xquery/modules-and-prologs-xquery.md)|Beschreibt den XQuery-Prolog.|  
|[XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)|Beschreibt eine Liste der unterstützten XQuery-Funktionen.|  
|[XQuery Operators Against the xml Data Type (XQuery-Operatoren für den xml-Datentyp)](../xquery/xquery-operators-against-the-xml-data-type.md)|Beschreibt unterstützte XQuery-Operatoren.|  
|[Additional Sample XQueries Against the xml Data Type (Zusätzliches Beispiel für XQuery-Abfragen für den XML-Datentyp)](../xquery/additional-sample-xqueries-against-the-xml-data-type.md)|Stellt zusätzliche XQuery-Beispiele bereit.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Daten &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Beispiele für den Massenimport und -export von XML-Dokumenten &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
