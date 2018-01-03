---
title: Deklarieren die Anwendung &#39; s ODBC-Version | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c021fb123e0a8cf861fa91fe78d3882ba16111e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="declaring-the-application39s-odbc-version"></a>Deklarieren die Anwendung &#39; s ODBC-Version
Bevor eine Verbindung mit eine Anwendung belegt wird, müssen sie die SQL_ATTR_ODBC_VERSION Umgebung-Attribut festgelegt. Dieses Attribut gibt an, dass die Anwendung die ODBC 2. folgt. *x* oder ODBC-3. *X* Spezifikation bei Verwendung der folgenden Elemente:  
  
-   **SQLSTATEs**. Viele SQLSTATE-Werten unterscheiden sich in ODBC 2. *x* und ODBC-3. *X*.  
  
-   **Date, Time und Timestamp-Typ-IDs**. Die folgende Tabelle zeigt die Typ-IDs für Date, Time und Timestamp-Datentyp in ODBC 2. *x* und ODBC-3. *X*.  
  
    |ODBC-2. *x*|ODBC-3. *x*|  
    |----------------|----------------|  
    |**SQL-Typenbezeichner**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C-Typ-IDs**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   *Katalogname***Argument SQLTables**. In ODBC 2. *x*, die Platzhalterzeichen ("%" und "_") in der *CatalogName* Argument als solcher behandelt werden. In ODBC 3. *x*, werden sie als Platzhalterzeichen behandelt. Daher eine Anwendung, die die ODBC 2. folgt. *x* Spezifikation kann diese nicht als verwenden Zeichen und ist nicht mit Escapezeichen versehen werden als Literale Verwendung. Eine Anwendung, die die ODBC 3. folgt. *x* Spezifikation kann diese als Platzhalterzeichen verwenden oder mit Escapezeichen versehen und als Literale verwenden können. Weitere Informationen finden Sie unter [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 Die ODBC 3.*.x* Treiber-Manager und ODBC 3.*.x* Treiber prüfen die Version des ODBC-Spezifikation, die in den eine Anwendung geschrieben wird, und entsprechend reagieren. Beispielsweise, wenn die Anwendung die ODBC 2. beachtet. *x* -Spezifikation und ruft **SQLExecute** vor dem Aufruf **SQLPrepare**, die ODBC 3.*.x* -Treiber-Manager gibt SQLSTATE S1010 () Fehler bei Funktionssequenz). Wenn die Anwendung die ODBC 3. folgt*.x* -Spezifikation, die der Treiber-Manager gibt SQLSTATE HY010 (Sequenzfehler-Funktion). Weitere Informationen finden Sie unter [Abwärtskompatibilität und zur Einhaltung von Standards](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Anwendungen, die die ODBC 3. befolgen. *x* Spezifikation muss bedingten Code verwenden, um zu vermeiden, mithilfe von Funktionen noch nicht mit ODBC 3. *X* beim Arbeiten mit ODBC 2. *X* Treiber. ODBC-2. *x* Treiber unterstützen keine Funktionen, die noch nicht mit ODBC 3. *X* nur verwendet werden, weil die Anwendung wird deklariert, dass er die ODBC 3. folgt. *X* Spezifikation. Darüber hinaus ODBC 3. *x* Treiber zur Unterstützung von Funktionen, die noch nicht mit ODBC 3. nicht eingestellt werden. *X* nur verwendet werden, weil die Anwendung wird deklariert, dass er die ODBC 2. folgt. *X* Spezifikation.
