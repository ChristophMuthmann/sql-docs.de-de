---
title: Datenquellen (Assistentenbildschirm 4) (Odbcdriver for SQLServer) | Microsoft Docs
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: d3ba6607f717299bdeb60b649a8c6a1838ab0d17
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="data-source-wizard-screen-4"></a>Data Source-Assistent (Bildschirm 4)

Geben Sie die Sprache für SQL Server-Meldungen verwendet werden soll, die Übersetzung des Zeichensatzes und gibt an, ob der ODBC-Treiber für SQL Server die regionale Einstellungen verwenden soll. Sie können auch die Protokollierung von Abfragen mit langer Ausführungszeit und die Einstellungen der Treiberstatistik steuern.

## <a name="options"></a>enthalten

### <a name="change-the-language-of-sql-server-system-messages-to"></a>Ändern der Sprache von SQL Server-Systemmeldungen in

Jede Instanz von SQL Server kann mehrere Sätze an systemmeldungen, mit jeder Reihe in einer anderen Sprache (z. B. Englisch, Spanisch, Französisch usw.) aufweisen. Wenn eine Datenquelle für einen bestimmten Server definiert ist, die mehrere Sätze an Systemmeldungen aufweist, können Sie angeben, welche Sprache für Systemmeldungen verwendet werden soll. Klicken Sie in der Liste auf die Sprache. Diese Option ist nicht verfügbar, wenn nur eine Sprache auf dem SQL Server installiert ist.

### <a name="use-strong-encryption-for-data"></a>Starke Verschlüsselung für Daten verwenden

Wenn diese Option ausgewählt ist, werden Daten, die durch Verbindungen weitergeleitet werden, die mit diesem DSN hergestellt werden, verschlüsselt. Anmeldungen werden standardmäßig verschlüsselt, auch wenn das Kontrollkästchen deaktiviert wird.

### <a name="trust-server-certificate"></a>Serverzertifikat zu vertrauen

Diese Option ist nur anwendbar, wenn **starken Verschlüsselung für Daten verwenden** aktiviert ist. Bei Auswahl dieser Option wird das Zertifikat des Servers nicht überprüft werden, um, der richtige Hostname des Servers und von einer vertrauenswürdigen Zertifizierungsstelle ausgestellt werden. 

### <a name="perform-translation-for-character-data"></a>Übersetzung für Zeichendaten ausführen

Wenn dieses Kontrollkästchen aktiviert ist, konvertiert der ODBC-Treiber für SQL Server ANSI-Zeichenfolgen, die zwischen dem Clientcomputer und dem SQL Server mithilfe von Unicode gesendet. Der ODBC-Treiber konvertiert manchmal zwischen der SQL Server-Codepage und Unicode auf dem Clientcomputer. Dies erfordert, dass die von SQL Server verwendete Codepage eine der auf dem Clientcomputer verfügbaren Codepages sein.

Wenn dieses Kontrollkästchen deaktiviert wird, erfolgt keine Übersetzung von Sonderzeichen in ANSI-Zeichenfolgen, wenn sie zwischen der Clientanwendung und dem Server gesendet werden. Wenn der Clientcomputer eine ANSI-Codepage (ACP) von SQL Server-Codepage unterscheidet verwendet wird, können Sonderzeichen in ANSI-Zeichenfolgen fehlinterpretiert werden. Wenn der Clientcomputer dieselbe Codepage für seine ACP verwendet, die SQL Server verwendet wird, werden die Sonderzeichen ordnungsgemäß interpretiert werden.

### <a name="use-regional-settings-when-outputting-currency-numbers-dates-and-times"></a>Einstellungen für Land/Region für die Ausgabe von Währung, Zahlen, Datumsangaben und Uhrzeiten verwenden

Gibt an, dass der Treiber die Einstellungen des Clientcomputers für Land/Region für das Formatieren von Währung, Zahlen, Datumsangaben und Uhrzeiten, Datums- und Zeitdaten in ausgegebenen Zeichenfolgen verwenden soll. Der Treiber verwendet die Standardeinstellungen für Land/Region für das Windows-Anmeldekonto des Benutzers bei der Herstellung einer Verbindung durch die Datenquelle. Aktivieren Sie diese Option für Anwendungen, die Daten nur anzeigen, nicht für Anwendungen, die Daten verarbeiten.

### <a name="save-long-running-queries-to-the-log-file"></a>Abfragen mit langer Ausführungszeit in der Protokolldatei speichern

Gibt an, dass der Treiber jede Abfrage protokolliert, die länger dauert als die **lange Abfragezeit** Wert. Abfragen mit langer Ausführungszeit werden in der angegebenen Datei protokolliert. Um eine Protokolldatei anzugeben, den vollständigen Pfad und Dateinamen in das Feld ein, oder klicken Sie auf **Durchsuchen** um eine Protokolldatei durch Navigieren durch vorhandene Dateiverzeichnisse auszuwählen.

### <a name="long-query-time-milliseconds"></a>Lange Abfragezeit (Millisekunden)

Gibt einen Schwellenwert in Millisekunden für die Protokollierung von Abfragen mit langer Ausführungszeit an. Es wird jede Abfrage protokolliert, deren Ausführung länger dauert als diese Anzahl von Millisekunden.

### <a name="log-odbc-driver-statistics-to-the-log-file"></a>ODBC-Treiber-Statistik in der Protokolldatei protokollieren

Gibt an, dass die Statistik protokolliert werden soll. Die Statistik wird in der angegebenen Datei protokolliert. Um eine Protokolldatei anzugeben, geben Sie den vollständigen Pfad und Namen in das Feld oder klicken Sie auf **Durchsuchen** um eine Protokolldatei durch Navigieren durch vorhandene Dateiverzeichnisse auszuwählen.

Das Statistikprotokoll ist eine durch Tabstopps getrennte Datei, die in Microsoft Excel oder in jeder anderen Anwendung analysiert werden kann, die durch Tabstopps getrennte Dateien unterstützt.

### <a name="connect-retry-count"></a>Wiederholungsanzahl verbinden

Gibt die Anzahl der Wiederholungsversuche einen misslungenen Verbindungsversuch.

### <a name="connect-retry-interval-seconds"></a>Verbinden Sie das Wiederholungsintervall (Sekunden)

Gibt die Anzahl der Sekunden zwischen jedem Verbindungsversuch an. Weitere Informationen zum Vorgang dieses und die **verbinden Wiederholungsanzahl** Optionen finden Sie [Verbindungsresilienz im Windows ODBC-Treiber](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).

### <a name="back"></a>Zurück

Klicken Sie auf diese Schaltfläche, um zur vorherigen Seite des Assistenten zurückzukehren.

### <a name="finish"></a>Fertig stellen

Wenn die auf diesem Bildschirm angegebene Informationen abgeschlossen ist, können Sie klicken **Fertig stellen**. Der DSN wird mithilfe von alle zu dieser und anderen Bildschirmen des Assistenten angegebenen Attribute erstellt, und erhalten Sie Gelegenheit zum Testen des neu erstellten DSNS.

## <a name="next-steps"></a>Nächste Schritte

[Assistent Datenquellenbildschirm 3](../../../connect/odbc/windows/dsn-wizard-3.md)

