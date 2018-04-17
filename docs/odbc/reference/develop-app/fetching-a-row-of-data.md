---
title: Abrufen einer Datenzeile | Microsoft Docs
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
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 81fff470f916155e9b6d85571db46c46d9e63454
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="fetching-a-row-of-data"></a>Abrufen einer Datenzeile
Um eine Zeile mit Daten abzurufen, eine Anwendung ruft **SQLFetch**. **SQLFetch** kann mit jeder Art des Cursors aufgerufen werden, aber nur den Rowset-Cursor in eine Richtung vorwärts verschoben. **SQLFetch** verschiebt den Cursor auf die nächste Zeile und gibt die Daten für alle Spalten, die durch Aufrufe von gebunden wurden **SQLBindCol**. Wenn sich der Cursor auf das Ende des Resultsets erreicht festgelegt, **SQLFetch** gibt SQL_NO_DATA zurück. Beispiele für das Aufrufen von **SQLFetch**, finden Sie unter [SQLBindCol verwenden](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 Genau wie **SQLFetch** wird implementiert ist treiberspezifische, aber das allgemeine Muster ist für den Treiber zum Abrufen der Daten für alle Spalten aus der Datenquelle gebunden, konvertieren Sie sie entsprechend die Typen der gebundenen Variablen und platzieren Sie die konvertiert Daten in diese Variablen. Wenn der Treiber keine Daten konvertieren kann **SQLFetch** gibt einen Fehler zurück. Die Anwendung kann weiterhin das Abrufen von Zeilen, die Daten für die aktuelle Zeile geht jedoch verloren. Was geschieht, um die Daten für ungebundene Spalten, hängt davon ab, des Treibers, aber die meisten Treiber entweder abzurufen und verwerfen oder überhaupt nicht mehr abgerufen werden.  
  
 Der Treiber setzt auch die Werte der keine Längenindikator/Puffer, die gebunden wurden. Wenn der Datenwert für eine Spalte NULL ist, legt der Treiber die entsprechenden Längen-/Indikatorpuffers auf SQL_NULL_DATA fest. Wenn der Wert nicht NULL ist, legt der Treiber die Längen-/Indikatorpuffers auf die Bytelänge der Daten nach der Konvertierung an. Wenn diese Länge bestimmt werden kann wie in einigen Fällen mit long-Daten, die von mehr als ein Funktionsaufruf abgerufen wird, legt der Treiber die Längen-/Indikatorpuffers auf SQL_NO_TOTAL fest. Für fester Länge, die Datentypen, z. B. ganze Zahlen und Datum Strukturen ist die Bytelänge der Größe des Datentyps.  
  
 Für Daten mit variabler Länge, z. B. Zeichen- und Binärdaten überprüft der Treiber die Bytelänge der konvertierten Daten gegen die Bytelänge des Puffers an die Spalte gebunden. entspricht der Länge des Puffers die *Pufferlänge* Argument in **SQLBindCol**. Wenn die Bytelänge der konvertierten Daten größer als die Bytelänge des Puffers ist, wird der Treiber schneidet die Daten für den Schreibpuffer, gibt die ungekürzte Länge in Längen-/Indikatorpuffers gibt SQL_SUCCESS_WITH_INFO und SQLSTATE 01004 (Data platziert abgeschnitten) bei der Diagnose. Die einzige Ausnahme hierbei ist, wenn ein Lesezeichen variabler Länge abgeschnitten wird, wenn vom **SQLFetch**, womit SQLSTATE 22001 (Zeichenfolgendaten, rechts abgeschnitten).  
  
 Daten fester Länge werden nie abgeschnitten, da der Treiber wird davon ausgegangen, dass die Größe des gebundenen Puffer die Größe des Datentyps. Abschneiden von Daten ist nur selten auftreten, werden, weil die Anwendung in der Regel einen Puffer groß genug für den gesamten Datenwert gebunden; Sie bestimmt die erforderliche Größe aus den Metadaten. Die Anwendung möglicherweise jedoch explizit einen Puffer binden, den dieser weiß, dass klein ist. Beispielsweise könnte es abzurufen und anzuzeigen, der eine Beschreibung für die ersten 20 Zeichen oder die ersten 100 Zeichen ein langer Text-Spalte.  
  
 Zeichendaten müssen Null-terminiert sein vom Treiber vor der Rückgabe an die Anwendung, auch wenn es abgeschnitten wurde. Die Null-Abschlusszeichen benötigt Speicherplatz in der gebundenen Puffer jedoch nicht in der zurückgegebenen Bytelänge enthalten ist. Nehmen Sie z. B. an eine Anwendung verwendet Zeichenfolgen, die Zeichendaten in ASCII-Zeichensatz besteht, ein Treiber ist 50 Zeichen mit Daten zurückgegeben und die Anwendung Puffer ist 25 Byte lang. Im Puffer der die Anwendung, gibt der Treiber die ersten 24 Zeichen, gefolgt von einer Null-Abschlusszeichen. In der Längen-/Indikatorpuffers wird eine Länge von 50 zurückgegeben.  
  
 Die Anwendung kann eine beschränkte Anzahl an Zeilen im Resultset durch Festlegen von SQL_ATTR_MAX_ROWS-Anweisungsattribut vor dem Ausführen der Anweisung, die das Ergebnis erstellt. Der Seitenansicht in einer Anwendung, die zum Formatieren von Berichten benötigt beispielsweise nur genügend Daten für die erste Seite des Berichts anzuzeigen. Beschränken die Größe des Resultsets, würde eine solche Funktion schneller ausgeführt. Dieses Anweisungsattribut richtet sich an den Netzwerkverkehr zu reduzieren und möglicherweise vom alle Treiber nicht unterstützt werden.
