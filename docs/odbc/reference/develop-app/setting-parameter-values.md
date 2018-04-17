---
title: Festlegen von Parameterwerten | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88b8ea3a21f7b2d0bd5790aad934e784b4ca3e87
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="setting-parameter-values"></a>Festlegen von Parameterwerten
Um den Wert eines Parameters festlegen, legt die Anwendung einfach den Wert der an den Parameter gebundenen Variablen. Es ist nicht wichtig, wenn dieser Wert festgelegt ist, solange er festgelegt ist, bevor die Anweisung ausgeführt wird. Die Anwendung kann den Wert festlegen, vor oder nach dem die Variable binden, und kann es ändern Sie den Wert so oft wie möglich. Wenn die Anweisung ausgeführt wird, ruft der Treiber einfach den aktuellen Wert der Variablen ab. Dies ist besonders nützlich, wenn mehr als einmal eine vorbereitete Anweisung ausgeführt wird; die Anwendung legt neue Werte für einige oder alle Variablen jedes Mal, wenn die Anweisung ausgeführt wird. Ein Beispiel hierfür finden Sie unter [vorbereitete Ausführung](../../../odbc/reference/develop-app/prepared-execution-odbc.md)weiter oben in diesem Abschnitt.  
  
 Wenn ein Längen-/Indikatorpuffers, in dem Aufruf von gebunden wurde **SQLBindParameter**, er muss auf einen der folgenden Werte festgelegt werden, bevor die Anweisung ausgeführt wird:  
  
-   Die Bytelänge der Daten in die gebundene Variable. Der Treiber überprüft diese Länge nur dann, wenn die Variable, Zeichen- oder Binärzeichenfolgen ist (*ValueType* SQL_C_CHAR oder sql_c_binary angegeben ist).  
  
-   SQL_NTS. Die Daten sind eine Null-terminierte Zeichenfolge.  
  
-   SQL_NULL_DATA. Der Datenwert NULL ist, und der Treiber ignoriert den Wert der gebundenen Variablen.  
  
-   SQL_DATA_AT_EXEC oder das Ergebnis des SQL_LEN_DATA_AT_EXEC Makros. Der Wert des Parameters wird mit Versand **SQLPutData**. Weitere Informationen finden Sie unter [Long-Daten senden](../../../odbc/reference/develop-app/sending-long-data.md)weiter unten in diesem Abschnitt.  
  
 Die folgende Tabelle zeigt die Werte für die gebundene Variable und die Längen-/Indikatorpuffers, durch die die Anwendung für eine Vielzahl von Parameterwerten festgelegt.  
  
|Parameter<br /><br /> Wert|Parameter<br /><br /> (SQL)<br /><br /> Datentyp|Variable (C)<br /><br /> Datentyp|Wert in<br /><br /> gebunden<br /><br /> variable|Wert in<br /><br /> Länge-Indikator<br /><br /> Puffer [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS oder 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0 [a]|SQL_NTS oder 2|  
|13 UHR|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0 [b]|--|  
|13 UHR|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a] "," [c]|SQL_NTS oder 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0" stellt eine Null-Abschlusszeichen. Die Null-Abschlusszeichen ist erforderlich, nur dann, wenn der Wert in die Längen-/Indikatorpuffers SQL_NTS ist.  
  
 [b] die Zahlen in dieser Liste werden die Zahlen in die Felder der Struktur TIME_STRUCT gespeichert.  
  
 [c] verwendet der Escape-Klausel von ODBC-Datum. Weitere Informationen finden Sie unter [Date, Time und Timestamp-Literale](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 [d] Treiber müssen immer überprüfen Sie diesen Wert, um festzustellen, ob er einen Spezialwert, z. B. SQL_NULL_DATA ist.  
  
 Leistungsumfang der Treiber mit einem Parameterwert zum Zeitpunkt der Ausführung hängt vom Treiber. Bei Bedarf konvertiert der Treiber den Wert aus der C-Data Type und Byte der Länge der gebundenen Variablen in der SQL-Datentyp, Genauigkeit und Dezimalstellen des Parameters an. In den meisten Fällen sendet der Treiber klicken Sie dann den Wert an die Datenquelle. In einigen Fällen den Wert als Text formatiert und fügt sie in der SQL-Anweisung vor dem Senden der Anweisung an die Datenquelle.
