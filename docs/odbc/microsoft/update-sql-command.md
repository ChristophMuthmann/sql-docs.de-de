---
title: UPDATE - SQL-Befehl | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d25d4c07f0949598048ab12905d6176c4a2b397
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="update---sql-command"></a>UPDATE - SQL-Befehl
Datensätze in einer Tabelle mit neuen Werten aktualisiert.  
  
 Der Visual FoxPro-ODBC-Treiber unterstützt die systemeigene Visual FoxPro-Sprachsyntax für diesen Befehl an. Treiberspezifische Informationen finden Sie unter **Treiber "Hinweise"**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>Argumente  
 UPDATE [ *DatabaseName1!*] *TableName1*  
 Gibt die Tabelle, in der Datensätze mit neuen Werten aktualisiert werden.  
  
 *DatabaseName1!* Gibt den Namen einer Datenbank als der Datenbank mit der Datenquelle, die die Tabelle angegeben. Sie umfasst den Namen der Datenbank mit der Tabelle aus, wenn die Datenbank nicht mit dem aktuellen Objekt ist. Schließen Sie das Ausrufezeichen (!)-Trennzeichen an, nach dem Datenbanknamen und vor dem Tabellennamen.  
  
 Legen Sie *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Gibt die Spalten, die aktualisiert werden und die neuen Werte. Wenn Sie die WHERE-Klausel weglassen, wird jede Zeile in der Spalte mit den gleichen Wert aktualisiert.  
  
 WOBEI *FilterCondition1*[AND &#124; oder *FilterCondition2*...]  
 Gibt an, die Datensätze, die mit neuen Werten aktualisiert werden.  
  
 *FilterCondition* gibt die Kriterien, die Datensätze erfüllen muss, um mit neuen Werten aktualisiert werden. Sie können so viele Bedingungen filtern, wie Sie mit den AND-Operator verbindenden einschließen oder OR-Operator. Sie können auch den NOT-Operator verwenden, um den Wert eines logischen Ausdrucks umzukehren, oder Sie können **leere**(), um ein leeres Feld überprüfen.  
  
## <a name="remarks"></a>Hinweise  
 UPDATE - SQL kann nur die Datensätze in einer einzelnen Tabelle aktualisieren.  
  
 Im Gegensatz zu ersetzen verwendet die UPDATE - SQL Datensatz zu sperren, wenn mehrere Datensätze in Tabellen aktualisiert werden, für den gemeinsamen Zugriff geöffnet. Dies verringert Datensatz Konflikte in Mehrbenutzer Situationen jedoch kann die Leistung verringern. Öffnen Sie die Tabelle, um eine optimale Leistung für exklusive verwenden oder **Bestand**(), um die Tabelle zu sperren.  
  
## <a name="driver-remarks"></a>Treiber "Hinweise".  
 Wenn Ihre Anwendung die ODBC-SQL-Anweisung UPDATE an die Datenquelle gesendet wird, konvertiert der Visual FoxPro-ODBC-Treiber den Befehl in den Visual FoxProUPDATE-Befehl ohne Übersetzung an.  
  
## <a name="see-also"></a>Siehe auch  
 [Löschen - SQL-Befehl](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT (SQL-Befehl)](../../odbc/microsoft/insert-sql-command.md)
