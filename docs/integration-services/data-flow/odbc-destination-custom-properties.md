---
title: Benutzerdefinierte Eigenschaften von ODBC-Zielen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 07508c40-6c08-4359-96cd-8ff17671244d
caps.latest.revision: "8"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4dacb3a2eea675e85b23fc2b05443d14a95983c6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-destination-custom-properties"></a>Benutzerdefinierte Eigenschaften von ODBC-Zielen
  In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften des ODBC-Ziels beschrieben. Alle Eigenschaften können über SSIS-Eigenschaftsausdrücke festgelegt werden.  
  
|Eigenschaftsname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|Verbindung|ODBC-Verbindung|Eine ODBC-Verbindung für den Zugriff auf die Zieldatenbank.|  
|BatchSize|Integer|Die Größe des Batches für den Massenladevorgang. Dies ist die Anzahl der Zeilen, die als Batch geladen werden. Ist nur gültig, wenn die Parameterbindung pro Zeile unterstützt wird. Wenn die Parameterbindung pro Zeile nicht unterstützt wird, beträgt die Batchgröße 1.|  
|BindCharColumnAs|Ganze Zahl (Enumeration)|Diese Eigenschaft bestimmt, wie das ODBC-Ziel Spalten an Zeichenfolgentypen mit mehreren Byte bindet, z. B. SQL_CHAR, SQL_VARCHAR oder SQL_LONGVARCHAR.<br /><br /> Die möglichen Werte sind Unicode (0), wobei die Spalten als SQL_C_WCHAR gebunden werden, und ANSI (1), wobei die Spalten als SQL_C_CHAR gebunden werden. Der Standardwert ist Unicode (0).<br /><br /> Unicode ist am besten für die meisten ODBC 3.x-Anbieter und ODBC 2.x-Anbieter geeignet, die das Binden von CHAR-Parametern als breite Zeichenfolgen unterstützen. Wenn Sie Unicode wählen und für ExposeCharColumnsAsUnicode die Einstellung True gilt, müssen Benutzer die von der Quelldatenbank verwendete Codepage nicht angeben.<br /><br /> **Hinweis:** Diese Eigenschaft ist nicht im **Ziel-Editor für ODBC**verfügbar, kann jedoch mit dem **Erweiterten Editor**festgelegt werden.|  
|BindNumericAs|Ganze Zahl (Enumeration)|Diese Eigenschaft bestimmt, wie das ODBC-Ziel Spalten mit numerischen Daten an die Datentypen SQL_TYPE_NUMERIC und SQL_TYPE_DECIMAL bindet.<br /><br /> Die möglichen Werte sind Char (0), wobei die Spalten als SQL_C_CHAR gebunden werden, und Numeric (1), wobei die Spalten als SQL_C_NUMERIC gebunden werden. Der Standardwert ist Char (0).<br /><br /> **Hinweis**: Diese Eigenschaft ist nicht im **Ziel-Editor für ODBC**verfügbar, kann jedoch mit dem **Erweiterten Editor**festgelegt werden.|  
|DefaultCodePage|Integer|Die Codepage, die für Zeichenfolgenspalten verwendet werden soll.<br /><br /> **Hinweis**: Diese Eigenschaft ist nicht im **Ziel-Editor für ODBC**verfügbar, kann jedoch mit dem **Erweiterten Editor**festgelegt werden.|  
|InsertMethod|Ganze Zahl (Enumeration)|Die Methode, die zum Einfügen der Daten verwendet wird. Die möglichen Werte sind Zeile für Zeile (0) und Batch (1). Der Standardwert ist Batch (1).<br /><br /> Weitere Informationen zu diesen Optionen finden Sie unter Ladeoptionen in [ODBC Destination](../../integration-services/data-flow/odbc-destination.md).|  
|StatementTimeout|Integer|Die Anzahl der Sekunden, wie lange auf die Ausführung einer SQL-Anweisung gewartet wird, bevor – mit einem Fehler – zur Anwendung zurückgekehrt wird. Der Standardwert ist 120.|  
|TableName|String|Der Name der Zieltabelle, in die die Daten eingefügt werden.|  
|TransactionSize|Integer|Die Anzahl von Einfügungen in einer einzelnen Transaktion. Der Standardwert ist 0. Dies bedeutet, dass das ODBC-Ziel im automatischen Commit-Modus arbeitet.<br /><br /> Da der ODBC-Verbindungs-Manager keine verteilten Transaktionen unterstützt, ist es möglich, diese Eigenschaft auf einen anderen Wert als 0 festzulegen. Wenn die **RetainSameConnection** -Eigenschaft für den Verbindungs-Manager jedoch auf **true** festgelegt ist, muss diese Eigenschaft auf 0 festgelegt werden.<br /><br /> **Hinweis**: Diese Eigenschaft ist nicht im **Ziel-Editor für ODBC**verfügbar, kann jedoch mit dem **Erweiterten Editor**festgelegt werden.|  
|LobChunkSize|Integer|Die Segmentgrößenzuordnung für LOB-Spalten.|  
  
  
