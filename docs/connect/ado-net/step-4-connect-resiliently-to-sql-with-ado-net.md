---
title: 'Schritt 4: Herstellen belastbarer SQL mit ADO.NET | Microsoft Docs'
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8985e162d0a1d72d2ca655be26b6c5c1a1607358
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>Schritt 4: Herstellen Sie belastbarer SQL mit ADO.NET

- Vorherigen Artikel:&nbsp;&nbsp;&nbsp;[Schritt 3: Herstellen einer Verbindung mit SQL mithilfe von ADO.NET Machbarkeitsstudie](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
Dieses Thema enthält ein C#-Codebeispiel zur Veranschaulichung der benutzerdefinierten Wiederholungslogik. Die Wiederholungslogik bietet Zuverlässigkeit. Die Wiederholungslogik dient zur temporären Fehler ordnungsgemäß verarbeiten oder *vorübergehende Fehler* die tendenziell behoben, wenn die Anwendung mehrere Sekunden und Wiederholungen wartet.  
  
Ursachen für vorübergehende Fehler sind:  
  
- Eine kurze Fehler der Netzwerke, die im Internet unterstützt.  
- Ein cloudsystem möglicherweise ihre Ressourcen im Moment abgefragten gesendet Lastenausgleich.  
  
  
Die ADO.NET-Klassen zum Herstellen einer Verbindung mit Ihrem lokalen Microsoft SQL Server können auch mit Azure SQL-Datenbank verbinden. Die ADO.NET-Klassen können keine Klassen jedoch die Stabilität und Zuverlässigkeit in Produktion erforderlich bereitstellen. Ihr Clientprogramm kann vorübergehende Fehler auftreten, von denen er im Hintergrund und ordnungsgemäß wiederherstellen und selbst zu fortfahren sollte.  
  
## <a name="step-1-identify-transient-errors"></a>Schritt 1: Ermitteln von vorübergehenden Fehlern  
  
Das Programm muss zwischen vorübergehende Fehler im Vergleich zu permanenten Fehlern unterscheiden. Vorübergehende Fehler werden fehlerbedingungen, die innerhalb kurzer Zeit, z. B. vorübergehende Netzwerkprobleme gelöscht können.  Ein Beispiel für ein beständiger Fehler würde sein, wenn das Programm eine falsche Schreibweise für den Namen der Zieldatenbank hat – in diesem Fall die Fehlermeldung "Datenbank nicht gefunden" beibehalten möchten, und verfügt über keine Chance, das Bereinigen von innerhalb einer kurzen Zeitspanne.  
  
Die Liste der Fehlernummern, die als vorübergehende Fehler eingestuft werden finden Sie unter am [Fehlermeldungen für Clientanwendungen für die SQL-Datenbank](http://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>Schritt 2: Erstellen Sie und führen Sie der beispielanwendung aus  
  
In diesem Beispiel geht davon aus .NET Framework 4.5.1 oder höher installiert ist.  Die C#-Codebeispiel besteht aus einer Datei mit dem Namen "Program.cs". Der Code wird im nächsten Abschnitt bereitgestellt.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>Schritt 2 festgelegte Kandidatenzeile: erfassen und kompilieren Sie das Codebeispiel  
  
Sie können das Beispiel mit den folgenden Schritten kompilieren:  
  
1. In der [kostenlose Visual Studio Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs), erstellen Sie ein neues Projekt aus der C#-Konsolenanwendungsvorlage.  
    - Datei > Neu > Projekt > installiert > Vorlagen > Visual C#-> Windows > klassischen Desktop > Konsolenanwendung  
    - Nennen Sie das Projekt **RetryAdo2**.  
2. Öffnen Sie im Projektmappen-Explorer-Bereich.  
    - Der Name des Projekts angezeigt.  
    - Der Name der Datei "Program.cs" angezeigt.  
3. Öffnen Sie die Datei "Program.cs".  
4. Ersetzen Sie den Inhalt der Datei "Program.cs" vollständig durch den Code in den folgenden Codeblock.  
5. Klicken Sie auf das Menü Build > Projektmappe erstellen.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>Schritt 2.b: Kopieren und Einfügen von Beispielcode  
  
Fügen Sie diesen Code in Ihrem **"Program.cs"** Datei.  
  
Sie müssen die Zeichenfolgen für den Servernamen, Kennwort und So weiter bearbeiten. Diese Zeichenfolgen finden Sie in der Methode mit dem Namen **GetSqlConnectionStringBuilder**.  
  
Hinweis: Die Verbindungszeichenfolge für den Servernamen ist dafür konzipiert Azure SQL-Datenbank, da er die vier Zeichen-Präfix des enthält **Tcp:**. Aber Sie können die serverzeichenfolge für die Verbindung zu Microsoft SQL Server anpassen.  
  
  
```CSharp  
    using System;  // C#  
    using CG = System.Collections.Generic;  
    using QC = System.Data.SqlClient;  
    using TD = System.Threading;  
        
    namespace RetryAdo2  
    {  
      public class Program  
      {  
        static public int Main(string[] args)  
        {  
          bool succeeded = false;  
          int totalNumberOfTimesToTry = 4;  
          int retryIntervalSeconds = 10;  
        
          for (int tries = 1;  
            tries <= totalNumberOfTimesToTry;  
            tries++)  
          {  
            try  
            {  
              if (tries > 1)  
              {  
                Console.WriteLine  
                  ("Transient error encountered. Will begin attempt number {0} of {1} max...",  
                  tries, totalNumberOfTimesToTry  
                  );  
                TD.Thread.Sleep(1000 * retryIntervalSeconds);  
                retryIntervalSeconds = Convert.ToInt32  
                  (retryIntervalSeconds * 1.5);  
              }  
              AccessDatabase();  
              succeeded = true;  
              break;  
            }  
        
            catch (QC.SqlException sqlExc)  
            {  
              if (TransientErrorNumbers.Contains  
                (sqlExc.Number) == true)  
              {  
                Console.WriteLine("{0}: transient occurred.", sqlExc.Number);  
                continue;  
              }  
              else  
              {  
                Console.WriteLine(sqlExc);  
                succeeded = false;  
                break;  
              }  
            }  
        
            catch (TestSqlException sqlExc)  
            {  
              if (TransientErrorNumbers.Contains  
                (sqlExc.Number) == true)  
              {  
                Console.WriteLine("{0}: transient occurred. (TESTING.)", sqlExc.Number);  
                continue;  
              }  
              else  
              {  
                Console.WriteLine(sqlExc);  
                succeeded = false;  
                break;  
              }  
            }  
        
            catch (Exception Exc)  
            {  
              Console.WriteLine(Exc);  
              succeeded = false;  
              break;  
            }  
          }  
        
          if (succeeded == true)  
          {  
            return 0;  
          }  
          else  
          {  
            Console.WriteLine("ERROR: Unable to access the database!");  
            return 1;  
          }  
        }  
        
        /// <summary>  
        /// Connects to the database, reads,  
        /// prints results to the console.  
        /// </summary>  
        static public void AccessDatabase()  
        {  
          //throw new TestSqlException(4060); //(7654321);  // Uncomment for testing.  
        
          using (var sqlConnection = new QC.SqlConnection  
              (GetSqlConnectionString()))  
          {  
            using (var dbCommand = sqlConnection.CreateCommand())  
            {  
              dbCommand.CommandText = @"  
    SELECT TOP 3  
        ob.name,  
        CAST(ob.object_id as nvarchar(32)) as [object_id]  
      FROM sys.objects as ob  
      WHERE ob.type='IT'  
      ORDER BY ob.name;";  
        
              sqlConnection.Open();  
              var dataReader = dbCommand.ExecuteReader();  
        
              while (dataReader.Read())  
              {  
                Console.WriteLine("{0}\t{1}",  
                  dataReader.GetString(0),  
                  dataReader.GetString(1));  
              }  
            }  
          }  
        }  
        
        /// <summary>  
        /// You must edit the four 'my' string values.  
        /// </summary>  
        /// <returns>An ADO.NET connection string.</returns>  
        static private string GetSqlConnectionString()  
        {  
          // Prepare the connection string to Azure SQL Database.  
          var sqlConnectionSB = new QC.SqlConnectionStringBuilder();  
        
          // Change these values to your values.  
          sqlConnectionSB.DataSource = "tcp:myazuresqldbserver.database.windows.net,1433"; //["Server"]  
          sqlConnectionSB.InitialCatalog = "MyDatabase"; //["Database"]  
        
          sqlConnectionSB.UserID = "MyLogin";  // "@yourservername"  as suffix sometimes.  
          sqlConnectionSB.Password = "MyPassword";  
          sqlConnectionSB.IntegratedSecurity = false;  
        
          // Adjust these values if you like. (ADO.NET 4.5.1 or later.)  
          sqlConnectionSB.ConnectRetryCount = 3;  
          sqlConnectionSB.ConnectRetryInterval = 10;  // Seconds.  
        
          // Leave these values as they are.  
          sqlConnectionSB.IntegratedSecurity = false;  
          sqlConnectionSB.Encrypt = true;  
          sqlConnectionSB.ConnectTimeout = 30;  
        
          return sqlConnectionSB.ToString();  
        }  
        
        static public CG.List<int> TransientErrorNumbers =  
          new CG.List<int> { 4060, 40197, 40501, 40613,  
          49918, 49919, 49920, 11001 };  
      }  
        
      /// <summary>  
      /// For testing retry logic, you can have method  
      /// AccessDatabase start by throwing a new  
      /// TestSqlException with a Number that does  
      /// or does not match a transient error number  
      /// present in TransientErrorNumbers.  
      /// </summary>  
      internal class TestSqlException : ApplicationException  
      {  
        internal TestSqlException(int testErrorNumber)  
        { this.Number = testErrorNumber; }  
        
        internal int Number  
        { get; set; }  
      }  
    }  
```  
  
###  <a name="step-2c-run-the-program"></a>Schritt 2.c: Führen Sie das Programm  
  
  
Die **RetryAdo2.exe** ausführbare Datei Eingaben keine Parameter. So führen Sie die .exe aus:  
  
1. Öffnen Sie ein Konsolenfenster, in dem Sie die Binärdatei RetryAdo2.exe kompiliert haben.  
2. Führen Sie RetryAdo2.exe, mit keine Eingabeparameter.  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>Schritt 3: Möglichkeiten, um Ihre Wiederholungslogik zu testen.  
  
Es gibt zahlreiche Möglichkeiten können Sie einen vorübergehenden Fehler, um Ihre Wiederholungslogik zu testen simulieren.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>Schritt 3.a: ein Test-Ausnahme  
  
Das Codebeispiel enthält:  
  
- Eine kleine zweite Klasse **TestSqlException**, mit dem Namen einer Eigenschaft **Anzahl**.  
- `//throw new TestSqlException(4060);`, die Sie kommentieren können.  
  
Auskommentieren der Throw-Anweisung, und diese erneut kompilieren, nächsten Ausführung des **RetryAdo2.exe** ähnlich der folgenden ausgegeben.  
  
```  
    [C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
    >> RetryAdo2.exe  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 2 of 4 max...  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 3 of 4 max...  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 4 of 4 max...  
    4060: transient occurred. (TESTING.)  
    ERROR: Unable to access the database!  
      
    [C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
    >>  
```  
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>Schritt 3 Abschnitt b: versuchen Sie es mit ein beständiger Fehler  
  
Handles, die persistente Fehler ordnungsgemäß, mit Ausnahme der vorangehenden Test erneut ausführen verwenden um nachzuweisen, dass den Code nicht die Anzahl der tatsächlichen vorübergehender Fehler wie 4060. Verwenden Sie stattdessen die Unsinn enthält-Nummer 7654321 ein. Das Programm sollte dies als ein beständiger Fehler behandeln und umgehen, sollten alle versuchen Sie es erneut.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>Schritt 3.c: Trennen der Netzwerkverbindung  
  
1. Trennen Sie den Clientcomputer aus dem Netzwerk.  
    - Trennen Sie für eine Desktop-die Netzwerkkabel.  
    - Drücken Sie für einen Laptop die Funktion Kombination von Schlüsseln zu für den Netzwerkadapter deaktivieren.  
2. Starten Sie RetryAdo2.exe, und warten Sie, bis die Konsole den ersten vorübergehenden Fehler, wahrscheinlich 11001 angezeigt.  
3. Verbinden Sie mit dem Netzwerk, während RetryAdo2.exe weiterhin ausgeführt.  
4. Sehen Sie sich die Konsole Bericht Erfolg bei einer nachfolgenden Wiederholung.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>Schritt 2.d erhalten haben: vorübergehend zuerst falsch schreiben und den Namen des Servers  
  
1. Vorübergehend als eine andere Fehlernummer hinzufügen 40615 **TransientErrorNumbers**, und kompilieren Sie erneut.  
2. Legen Sie einen Haltepunkt in Zeile: `new QC.SqlConnectionStringBuilder()`.  
3. Verwenden der *bearbeiten und Fortfahren* Feature absichtlich einige Zeilen im folgenden auf den Servernamen richtig geschrieben.  
    - Lassen Sie das Programm ausführen und zurückkehren, um den Haltepunkt.  
    - Die 40615-Fehler tritt auf.  
4. Korrigieren Sie die falsche Schreibweise.  
5. Lassen Sie das Programm werden ausgeführt und erfolgreich abgeschlossen.  
6. 40615 entfernen und neu kompilieren.  
  
## <a name="next-steps"></a>Nächste Schritte  
  
Um andere bewährte Practicies und Richtlinien für den Entwurf zu untersuchen, besuchen Sie [Herstellen einer Verbindung mit SQL-Datenbank: Links, Best Practices und Entwurfsrichtlinien](http://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  

