---
title: Löschen - SQL-Befehl | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e00f1d819f792f88ffb4495385be5abd754af21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="delete---sql-command"></a>Löschen - SQL-Befehl
Datensätze zum Löschen markiert.  
  
 Der Visual FoxPro-ODBC-Treiber unterstützt die systemeigene Visual FoxPro-Sprachsyntax für diesen Befehl an. Treiberspezifische Informationen finden Sie unter den Hinweisen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Argumente  
 AUS [ *DatabaseName!*] *TableName*  
 Gibt die Tabelle, in der Datensätze zum Löschen markiert sind.  
  
 *DatabaseName!* Gibt den Namen einer Datenbank, die die Tabelle enthält, wenn die enthaltene Datenbank nicht die Datenbank mit der Datenquelle angegeben ist. Sie müssen den Namen einer Datenbank einschließen, die die Tabelle enthält, wenn die Datenbank nicht die Datenbank mit der Datenquelle angegeben ist. Schließen Sie das Ausrufezeichen (!)-Trennzeichen an, nach dem Datenbanknamen und vor dem Tabellennamen.  
  
 WOBEI *FilterCondition1*[AND &#124; oder *FilterCondition2*...]  
 Gibt an, dass Visual FoxPro nur bestimmte Einträge zum Löschen markiert.  
  
 *FilterCondition* gibt die Kriterien, die Datensätze erfüllen muss, um zum Löschen markiert war. Sie können so viele Bedingungen filtern, wie Sie möchten das Verbinden mit den AND-Operator, einschließen oder OR-Operator. Sie können auch den NOT-Operator verwenden, um den Wert eines logischen Ausdrucks umzukehren, oder Sie können **leere**(), um ein leeres Feld überprüfen.  
  
## <a name="remarks"></a>Hinweise  
 Wenn SET DELETED auf ON festgelegt ist, werden zum Löschen markierte Einträge durch alle Befehle, die einen Bereich enthalten, ignoriert.  
  
 Löschen Sie: SQL Verwendungen des Öffnens datensatzsperrung, wenn mehrere Datensätze in Tabellen zum Löschen markieren für gemeinsamen Zugriff. Dies verringert Datensatz Konflikte in Mehrbenutzer Situationen jedoch kann die Leistung reduzieren. Öffnen Sie die Tabelle für die ausschließliche Verwendung, um eine optimale Leistung.  
  
## <a name="driver-remarks"></a>Treiber "Hinweise".  
 Wenn Ihre Anwendung die ODBC-SQL-Anweisung DELETE an die Datenquelle gesendet wird, konvertiert der Visual FoxPro-ODBC-Treiber den Befehl in der Visual FoxPro-löschen-Befehl ohne Übersetzung an.  
  
## <a name="see-also"></a>Siehe auch  
 [Befehl SET DELETED](../../odbc/microsoft/set-deleted-command.md)
