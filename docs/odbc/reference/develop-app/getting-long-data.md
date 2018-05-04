---
title: Abrufen von Long-Daten | Microsoft Docs
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
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a465c8200181c87caa49d6e36df50cb5c158cdbf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getting-long-data"></a>Abrufen von Long-Daten
Definieren eines DBMS *long-Daten* als beliebiges Zeichen oder Binärdaten über eine bestimmte Größe, z. B. 255 Zeichen lang sein. Diese Daten möglicherweise klein genug, um in einem einzigen Puffer, z. B. eine Beschreibung für den mehrere Tausend Zeichen gespeichert werden. Allerdings möglicherweise zu lang im Arbeitsspeicher, z. B. lange Dokumente oder Bitmaps gespeichert sein. Da diese Daten in einem einzigen Puffer gespeichert werden können, aus dem Treiber des Webparts mit abgerufen **SQLGetData** nach die anderen Daten in der Zeile abgerufen wurde.  
  
> [!NOTE]  
>  Eine Anwendung kann eigentlich jeden Datentyp mit abrufen **SQLGetData**, nicht nur Daten, long, obwohl nur Zeichen- und Binärdaten in Teilen abgerufen werden können. Wenn die Daten klein genug, um einen einzelnen Puffer zu groß ist, besteht jedoch im Allgemeinen kein Grund zur Verwendung **SQLGetData**. Es ist viel leichter, binden einen Puffer der Spalte, und lassen den Treiber, die die Daten im Puffer zurück.  
  
 Abrufen von long-Daten aus einer Spalte Ruft eine Anwendung zunächst **SQLFetchScroll** oder **SQLFetch** in eine Zeile verschoben, und die Daten für gebundene Spalten abzurufen. Die Anwendung ruft dann **SQLGetData**. **SQLGetData** hat die gleichen Argumente wie **SQLBindCol**: ein Anweisungshandle; eine Spaltennummer; die C Typ, Adresse und Byte Datenlänge von einer Anwendungsvariablen; und die Adresse des ein Längen-/Indikatorpuffers. Beide Funktionen haben die gleichen Argumenten, daran, dass sie im Wesentlichen die gleiche Aufgabe ausführen: beide beschreiben eine Anwendungsvariablen an den Treiber und gibt an, dass die Daten für eine bestimmte Spalte in der Variable zurückgegeben werden soll. Die Hauptunterschiede sind, die **SQLGetData** wird aufgerufen, nachdem eine Zeile abgerufen wird (und wird manchmal als *spätes Binden* aus diesem Grund) und dass die Bindung von angegeben **SQLGetData**  dauert nur für die Dauer des Aufrufs.  
  
 Im Hinblick auf eine einzelne Spalte **SQLGetData** verhält sich wie **SQLFetch**: er ruft die Daten für die Spalte ab, konvertiert es in den Typ der Anwendungsvariablen und wird in dieser Variablen zurückgegeben. Es gibt auch die Bytelänge der Daten in die Längen-/Indikatorpuffers zurück. Weitere Informationen dazu, wie **SQLFetch** gibt-Daten finden Sie unter [Abrufen von Zeilendaten](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** unterscheidet sich von **SQLFetch** in ein wichtiger Punkt. Wenn sie mehrmals nacheinander für dieselbe Spalte aufgerufen wird, gibt jeder Aufruf einen aufeinander folgenden Teil der Daten zurück. Jeder Aufruf außer dem letzten Aufruf gibt SQL_SUCCESS_WITH_INFO und SQLSTATE 01004 (Zeichenfolgendaten, rechts abgeschnitten); der letzte Aufruf gibt SQL_SUCCESS zurück. Dies ist wie **SQLGetData** dient zum Abrufen von long-Daten in Teilen. Wenn keine weitere Daten zurückgeben, **SQLGetData** gibt SQL_NO_DATA zurück. Die Anwendung ist verantwortlich für den Entwurf der long-Daten, die kann bedeuten, dass die Teile der Daten zu verketten. Jeder Teil ist Null-terminiert. die Anwendung muss die Null-Abschlusszeichen entfernen, wenn die Teile zu verketten. Abrufen von Daten in Teilen kann für variabler Länge Lesezeichen ebenso wie bei anderen long-Daten ausgeführt werden. Durch die Anzahl der Bytes in den vorhergehenden Aufruf zurückgegeben, obwohl es üblich, für den Treiber ist an, in der Lage, die Menge der verfügbaren Daten ermitteln und eine Länge von SQL_NO_TOTAL zurück in den Längenindikator/Puffer verringert bei jedem Aufruf zurückgegebene Wert. Beispiel:  
  
```  
// Declare a binary buffer to retrieve 5000 bytes of data at a time.  
SQLCHAR       BinaryPtr[5000];  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd, BinaryLenOrInd, NumBytes;  
SQLRETURN     rc;   
SQLHSTMT      hstmt;  
  
// Create a result set containing the ID and picture of each part.  
SQLExecDirect(hstmt, "SELECT PartID, Picture FROM Pictures", SQL_NTS);  
  
// Bind PartID to the PartID column.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &PartID, 0, &PartIDInd);  
  
// Retrieve and display each row of data.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // Display the part ID and initialize the picture.  
   DisplayID(PartID, PartIDInd);  
   InitPicture();  
  
   // Retrieve the picture data in parts. Send each part and the number   
   // of bytes in each part to a function that displays it. The number   
   // of bytes is always 5000 if there were more than 5000 bytes   
   // available to return (cbBinaryBuffer > 5000). Code to check if   
   // rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLGetData(hstmt, 2, SQL_C_BINARY, BinaryPtr, sizeof(BinaryPtr),  
                           &BinaryLenOrInd)) != SQL_NO_DATA) {  
      NumBytes = (BinaryLenOrInd > 5000) || (BinaryLenOrInd == SQL_NO_TOTAL) ?  
                  5000 : BinaryLenOrInd;  
      DisplayNextPictPart(BinaryPtr, NumBytes);  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 Es gibt mehrere Einschränkungen bei der Verwendung **SQLGetData**. Im allgemeinen Zugriff auf Spalten mit **SQLGetData**:  
  
-   Muss in der Reihenfolge ihrer spaltenzahlfolge (aufgrund der Art und Weise, in die Spalten eines Resultsets aus einer Datenquelle gelesen werden) zugegriffen werden. Es ist z. B. ein Fehler auf, rufen Sie **SQLGetData** für Spalte 5 und dann für die Spalte 4 aufgerufen wird.  
  
-   Kann nicht gebunden werden.  
  
-   Sie benötigen eine Spalte größer als der letzten gebundenen Spalte. Z. B. die letzte gebundene Spalte Spalte 3, es ist ein Fehler auf, rufen Sie **SQLGetData** für die Spalte 2. Aus diesem Grund sollten Anwendungen Spalten long-Daten am Ende der select-Liste platziert sicherstellen.  
  
-   Kann nicht verwendet werden, wenn **SQLFetch** oder **SQLFetchScroll** wurde aufgerufen, um mehr als eine Zeile abzurufen. Weitere Informationen finden Sie unter [Verwenden von Blockcursorn](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 Einige Treiber erzwungen diese Einschränkungen nicht. Interoperable Anwendungen ausführen können, sollte entweder voraussetzen, vorhanden, oder bestimmen, welche Einschränkungen durch den Aufruf nicht erzwungen werden **SQLGetInfo** mit der Option SQL_GETDATA_EXTENSIONS.  
  
 Wenn die Anwendung nicht alle Daten in ein Zeichen oder eine Spalte mit binary-möchten, können sie den Netzwerkdatenverkehr im DBMS-basierten Treibern reduzieren, indem SQL_ATTR_MAX_LENGTH-Anweisungsattribut festlegen, bevor die Anweisung ausgeführt. Dies schränkt die Anzahl der Datenbytes, die für beliebiges Zeichen oder binary-Spalte zurückgegeben werden. Nehmen wir beispielsweise an, dass eine Spalte mit langen Textdokumente enthält. Eine Anwendung, die durchsucht, die Tabelle, enthält diese Spalte, möglicherweise nur die erste Seite des jeweiligen Dokuments anzuzeigen. Obwohl diese Anweisungsattribut im Treiber simuliert werden kann, besteht kein Grund dazu. Insbesondere, wenn eine Anwendung wünscht eine Zeichen- oder Binärdaten abgeschnitten, es sollte binden einen kleinen Puffer auf die Spalte mit **SQLBindCol** , und lassen Sie den Treiber, die die Daten abgeschnitten.
