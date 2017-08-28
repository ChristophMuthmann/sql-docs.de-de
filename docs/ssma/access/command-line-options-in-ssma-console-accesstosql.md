---
title: Befehlszeilenoptionen in SSMA-Konsole (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
caps.latest.revision: 11
author: sabotta
ms.author: carlasab
manager: murato
ms.translationtype: MT
ms.sourcegitcommit: 80642503480add90fc75573338760ab86139694c
ms.openlocfilehash: 827257d90042aa1655545edd9fc20d114952f426
ms.contentlocale: de-de
ms.lasthandoff: 08/21/2017

---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>Befehlszeilenoptionen in der Konsole SSMA (AccessToSQL)
Microsoft stellt Ihnen eine Reihe robuster Befehlszeilenoptionen auszuführen und zu steuern SSMA-Aktivitäten. Die folgenden Abschnitte enthalten zusätzliche Details.  
  
## <a name="command-line-options-in-the-ssma-console"></a>In der Konsole SSMA Befehlszeilenoptionen  
Hierin beschriebenen sind die Konsole die Befehlsoptionen an.  
  
In diesem Abschnitt wird der Begriff "Option" auch als "Switch" bezeichnet.  
  
Optionen Groß-/Kleinschreibung nicht und integritätsdienststatus entweder mit der "**-**'oder'**/**" Zeichen.  
  
Wenn Optionen angegeben werden, ist es unbedingt erforderlich, dass Sie die entsprechende Optionsparameter angeben.  
  
Optionsparameter müssen vom Option Zeichen durch ein Leerzeichen voneinander getrennt werden.  
  
**Beispiele für die Abfrageausdruckssyntax:**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml” –v “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml” –c “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml”`  
  
Ordner oder eine Datei Namen, die Leerzeichen enthalten, sollte in doppelte Anführungszeichen angegeben werden.  
  
Die Ausgabe des Befehlszeilen-Einträge und Fehlermeldungen ist in "stdout" oder in einer angegebenen Datei gespeichert.  
  
### <a name="script-file-option-sscript"></a>Skript-Dateioption: – s-Skript  
Ein erforderlicher Parameter, der Pfad/Skriptdateiname gibt das Skript an der Befehlssequenzen SSMA ausgeführt werden soll.  
  
**Beispiele für die Abfrageausdruckssyntax:**  
  
`C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>Variablenwert-Dateioption: – V-Variable  
Die Wert der Variablen-Datei besteht aus Variablen, die in der Skriptdatei verwendet. Der Schalter ist optional. Wenn Variablen werden nicht im Oval-Variablendatei deklariert und in der Skriptdatei verwendet, wird die Anwendung generiert einen Fehler und beendet die Ausführung der Konsole.  
  
**Beispiele für die Abfrageausdruckssyntax:**  
  
-   Variablen, die in mehreren Variablenwert-Dateien, z. B. eins hat den Standardwert und ein anderes mit einem instanzspezifischen-Wert, sofern zutreffend, definiert werden. Der letzte in die Befehlszeilenargumente angegeben Variablendatei nimmt die Voreinstellung für den Fall, dass eine der Variablen Doppelung:  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>Server-Verbindung-Dateioption: – C/Serverconnection  
Diese Datei enthält die Serververbindungsinformationen für jeden Server. Jede Serverdefinition wird durch eine eindeutige Server-ID identifiziert. Die Server-IDs werden in der Skriptdatei für die Verbindung-bezogenen Befehlen auf die verwiesen wird.  
  
Serverdefinition kann ein Teil des Server-Verbindungsdatei und/oder Skriptdatei sein. Server-Id in der Skriptdatei hat Vorrang vor den Server-Verbindungsdatei, für den Fall, dass eine Duplizierung der Server-Id vorhanden ist.  
  
**Beispiele für die Abfrageausdruckssyntax:**  
  
-   Server-IDs werden in der Skriptdatei verwendet. Sie werden in einem separaten Server Verbindungsdatei definiert. Diese Datei verwendet Variablen, die in der Variablenwert-Datei definiert sind:  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   Serverdefinition wird in der Skriptdatei eingebettet:  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML-Ausgabe Option: - X / Xmloutput [Xmloutputfile]  
Mit diesem Befehl wird verwendet, für die Ausgabenachrichten Befehl in einem XML-Format an Konsole oder in eine XML-Datei ausgeben.  
  
Es stehen zwei Optionen für Xmloutput, nämlich:  
  
-   Wenn der Dateipfad nach dem Wechsel Xmloutput bereitgestellt wird, wird die Ausgabe in die Datei umgeleitet.  
  
    **Syntaxbeispiel:**  
  
    `C:\>SSMAforAccessConsole.EXE –s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   Wenn keine Filepath nach dem Wechsel Xmloutput bereitgestellt wird, wird die Xmlout auf der Konsole angezeigt.  
  
    **Syntaxbeispiel:**  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>Melden Sie sich-Dateioption: – l/Log  
Die SSMA-Vorgänge in der Konsolenanwendung werden in einer Protokolldatei aufgezeichnet, und der Schalter ist optional. Wenn eine Protokolldatei und der zugehörige Pfad in der Befehlszeile angegeben werden, ruft das Protokoll in der angegebenen Position generiert. Andernfalls ruft es an seinem Standardspeicherort generiert.  
  
**Syntaxbeispiel:**  
  
`C:\>SSMAforAccessConsole.EXE`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>Ordner Umgebungsoption Projekt: – e/Projectenvironment  
Diese optionale Schalter kennzeichnet den Projektordner für die Einstellungen von Umgebung für das aktuelle SSMA-Projekt.  
  
**Syntaxbeispiel:**  
  
`C:\>SSMAforAccessConsole.EXE –s`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
||  
|-|  
||  
  
### <a name="secure-password-option-psecurepassword"></a>Secure Password-Option: – p/Securepassword  
Diese Option gibt das verschlüsselte Kennwort für den Server-Verbindungen an. Es unterscheidet sich von alle anderen Optionen nicht allen möglichen Skripts ausführen oder Hilfe bei der Migration-bezogenen Aktivitäten, jedoch können verwalten kennwortverschlüsselung für die Server-Verbindungen, die in das Migrationsprojekt verwendet.  
  
Sie können nicht als den Befehlszeilenparameter beliebige andere Option oder ein Kennwort eingeben. Andernfalls führt dies zu einem Fehler. Weitere Informationen finden Sie unter der [Verwalten von Kennwörtern](http://msdn.microsoft.com/b099d0f9-dd37-4c87-8b6f-ed0177881ea4) Abschnitt.  
  
Unterstützt die folgenden Unteroptionen `–p/securepassword`:  
  
-   Hinzufügen eines Kennworts oder Aktualisieren eines vorhandenen Kennworts in geschützten Speicher für eine angegebene ID oder für alle Server-IDs, die in Server-Verbindungsdatei definiert:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   So entfernen Sie das verschlüsselte Kennwort aus dem geschützten Speicher, der die angegebene ID für den Server oder für alle Server-IDs:  
  
    `–p/securepassword –r/remove {<server_id> [, …n] | all}`  
  
-   Um eine Liste der Server-IDs anzuzeigen, für die das Kennwort verschlüsselt wird:  
  
    `–p/securepassword –l/list`  
  
-   So exportieren Sie die Kennwörter im geschützten Speicher zu einer verschlüsselten Datei gespeichert. Diese Datei ist mit benutzerdefinierten-Passphrase verschlüsselt.  
  
    `–p/securepassword –e/export {<server-id> [, …n] | all} <encrypted-password -file>`  
  
-   Verschlüsselt-Datei, die zuvor exportierte wird in den lokalen geschützten Speicher, die mit der Passphrase benutzerdefiniertes importiert. Nachdem die Datei entschlüsselt wird, wird es in einer neuen Datei gespeichert, die wiederum auf dem lokalen Computer verschlüsselt ist.  
  
    `–p/securepassword –i/import {<server-id> [, …n] | all} <encrypted-password -file>`  
  
    Mehrere Server-IDs können mithilfe von Kommas – als Trennzeichen angegeben werden.  
  
### <a name="help-option-help"></a>Hilfe-Option: –? / Help  
Zeigt eine syntaxzusammenfassung der Optionen SSMA-Konsole:  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
Einer tabellarischen Ansicht der Befehlszeilenoptionen SSMA-Konsole finden Sie unter [Anhang - 1 &#40; AccessToSQL &#41; ](../../ssma/access/appendix-1-accesstosql.md).  
  
### <a name="securepassword-help-option-securepassword--help"></a>Option SecurePassword Hilfe: – Securepassword-? / Help  
Zeigt eine syntaxzusammenfassung der Optionen SSMA-Konsole:  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
Einer tabellarischen Ansicht der Befehlszeilenoptionen SSMA-Konsole finden Sie unter [Anhang - 1 &#40; AccessToSQL &#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>Nächste Schritte  
Der nächste Schritt hängt davon ab, auf die Anforderungen Ihres Projekts:  
  
1.  Zur Angabe eines Kennworts oder einer Exportieren / Importieren von Kennwörtern, finden Sie unter [Verwalten von Kennwörtern &#40; AccessToSQL &#41; ](../../ssma/access/managing-passwords-accesstosql.md).  
  
2.  Generieren von Berichten, finden Sie unter [Generieren von Berichten &#40; AccessToSQL &#41; ](../../ssma/access/generating-reports-accesstosql.md).  
  
3.  Behandlung von Problemen in der Konsole, finden Sie unter [Problembehandlung &#40; AccessToSQL &#41; ](../../ssma/access/troubleshooting-accesstosql.md).  
  

