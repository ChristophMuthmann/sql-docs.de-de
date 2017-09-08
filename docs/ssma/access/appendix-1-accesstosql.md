---
title: Anhang - 1 (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4885ae2592285cdd1e948810de7c1e786afb9134
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="appendix---1-accesstosql"></a>Anhang - 1 (AccessToSQL)
Kurze Übersicht über die Befehlszeilenoptionen SSMA-Konsole:  
  
|"SL". Nein.|Schalter|Erforderlich?|Switch-Argument|Zulässige Werte|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s-Skript|ja|scriptfile|XML-Dateiname ist ungültig.<br /><br />-Konsole Definition Skriptdatei an.|  
|2|-V-variable|Nein|variablevaluefile|XML-Dateiname ist ungültig. Wenn Variablen in einer Skriptdatei verwendet werden, muss diese Datei angegeben werden.|  
|3|-c/serverconnection|Nein|serverconnectionfile|XML-Dateiname ist ungültig. Diese Datei enthält Informationen zur Serververbindung.|  
|4|X-/ Xmloutput|Nein|xmloutputfile|Diese Option gibt die Konsolenausgabe in das XML-Format an. Wenn diese Option nicht angegeben ist, wird die standardmäßigen Ausgabe im Textformat.<br /><br />Wenn Xmloutputfile nicht angegeben ist, wird die XML-Ausgabe an "stdout" umgeleitet.<br /><br />Xmloutputfile ist der Name der Datei, die in die Konsolenausgabe in das XML-Format geschrieben wird.|  
|5|-l/log|Nein|logfile|Der Dateiname ist ungültig.|  
|6|-e/projectenvironment|Nein|projectenvironmentfolder|Gültigen Ordnernamen an, die Dateien der SSMA-Projekt enthält.|  
|7|-p/securepassword|Nein|-a/hinzufügen {< Server_id > [,... n] &#124; alle} – c &#124; Serverconnection < Server-Verbindungsdatei > [-V &#124; Variable < Variable-Wert-Datei >] [-o/overwrite]<br /><br />oder<br /><br />-a/hinzufügen {< Server_id > [,... n] &#124; alle} – s &#124; Skript < Skriptdatei > [-V &#124; Variable < Variable-Wert-Datei >] [-o/overwrite]<br /><br />– R Reparaturprogramm {< Server_id > [,... n] &#124; alle}<br /><br />-l/list<br /><br />– e/Export {< Server-Id > [,... n] &#124; alle} < verschlüsselt-Kennwort - Datei ><br /><br />– i / importieren {< Server-Id > [,... n] &#124; alle} < verschlüsselt-Kennwort-Datei >|Wenn angegeben, muss diese Option nicht mit anderen Optionen kombiniert werden.<br /><br />Server-Id: eine eindeutige ID für einen Server {String} bereitgestellt<br /><br />Server-Verbindungsdatei: Server-Definitionsdatei (Serverconnectionfile oder Scriptfile).<br /><br />Variable-Wert-Datei: Es ist eine Variablendefinition-Datei und in Server-Verbindungsdatei verwendet.<br /><br />verschlüsselt ein Kennwort – Datei: eine Datei mit Servern Kennwörter verschlüsselt mit einer Passphrase Benutzer angegeben ist.|  
|8|-?|Nein|Nicht zutreffend|Nicht zutreffend|  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen der Konsole SSMA (Access)](http://msdn.microsoft.com/en-us/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  

