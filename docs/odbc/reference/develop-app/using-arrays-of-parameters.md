---
title: Verwenden von Arrays von Parametern | Microsoft Docs
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
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a7c6a6ee4f066925d2a7ec46a2186134d75cb7e4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-arrays-of-parameters"></a>Verwenden von Arrays von Parametern
Verwenden von Arrays von Parametern, die Anwendung ruft **SQLSetStmtAttr** mit einer *Attribut* Argument SQL_ATTR_PARAMSET_SIZE auf die Anzahl von Parametersätzen angeben. Ruft **SQLSetStmtAttr** mit einem *Attribut* Argument SQL_ATTR_PARAMS_PROCESSED_PTR zum Angeben der Adresse einer Variablen, in dem der Treiber kann die Anzahl von Parametersätzen verarbeitet, zurückgeben, Legt fest, einschließlich Fehler. Sie ruft **SQLSetStmtAttr** mit einer *Attribut* Argument des SQL_ATTR_PARAM_STATUS_PTR, zeigen Sie auf ein Array, in dem Statusinformationen für jede Zeile von Parameterwerten zurückgegeben. Der Treiber speichert diese Adressen in der Struktur, die es für die Anweisung enthält.  
  
> [!NOTE]  
>  In ODBC 2. *x*, **SQLParamOptions** wurde aufgerufen, um mehrere Werte für einen Parameter angeben. In ODBC 3. *x*, den Aufruf von **SQLParamOptions** wurde ersetzt durch Aufrufe von **SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE und SQL_ATTR_PARAMS_PROCESSED_ARRAY-Attribute festlegen .  
  
 Vor der Ausführung der Anweisung an, legt die Anwendung den Wert jedes Elements des jedes gebundene Array. Wenn die Anweisung ausgeführt wird, verwendet der Treiber die Informationen, die sie gespeichert, um die Parameterwerte abgerufen und an die Datenquelle senden; der Treiber sollte nach Möglichkeit, diese Werte als Arrays senden. Obwohl die Verwendung von Arrays von Parametern am besten durch Ausführen der SQL-Anweisung mit allen Parametern im Array mit einem einzigen Aufruf an die Datenquelle implementiert ist, steht diese Funktion nicht weit in DBMS heute. Allerdings können Treiber Simulation erzielt werden durch das Ausführen einer SQL-Anweisung mehrere Male mit einem einzelnen Satz von Parametern.  
  
 Damit eine Anwendung Arrays von Parametern verwendet, müssen Sie sicher, dass darauf, dass sie durch die von der Anwendung verwendeten Treiber unterstützt werden. Hierfür gibt es zwei Möglichkeiten:  
  
-   Verwenden Sie nur die Treiber zur Unterstützung von Arrays von Parametern bezeichnet. Die Anwendung hartcodieren können die Namen dieser Treiber oder der Benutzer kann angewiesen werden, um nur diese Treiber verwenden. Benutzerdefinierte Anwendungen und vertikale Anwendungen verwenden im Allgemeinen eine begrenzte Anzahl von Treibern.  
  
