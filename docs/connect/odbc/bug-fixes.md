---
title: Liste der behobenen Fehler | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
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
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: genemi
manager: kenvh
ms.openlocfilehash: 200e5796866527110bb1e57d35ac35a9229e3716
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="list-of-bugs-fixed"></a>Liste der behobenen Fehler

Diese Seite enthält eine Liste von Fehlern in jeder Version, beginnend mit fester [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC-Treiber 17 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>Fehlerkorrekturen in der [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC-Treiber 17.1 für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Feste 1 Sekunde Verzögerung beim Aufrufen von SQLFreeHandle bei aktivierter MARS-Verbindungsattribut "Encrypt = Yes"
- Korrektur einer Fehler 22003 Absturzes SQLGetData, wenn die Größe des übergebenen Puffers kleiner ist und Sie dann die Daten abgerufen werden (Windows)
- Abgeschnittene ADAL Fehlermeldungen behoben
- Korrektur eines seltenen Fehlers auf 32-Bit-Windows, bei der Konvertierung eine Gleitkommazahl Gleitkommazahl in eine ganze Zahl
- Ein Problem behoben, in denen würde in Feld "decimal" mit Always Encrypted auf doppelte einfügen datenabschneidefehler zurückgeben
- Eine Warnung behoben auf MacOS installer
- Feste falschen Status auf SQL Server während der Sitzung Wiederherstellungsversuch senden, wenn Connection Resiliency sowohl Verbindungspooling aktiviert sind verursacht Sitzung vom Server gelöscht werden,

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>Fehlerkorrekturen in der [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC-Treiber 17 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Korrektur eines Fehlers, bei Verwendung der Kerberos-Authentifizierung mit dem Fehler "Zugriff verweigert" Bulk Insert ausgeführt wurde
- Entfernte problemumgehung für einen UnixODBC-Fehler, die in Version unter 2.3.1 vorhanden (Treiber verdoppelt die Größen der bestimmte an UnixODBC übergebene Puffer)
- Feste Connection Resiliency (Verbindung) hängenden Verwendung ColumnEncryption = aktiviert
- DSN-Erstellung-Fehler, behoben, wenn mithilfe "Interaktive Active Directory-Authentifizierung" option Azure-Authentifizierung kann Fenster nicht reagierenden (Windows) werden
- Korrektur eines seltenen Absturzes während des Herunterfahrens von ODBC, wenn die asynchrone Ausführung aktiviert ist (wird geschah, als Verbindungshandle deaktivieren)
- Es wurde ein Problem verursacht hat, in denen hohe CPU-Auslastung beim Ausführen gespeicherter Prozeduren SQL-Treiber
- Feste Funktion zum Abrufen von Daten in einer verschlüsselten varbinary(max)-Spalte ohne Konvertierung
- Ein Problem behoben, in dem nach einer null varchar(max) verschlüsselte Spalte abgerufen SQLGetData() in einem statischen Cursor verwenden, wird die folgende Spalte auch gelöscht, auch wenn es Daten enthält
- Wurde ein Problem mit varbinary(max) Feld mit Always Encrypted auf Abrufen
- Behebt ein Problem der setlocale() funktioniert nicht mit Always Encrypted
- Wurde ein Problem mit SQLDescribeParam() Fehler bei einem Aufruf in XML-Datentyp gespeicherten Prozedurparameter mit Always Encrypted auf zurückgeben
- Feste mit Escapezeichen versehene Unterstriche funktioniert nicht in SQLTables
- Korrektur eines Fehlers, bei hebräische Daten (Varchar) abgeschnitten wird, wenn als Breitzeichen unter Linux zurückgegeben
- Wurde ein Problem mit Abfragen Shift-JIS codiert Char/Varchar aus UTF-8-Anwendung
- Korrektur der Fehlers zurückgegeben, Aufrufen von SQLGetInfo mit SQL_DRIVER_NAME Parameter Filename Linux-Stil auf MacOS
- Ein Problem behoben, in denen Dateien laden Windows-1252-Zeichendaten mithilfe von Eingaben größer als 32 KB, die Bytes in den VARCHAR-Spalten, die mit dem BCP-Hilfsprogramm zu Fehlern führen würde
