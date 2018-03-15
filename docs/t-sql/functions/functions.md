---
title: Was sind Microsoft SQL-Datenbank-Funktionen? | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- built-in functions [SQL Server]
- function [SQL Server] See functions [SQL Server]
- functions [Transact-SQL]
- functions [SQL Server], about functions
- scalar functions
- functions [SQL Server]
ms.assetid: 17186213-5ab5-40b0-b470-b660af1ec44c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: fa55a0b066db617ef0d6f2f0471ad6866cac2d73
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="what-are-the-sql-database-functions"></a>Was sind SQL-Datenbankfunktionen?
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

Informationen zu den Kategorien von integrierten Funktionen, die Sie mit SQL-Datenbanken verwenden können. Sie können die integrierten Funktionen verwenden oder Ihre eigenen benutzerdefinierten Funktionen erstellen.
  
## <a name="aggregate-functions"></a>Aggregatfunktionen

Aggregatfunktionen führen Berechnungen für eine Wertemenge durch und geben einen einzelnen Wert zurück. Sie sind in der SELECT-Auswahlliste oder der HAVING-Klausel einer SELECT-Anweisung zulässig. Sie können eine Aggregation in Kombination mit der GROUP BY-Klausel verwenden, um die Aggregation auf Kategorien von Zeilen zu berechnen. Verwenden Sie die OVER-Klausel, um die Aggregation auf einen bestimmten Wertebereich zu berechnen. Die OVER-Klausel darf nicht den Aggregationen GROUPING und GROUPING_ID folgen.

Alle Aggregatfunktionen sind deterministisch, d.h. sie geben immer denselben Wert zurück, wenn sie mit den gleichen Eingabewerten ausgeführt werden. Weitere Informationen finden Sie unter [Deterministische und nicht deterministische Funktionen](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).

## <a name="analytic-functions"></a>Analytische Funktionen
Analytische Funktionen berechnen auf Grundlage einer Gruppe von Zeilen einen Aggregatwert. Sie können jedoch im Gegensatz zu Aggregatfunktionen mehrere Zeilen für jede Gruppe zurückgeben. Sie können analytische Funktionen verwenden, um gleitende Durchschnitte, laufende Summen, Prozentsätze oder die ersten N-Ergebnisse innerhalb einer Gruppe zu berechnen.

## <a name="ranking-functions"></a>Rangfolgefunktionen
Rangfolgefunktionen geben für jede Partitionszeile einen Rangfolgenwert zurück. Je nach verwendeter Funktion empfangen einige Zeilen möglicherweise dieselben Werte wie andere Zeilen. Rangfolgefunktionen sind nicht deterministisch.

## <a name="rowset-functions"></a>Rowsetfunktionen
Rowsetfunktionen geben ein Objekt zurück, das wie Tabellenverweise in einer SQL-Anweisung verwendet werden kann.

## <a name="scalar-functions"></a>Skalare Funktionen
Verarbeiten einen einzelnen Wert und geben einen einzelnen Wert zurück. Skalare Funktionen können überall dort verwendet werden, wo ein Ausdruck zulässig ist.

### <a name="categories-of-scalar-functions"></a>Kategorien von skalaren Funktionen
  
|Funktionskategorie|Description|  
|-----------------------|-----------------|  
|[Konfigurationsfunktionen](configuration-functions-transact-sql.md)|Geben Informationen zur aktuellen Konfiguration zurück.|  
|[Konvertierungsfunktionen](conversion-functions-transact-sql.md)|Unterstützen die Umwandlung und Konvertierung von Datentypen.|  
|[Cursorfunktionen](cursor-functions-transact-sql.md)|Geben Informationen zu Cursorn zurück.|  
|[Datums- und Uhrzeitdatentypen und Funktionen](date-and-time-data-types-and-functions-transact-sql.md)|Führen Operationen für Datums- und Zeiteingabewerte aus und geben eine Zeichenfolge, einen Zahlen-, Datums- oder Zeitwert zurück.|  
|[JSON-Funktionen](json-functions-transact-sql.md)|Überprüfen, Abfragen oder Ändern von JSON-Daten|  
|[Logische Funktionen](http://msdn.microsoft.com/library/5b2b4546-951b-462d-91d5-e41fc5acd6f9)|Führen logische Operationen aus.|  
|[Mathematische Funktionen](mathematical-functions-transact-sql.md)|Führen Berechnungen auf der Grundlage von Eingabewerten aus, die als Parameter für die Funktionen bereitgestellt werden, und geben einen numerischen Wert zurück.|  
|[Metadatenfunktionen](metadata-functions-transact-sql.md)|Geben Informationen zur Datenbank und zu Datenbankobjekten zurück.|  
|[Sicherheitsfunktionen](security-functions-transact-sql.md)|Diese Funktionen geben Informationen über Benutzer und Rollen zurück.|  
|[Zeichenfolgenfunktionen](string-functions-transact-sql.md)|Führen Operationen für den Eingabewert einer Zeichenfolge (**char** oder **varchar**) aus und geben eine Zeichenfolge oder einen numerischen Wert zurück.|  
|[Systemfunktionen](../../relational-databases/system-functions/system-functions-for-transact-sql.md)|Führen Operationen bezüglich Werten, Objekten und Einstellungen in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus und geben Informationen zu diesen zurück.|  
|[Statistische Systemfunktionen](system-statistical-functions-transact-sql.md)|Geben statistische Informationen zum System zurück.|  
|[Text- und Imagefunktionen](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|Führen Operationen zu Text- bzw. Image-Eingabewerten oder -Spalten aus und geben Informationen zu diesen Werten zurück.|  
  
## <a name="function-determinism"></a>Funktionsdeterminismus  
 Eine integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktion ist entweder deterministisch oder nicht deterministisch. Funktionen sind deterministisch, wenn sie bei jedem Aufrufen mit bestimmten Eingabewerten immer das gleiche Ergebnis zurückgeben. Funktionen sind nicht deterministisch, wenn sie bei jedem Aufrufen selbst mit denselben bestimmten Eingabewerten verschiedene Ergebnisse zurückgeben können. Weitere Informationen finden Sie unter [Deterministische und nicht deterministische Funktionen](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="function-collation"></a>Funktionssortierung  
 Funktionen, die als Eingabe eine Zeichenfolge erhalten und als Ausgabe eine Zeichenfolge zurückgeben, verwenden für die Ausgabe die Sortierung der Eingabezeichenfolge.  
  
 Funktionen, die als Eingabe einen Wert erhalten, der keine Zeichenfolge ist, und als Ausgabe eine Zeichenfolge zurückgeben, verwenden für die Ausgabe die Standardsortierung der aktuellen Datenbank.  
  
 Funktionen, die als Eingabe mehrere Zeichenfolgen erhalten und als Ausgabe eine Zeichenfolge zurückgeben, verwenden die Regeln zur Sortierungspriorität, um die Sortierung der Ausgabezeichenfolge festzulegen. Weitere Informationen finden Sie unter [Rangfolge von Sortierungen &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [Deterministische und nicht deterministische Funktionen](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)   
 [Verwenden von gespeicherten Prozeduren &#40;MDX&#41;](../../mdx/using-stored-procedures-mdx.md)  
  
  