-   Überprüfen Sie zur Laufzeit für die Unterstützung von Arrays von Parametern. Ein Treiber unterstützt Arrays mit Parameter an, wenn es möglich ist, verweist SQL_ATTR_PARAMSET_SIZE-Anweisungsattribut auf einen Wert größer als 1 festgelegt. Generische und vertikale Anwendungen überprüfen Sie häufig für die Unterstützung von Arrays von Parametern zur Laufzeit.  
  
 Die Verfügbarkeit der Zeilenanzahl und Resultsets, parametrisierten Ausführung kann bestimmt werden, durch den Aufruf **SQLGetInfo** mit den Optionen SQL_PARAM_ARRAY_ROW_COUNTS und SQL_PARAM_ARRAY_SELECTS. Für **einfügen**, **UPDATE**, und **löschen** -Anweisungen, die Option SQL_PARAM_ARRAY_ROW_COUNTS angibt, ob einzelne Zeilenanzahl (eine für jeden Parametersatz) verfügbar (SQL_PARC_BATCH) oder gibt an, ob Zeilenanzahl in einem (SQL_PARC_NO_BATCH) Rollup enthalten sind. Für **wählen** -Anweisungen, die SQL_PARAM_ARRAY_SELECTS-Option gibt an, ob ein Resultset für jeden Satz von Parametern (SQL_PAS_BATCH) verfügbar ist, oder ob nur ein Resultset verfügbar (SQL_PAS_NO_BATCH) ist. Wenn der Treiber Ergebnis Satz – Generieren von Anweisungen mit einem Array von Parametern ausgeführt werden nicht zulässig ist, gibt SQL_PARAM_ARRAY_SELECTS SQL_PAS_NO_SELECT zurück. Es handelt es sich um Daten datenquellenspezifischen, ob Arrays von Parametern mit anderen Typen von Anweisungen verwendet werden können, insbesondere, da die Verwendung von Parametern in diesen Anweisungen Daten datenquellenspezifischen gib und würde nicht die ODBC-SQL-Grammatik.  
  
 Das Array verweist das Anweisungsattribut SQL_ATTR_PARAM_OPERATION_PTR kann zum Ignorieren von Zeilen der Parameter verwendet werden. Wenn ein Element des Arrays auf SQL_PARAM_IGNORE festgelegt ist, wird der Satz an Parametern, die diesem Element ausgeschlossen der **SQLExecute** oder **SQLExecDirect** aufrufen. Das Array verweist das Attribut SQL_ATTR_PARAM_OPERATION_PTR Zuweisung und von der Anwendung ausgefüllt und vom Treiber lesen. Wenn abgerufene Zeilen als Eingabeparameter verwendet werden, können die Werte der zeilenstatusarray im Parameterarray Vorgang verwendet werden.  
  
## <a name="error-processing"></a>Fehlerverarbeitung  
 Wenn ein Fehler auftritt, während der Ausführung der Anweisung, wird die Ausführungsfunktion gibt einen Fehler zurück und wird die Zeile Nummer-Variable auf die Nummer der Zeile, die den Fehler enthält. Es handelt es sich um Daten datenquellenspezifischen, ob alle Zeilen außer der festgelegten Fehler ausgeführt wird oder, ob alle Zeilen (jedoch nicht nach) vor dem festgelegten Fehler ausgeführt werden. Da es von Parametersätzen verarbeitet wird, legt der Treiber den Puffer, der durch das SQL_ATTR_PARAMS_PROCESSED_PTR-Anweisungsattribut auf die Anzahl der derzeit verarbeitete Zeile angegeben. Wenn alle festlegt, außer dem festgelegten Fehler ausgeführt werden, legt der Treiber dieser Puffer, verweist SQL_ATTR_PARAMSET_SIZE, nachdem alle Zeilen verarbeitet wurden.  
  
 Wenn das SQL_ATTR_PARAM_STATUS_PTR-Anweisungsattribut festgelegt wurde, **SQLExecute** oder **SQLExecDirect** gibt die *Status Parameterarray* stellt den Status Jeder Satz von Parametern. Das Parameterarray-Status wird von der Anwendung belegt und vom Treiber ausgefüllt. Seine Elemente anzugeben, ob die SQL-Anweisung für die Zeile von Parametern erfolgreich ausgeführt wurde, oder gibt an, ob ein Fehler bei der Verarbeitung des Satz an Parametern. Wenn ein Fehler aufgetreten ist, wird der Treiber legt den entsprechenden Wert im Parameters Statusarray SQL_PARAM_ERROR und gibt SQL_SUCCESS_WITH_INFO zurück. Die Anwendung kann überprüfen, die Statusarray, um zu bestimmen, welche Zeilen verarbeitet wurden. Verwenden die Nummer der Zeile, die Anwendung kann häufig korrigieren Sie den Fehler und die Verarbeitung fort.  
  
 Verwendungsweise der Status Parameterarray richtet sich nach der SQL_PARAM_ARRAY_ROW_COUNTS und SQL_PARAM_ARRAY_SELECTS-Optionen, die durch einen Aufruf zurückgegeben **SQLGetInfo**. Für **einfügen**, **UPDATE**, und **löschen** Anweisungen, die das Parameterarray-Status wird mit Informationen zum Status der ausgefüllt, wenn SQL_PARC_BATCH für SQL_PARAM_ARRAY_ zurückgegeben wird ROW_COUNTS, jedoch nicht, wenn SQL_PARC_NO_BATCH zurückgegeben wird. Für **wählen** -Anweisungen das Parameterarray-Status wird ausgefüllt, wenn SQL_PAS_BATCH für SQL_PARAM_ARRAY_SELECT zurückgegeben wird, aber keine SQL_PAS_NO_BATCH oder SQL_PAS_NO_SELECT zurückgegeben wird.  
  
