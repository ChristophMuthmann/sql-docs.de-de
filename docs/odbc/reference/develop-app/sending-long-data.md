---
title: Long-Daten senden | Microsoft Docs
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
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 260c62d849f1b771b6d9fc40245fd1b0bfd2c5ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sending-long-data"></a>Long-Daten senden
Definieren eines DBMS *long-Daten* als beliebiges Zeichen oder Binärdaten über eine bestimmte Größe, z. B. 254 Zeichen. Es eventuell nicht möglich, speichern Sie ein gesamtes Element der long-Daten im Arbeitsspeicher, z. B. wenn das Element ein langer Text-Dokument oder eine Bitmap darstellt. Da diese Daten in einem einzigen Puffer gespeichert werden können, sendet die Datenquelle er an den Treiber in Teilen mit **SQLPutData** Wenn die Anweisung ausgeführt wird. Parameter für die Daten zum Zeitpunkt der Ausführung gesendet werden, werden als bezeichnet *Data-at-Execution-Parameter*.  
  
> [!NOTE]  
>  Eine Anwendung kann eigentlich jeden Datentyp zum Zeitpunkt der Ausführung mit senden **SQLPutData**, obwohl nur Zeichen- und Binärdaten in Teilen gesendet werden können. Wenn die Daten klein genug, um einen einzelnen Puffer zu groß ist, besteht jedoch im Allgemeinen kein Grund zur Verwendung **SQLPutData**. Es ist viel leichter, den Puffer zu binden, und lassen den Treiber, die Abrufen der Daten aus dem Puffer.  
  
 Zum Senden von Daten zum Zeitpunkt der Ausführung, führt die Anwendung die folgenden Aktionen aus:  
  
1.  Übergibt einen 32-Bit-Wert, der im Parameters identifiziert die *ParameterValuePtr* Argument in **SQLBindParameter** anstatt die Adresse eines Puffers übergeben. Dieser Wert wird vom Treiber nicht analysiert werden. Er wird an die Anwendung später zurückgegeben werden, damit es etwas, um die Anwendung bedeuten sollte. Es kann z. B. die Nummer des Parameters oder das Handle einer Datei mit Daten sein.  
  
2.  Übergibt die Adresse ein Längen-/Indikatorpuffers in der *StrLen_or_IndPtr* Argument **SQLBindParameter**.  
  
3.  Speichert SQL_DATA_AT_EXEC oder das Ergebnis der SQL_LEN_DATA_AT_EXEC (*Länge*) Makro in Längen-/Indikatorpuffers. Beide Werte angegeben werden, den Treiber, die die Daten für den Parameter mit gesendet werden, **SQLPutData**. SQL_LEN_DATA_AT_EXEC (*Länge*) wird verwendet, wenn der long-Daten mit einer Datenquelle zu senden, die muss wissen, wie viele Bytes an Daten vom Typ long gesendet werden, damit er Speicherplatz vorab zugeordnet werden kann. Um zu bestimmen, wenn dieser Wert von eine Datenquelle erforderlich ist, ruft die Anwendung **SQLGetInfo** mit der Option SQL_NEED_LONG_DATA_LEN. Alle Treiber müssen dieses Makro unterstützt werden Wenn die Bytelänge in die Datenquelle nicht erforderlich ist, können Sie von der Treiber ignorieren.  
  
4.  Aufrufe **SQLExecute** oder **SQLExecDirect**. Der Treiber ermittelt, dass ein Längen-/Indikatorpuffers, den Wert SQL_DATA_AT_EXEC oder das Ergebnis der SQL_LEN_DATA_AT_EXEC enthält (*Länge*)-Makro und gibt SQL_NEED_DATA zurück, als der Rückgabewert der Funktion.  
  
5.  Aufrufe **SQLParamData** Rückgabewert als Antwort auf die SQL_NEED_DATA zurück. Wenn long-Daten gesendet werden, müssen **SQLParamData** wird SQL_NEED_DATA zurückgegeben. In den Puffer, die durch die *ValuePtrPtr* Argument, gibt der Treiber den Wert, der den Data-at-Execution-Parameter identifiziert. Wenn mehr als eine Data-at-Execution-Parameter vorhanden ist, muss die Anwendung diesen Wert verwenden, um zu bestimmen, welche Parameter zum Senden von Daten für; der Treiber ist nicht erforderlich, Anfordern von Daten für Data-at-Execution-Parameter in einer bestimmten Reihenfolge.  
  
6.  Aufrufe **SQLPutData** zum Senden der Parameterdaten an den Treiber. Wenn die Parameterdaten wie häufig der Fall mit long-Daten ist in einem einzigen Puffer nicht passt, die Anwendung aufruft, **SQLPutData** wiederholt zum Senden der Daten in Teilen; es obliegt dem Treiber und der Datenquelle, die Daten wieder zusammenzusetzen. Wenn die Anwendung auf Null endende Zeichenfolgendaten übergibt, muss die Treiber oder die Datenquelle der Null-Terminierung Zeichen als Teil des Prozesses für die Reassemblierung entfernen.  
  
7.  Aufrufe **SQLParamData** erneut aus, um anzugeben, dass sie alle Daten für den Parameter gesendet hat. Wenn Data-at-Execution-Parameter für die Daten nicht der Treiber gibt SQL_NEED_DATA zurück, und der Wert, der den nächsten Parameter bezeichnet gesendet wurde, vorhanden sind; Gibt zurück, die Anwendung mit Schritt 6 fort. Wenn Daten für alle Data-at-Execution-Parameter gesendet wurde, wird die Anweisung ausgeführt. **SQLParamData** gibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO und kann zurückgeben, einem Rückgabewert oder Diagnose, die **SQLExecute** oder **SQLExecDirect** zurückgeben kann.  
  
 Nach dem **SQLExecute** oder **SQLExecDirect** wird SQL_NEED_DATA zurückgegeben, und bevor die Daten vollständig für den letzten Data-at-Execution-Parameter gesendet wurde, wird die Anweisung in einem Zustand benötigen. Während eine Anweisung in einem Zustand erforderlich ist, kann nur die Anwendung aufrufen **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, oder **SQLGetDiagRec**; alle anderen Funktionen zurückgeben SQLSTATE HY010 (Sequenzfehler-Funktion). Aufrufen von **SQLCancel** bricht die Ausführung der Anweisung ab und gibt sie an den ursprünglichen Zustand zurück. Weitere Informationen finden Sie unter [Anhang B: ODBC-Übergang-Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Ein Beispiel für das Senden von Daten zum Zeitpunkt der Ausführung, finden Sie unter der [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) funktionsbeschreibung.
