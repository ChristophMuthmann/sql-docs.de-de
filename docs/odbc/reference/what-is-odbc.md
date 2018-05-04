---
title: Was ist "ODBC"? | Microsoft-Dokumentation
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
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f503c1c55bd2ec10c8d74452c5c65d1751ab3c08
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="what-is-odbc"></a>Was ist "ODBC"?
Viele Missverständnisse über ODBC, die in der IT-Welt vorhanden sein. Für den Endbenutzer ist es ein Symbol in der Microsoft® Windows®-Systemsteuerung. Für den Anwendungsprogrammierer ist es eine Bibliothek mit Data Access-Routinen. Zu viele andere ist es die Antwort auf alle Datenbank-Access-Probleme, die jemals gestaltete.  
  
 Zunächst ist ODBC eine Spezifikation für eine Datenbank-API. Diese API ist unabhängig von einem DBMS oder Betriebssystem. Obwohl dieses Handbuchs C verwendet wird, wird die ODBC-API sprachunabhängige. Die ODBC-API basiert auf den CLI-Spezifikationen von Open Group und ISO/IEC. ODBC-3. *x* vollständig implementiert beide gemäß diesen Spezifikationen – frühere Versionen von ODBC wurden basierend auf vorläufige Versionen dieser Spezifikationen, aber wurde nicht vollständig implementiert werden – und bietet Features, die häufig von Entwicklern der Bildschirm-basierten erforderlich. datenbankanwendungen, z. B. bildlauffähige Cursor.  
  
 Die Funktionen der ODBC-API werden von den Entwicklern der DBMS-spezifische Treiber implementiert. Anwendungen rufen die Funktionen in diese Treiber, um Daten in einer DBMS-unabhängige Weise zugreifen. Eine Treiber-Manager verwaltet die Kommunikation zwischen Anwendungen und Treiber.  
  
 Obwohl Microsoft bietet einen Treiber-Manager für Computer unter Microsoft Windows® 95 und höher geschrieben hat mehrere ODBC-Treiber und ruft ODBC-Funktionen aus einigen seiner Anwendungen jeder ODBC-Anwendungen und-Treiber schreiben kann. In der Tat die meisten ODBC-Anwendungen und-Treiber verfügbar heute werden geschrieben von Herstellern als Microsoft. Darüber hinaus sind ODBC-Treiber und Anwendungen auf die Macintosh® sowie eine Vielzahl von UNIX-Plattformen vorhanden.  
  
 Um Anwendungs- und Treibersoftware Entwicklern zu helfen, bietet Microsoft eine ODBC-Software Development Kit (SDK) für Computer unter Windows 95 und höher, die der Treiber-Manager, Installer DLL TestTools und Beispielanwendungen bereitstellt. Microsoft hat mit Visigenic Software so portieren Sie diese SDKs für den Macintosh sowie eine Vielzahl von UNIX-Plattformen zusammengeschlossen.  
  
 Es ist wichtig zu verstehen, dass ODBC entworfen wurde, verfügbar machen Datenbankfunktionen, die nicht zu ergänzen. Anwendungsentwickler sollten deshalb nicht erwarten, dass eine einfache Datenbank in ein voll funktionsfähiges relationalen Datenbankmodul mithilfe von ODBC plötzlich transformiert wird. Noch voraussichtlich Treiber Writer implementieren Funktionen, die in der zugrunde liegenden Datenbank nicht gefunden. Eine Ausnahme ist, dass Entwickler, die Treiber zu schreiben, die Daten (z. B. Daten in eine Datei Xbase) direkten Zugriff auf eine Datenbank-Engine schreiben, die mindestens Mindestfunktionalität SQL unterstützt erforderlich sind. Eine andere Ausnahme, die die ODBC-Komponente des Windows SDK, früher im Microsoft Data Access Components (MDAC) SDK enthalten ist, stellt eine Cursorbibliothek, die für Treiber bildlauffähige Cursor simuliert, die ein gewisses Maß an Funktionalität zu implementieren.  
  
 Anwendungen, die ODBC verwenden, sind für alle Funktionen datenbankübergreifende zuständig. Z. B. ODBC heterogenen joinmoduls, trotzdem nicht unbedingt eine Prozessors der verteilten Transaktion. Allerdings DBMS unabhängig sein, es dient datenbankübergreifende Tools zu erstellen.