## <a name="data-at-execution-parameters"></a>Data-at-Execution-Parameter  
 Wenn einer der Werte im Array Längenindikator/SQL_DATA_AT_EXEC oder das Ergebnis der SQL_LEN_DATA_AT_EXEC (*Länge*) Makros, die Daten für diese Werte mit gesendet **SQLPutData** auf die übliche Weise. Die folgenden Aspekte dieses Vorgangs tragen spezielle Kommentar an, da sie nicht sofort offensichtlich sind:  
  
-   Wenn der Treiber gibt SQL_NEED_DATA zurück, muss er die Adresse der Variablen Zahl Zeile auf die Zeile festgelegt, für die Daten benötigt. Wie im Fall einwertig kann nicht die Anwendung keine Annahmen über die Reihenfolge vornehmen, in dem der Treiber Parameterwerte in einer einzigen Gruppe von Parametern anfordert. Bei einem bei der Ausführung von Data-at-Execution-Parameter Fehler, ist der Puffer, die durch das SQL_ATTR_PARAMS_PROCESSED_PTR-Anweisungsattribut angegeben festgelegt, die Anzahl der Zeilen, die auf dem der Fehler aufgetreten ist, den Status für die Zeile in der zeilenstatusarray gemäß Das SQL_ATTR_PARAM_STATUS_PTR-Anweisungsattribut festgelegt ist, um SQL_PARAM_ERROR und der Aufruf von **SQLExecute**, **SQLExecDirect**, **SQLParamData**, oder ** SQLPutData** gibt SQL_ERROR zurück. Der Inhalt dieses Puffers nicht definiert werden, wenn **SQLExecute**, **SQLExecDirect**, oder **SQLParamData** SQL_STILL_EXECUTING zurück.  
  
-   Da der Treiber nicht mit den Wert in interpretiert der *ParameterValuePtr* Argument **SQLBindParameter** für Data-at-Execution-Parameter, wenn die Anwendung einen Zeiger auf ein Array bereitstellt ** SQLParamData** nicht extrahieren und an die Anwendung ein Element dieses Arrays zurück. Stattdessen wird zurückgegeben, dass der skalare Wert an die Anwendung bereitgestellt wurde. Dies bedeutet, dass der Rückgabewert von **SQLParamData** ist nicht ausreichend, um anzugeben, die Parameter für die die Anwendung muss zum Senden von Daten, die Anwendung muss außerdem berücksichtigt die aktuelle Zeilennummer.  
  
     Wenn nur einige der Elemente eines Arrays von Parametern Data-at-Execution-Parameter sind, leitet die Anwendung muss die Adresse eines Arrays in *ParameterValuePtr* , die Elemente für alle Parameter enthält. Dieses Array wird normalerweise für die Parameter interpretiert, die keine Data-at-Execution-Parameter sind. Für die Data-at-Execution-Parameter den Wert, der **SQLParamData** bietet auf die Anwendung, die normalerweise verwendet werden kann, die Daten zu identifizieren, die der Treiber bei dieser Gelegenheit anfordert, wird immer die Adresse des Arrays.
