---
title: Desktop-Treiber Datenbankarchitektur | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f5c7b12e5413441476e70dc63fe9d3da9284635
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="desktop-database-drivers-architecture"></a>Desktop-Treiber-Datenbankarchitektur
Diese Treiber sind für die Verwendung auf Microsoft Windows 95 oder höher oder Windows NT 4.0 oder Windows 2000 vorgesehen. Nur 32-Bit-Anwendungen werden unter Windows 95 oder höher unterstützt. 16-Bit- und 32-Bit-Anwendungen werden unter Windows NT 4.0 und Windows 2000 unterstützt.  
  
> [!NOTE]  
>  Informationen über die Version von ODBC mit diese Treiber verwendet werden soll, finden Sie in der *ODBC Programmer's Reference*, und die letzten und aktuellen Versionshinweise. Mit Ausnahme der angegebenen Bereiche sind diese Treiber mit der *ODBC Programmer's Reference*.  
  
 Der ODBC-Datenbanktreiber Desktop enthalten 32-Bit-Treiber für Microsoft Access, dBASE, Microsoft Excel, Paradox und Text. Es sind keine 16 - Bit-Treiber enthalten. (Ein Treiber für Microsoft FoxPro steht getrennt.)  
  
 Die Anwendung/Treiberarchitektur unter Windows 95 oder höher ist:  
  
 ![App &#47; Treiberarchitektur: Windows 95 und höher](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Die Verwendung dieser Treiber von 16-Bit-Anwendungen unter Windows 95 wird nicht unterstützt.  
  
 Die Anwendung/Treiberarchitektur unter Windows NT 4.0 und Windows 2000 ist:  
  
 ![App &#47; Treiberarchitektur: NT 4.0 oder Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 Der Desktop-Datenbanktreiber sind zwei Ebenen-Treiber. In einer Konfiguration mit zwei Ebenen führt der Treiber nicht den Prozess der Analyse, Überprüfung, optimieren und Ausführen der Abfrage aus. Stattdessen führt Microsoft Jet diese Aufgaben. Er verarbeitet die ODBC-API-Aufrufe und fungiert als eine SQL-Datenbankmodul. Microsoft Jet geworden ist ein integraler, untrennbar Teil der Treiber: Es wird mit dem Treiber geliefert und mit dem Treiber befindet, auch wenn keine andere Anwendung auf dem Computer verwendet wird.  
  
 Der Desktop-Datenbanktreiber bestehen aus sechs verschiedenen Treiber – oder genauer gesagt, eine Treiberdatei (Odbcjt32.dll), die die ODBC [Treibermanager](../../odbc/reference/the-driver-manager.md) sechs unterschiedlich verwendet. Das DRIVERID-Flag in der Registrierung für eine Datenquelle bestimmt, welcher Treiber in Odbcjt32.dll der Treiber-Manager verwendet. Eine Anwendung übergibt dieses Flag in der Verbindungszeichenfolge enthalten, die in einem Aufruf von **SQLDriverConnect**. Standardmäßig ist das Flag für die ID des Treibers für Microsoft Access.  
  
 Der Setup-Datei des Treibers ändert das DRIVERID-Flag beim Setup. Alle Treiber außer dem Microsoft Access-Treiber haben eine zugeordnete Setup-DLL. Beim Klicken auf **Setup** in der [Microsoft ODBC-Datenquellen-Administrator](../../odbc/admin/odbc-data-source-administrator.md) für eine Datenquelle, lädt der ODBC-Installer-DLL (die Datei Odbcinst.dll) der Setup-DLL. Der Setup-DLL exportiert die ODBC-Installer-Funktion **SQLConfigDataSource**. Wenn ein Fensterhandle, um übergeben wird **SQLConfigDataSource**, diese Funktion zeigt ein Setup-Fenster und ändert die Kennzeichnung DRIVERID gemäß den Treiber, die über die Benutzeroberfläche ausgewählt.  
  
 Wenn eine Datei programmgesteuert erstellt wird, wird ein NULL-Fensterhandle an übergeben **SQLConfigDataSource**, und die Funktion erstellt eine Datenquelle dynamisch, ändern das Flag DRIVERID gemäß der *LpszDriver*Argument im Funktionsaufruf.  
  
 Odbcjt32.dll implementiert ODBC-Funktionen auf der Microsoft Jet-API. Es ist jedoch keine direkte Zuordnung zwischen ODBC und Microsoft Jet-Funktionen. Viele Faktoren, z. B. die Cursormodelle und SQL-Zuordnung zu verhindern, dass eine direkte Korrelation der Funktionen.  
  
 Der ODBC-Treiber befindet sich zwischen dem Microsoft Jet-Datenbankmodul und der ODBC-Treiber-Manager. Einige ODBC-Funktionen, die von einer Anwendung aufgerufen werden vom Treiber-Manager behandelt und nicht an den Treiber übergeben. Für diese Funktionen sieht Microsoft Jet nie die Funktion aufgerufen werden, da sie nicht über eine direkte Verbindung zu der Treiber-Manager verfügt.
