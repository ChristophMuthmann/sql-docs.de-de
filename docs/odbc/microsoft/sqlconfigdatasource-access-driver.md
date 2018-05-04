---
title: SQLConfigDataSource (Access-Treiber) | Microsoft Docs
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
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a792a34bc80ae7e25641aaea7aae88ed7b2349ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Access-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Access-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Die **SQLConfigDataSource** -Funktion, die verwendet wird, hinzuzufügen, ändern oder Löschen einer Datenquelle verwendet, die dynamisch die folgenden Schlüsselwörter.  
  
|Schlüsselwort|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Die Reihenfolge, in der die Felder sortiert werden.<br /><br /> Dadurch wird die gleiche Option als **sortieren Sequenz** im Dialogfeld "Setup".|  
|COMPACT_DB|Führt die Komprimierung von Daten für eine Datenbankdatei an. Weist das folgende Format: COMPACT_DB = < Lokales_Laufwerk >< OptionaL_sort_order >\<optional ENCRYPT-Schlüsselwort >.<br /><br /> Wenn Sie das Schlüsselwort COMPACT_DB in derselben Anweisung mit einem DSN-Schlüsselwort verwenden, ignoriert diese Treiber das DSN-Schlüsselwort. Aus diesem Grund wird durch das Komprimieren einer Datenbank und einen DSN angeben ein zweistufiger Prozess.|  
|CREATE_DB|Erstellt eine Datenbankdatei an. Weist das folgende Format: CREATE_DB = < Lokales_Laufwerk >\<Optional_sort Ordnung >< Optional_ENCRYPT-Schlüsselwort, >, in dem der Pfadname ist der vollständige Pfad zu einer Microsoft Access-Datenbank. Wenn der Pfadname eine vorhandene Datenbank angibt, wird ein Fehler zurückgegeben werden. Die Sortierreihenfolge wird oben festgelegt im Dialogfeld neue Datenbank angezeigt, wenn die Schaltfläche "erstellen" in das Setup für Microsoft Access-Dialogfeld gedrückt wird. Wenn keine Sortierreihenfolge angegeben ist, wird allgemein verwendet.<br /><br /> Wenn Sie das Schlüsselwort CREATE_DB in derselben Anweisung mit einem DSN-Schlüsselwort verwenden, ignoriert diese Treiber das DSN-Schlüsselwort. Daher ist eine Datenbank erstellen und Angeben von einem DSN ein zweistufiger Prozess. Wenn das Schlüsselwort CREATE_DB verwenden der Pfadnamen der Microsoft Access-Datenbank erstellt werden ein oder mehrere Leerzeichen enthält, muss dann der gesamte Pfadnamen durch doppelte Anführungszeichen eingeschlossen werden wie in den folgenden Beispielen gezeigt:<br /><br /> "C:\PROGRAM FILES\COMMON c:\programme\ MyAccess.mdb"<br /><br /> "C:\Programme\Microsoft FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (es werden keine Anführungszeichen erforderlich)|  
|CREATE_SYSDB|Erstellt eine System-Datenbankdatei an. Weist das folgende Format: CREATE_SYSDB =\<-Pfadname >\<optional Sortierreihenfolge >, wobei der Name des Pfads den vollständigen Pfad zu einer Microsoft Access-Datenbank ist. Wenn der Pfadname eine vorhandene Datenbank angibt, wird ein Fehler zurückgegeben werden. Die Sortierreihenfolge werden als Satz von in der **neue Datenbank** das Dialogfeld angezeigt, wenn die **erstellen** geklickt wird die **ODBC-Setup für Microsoft Access** (Dialogfeld). Wenn keine Sortierreihenfolge angegeben ist, wird allgemein verwendet.|  
|CREATE_V2DB|Erstellt eine Datei, die mit Microsoft Access 2.0 kompatibel ist. Weist das folgende Format: CREATE_V2DB =\<-Pfadname >\<optional Sortierreihenfolge >, wobei der Name des Pfads den vollständigen Pfad zu einer Microsoft Access-Datenbank ist. Wenn der Pfadname eine vorhandene Datenbank angibt, wird ein Fehler zurückgegeben werden. Die Sortierreihenfolge wird oben festgelegt im Dialogfeld neue Datenbank angezeigt, wenn die Schaltfläche "erstellen" in das Setup für Microsoft Access-Dialogfeld gedrückt wird. Wenn keine Sortierreihenfolge angegeben ist, wird allgemein verwendet.<br /><br /> Wenn Sie das Schlüsselwort CREATE_V2DB in derselben Anweisung mit einem DSN-Schlüsselwort verwenden, ignoriert diese Treiber das DSN-Schlüsselwort. Daher ist eine Datenbank erstellen und Angeben von einem DSN ein zweistufiger Prozess.<br /><br /> Wenn das Schlüsselwort CREATE_V2DB verwenden der Pfadnamen der Microsoft Access-Datenbank erstellt werden ein oder mehrere Leerzeichen enthält, muss dann der gesamte Pfadnamen durch doppelte Anführungszeichen eingeschlossen werden wie in den folgenden Beispielen gezeigt:<br /><br /> "C:\PROGRAM FILES\COMMON c:\programme\ MyAccess.mdb"<br /><br /> "C:\Programme\Microsoft FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (es werden keine Anführungszeichen erforderlich)|  
|DBQ|Der Name der Datenbankdatei.<br /><br /> Dadurch wird die gleiche Option als **Datenbank** im Dialogfeld "Setup".|  
|WERT|Die Pfadangabe zur Datenbankdatei.|  
|DESCRIPTION|Eine Beschreibung der Daten in der Datenquelle.<br /><br /> Dadurch wird die gleiche Option als **Beschreibung** im Dialogfeld "Setup".|  
|DRIVER|Die Pfadangabe an den Treiber-DLL.|  
|DRIVERID|Eine ganzzahlige ID für den Treiber.  25 (Microsoft Access)|  
|FIL|Dateityp MS Access für Microsoft Access|  
|IMPLICITCOMMITSYNC|Bestimmt, ob die Microsoft Access-Treiber intern oder implizite Commits asynchron ausgeführt wird. Dieser Wert wird anfangs festgelegt, auf "Ja", was bedeutet, dass der Microsoft Access-Treiber Commits in eine interne/implizite Transaktion abgeschlossen werden gewartet wird.<br /><br /> Der Wert dieser Option sollten nicht ohne sorgfältiger Überlegung der möglichen Konsequenzen geändert werden. Weitere Informationen zu dieser Option finden Sie unter der *Microsoft Jet-Datenbank-Engine-Programmiererhandbuch*.<br /><br /> Dadurch wird die gleiche Option als **ImplicitCommitSync** im Dialogfeld "Setup".|  
|MAXBUFFERSIZE|Die Größe des internen Puffers, in Kilobyte, die von Microsoft Access, zum Übertragen von Daten in und aus dem Datenträger verwendet wird. Die Standardpuffergröße beträgt 2048 KB, die (als 2048 angezeigt). Jeder ganzzahlige Wert teilbar von 256 kann verwendet werden. Dadurch wird die gleiche Option als **Puffergröße** im Dialogfeld "Setup".|  
|MAXSCANROWS|Die Anzahl der Zeilen, die beim Festlegen des Datentyps einer Spalte, die basierend auf vorhandenen Daten geprüft werden.<br /><br /> Eine Zahl zwischen 1 und 16 kann für die Zeilen eingegeben werden. Der Standardwert ist 8; Wenn es auf 0 festgelegt ist, werden alle Zeilen gescannt. (Eine Zahl außerhalb der Grenzwert wird einen Fehler zurückgegeben.)<br /><br /> Dadurch wird die gleiche Option als **zu scannende Zeilen** im Dialogfeld "Setup".|  
|' PAGETIMEOUT '|Gibt die Zeitspanne in Millisekunden, die eine Seite (sofern nicht verwendet) in den Puffer bleibt, bevor Sie entfernt werden. Der Standardwert beträgt fünf-Zehntelsekunden (0,5 Sekunden). Beachten Sie, dass diese Option für alle Datenquellen gilt, die den ODBC-Treiber verwenden.<br /><br /> Dadurch wird die gleiche Option als **Page Timeout** im Dialogfeld "Setup".|  
|PWD|Das Kennwort.|  
|READONLY|True, um die Datei schreibgeschützt machen. "False", um die Datei nicht schreibgeschützt sein.<br /><br /> Dadurch wird die gleiche Option als **Read Only** im Dialogfeld "Setup".|  
|REPAIR_DB|Repariert eine Datenbank beschädigt durch einen Fehler, der während der Commitvorgang auftritt.<br /><br /> Wenn Sie das Schlüsselwort REPAIR_DB in derselben Anweisung mit einem DSN-Schlüsselwort verwenden, ignoriert diese Treiber das DSN-Schlüsselwort. Deshalb ist die Reparatur einer Datenbank und Angeben von einem DSN ein zweistufiger Prozess.|  
|SYSTEMDB|Für die Microsoft Access-Treiber die Pfadangabe in der System-Datenbankdatei.<br /><br /> Dadurch wird die gleiche Option als **Systemdatenbank** im Dialogfeld "Setup".|  
|THREADS|Die Anzahl der Hintergrundthreads für das Modul nutzen. Dieser Wert kann wird standardmäßig auf 3, jedoch geändert werden.<br /><br /> Dadurch wird die gleiche Option als **Threads** im Dialogfeld "Setup".|  
|UID|Microsoft Access-Treiber für die Anmeldung verwendeten Benutzer-ID-Namen.|  
|USERCOMMITSYNC|Bestimmt, ob die Microsoft Access-Treiber eine benutzerdefinierte Transaktionen asynchron durchführen. Dieser Wert wird anfangs festgelegt, auf "Ja", was bedeutet, dass der Microsoft Access-Treiber in einer benutzerdefinierten Transaktion ausgeführt werden Commits wartet.<br /><br /> Der Wert dieser Option sollten nicht ohne sorgfältiger Überlegung der möglichen Konsequenzen geändert werden. Weitere Informationen zu dieser Option finden Sie unter der *Microsoft Jet-Datenbank-Engine-Programmiererhandbuch*.<br /><br /> Dadurch wird die gleiche Option als **UserCommitSync** im Dialogfeld "Setup".|
