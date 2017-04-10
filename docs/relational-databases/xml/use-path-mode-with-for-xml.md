---
title: "Verwenden des PATH-Modus mit FOR XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR XML PATH-Modus"
  - "Zeichen [SQL Server], XML"
  - "Aliase [SQL Server],XML"
  - "FOR XML-Klausel, PATH-Modus"
  - "FOR XML PATH-Modus"
  - "Spaltennamen [SQL Server]"
  - "XPath-Abfragen [SQL Server]"
ms.assetid: a685a9ad-3d28-4596-aa72-119202df3976
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Verwenden des PATH-Modus mit FOR XML
  Wie unter [Erstellen von XML mithilfe von FOR XML](../../relational-databases/xml/for-xml-sql-server.md)beschrieben, bietet der PATH-Modus ein vereinfachtes Verfahren zum Mischen von Elementen und Attributen. Außerdem eignet sich der PATH-Modus auch dazu, auf einfache Weise zusätzliche Schachtelungen zum Darstellen komplexer Eigenschaften einzuführen. Sie können Abfragen im FOR XML EXPLICIT-Modus verwenden, um einen solchen XML-Code aus einem Rowset zu konstruieren; der PATH-Modus stellt jedoch eine einfachere Alternative zu den potenziell aufwendigen Abfragen im EXPLICIT-Modus bereit. Der PATH-Modus ermöglicht in Kombination mit der Möglichkeit, verschachtelte FOR XML-Abfragen zu schreiben und die TYPE-Direktive zum Zurückgeben von Instanzen des Typs **xml** zu verwenden, das Schreiben von Abfragen mit geringerer Komplexität.  
  
 Im PATH-Modus werden Spaltennamen und Spaltenaliasse als XPath-Ausdrücke behandelt. Diese Ausdrücke zeigen an, wie die Werte dem XML-Code zugeordnet werden. Jeder XPath-Ausdruck ist ein relativer XPath, der den Typ des Elements bereitstellt, wie z. B. das Attribut, das Element, den skalaren Wert sowie den Namen und die Hierarchie des Knotens, der in Zusammenhang mit dem Zeilenelement generiert werden soll.  
  
 In diesem Abschnitt wird das Zuordnen von Spalten in einem Rowset unter verschiedenen Bedingungen beschrieben. Zudem werden Beispiele gegeben.  
  
## In diesem Abschnitt  
  
-   [Spalten ohne Namen](../../relational-databases/xml/columns-without-a-name.md)  
  
-   [Spalten mit Namen](../../relational-databases/xml/columns-with-a-name.md)  
  
-   [Spalten mit als Platzhalterzeichen angegebenen Namen](../../relational-databases/xml/columns-with-a-name-specified-as-a-wildcard-character.md)  
  
-   [Spalten mit Namen von XPath-Knotentests](../../relational-databases/xml/columns-with-the-name-of-an-xpath-node-test.md)  
  
-   [Spaltennamen, deren Pfad als „data&#40;&#41;“ angegeben ist](../../relational-databases/xml/column-names-with-the-path-specified-as-data.md)  
  
-   [Spalten, die standardmäßig einen NULL-Wert enthalten](../../relational-databases/xml/columns-that-contain-a-null-value-by-default.md)  
  
-   [Namespaceunterstützung im PATH-Modus](../../relational-databases/xml/namespace-support-in-path-mode.md)  
  
-   [Beispiele: Verwenden des PATH-Modus](../../relational-databases/xml/examples-using-path-mode.md)  
  
## Siehe auch  
 [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  