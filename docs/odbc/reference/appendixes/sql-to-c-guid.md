---
title: SQL in "c:" GUID | Microsoft Docs
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
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a33d7e2ada5aa13bbd2bf42f85a9aa7e4bbdc44b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sql-to-c-guid"></a>SQL in "c:" GUID
Der Bezeichner für die GUID ODBC SQL-Datentyp ist:  
  
 SQL_GUID  
  
 In der folgenden Tabelle wird gezeigt, auf den ODBC C-Datentypen, die in die GUID-SQL-Daten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Pufferlänge* > Byte Zeichenlänge|data|36|–|  
||*Pufferlänge* < 37|Nicht definiert|Nicht definiert|22003|  
|SQL_C_WCHAR|*Pufferlänge* > Zeichenlänge|data|36|–|  
||*Pufferlänge* < 37|Nicht definiert|Nicht definiert|22003|  
|SQL_C_BINARY|Die Bytelänge der Daten \< =  *Pufferlänge*|data|Länge der Daten in bytes|–|  
||Die Bytelänge der Daten > *Pufferlänge*|Nicht definiert|Nicht definiert|22003|  
|SQL_C_GUID|Keine [a]|data|16 [b]|–|  
  
 [a] der Wert der *Pufferlänge* für diese Konvertierung ignoriert wird. Der Treiber setzt voraus, dass die Größe der **TargetValuePtr* ist die Größe der C-Datentyp.  
  
 [b] Dies ist die Größe des entsprechenden C-Datentyp.
