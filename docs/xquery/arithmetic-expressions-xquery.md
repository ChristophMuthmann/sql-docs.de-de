---
title: "Arithmetische Ausdrücke (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0736594cec09f9deb31340ab4d4e3c1fa052496b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="arithmetic-expressions-xquery"></a>Arithmetische Ausdrücke (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Alle arithmetische Operatoren werden unterstützt, mit Ausnahme von **Idiv**. Die folgenden Beispiele veranschaulichen die Grundlagen der Verwendung von arithmetischen Operatoren:  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 Da **Idiv** wird nicht unterstützt, eine Lösung besteht darin, mithilfe der **Xs:integer()** Konstruktor:  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 Der aus einem arithmetischen Operator resultierende Datentyp ist vom Datentyp des Eingabewerts abhängig. Wenn die Operanden unterschiedliche Typen aufweisen, wird entweder einer oder gegebenenfalls werden beide Typen entsprechend der Typhierarchie zu einem gemeinsamen Grundtyp umgewandelt. Informationen zur Typhierarchie finden Sie unter [Typumwandlungsregeln in XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 Die numerische Typhöherstufung erfolgt, wenn zwei Operationen verschiedene numerische Basistypen aufweisen. Z. B. Hinzufügen einer **xs: decimal** auf eine **xs: double** ändern würde zuerst den Dezimalwert in einen Double-Wert. Anschließend wird die Addition durchgeführt und das Ergebnis als double-Wert angezeigt.  
  
 Nicht typisierte atomare Werte werden umgewandelt, in der andere Operand numerischen Basistyp oder auf **xs: double** , wenn der andere Operand ebenfalls nicht typisiert ist.  
  
## <a name="implementation-limitations"></a>Implementierungseinschränkungen  
 Die folgenden Einschränkungen sind zu beachten:  
  
-   Argumente für die arithmetischen Operatoren numerischen Typ aufweisen müssen oder **UntypedAtomic**.  
  
-   Vorgänge für **xs: Integer** Werte ergeben einen Wert vom Typ **xs: decimal** anstelle von **xs: Integer**.  
  
  
