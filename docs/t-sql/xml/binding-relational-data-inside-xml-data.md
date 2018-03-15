---
title: Einbinden relationaler Daten in XML-Daten | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87dca9b5bcd70335a6121b1be1e49f4cc352826e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="binding-relational-data-inside-xml-data"></a>Einbinden relationaler Daten in XML-Daten
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Sie können [XML-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md) für eine **XML**-Datentypvariable oder -spalte angeben. So führt die [&#40;Abfragemethode&#41; &#40;XML-Datentyp&#41;](../../t-sql/xml/query-method-xml-data-type.md) beispielsweise die angegebene XQuery für eine XML-Instanz aus. Beim Erstellen von XML-Code auf diese Art sollten Sie einen Wert aus einer Nicht-XML-Typspalte oder eine Transact-SQL-Variable einbringen. Dieser Prozess wird als Einbinden relationaler Daten in XML bezeichnet.  
  
 Um relationale Nicht-XML-Daten in XML zu binden, bietet das SQL Server-Datenbankmodul folgende Pseudofunktionen:  
  
-   Mithilfe von [sql:column&#40;&#41; Function &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-column.md) können Sie die Werte aus einer relationalen Spalte in Ihrem XQuery- oder XML DML-Ausdruck verwenden.  
  
-   [sql:variable&#40;&#41; Function &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-variable.md) . Gibt Ihnen die Möglichkeit, den Wert einer SQL-Variablen im XQuery- oder XML DML-Ausdruck zu verwenden.  
  
 Sie können diese Funktionen jedes Mal mit **XML**-Datentypmethoden verwenden, wenn Sie einen relationalen Wert in XML verfügbar machen möchten.  
  
 Diese Funktionen können nicht für den Verweis auf Daten in Spalten oder Variablen der benutzerdefinierten CLR-Typen des Datentyps **XML** sowie der Typen datetime, smalldatetime, **text**, **ntext**, **sql_variant** und **image** verwendet werden.  
  
 Das Einbinden ist außerdem nur zur Leseberechtigung. Deshalb können Sie in Spalten keine Daten schreiben, die diese Funktion verwenden. Beispielsweise ist sql:variable("@x")="*some expression"* nicht zulässig.  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>Beispiel: Domänenübergreifende Abfrage mithilfe von sql:variable()  
 In diesem Beispiel wird gezeigt, wie eine Anwendung mit **sql:variable()** eine Abfrage parametrisieren kann. Die ISBN wird mit der SQL-Variablen @isbn übergeben. Durch Ersetzen der Konstante durch **sql:variable()** kann die Abfrage für die Suche nach einer beliebigen ISBN verwendet werden, nicht nur für die Suche nach der ISBN 0-7356-1588-2.  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **sql:column()** kann auf ähnliche Weise verwendet werden und bietet weitere Vorteile. Indizes für die Spalte können aus Effizienzgründen verwendet werden, was durch den kostenbasierten Abfrageoptimierer entschieden wird. Außerdem kann die berechnete Spalte zum Speichern einer heraufgestuften Eigenschaft verwendet werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [xml Data Type Methods (xml-Datentypmethoden)](../../t-sql/xml/xml-data-type-methods.md)  
  
  
