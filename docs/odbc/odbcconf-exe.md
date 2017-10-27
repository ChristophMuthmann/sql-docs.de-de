---
title: ODBCCONF. EXE-DATEI | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db8ff09a2b77f51c97ab73d6d994e1e1b4dce2a1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="odbcconfexe"></a>ODBCCONF. EXE-DATEI
ODBCCONF.exe ist ein Befehlszeilentool, das Sie zum Konfigurieren der ODBC-Treiber und Namen von Datenquellen ermöglicht.  
  
> [!NOTE]  
>  ODBCCONF.exe wird in einer zukünftigen Version von Windows Data Access Components entfernt werden. Verwenden Sie diese Funktion, und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Sie können PowerShell-Befehle zum Verwalten von Treibern und Datenquellen verwenden. Weitere Informationen zu diesen PowerShell-Befehlen finden Sie unter [Windows Data Access Components Cmdlets](https://technet.microsoft.com/library/hh771019.aspx).  
  
## <a name="syntax"></a>Syntax  
  
```  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>Argumente  
 *Switches*  
 0 (null) oder mehrere Switch-Optionen. Die Liste der verfügbaren Befehlszeilenoptionen finden Sie unter dem Abschnitt "Hinweise" weiter unten in diesem Thema.  
  
 *Aktion*  
 Eine Aktion ausführen. Finden Sie für die Liste der verfügbaren Optionen im Abschnitt "Hinweise".  
  
## <a name="remarks"></a>Hinweise  
 Die folgenden Optionen sind verfügbar:  
  
|Schalter|Description|  
|------------|-----------------|  
|/ A {*Aktion*}|Geben Sie eine Aktion.<br /><br /> / A ist optional, wenn nur eine Aktion angegeben wird.|  
|/?|Syntax für ODBCCONF anzeigen. EXE-DATEI.|  
|/ C|Verarbeitung wird fortgesetzt, wenn eine Aktion ein Fehler auftritt.|  
|/E|Löschen Sie die Antwortdatei mit/f angegeben wird, wenn die Verarbeitung beendet wird.|  
|/F|Verwenden Sie eine Antwortdatei, z. B. `odbcconf /F my.rsp`.<br /><br /> My.rsp kann wie folgt aussehen:`REGSVR c:\my.dll`<br /><br /> / A wird in einer Antwortdatei nicht verwendet.|  
|/H|Zeigen Sie Verbrauch (Hilfe). Diese Option ist identisch mit /?.|  
|/ L [*Modus*] *Dateiname*|Senden von Ausgabe in eine Datei in einem von drei Modi: Normal (n), verbose (V) und Debug (d). Das Debuggen des Modus zeichnet die DLLs, die von odbcconf.exe geladen werden.<br /><br /> Wenn Sie/l ohne einen Modus angeben, wird die Protokolldatei leer sein.<br /><br /> Beispielsweise **LV log.txt**.|  
|/R|Die Aktion wird nach einem Neustart ausgeführt werden.|  
|/S|Unbeaufsichtigter Modus. Fehlermeldungen werden nicht angezeigt werden.|  
  
 Die folgenden Aktionen sind verfügbar:  
  
|Aktion|Description|  
|------------|-----------------|  
|CONFIGDRIVER *Treibername**Params-Treiber-spezifischen Konfigurationsaufgaben*|Lädt die Setup-DLL für geeigneter Treiber und ruft die **ConfigDriver** Funktion.<br /><br /> Entspricht der [SQLConfigDriver Funktion](../odbc/reference/syntax/sqlconfigdriver-function.md).<br /><br /> Beispiel:<br /><br /> / A {CONFIGDRIVER "Treibername" "CPTimeout = 60"}<br /><br /> / A {CONFIGDRIVER "Treibername" "DriverODBCVer 03.80 ="}|  
|CONFIGDSN *Treibername* DSN =*Namen* &#124; *Attribute*|Fügt oder eine Systemdatenquelle ändert.<br /><br /> Entspricht der [SQLConfigDataSource-Funktion](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Beispiel:<br /><br /> / A {CONFIGDSN "SQLServer" "DSN = Name &#124; Server Srv = "}|  
|CONFIGSYSDSN *Treibername* DSN =*Namen* &#124; *Attribute*|Fügt oder eine Systemdatenquelle ändert.<br /><br /> Entspricht der [SQLConfigDataSource-Funktion](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Beispiel:<br /><br /> / A {CONFIGSYSDSN "SQLServer" "DSN = Name &#124; Server Srv = "}|  
|INSTALLDRIVER|Entspricht [SQLInstallDriverEx Funktion](../odbc/reference/syntax/sqlinstalldriverex-function.md).<br /><br /> Weitere Informationen über die Syntax der Schlüsselwort-Wert-Paare an INSTALLDRIVER übergeben, finden Sie unter [Treiber Spezifikation Unterschlüssel](../odbc/reference/install/driver-specification-subkeys.md).<br /><br /> Beispiel:<br /><br /> / A {INSTALLDRIVER "des Treibers &#124; Driver=c:\Your.dll &#124; Setup=c:\Your.dll &#124; APILevel = 2 &#124; ConnectFunctions = YYY &#124; DriverODBCVer = 03.50 &#124; FileUsage = 0 &#124; SQLLevel = 1"}|  
|INSTALLTRANSLATOR *Konvertierer Konfiguration**Treiberpfad*|Fügt Informationen über eine konvertierers, damit die **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC Übersetzer** Registrierungsschlüssel.<br /><br /> Entspricht [SQLInstallTranslatorEx Funktion](../odbc/reference/syntax/sqlinstalltranslatorex-function.md).<br /><br /> Weitere Informationen über die Syntax der Schlüsselwort-Wert-Paare an INSTALLDRIVER übergeben, finden Sie unter [Konvertierer Spezifikation Unterschlüssel](../odbc/reference/install/translator-specification-subkeys.md).<br /><br /> Beispiel:<br /><br /> / A {INSTALLTRANSLATOR "Meine Konvertierer &#124; Translator=c:\My.dll &#124; Setup=c:\My.dll"}|  
|REGSVR *Dll*|Registriert eine DLL.<br /><br /> Regsvr32.exe entspricht.<br /><br /> Beispiel:<br /><br /> / A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|Wenn HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. INI\ODBC Datei DSN\DefaultDSNDir ist nicht vorhanden, die SETFILEDSNDIR-Aktion erstellt, und weisen sie den Wert am HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir, \ODBC\Data Quellen angefügt.<br /><br /> Der Wert im HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. INI\ODBC Datei DSN\DefaultDSNDir gibt den Standardspeicherort von ODBC-Datenquellen-Administrator verwendet, wenn eine Datei basierende Datenquelle erstellen.<br /><br /> Beispiel:<br /><br /> / A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Open Database Connectivity (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)

