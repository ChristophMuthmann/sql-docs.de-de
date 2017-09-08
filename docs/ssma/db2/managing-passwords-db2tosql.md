---
title: "Verwalten von Kennwörtern (DB2ToSQL) | Microsoft Docs"
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
ms.assetid: 56d546e3-8747-4169-aace-693302667e94
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7135e7c69f202ce81ebe19c8f31ff3cc50944cb7
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="managing-passwords-db2tosql"></a>Verwalten von Kennwörtern (DB2ToSQL)
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
  
        -   Führen Sie die `SSMAforDB2Console.exe` mit der `–securepassword` und Schalter an die Befehlszeile übergeben den Server Verbindung oder Skript-Datei mit dem kennwortknoten im Abschnitt Definition Server hinzufügen.  
  
        -   An der Eingabeaufforderung wird der Benutzer gebeten, geben das Datenbankkennwort, und bestätigen Sie es.  
  
            Die Server-Definition-Ids und ihre entsprechenden verschlüsselte Kennwörter werden in einer Datei auf dem lokalen Computer gespeichert.  
            
            Beispiel 1:
            
                Specify password
                C:\SSMA\SSMAforDB2Console.EXE –securepassword –add all –s "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\AssessmentReportGenerationSample.xml" –v "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx
            
            Beispiel 2:
            
                C:\SSMA\SSMAforDB2Console.EXE –securepassword –add "source_1,target_1" –c "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\ServersConnectionFileSample.xml" – v "D:\Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
    
    -   **Verschlüsselte Kennwörter entfernen**  
  
        Führen Sie die `SSMAforDB2Console.exe` mit der`–securepassword` und `–remove` -Schalter an der Befehlszeile übergeben die Server-Ids, um die verschlüsselte Kennwörter aus der geschützten Speicher-Datei vorhanden auf dem lokalen Computer zu entfernen.  
  
        Beispiel:  
        
            C:\SSMA\SSMAforDB2Console.EXE –securepassword –remove all
            C:\SSMA\SSMAforDB2Console.EXE –securepassword –remove "source_1,target_1"  
  
    -   **Auflisten von Server-Ids, deren Kennwörter verschlüsselt werden**  
  
        Führen Sie die `SSMAforDB2Console.exe` mit der `–securepassword` und `–list` -Schalter an der Befehlszeile angeben, um die Server-Ids auflisten, deren Kennwörter verschlüsselt wurden.  
  
        Beispiel:  
        
            C:\SSMA\SSMAforDB2Console.EXE –securepassword –list  

  
    > [!NOTE]  
    > 1.  Das Kennwort in Klartext im Skript oder Server-Verbindungsdatei erwähnten Vorrang vor das verschlüsselte Kennwort in gesicherte Datei.  
    > 2.  Wenn kein Kennwort im Abschnitt "Server" des Server-Verbindungsdatei oder die Skriptdatei vorhanden ist, oder wenn sie nicht auf dem lokalen Computer gesichert wurden, werden Sie von die Konsole aufgefordert, das Kennwort einzugeben.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportieren oder importieren verschlüsselte Kennwörter  
Die SSMA-Konsolenanwendung können Sie verschlüsselte Datenbankkennwörter in einer Datei auf dem lokalen Computer vorhanden, eine geschützte Datei und umgekehrt zu exportieren. Sie können darin, die verschlüsselte Kennwörter Maschine unabhängig. Exportfunktion liest die Server-Id und Kennwort vom lokalen Speicher geschützt und speichert die Informationen in einer verschlüsselten Datei. Der Benutzer wird aufgefordert, das Kennwort für die geschützte Datei eingeben. Stellen Sie sicher, dass das eingegebene Kennwort Zeichenlänge von 8 oder mehr ist. Diese gesicherte Datei ist auf verschiedenen Computern übertragbar. Importfunktion liest die Server-Id und Kennwort aus der gesicherten Datei. Der Benutzer wird aufgefordert, geben das Kennwort für die geschützte Datei und fügt die Informationen in den geschützten lokalen Speicher.  
  
Beispiel:  

    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforDB2Console.EXE –securepassword –export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforDB2Console.EXE –p –e "DB2DB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
Beispiel:  

    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforDB2Console.EXE –securepassword –import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforDB2Console.EXE –p –i "DB2DB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx

  
## <a name="see-also"></a>Siehe auch  
[Ausführen der SSMA-Konsole](http://msdn.microsoft.com/en-us/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  

