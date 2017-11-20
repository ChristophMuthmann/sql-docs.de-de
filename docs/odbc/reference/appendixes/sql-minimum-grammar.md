---
title: Minimale SQL-Grammatik | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c225ab76f4c67938590bd19f21bfafafa20742d8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sql-minimum-grammar"></a>Minimale SQL-Grammatik
Dieser Abschnitt beschreibt die minimale SQL-Syntax, die ein ODBC-Treiber unterstützen muss. Die in diesem Abschnitt erläuterten Syntax ist eine Teilmenge der Eintrag Ebene Syntax der SQL-92.  
  
 Eine Anwendung keines der Syntax in diesem Abschnitt verwenden kann und sicher sein, dass alle ODBC-kompatiblen Treiber, dass die Syntax unterstützt wird. Um zu bestimmen, ob zusätzliche Funktionen von SQL-92 in diesem Abschnitt nicht unterstützt werden, sollte die Anwendung aufrufen **SQLGetInfo** mit dem Typ der SQL_SQL_CONFORMANCE-Informationen. Auch wenn der Treiber keine SQL-92-Konformitätsgrad entspricht, kann eine Anwendung weiterhin die in diesem Abschnitt erläuterten Syntax verwenden. Wenn ein Treiber eine SQL-92-Ebene entspricht, andererseits, unterstützt es gesamte Syntax, die in dieser Ebene enthalten. Dies schließt die Syntax in diesem Abschnitt aus, da die hier beschriebene minimalen Grammatik reinen Teil der niedrigsten Ebene der SQL-92-Konformität ist. Sobald die Anwendung die SQL-92-Ebene unterstützt erkennt, können sie bestimmen, ob eine Funktion auf höherer Ebene (sofern vorhanden) durch den Aufruf unterstützt wird **SQLGetInfo** mit den einzelnen Informationstyp, der auf diese Funktion entspricht.  
  
 Treiber, die funktionieren nur mit schreibgeschützten Datenquellen unterstützen möglicherweise nicht die Teile der Grammatik in diesem Abschnitt enthalten, das Ändern von Daten behandeln. Eine Anwendung kann bestimmen, ob eine Datenquelle durch den Aufruf ohne Schreibzugriff ist **SQLGetInfo** mit dem Typ der SQL_DATA_SOURCE_READ_ONLY-Informationen.  
  
## <a name="statement"></a>-Anweisung.  
 *Anweisung CREATE Table* :: =  
  
 CREATE TABLE *Base Tabellenname*  
  
 (*Spaltenbezeichner Datentyp* [*, Spaltenbezeichner Datentyp*]...)  
  
> [!IMPORTANT]  
>  Als eine *Datentyp* in einer *-Anweisung create Table*, Anwendungen müssen einen Datentyp aus der TYPE_NAME-Spalte des Resultsets zurückgegebenes verwenden **SQLGetTypeInfo**.  
  
 *DELETE-Anweisung durchsucht* :: =  
  
 DELETE FROM *Tabellenname* [, in denen *Suchbedingung*]  
  
 *Drop-Table-Anweisung* :: =  
  
 DROP TABLE *Base Tabellenname*  
  
 *INSERT-Anweisung* :: =  
  
 INSERT INTO *Tabellenname* [( *Spaltenbezeichner* [, *Spaltenbezeichner*]...)]      Werte (*Wert einfügen*[, *Wert einfügen*]...)  
  
 *SELECT-Anweisung* :: =  
  
 Wählen Sie [alle &#124; DISTINCT] *Select-Liste*  
  
 AUS *Tabelle Verweisliste*  
  
 [, In denen *Suchbedingung*]  
  
 [*Order by-Klausel*]  
  
 *Anweisung* :: = *-Anweisung create Table*  
  
 &#124; *Delete-Anweisung durchsucht*  
  
 &#124; *Drop-Table-Anweisung*  
  
 &#124; *Insert-Anweisung*  
  
 &#124; *Select-Anweisung*  
  
 &#124; *Update-Anweisung durchsucht*  
  
 *Update-Anweisung durchsucht*  
  
 UPDATE *Tabellenname*  
  
 Legen Sie *Spaltenbezeichner* = {*Ausdruck* &#124; NULL}  
  
 [, *Spaltenbezeichner* = {*Ausdruck* &#124; NULL}]...  
  
 [, In denen *Suchbedingung*]  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Elemente, die in SQL­Anweisungen verwendet werden](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Datentypunterstützung](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Parameterdatentypen](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Parametermarkierungen](../../../odbc/reference/appendixes/parameter-markers.md)

