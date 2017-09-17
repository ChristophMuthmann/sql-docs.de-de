---
title: "Löschen - SQL-Befehl | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8effde0f80a219f11af460bdc941a9b6d9681455
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
 WOBEI *FilterCondition1*[AND &#124; ODER *FilterCondition2*...]  
 Gibt an, dass Visual FoxPro nur bestimmte Einträge zum Löschen markiert.  
  
 *FilterCondition* gibt die Kriterien, die Datensätze erfüllen muss, um zum Löschen markiert war. Sie können so viele Bedingungen filtern, wie Sie möchten das Verbinden mit den AND-Operator, einschließen oder OR-Operator. Sie können auch den NOT-Operator verwenden, um den Wert eines logischen Ausdrucks umzukehren, oder Sie können **leere**(), um ein leeres Feld überprüfen.  
  
## <a name="remarks"></a>Hinweise  
 Wenn SET DELETED auf ON festgelegt ist, werden zum Löschen markierte Einträge durch alle Befehle, die einen Bereich enthalten, ignoriert.  
  
 Löschen Sie: SQL Verwendungen des Öffnens datensatzsperrung, wenn mehrere Datensätze in Tabellen zum Löschen markieren für gemeinsamen Zugriff. Dies verringert Datensatz Konflikte in Mehrbenutzer Situationen jedoch kann die Leistung reduzieren. Öffnen Sie die Tabelle für die ausschließliche Verwendung, um eine optimale Leistung.  
  
## <a name="driver-remarks"></a>Treiber "Hinweise".  
 Wenn Ihre Anwendung die ODBC-SQL-Anweisung DELETE an die Datenquelle gesendet wird, konvertiert der Visual FoxPro-ODBC-Treiber den Befehl in der Visual FoxPro-löschen-Befehl ohne Übersetzung an.  
  
## <a name="see-also"></a>Siehe auch  
 [SET DELETED-Befehl](../../odbc/microsoft/set-deleted-command.md)
