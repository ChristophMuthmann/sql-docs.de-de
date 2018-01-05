---
title: NULL und UNKNOWN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
caps.latest.revision: "5"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6a581045af3d5ed73e9cf9736c60588d87733369
ms.sourcegitcommit: 7673ad0e84a6de69420e19247a59e39ca751a8aa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2018
---
# <a name="null-and-unknown-transact-sql"></a>NULL und UNKNOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL gibt an, dass der Wert unbekannt ist. Ein null-Wert unterscheidet sich von einem leeren Wert oder NULL-Wert. NULL-Werte sind niemals identisch. Vergleiche zwischen zwei null-Werte, oder ein null-Wert und ein anderer Wert zurückgeben unbekannt, da der Wert jedes NULL unbekannt ist.  
  
 NULL-Werte in der Regel Daten hin, die ist unbekannt oder nicht zutreffend, oder zu einem späteren Zeitpunkt hinzugefügt werden. Beispielsweise ist es möglich, dass der Anfangsbuchstabe des zweiten Vornamens eines Kunden noch nicht bekannt ist, wenn der Kunde eine Bestellung aufgibt.  
  
 Beachten Sie Folgendes im Zusammenhang mit null-Werte aus:  
  
-   Um das Vorhandensein von NULL-Werten in einer Abfrage zu testen, verwenden Sie IS NULL oder IS NOT NULL in der WHERE-Klausel.  
  
-   NULL-Werte können in eine Spalte eingefügt werden, indem NULL explizit in einer INSERT- oder UPDATE-Anweisung, oder indem Sie eine Spalte aus einer INSERT-Anweisung zu verlassen.  
  
-   NULL-Werte können nicht als Informationen verwendet werden, die erforderlich sind, um eine Zeile in einer Tabelle von einer anderen Zeile in einer Tabelle, z. B. Primärschlüssel, oder Informationen, die zum Verteilen von Zeilen, z. B. Verteilung Schlüssel verwendet zu unterscheiden.  
  
 Sind NULL-Werte in den Daten vorhanden, ist es möglich, dass logische Operatoren und Vergleichsoperatoren nicht nur TRUE oder FALSE zurückgeben, sondern ein drittes Ergebnis: UNKNOWN. Diese Notwendigkeit einer dreiwertigen Logik ist die Ursache für zahlreiche Anwendungsfehler. Logische Operatoren in einem booleschen Ausdruck, der unbekannte enthält werden UNKNOWN zurückgegeben, es sei denn, das Ergebnis des Operators, nicht auf dem unbekannten Ausdruck abhängt. Diese Tabellen enthalten Beispiele für dieses Verhalten.  
  
 Die folgende Tabelle zeigt die Ergebnisse des Anwendens eines AND-Operators auf zwei boolesche Ausdrücke, in denen ein Ausdruck UNKNOWN zurückgibt.  
  
|Ausdruck 1|Ausdruck 2|Ergebnis|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|UNKNOWN|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|FALSE|  
  
 Die folgende Tabelle zeigt die Ergebnisse des Anwendens eines OR-Operators auf zwei boolesche Ausdrücke, in denen ein Ausdruck UNKNOWN zurückgibt.  
  
|Ausdruck 1|Ausdruck 2|Ergebnis|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|TRUE|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|UNKNOWN|  
  
## <a name="see-also"></a>Siehe auch  
 [UND &#40; Transact-SQL &#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [ODER &#40; Transact-SQL &#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [NICHT &#40; Transact-SQL &#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [IST NULL &#40; Transact-SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
