---
title: XML-Datenbearbeitungssprache (XML DML) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- modifying data [SQL Server], XML DML
- XML [SQL Server], DML
- XML DML [SQL Server]
- data modification language [XML DML]
- data modifications [XML DML]
- DML [XML in SQL Server]
- XQuery, XML DML
- xml data type [SQL Server], XML DML
ms.assetid: 20ce50d2-c07b-4e41-93a7-1380d2cd49cb
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 74f591801b50df0bacf3c873f73d6cc9ee28f4d8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="xml-data-modification-language-xml-dml"></a>XML DML (Data Modification Language)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML DML (Data Modification Language) ist eine Erweiterung der XQuery-Sprache. Gemäß der Definition durch W3C fehlt der XQuery-Sprache der DML-Anteil (Data Manipulation). XML DML eingeführt, die in diesem Thema und auch die XQuery-Sprache bietet eine voll funktionsfähige Abfrage- und Datenbearbeitungssprache, mit denen Sie anhand der **Xml** -Datentyp.  
  
 XML DML fügt XQuery die folgenden Schlüsselwörter hinzu, für die zwischen Groß- und Kleinschreibung unterschieden wird:  
  
-   **insert**  
  
-   **Löschen**  
  
-   **Ersetzen Sie Wert des**  
  
 Wie in beschrieben [XML-Datentyp und-Spalten &#40; SQLServer &#41; ](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md), Sie können Variablen und Spalten des Erstellen der **Xml** geben und XML-Dokumente oder-Fragmente zuweisen. Gehen Sie folgendermaßen vor, um diese XML-Instanzen zu ändern oder zu aktualisieren:    
  
-   Verwenden Sie die [modify() Methode Xml-Datentyp)](../../t-sql/xml/modify-method-xml-data-type.md) von der **Xml** -Datentyp.  
  
-   Geben Sie die entsprechenden XML DML-Anweisungen innerhalb der **modify()** Methode.  
  
 Beachten Sie, dass einige Attribute nicht eingefügt, gelöscht oder einer Wertänderung unterzogen werden können. Beispiel:  
  
-   Für typisiertes oder nicht typisiertes **Xml** die Attribute sind **Xmlns**, **Xmlns:\***, und **XML: Base**.  
  
-   Für typisiertes **Xml** nur die Attribute sind **xsi: nil**, und **xsi: Type**.  
  
 Außerdem gelten die folgenden Einschränkungen:  
  
-   Für typisiertes oder nicht typisiertes **Xml**, Einfügen des Attributs **XML: Base** schlägt fehl.  
  
-   Für typisiertes **Xml**, löschen und Ändern der **xsi: nil** -Attributs fehl. Für nicht typisiertes **Xml**, können Sie dieses Attribut löschen oder seinen Wert ändern.  
  
-   Für typisiertes **Xml**, Ändern des Werts der **xs: Type** -Attributs fehl. Für nicht typisiertes **Xml**, können Sie diesen Attributwert ändern.  
  
 Wenn Sie eine typisierte XML-Instanz ändern, muss das endgültige Format eine gültige Instanz des betreffenden Typs sein. Anderenfalls wird ein Überprüfungsfehler zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [INSERT &#40; XML DML &#41;](../../t-sql/xml/insert-xml-dml.md)   
 [Delete &#40; XML DML &#41;](../../t-sql/xml/delete-xml-dml.md)   
 [Replace-Wert, der &#40; XML DML &#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml Data Type Methods (xml-Datentypmethoden)](../../t-sql/xml/xml-data-type-methods.md)  
  
  
