---
title: 'Anhang B: ODBC-Übergang Statustabellen | Microsoft Docs'
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
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 27d719a9ab41bfa7594231462ea5c6318d95247d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="appendix-b-odbc-state-transition-tables"></a>Anhang B: ODBC-Übergang Statustabellen
In den Tabellen in diesem Anhang werden wie die ODBC-Funktionen Übergang von der Umgebung, Verbindungs-, Anweisung und Deskriptor Zustände verursachen. Der Status der Umgebung, die Verbindung, die Anweisung oder die Deskriptor bestimmt in der Regel an, wenn Funktionen, die verwenden den entsprechenden Typ des Handles (Umgebung, Verbindung, Anweisung oder Deskriptor) aufgerufen werden kann. Die Status-Umgebung, Verbindung, anweisungs- und Deskriptorstatuswerte überlappen ungefähr wie in der folgenden Abbildung dargestellt. Angenommen, die genaue Überlappung der Verbindung gibt, C5 und C6 und Anweisung besagt, dass S1 bis S12 ist datenquellenabhängig, da Transaktionen zu unterschiedlichen Zeiten auf verschiedenen Datenquellen starten und Deskriptor Status D1i (implizit Deskriptor zugeordnet) abhängt den Status der Anweisung, die mit der Deskriptor verknüpft ist, ist beim Status D1e (explizit Deskriptor reserviert) unabhängig von den Zustand einer beliebigen Anweisung. Eine Beschreibung der einzelnen Zustände, finden Sie unter [Umgebungsübergänge](../../../odbc/reference/appendixes/environment-transitions.md), [Verbindung Übergänge](../../../odbc/reference/appendixes/connection-transitions.md), [Anweisung Übergänge](../../../odbc/reference/appendixes/statement-transitions.md), und [Deskriptor Übergänge ](../../../odbc/reference/appendixes/descriptor-transitions.md)weiter unten in diesem Anhang.  
  
 Der umgebungs- und verbindungsstatuswerte überlappen wie folgt aus:  
  
 ![Umgebungs- und verbindungsstatuswerte überlappen](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 Die Verbindungs- und Zustände überlappen wie folgt aus:  
  
 ![Verbindungs- und Zustände Überlappung](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 Die Zustände anweisungs- und Deskriptorstatuswerte überlappen wie folgt aus:  
  
 ![Anweisungs- und Deskriptorstatuswerte besagt Überlappung](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 Die Zustände Verbindungs- und Deskriptorstatuswerte überlappen wie folgt aus:  
  
 ![Gibt an Verbindungs- und Deskriptorstatuswerte überlappen](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 Jeder Eintrag in einer Tabelle kann einen der folgenden Werte sein:  
  
-   **--** – Der Zustand ist nach der Ausführung der Funktion unverändert.  
  
-   **E**  
     ***n*** , **C*n***, **S*n***, oder **D*n*** – die Umgebung, Verbindung, Anweisung oder Deskriptor Zustand wechselt zum die angegebenen Status.  
  
-   **(SODASS)** – Ein ungültiges Handle wurde an die Funktion übergeben. Wenn das Handle ein null-Handle wurde oder ein gültiges Handle des falschen Typs wurde – beispielsweise ein Verbindungshandle übergeben wurde, wenn ein Anweisungshandle erforderlich ist – die Funktion gibt SQL_INVALID_HANDLE; Andernfalls ist das Verhalten nicht definiert "und" wahrscheinlich schwerwiegend. Dieser Fehler wird angezeigt, nur bei der einzig mögliche Ergebnis des Aufrufs der Funktion im angegebenen Status. Dieser Fehler ändert sich nicht auf den Status und von der Treiber-Manager wird immer erkannt werden, wie durch die Klammern angegeben.  
  
-   **NS** – Status weiter. Der Anweisung Übergang ist identisch, als wäre die Anweisung die asynchronen Status nicht durchgearbeitet hatte. Nehmen wir beispielsweise an eine Anweisung, die ein Resultset erstellt Status S11 vom Zustand S1 eingibt, da **SQLExecDirect** SQL_STILL_EXECUTING zurückgegeben. Die Notation "NS" im Zustand S11 bedeutet, dass die Übergänge für die Anweisung sind identisch mit denen für eine Anweisung im Zustand S1, die ein Resultset erstellt. Wenn **SQLExecDirect** einen Fehler zurückgibt, die Anweisung bleibt im Zustand S1; Wenn erfolgreich ist, verschiebt der Anweisung in den Status der S5; Wenn es Daten benötigt, verschiebt der Anweisung in den Status von a8; und wenn er immer noch ausgeführt wird, bleibt im Zustand S11.  
  
-   ***XXXXX*** oder **(*XXXXX*)** – ein SQLSTATE, die mit der Tabelle der Zustandsübergänge; verknüpft ist SQLSTATEs, die vom Treiber-Manager erkannt werden in Klammern eingeschlossen. Die Funktion zurückgegeben wird, SQL_ERROR zurück, und der angegebenen SQLSTATE, aber der Status ändert sich nicht. Z. B. wenn **SQLExecute** wird aufgerufen, bevor **SQLPrepare**, SQLSTATE HY010 zurückgegeben (Sequenzfehler-Funktion).  
  
> [!NOTE]  
>  Die Tabellen nicht mehr anzeigen Fehler unabhängig vom stagingstatus Übergang-Tabellen, die den Status nicht geändert werden. Beispielsweise, wenn **SQLAllocHandle** wird im Status der Umgebung E1 aufgerufen und SQLSTATE HY001 zurückgegeben (Fehler bei der speicherbelegung), die Umgebung bleibt im Zustand E1; Dies wird nicht angezeigt, in der Umgebung übergangstabelle für  **SQLAllocHandle**.  
  
 Wenn die Umgebung, Verbindung, Anweisung oder -Deskriptor in mehr als einen Statuswert verschieben kann, jedem möglicher Status wird angezeigt, und eine oder mehrere Fußnoten erläutern die Bedingungen, unter denen jeder Übergang stattfindet. Die folgenden Fußnoten möglicherweise in einer beliebigen Tabelle angezeigt.  
  
|Fußnote|Bedeutung|  
|--------------|-------------|  
|b|Vor oder nach. Der Cursor wurde vor dem Start des Resultsets oder nach dem Ende des Resultsets.|  
|c|Aktuelle Funktion. Die aktuelle Funktion wurde asynchron ausgeführt.|  
|d|Benötigen Sie Daten. Die Funktion hat SQL_NEED_DATA zurückgegeben.|  
|e|Error (Fehler). Die Funktion hat SQL_ERROR zurückgegeben.|  
|i|Ungültige Zeile. Der Cursor positioniert wurde in einer Zeile im Resultset Satz und entweder die Zeile wurde wurde gelöscht oder in einem Vorgang für die Zeile ist ein Fehler aufgetreten. Wenn die zeilenstatusarray vorhanden war, wurde der Wert in der zeilenstatusarray für die Zeile SQL_ROW_DELETED oder SQL_ROW_ERROR. (Die zeilenstatusarray wird durch das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR verwiesen.)|  
|Nf|Nicht gefunden. Die Funktion hat SQL_NO_DATA zurückgegeben. Dies gilt nicht beim **SQLExecDirect**, **SQLExecute**, oder **SQLParamData** gibt SQL_NO_DATA nach der Ausführung einer gesuchten update oder delete-Anweisung.|  
|np|Nicht vorbereitet. Die Anweisung wurde nicht vorbereitet.|  
|Nr.|Keine Ergebnisse. Die Anweisung wird nicht oder ein Resultset erstellt wurde.|  
|o|Andere Funktion. Eine andere Funktion wurde asynchron ausgeführt.|  
|p|Vorbereitet. Die Anweisung vorbereitet wurde.|  
|r|Ergebnisse. Die Anweisung oder hat ein Resultset (möglicherweise leere) erstellt wird.|  
|s|Erfolg. Die Funktion hat SQL_SUCCESS_WITH_INFO oder SQL_SUCCESS zurückgegeben.|  
|v|Gültige Zeile. Der Cursor wurde in einer Zeile im Resultset positioniert, und die Zeile wurde erfolgreich eingefügt wurde, wurde erfolgreich aktualisiert oder ein anderer Vorgang auf die Zeile wurde erfolgreich abgeschlossen. Wenn die zeilenstatusarray vorhanden war, wurde der Wert in der zeilenstatusarray für die Zeile SQL_ROW_ADDED, SQL_ROW_SUCCESS oder SQL_ROW_UPDATED. (Die zeilenstatusarray wird durch das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR verwiesen.)|  
|x|Wird ausgeführt. Der Funktion zurückgegebene SQL_STILL_EXECUTING.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 In diesem Beispiel wird die Zeile in der Umgebung Zustandsübergang für Tabelle **SQLFreeHandle** Wenn *HandleType* ist SQL_HANDLE_ENV lautet wie folgt.  
  
|E0<br /><br /> Nicht zugeordnet|E1<br /><br /> Belegt|E2<br /><br /> Verbindung|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 Wenn **SQLFreeHandle** wird aufgerufen, in der Umgebung Zustand E0 mit *HandleType* auf SQL_HANDLE_ENV auf festgelegt ist, gibt der Treiber-Manager SQL_INVALID_HANDLE. Wenn sie aufgerufen wird, im Zustand E1 mit *HandleType* auf SQL_HANDLE_ENV auf festgelegt ist, die Umgebung verschiebt in E0 angeben, wenn die Funktion erfolgreich ist, und im Status E1, verbleibt Wenn die Funktion fehlschlägt. Wenn er aufgerufen wird, im Zustand E2 mit *HandleType* auf SQL_HANDLE_ENV auf festgelegt ist, der Treiber-Manager immer gibt SQL_ERROR und SQLSTATE HY010 (Sequenzfehler-Funktion) und die Umgebung im Zustand E2 bleibt.  
  
 Um die Statustabellen für den Übergang zu verstehen, ist es erforderlich, um zu verstehen, welches Element (Umgebung, Verbindung, Anweisung oder Deskriptor) auf die sie verweisen. Angenommen Sie, eine Funktion das Handle für ein Element vom Typ X akzeptiert. X Tabelle der Zustandsübergänge für diese Funktion wird beschrieben, wie die aufrufende Funktion, mit das Handle für ein Element vom Typ X, dieses Element beeinflusst. Beispielsweise **SQLDisconnect** akzeptiert ein Verbindungshandle. Verbindungstabelle der Zustandsübergänge für **SQLDisconnect** wird beschrieben, wie **SQLDisconnect** wirkt sich auf den Zustand der Verbindung für den sie aufgerufen wird.  
  
 Angenommen Sie, eine Funktion das Handle für ein Element vom Typ Y, akzeptiert, wobei Y nicht X gleich ist. X Tabelle der Zustandsübergänge für diese Funktion wird beschrieben, wie die aufrufende Funktion, mit der ein Handle vom Typ X, die das Element vom Typ Y, zugeordnet ist das Element vom Typ Y wirkt sich auf. Beispielsweise Anweisungstabelle der Zustandsübergänge für **SQLDisconnect** wird beschrieben, wie **SQLDisconnect** wirkt sich auf den Zustand einer Anweisung, die bei einem Aufruf mit das Handle für die Verbindung mit dem die Anweisung ist verknüpft.  
  
 Dieser Anhang enthält die folgenden Themen.  
  
-   [Umgebungsübergänge](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [Verbindungsübergänge](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [Statusübergänge](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [Descriptor Transitions (Deskriptorübergänge)](../../../odbc/reference/appendixes/descriptor-transitions.md)
