---
title: Anhang - 1 (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e01f8be5-ce68-4c9f-bd13-d65e73a16470
caps.latest.revision: "15"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 8e415cb8fddf1a2c37fa44f38ff23a2c5c64c568
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="appendix---1-oracletosql"></a>Anhang - 1 (OracleToSQL)
Kurze Übersicht über die Befehlszeilenoptionen SSMA-Konsole:  
  
|"SL". Nein.|Schalter|Erforderlich?|Switch-Argument|Zulässige Werte|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s-Skript|ja|scriptfile|XML-Dateiname ist ungültig.<br /><br />-Konsole Definition Skriptdatei an.|  
|2|-V-variable|nein|variablevaluefile|XML-Dateiname ist ungültig.<br /><br />Wenn Variablen in einer Skriptdatei verwendet werden, muss diese Datei angegeben werden.|  
|3|-c/serverconnection|nein|serverconnectionfile|XML-Dateiname ist ungültig.<br /><br />Diese Datei enthält Informationen zur Serververbindung.|  
|4|X-/ Xmloutput|nein|xmloutputfile|Diese Option gibt die Konsolenausgabe in das XML-Format an. Wenn diese Option nicht angegeben ist, wird die standardmäßigen Ausgabe im Textformat.<br /><br />Wenn Xmloutputfile nicht angegeben ist, wird ein XML-Ausgabe weitergeleitet, damit `STDOUT`.<br /><br />Xmloutputfile ist der Name der Datei, die in die Konsolenausgabe in das XML-Format geschrieben wird.|  
|5|-l/log|nein|logfile|Der Dateiname ist ungültig.|  
|6|-e/projectenvironment|nein|projectenvironmentfolder|Gültigen Ordnernamen an, die Dateien der SSMA-Projekt enthält.|  
|7|-p/securepassword|nein|-a/hinzufügen {< Server_id > [,... n] &#124; alle} – c &#124; Serverconnection < Server-Verbindungsdatei > [-V &#124; Variable < Variable-Wert-Datei >] [-o/overwrite]<br /><br />oder<br /><br />-a/hinzufügen {< Server_id > [,... n] &#124; alle} – s &#124; Skript < Skriptdatei > [-V &#124; Variable < Variable-Wert-Datei >] [-o/overwrite]<br /><br />– R Reparaturprogramm {< Server_id > [,... n] &#124; alle}<br /><br />-l/list<br /><br />– e/Export {< Server-Id > [,... n] &#124; alle} < verschlüsselt-Kennwort - Datei ><br /><br />– i / importieren {< Server-Id > [,... n] &#124; alle} < verschlüsselt-Kennwort-Datei >|Wenn angegeben, muss diese Option nicht mit anderen Optionen kombiniert werden.<br /><br />Server-Id: eine eindeutige ID für einen Server {String} bereitgestellt<br /><br />Server-Verbindungsdatei: Server-Definitionsdatei (Serverconnectionfile oder Scriptfile).<br /><br />Variable-Wert-Datei: Es ist eine Variablendefinition-Datei und in Server-Verbindungsdatei verwendet.<br /><br />verschlüsselte Kennwortdatei: Es handelt sich ein Server Kennwörter-Datei mit benutzerdefinierten-Passphrase verschlüsselt.|  
|8|-?|nein|Nicht zutreffend|Nicht zutreffend|  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen der Konsole SSMA (Oracle)](http://msdn.microsoft.com/en-us/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
