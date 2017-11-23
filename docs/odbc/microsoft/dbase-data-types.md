---
title: dBASE-Datentypen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0e2405001dbffc6421cb2f1ed6c7b44a138abca
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="dbase-data-types"></a>dBASE-Datentypen
Die folgende Tabelle zeigt, wie dBASE-Datentypen in ODBC-SQL-Datentypen zugeordnet werden. Beachten Sie, dass nicht alle ODBC-SQL-Datentypen unterstützt werden.  
  
|dBASE-Datentyp|ODBC-Datentyp|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|"FLOAT" [1]|SQL_DOUBLE|  
|LOGISCHE|SQL_BIT|  
|MEMO|SQL_LONGVARCHAR|  
|NUMERISCH (BCD)|SQL_DOUBLE|  
|OLEOBJECT-KLASSE [1]|SQL_LONGBINARY|  
  
 [1] gültig nur für dBASE, Version 5. *x*  
  
 Genauigkeit in dBASE III kann Zahlen mit oben um zweistellige Exponenten und dBASE IV Zahlen mit bis zu drei Ziffern Exponenten. Da Zahlen als Text gespeichert sind, werden sie in Zahlen umgewandelt. Wenn die zu konvertierende Zahl nicht in einem Feld unerklärliche Ergebnissen kommen passt.  
  
 Wenn dBASE, eine Genauigkeit und Dezimalstellen mit einem numerischen Datentyp angegeben werden kann, wird er vom dBASE ODBC-Treiber nicht unterstützt. Der ODBC-Treiber dBASE gibt immer eine Genauigkeit von 15 und einer Skala von 0 für einen numerischen Datentyp zurück.  
  
 Eine Spalte mit dem numerischen Datentyp mit der ODBC-dBASE Treiber ordnet den ODBC SQL_DOUBLE-Datentyp erstellt wird. Daher ist die Daten in dieser Spalte Rundung. Dieses Verhalten entspricht nicht dem, die der numerischen Daten in dBASE (Type-N) Geben Sie die Binary Coded Decimal (BCD) ist.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** gibt ODBC SQL-Datentypen. Alle Konvertierungen in Anhang D der *ODBC Programmer's Reference* werden für die ODBC-SQL-Datentypen, die weiter oben in diesem Thema aufgeführten unterstützt.  
  
 Die folgende Tabelle zeigt Einschränkungen auf dBASE Datentypen.  
  
|Datentyp|Description|  
|---------------|-----------------|  
|CHAR|Erstellen eine CHAR-Spalte 0 (null) oder nicht angegebene Länge gibt tatsächlich eine 254-Byte-Spalte.|  
|Verschlüsselte Daten|DBASE-Treiber unterstützt keine verschlüsselten dBASE-Tabellen.|  
|LOGISCHE|DBASE-Treiber kann nicht für eine logische Spalte einen Index erstellen.|  
|MEMO|Die maximale Länge einer Spalte MEMO ist 65.500 Bytes.|  
  
 Weitere Einschränkungen für Datentypen finden Sie in [Datentyp Einschränkungen](../../odbc/microsoft/data-type-limitations.md).
