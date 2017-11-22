---
title: Einbinden relationaler Daten in XML-Daten | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef249a7482610419873604637290cab3ef18e34b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="binding-relational-data-inside-xml-data"></a>Einbinden relationaler Daten in XML-Daten
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Sie können angeben, [Xml-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md) gegen eine **Xml** -Datentyp, Variable oder Spalte. Z. B. die [Query &#40; &#41; -Methode &#40; Xml-Datentyp &#41; ](../../t-sql/xml/query-method-xml-data-type.md) führt die angegebene XQuery-Abfrage für eine XML-Instanz. Beim Erstellen von XML-Code auf diese Art sollten Sie einen Wert aus einer Nicht-XML-Typspalte oder eine Transact-SQL-Variable einbringen. Dieser Prozess wird als Einbinden relationaler Daten in XML bezeichnet.  
  
 Um relationale Nicht-XML-Daten in XML zu binden, bietet das SQL Server-Datenbankmodul folgende Pseudofunktionen:  
  
-   [SQL: Column &#40; &#41; Function &#40; XQuery &#41; ](../../xquery/xquery-extension-functions-sql-column.md) Können Sie die Werte aus einer relationalen Spalte in einem XQuery- oder XML DML-Ausdruck verwenden.  
  
-   [SQL: Variable &#40; &#41; Function &#40; XQuery &#41; ](../../xquery/xquery-extension-functions-sql-variable.md) . Gibt Ihnen die Möglichkeit, den Wert einer SQL-Variablen im XQuery- oder XML DML-Ausdruck zu verwenden.  
  
 Sie können diese Funktionen mit **Xml** -Datentypmethoden tritt ein, wenn Sie einen relationalen Werts in XML verfügbar machen möchten.  
  
 Nicht möglich, verwenden Sie diese Funktionen zum Verweisen auf Daten in Spalten oder Variablen von der **Xml**, benutzerdefinierte CLR-Typen, Datetime, Smalldatetime, **Text**, **Ntext**, **Sql_variant**, und **Image** Typen.  
  
 Das Einbinden ist außerdem nur zur Leseberechtigung. Deshalb können Sie in Spalten keine Daten schreiben, die diese Funktion verwenden. Beispielsweise Sql:variable("@x") = "*einige Ausdruck"* ist nicht zulässig.  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>Beispiel: Domänenübergreifende Abfrage mithilfe von sql:variable()  
 Dieses Beispiel zeigt, wie **SQL:Variable()** kann eine Anwendung eine Abfrage parametrisieren aktiviert. Die ISBN mithilfe einer SQL-Variablen übergeben @isbn. Durch Ersetzen der Konstante mit **SQL:Variable()**, die Abfrage kann für die Suche nach jeder ISBN und nicht nur den, dessen ISBN-Nummer 0-7356-1588-2 ist, verwendet werden.  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **SQL:Column()** können auf ähnliche Weise verwendet werden und bietet zusätzliche Vorteile. Indizes für die Spalte können aus Effizienzgründen verwendet werden, was durch den kostenbasierten Abfrageoptimierer entschieden wird. Außerdem kann die berechnete Spalte zum Speichern einer heraufgestuften Eigenschaft verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [xml Data Type Methods (xml-Datentypmethoden)](../../t-sql/xml/xml-data-type-methods.md)  
  
  
