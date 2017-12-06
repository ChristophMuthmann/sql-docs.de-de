---
title: "Verwalten von Kennwörtern (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: b099d0f9-dd37-4c87-8b6f-ed0177881ea4
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb6fa242f2dce4d5a6eb3d96d620f663ce4883e5
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="managing-passwords-accesstosql"></a>Verwalten von Kennwörtern (AccessToSQL)
In diesem Abschnitt wird zum Schützen von Datenbankkennwörter und das Verfahren zum Importieren oder exportieren Sie sie über Server:  
  
1.  Sichern von Kennwort  
  
2.  Exportieren oder importieren verschlüsseltes Kennwort  
  
## <a name="securing-password"></a>Sichern von Kennwort  
SSMA können Sie Ihr Kennwort von einer Datenbank zu sichern.  
  
Verwenden Sie wie folgt vor, um eine sichere Verbindung zu implementieren:  
  
Geben Sie ein gültiges Kennwort ein, die mit einer der drei folgenden Methoden:  
  
1.  **Klartext:** Geben Sie das Datenbankkennwort, in der Value-Attribut des Knotens "Kennwort". Finden sie unter dem Serverknoten der Definition im Abschnitt "Server" des Server-Verbindungsdatei oder Skriptdatei.  
  
    Kennwörter in Klartext sind nicht sicher. Aus diesem Grund tritt die folgende Warnmeldung in der Konsolenausgabe: *"Server &lt;Server-Id&gt; Kennwort wird in Klartext unsicher, SSMA-Konsolenanwendung bietet eine Option aus, um das Kennwort durch Verschlüsselung zu schützen, finden Sie die Option" – Securepassword "in SSMA-Hilfedatei für Weitere Informationen."*  
  
    **Verschlüsselte Kennwörter:** das angegebene Kennwort ist in diesem Fall in verschlüsselter Form auf dem lokalen Computer im ProtectedStorage.ssma gespeichert.  
  
    -   **Sichern von Kennwörtern**  
  
        -   Führen Sie die `SSMAforAccessConsole.exe` mit der `–securepassword` und Schalter an die Befehlszeile übergeben den Server Verbindung oder Skript-Datei mit dem kennwortknoten im Abschnitt Definition Server hinzufügen.  
  
        -   An der Eingabeaufforderung wird der Benutzer gebeten, geben das Datenbankkennwort, und bestätigen Sie es.  
  
            Die Server-Definition-Ids und ihre entsprechenden verschlüsselte Kennwörter werden in einer Datei auf dem lokalen Computer gespeichert.  
  
            Beispiel 1:
            
                Specify password
                
                C:\SSMA\SSMAforAccessConsole.EXE –securepassword –add all –s "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" –v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx  
            
            Beispiel 2:
            
                C:\SSMA\SSMAforAccessConsole.EXE –securepassword –add "source_1,target_1" –c "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml" – v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
  
    -   **Verschlüsselte Kennwörter entfernen**  
  
        Führen Sie die `SSMAforAccessConsole.exe` mit der`–securepassword` und `–remove` -Schalter an der Befehlszeile übergeben die Server-Ids, um die verschlüsselte Kennwörter aus der geschützten Speicher-Datei vorhanden auf dem lokalen Computer zu entfernen.  
  
            C:\SSMA\SSMAforAccessConsole.EXE –securepassword –remove all
            C:\SSMA\SSMAforAccessConsole.EXE –securepassword –remove "source_1,target_1"  
  
    -   **Auflisten von Server-Ids, deren Kennwörter verschlüsselt werden**  
  
        Führen Sie die SSMAforAccessConsole.exe mit der `–securepassword` und `–list` -Schalter an der Befehlszeile angeben, um die Server-Ids auflisten, deren Kennwörter verschlüsselt wurden.  
  
            C:\SSMA\SSMAforAccessConsole.EXE –securepassword –list  
  
    > [!NOTE]  
    > 1.  Das Kennwort in Klartext im Skript oder Server-Verbindungsdatei erwähnten Vorrang vor das verschlüsselte Kennwort in gesicherte Datei.  
    > 2.  Wenn kein Kennwort im Abschnitt "Server" des Server-Verbindungsdatei oder die Skriptdatei vorhanden ist, oder wenn sie nicht auf dem lokalen Computer gesichert wurden, werden Sie von die Konsole aufgefordert, das Kennwort einzugeben.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportieren oder importieren verschlüsselte Kennwörter  
Die SSMA-Konsolenanwendung können Sie verschlüsselte Datenbankkennwörter in einer Datei auf dem lokalen Computer vorhanden, eine geschützte Datei und umgekehrt zu exportieren. Sie können darin, die verschlüsselte Kennwörter Maschine unabhängig. Exportfunktion liest die Server-Id und Kennwort vom lokalen Speicher geschützt und speichert die Informationen in einer verschlüsselten Datei. Der Benutzer wird aufgefordert, das Kennwort für die geschützte Datei eingeben. Stellen Sie sicher, dass das eingegebene Kennwort Zeichenlänge von 8 oder mehr ist. Diese gesicherte Datei ist auf verschiedenen Computern übertragbar. Importfunktion liest die Server-Id und Kennwort aus der gesicherten Datei. Der Benutzer wird aufgefordert, geben das Kennwort für die geschützte Datei und fügt die Informationen in den geschützten lokalen Speicher.  


    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforAccessConsole.EXE –securepassword –export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforAccessConsole.EXE –p –e "AccessDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  


    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforAccessConsole.EXE –securepassword –import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforAccessConsole.EXE –p –i "AccessDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen der Konsole SSMA (Access)](http://msdn.microsoft.com/en-us/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
