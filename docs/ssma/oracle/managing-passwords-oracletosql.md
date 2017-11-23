---
title: "Verwalten von Kennwörtern (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Managing Passwords in Oracle, Exporting or Importing Encrypted Password
- Managing passwords in Oracle, Securing Password
ms.assetid: 8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c
caps.latest.revision: "24"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 1360c23595b7ff81180352795f0a78ded3efd583
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="managing-passwords-oracletosql"></a>Verwalten von Kennwörtern (OracleToSQL)
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
  
        -   Führen Sie die `SSMAforOracleConsole.exe` mit der `–securepassword` und Schalter an die Befehlszeile übergeben den Server Verbindung oder Skript-Datei mit dem kennwortknoten im Abschnitt Definition Server hinzufügen.  
  
        -   An der Eingabeaufforderung wird der Benutzer gebeten, geben das Datenbankkennwort, und bestätigen Sie es.  
  
            Die Server-Definition-Ids und ihre entsprechenden verschlüsselte Kennwörter werden in einer Datei auf dem lokalen Computer gespeichert.  
            
            Beispiel 1:  
            
                Specify password
                
                C:\SSMA\SSMAforOracleConsole.EXE –securepassword –add all –s "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\AssessmentReportGenerationSample.xml" –v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            Beispiel 2:
            
                C:\SSMA\SSMAforOracleConsole.EXE –securepassword –add "source_1,target_1" –c "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ServersConnectionFileSample.xml" – v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
    
    -   **Verschlüsselte Kennwörter entfernen**  
  
        Führen Sie die `SSMAforOracleConsole.exe` mit der`–securepassword` und `–remove` -Schalter an der Befehlszeile übergeben die Server-Ids, um die verschlüsselte Kennwörter aus der geschützten Speicher-Datei vorhanden auf dem lokalen Computer zu entfernen.  
        
        Beispiel:  
        
            C:\SSMA\SSMAforOracleConsole.EXE –securepassword –remove all
            C:\SSMA\SSMAforOracleConsole.EXE –securepassword –remove "source_1,target_1"  
  
    -   **Auflisten von Server-Ids, deren Kennwörter verschlüsselt werden**  
  
        Führen Sie die `SSMAforOracleConsole.exe` mit der `–securepassword` und `–list` -Schalter an der Befehlszeile angeben, um die Server-Ids auflisten, deren Kennwörter verschlüsselt wurden.  
  
        Beispiel:  
        
            C:\SSMA\SSMAforOracleConsole.EXE –securepassword –list  
  
    > [!NOTE]  
    > 1.  Das Kennwort in Klartext im Skript oder Server-Verbindungsdatei erwähnten Vorrang vor das verschlüsselte Kennwort in gesicherte Datei.  
    > 2.  Wenn kein Kennwort im Abschnitt "Server" des Server-Verbindungsdatei oder die Skriptdatei vorhanden ist, oder wenn sie nicht auf dem lokalen Computer gesichert wurden, werden Sie von die Konsole aufgefordert, das Kennwort einzugeben.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportieren oder importieren verschlüsselte Kennwörter  
Die SSMA-Konsolenanwendung können Sie verschlüsselte Datenbankkennwörter in einer Datei auf dem lokalen Computer vorhanden, eine geschützte Datei und umgekehrt zu exportieren. Sie können darin, die verschlüsselte Kennwörter Maschine unabhängig. Exportfunktion liest die Server-Id und Kennwort vom lokalen Speicher geschützt und speichert die Informationen in einer verschlüsselten Datei. Der Benutzer wird aufgefordert, das Kennwort für die geschützte Datei eingeben. Stellen Sie sicher, dass das eingegebene Kennwort Zeichenlänge von 8 oder mehr ist. Diese gesicherte Datei ist auf verschiedenen Computern übertragbar. Importfunktion liest die Server-Id und Kennwort aus der gesicherten Datei. Der Benutzer wird aufgefordert, geben das Kennwort für die geschützte Datei und fügt die Informationen in den geschützten lokalen Speicher.  
  
Beispiel:  

    Export password
    
    Enter password for protecting the exported file C:\SSMA\SSMAforOracleConsole.EXE –securepassword –export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforOracleConsole.EXE –p –e "OracleDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
Beispiel:  

    Import an encrypted password
    
    Enter password for protecting the imported file C:\SSMA\SSMAforOracleConsole.EXE –securepassword –import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforOracleConsole.EXE –p –i "OracleDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen der Konsole SSMA (Oracle)](http://msdn.microsoft.com/en-us/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
