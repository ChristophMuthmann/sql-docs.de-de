---
title: Rolle des Treibers "" | Microsoft Docs
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
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2fe0d0545bcc787275bda3ba2154088f23eeda20
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="role-of-the-driver"></a>Rolle des Treibers ""
Der Treiber überprüft, ob alle Fehler und Warnungen, die vom Treiber-Manager nicht überprüft und orders Statusdatensätze, die sie generiert. (Eine ODBC-2. *x* Treiber sortiert Statusdatensätze nicht.) Dies schließt Fehler und Warnungen in das Abschneiden von Daten, die Datenkonvertierung, Syntax und einige Statusübergänge. Der Treiber kann auch Fehler und Warnungen, die nur teilweise aktiviert der Treiber-Manager überprüfen. Beispielsweise zwar der Treiber-Manager überprüft, ob der Wert der *Vorgang* in **SQLSetPos** ist zulässig ist, wird der Treiber muss überprüfen, ob es unterstützt wird.  
  
 Der Treiber ordnet auch *systemeigene Fehler* – d. h. von der Datenquelle zurückgegebenen Fehler – um SQLSTATEs. Beispielsweise könnte der Treiber eine Anzahl von unterschiedlichen systemeigene Fehler für ungültige SQL-Syntax SQLSTATE 42000 (Syntaxfehler oder zugriffsverletzung) zugeordnet. Der Treiber gibt die systemeigene Fehlernummer in der SQL_DIAG_NATIVE-Feld des Datensatzes Status zurück. Treiber-Dokumentation sollte anzeigen, wie Fehler und Warnungen aus der Datenquelle, in Argumente zugeordnet werden **SQLGetDiagRec** und **SQLGetDiagField**.

