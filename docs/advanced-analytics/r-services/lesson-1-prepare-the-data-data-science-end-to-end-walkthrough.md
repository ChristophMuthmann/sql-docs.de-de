---
title: "Lektion 1: Vorbereiten der Daten (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise) | Microsoft Docs"
ms.custom: ""
ms.date: "03/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 29
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 25
---
# Lektion 1: Vorbereiten der Daten (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise)
Als Vorbereitung auf diese exemplarische Vorgehensweise müssen Sie die folgenden Schritte ausführen:

1. Laden Sie die Daten und alle R-Skripts herunter, die in der exemplarischen Vorgehensweise verwendet werden. Ein PowerShell-Skript wird bereitgestellt, um das Herunterladen von GitHub zu vereinfachen.   

2. Installieren Sie einige zusätzliche R-Pakete, sowohl auf dem Server als auch auf Ihrer R-Arbeitsstation.  

3. Bereiten Sie die Umgebung vor, einschließlich der Datenbank und Daten, die für Modellierung und Bewertung verwendet werden.
 
    Hierzu verwenden Sie ein zweites PowerShell-Skript, RunSQL_R_Walkthrough.ps1.
    Das Skript konfiguriert die Datenbank und lädt die Daten in die Tabelle, die Sie angeben.  Es erstellt auch einige SQL-Funktionen und gespeicherte Prozeduren, um Data Science-Aufgaben zu vereinfachen. 
 

## <a name="1-download-the-data-and-scripts"></a>1. Herunterladen der Daten und Skripts  
Der Code, der zum Bearbeiten dieser exemplarischen Vorgehensweise erforderlich ist, wurde von einem GitHub-Repository bereitgestellt. Mithilfe eines PowerShell-Skripts können Sie eine lokale Kopie der Dateien erstellen.  
  
#### <a name="to-download-all-scripts-using-powershell"></a>Herunterladen aller Skripts mit PowerShell  
  
1.  Öffnen Sie auf Ihrem Data Science-Clientcomputer eine Windows PowerShell-Eingabeaufforderung als Administrator.  
  
2.  Wenn Sie PowerShell zuvor noch nicht in dieser Instanz ausgeführt haben, oder Sie über keine Berechtigung zum Ausführen von Skripts verfügen, kann möglicherweise ein Fehler auftreten. Ist dies der Fall, führen sie vor dem Ausführen des Skripts diesen Befehl aus, um vorübergehend Skripts zuzulassen, ohne die Systemstandards zu ändern.  
  
    ```  
    Set-ExecutionPolicy Unrestricted -Scope Process -Force  
    ```  
  
3.  Führen Sie den folgenden Befehl zum Herunterladen von Skriptdateien in ein lokales Verzeichnis aus. Wenn Sie kein anderes Verzeichnis angeben, wird standardmäßig der Ordner „c:\tempR“ erstellt, in dem alle Dateien gespeichert werden.  
  
    ```  
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'  
  
    ```  
  
    Wenn Sie die Dateien in einem anderen Verzeichnis speichern möchten, bearbeiten Sie die Werte des Parameters *DestDir*, und geben Sie einen anderen Ordner auf Ihrem Computer an. Wenn Sie einen Ordnernamen eingeben, der nicht vorhanden ist, erstellt das PowerShell-Skript den Ordner für Sie.  
  
4.  Nachdem der Download abgeschlossen ist, sollte die Windows PowerShell-Befehlskonsole wie folgt aussehen:  
  
    ![After completion of PowerShell script](../../advanced-analytics/r-services/media/rsql-e2e-psscriptresults.PNG "After completion of PowerShell script")  
  
5.  Führen Sie in der PowerShell-Konsole den Befehl `ls` zum Anzeigen einer Liste der Dateien aus, die in *DestDir* heruntergeladen wurden.  Eine Liste und Beschreibung der Dateien finden Sie unter [Inhalt des Downloads](#What-the-Download-Includes).
  
## <a name="2-install-required-packages"></a>2. Installieren der erforderlichen Pakete  
Diese exemplarische Vorgehensweise erfordert einige R-Bibliotheken, die nicht standardmäßig als Teil von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert sind. Sie müssen die Pakete jeweils auf dem Client installieren, auf dem Sie die Lösung entwickeln, und auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer, auf dem Sie die Lösung bereitstellen.  
  
### <a name="install-required-packages-on-the-client"></a>Installieren der erforderlichen Pakete auf dem Client  
Das R-Skript, das Sie heruntergeladen haben, enthält die Befehle zum Herunterladen und Installieren der Pakete.  
  
1.  Öffnen Sie die Skriptdatei RSQL_R_Walkthrough.R in Ihrer R-Umgebung.  
  
2.  Markieren Sie diese Zeilen, und führen Sie sie aus.  
  
    ```  
    # Install required R libraries for this walkthrough if they are not installed.   
  
    if (!('ggmap' %in% rownames(installed.packages()))){  
      install.packages('ggmap')  
    }  
    if (!('mapproj' %in% rownames(installed.packages()))){  
      install.packages('mapproj')  
    }  
    if (!('ROCR' %in% rownames(installed.packages()))){  
      install.packages('ROCR')  
    }  
    if (!('RODBC' %in% rownames(installed.packages()))){  
      install.packages('RODBC')  
    }  
    ```  
  
### <a name="install-required-packages-on-the-server"></a>Installieren der erforderlichen Pakete auf dem Server  

  
1.  Öffnen Sie auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer als Administrator RGui.exe.  Wenn Sie SQL Server R Services mithilfe der Standardeinstellungen installiert haben, finden Sie RGui.exe unter C:\Programme\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64).  
  
    Wenn Sie eine andere R-Umgebung auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computer installiert haben (z.B. RStudio), können Sie die R-Konsole zum Ausführen der Befehle verwenden.  
  
2.  Führen Sie an einer R-Eingabeaufforderung die folgenden R-Befehle aus:  
  
    ```  
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])  
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    ```  
  
**Hinweise:**  
  
-   Dieses Beispiel verwendet die „grep“-Funktion in R, um den Vektor der verfügbaren Pfade zu durchsuchen und denjenigen in „Programme“ zu finden. Weitere Informationen finden Sie unter [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep).   
  
-   Wenn Sie meinen, dass die Pakete bereits installiert seien, überprüfen Sie die Liste der installierten Pakete mithilfe der R-Funktion `installed.packages()`.  
  
-   Auf dem Client können Sie die Benutzerbibliothek installieren, wenn Sie keine Daten in die Hauptbibliothek in „Programme“ schreiben können. Wenn Pakete jedoch auf dem SQL Server-Computer installiert werden, müssen Sie sie in der von SQL Server R Services verwendeten Standardbibliothek installieren. Verwenden Sie keine Benutzerbibliothek. Weitere Informationen finden Sie unter [Installieren neuer R-Pakete in SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).
      

## <a name="3-run-powershell-script-runsqlrwalkthroughps1"></a>3. Ausführen des PowerShell-Skripts „RunSQL_R_Walkthrough.ps1“  

Sie können dieses PowerShell-Skript auf dem Computer ausführen, auf dem Sie die Projektmappe erstellen, z.B. auf dem Computer, auf dem Sie Ihren R-Code entwickeln und testen. Dieser Computer muss in der Lage sein, eine Verbindung zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer mithilfe des Named Pipes-Protokolls herzustellen.  
  
Das Skript führt folgende Aktionen aus:  
  
-   Überprüft, ob der SQL Native Client und das Befehlszeilenprogrammen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert sind. Das Befehlszeilentool wird für die Ausführung des [bcp Hilfsprogramms](../../tools/bcp-utility.md)benötigt, das für schnelles Massenladen von Daten in SQL-Tabellen verwendet wird.    
-   Stellt eine Verbindung mit der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her und führt einige [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts aus, die die Datenbank konfigurieren und die Tabellen für das Modell und die Daten erstellen.    
-   Führt eine SQL-Skript aus, um mehrere gespeicherte Prozeduren zu erstellen.    
-   Lädt die Daten, die Sie zuvor heruntergeladen haben, in die Tabelle nyctaxi_sample.    
-   Schreibt die Argumente in der R-Skriptdatei neu, um den von Ihnen angegebenen Datenbanknamen zu verwenden. 

### <a name="to-run-the-script"></a>So führen Sie das Skript aus
  
1.  Öffnen Sie als Administrator eine PowerShell-Befehlszeile.    
  
2.  Navigieren Sie zu dem Ordner, in dem Sie die Skripts heruntergeladen haben, und geben Sie den Namen des Skripts an, wie hier veranschaulicht. Drücken Sie die EINGABETASTE.  
  
    ```  
    .\RunSQL_R_Walkthrough.ps1  
    ```  
  
3.  Für jeden der folgenden Parameter werden Sie aufgefordert:  
  
    - Name der Datenbank, die Sie erstellen möchten. 
      Sie können beispielsweise **Tutorial** oder **Taxi** eingeben.  
    - Anmeldeinformationen, unter denen das Skript ausgeführt wird. Zwei Optionen stehen zur Verfügung:
        + Geben Sie den Namen einer SQL-Anmeldung mit CREATE DATABASE-Berechtigungen und das SQL-Kennwort an einer nachfolgenden Eingabeaufforderung an.
        + Drücken Sie die EINGABETASTE, ohne einen Namen einzugeben, damit Ihre eigene Windows-Identität verwendet wird. Geben Sie anschließend an einer geschützten Eingabeaufforderung Ihr Windows-Kennwort ein. PowerShell unterstützt nicht das Eingeben eines anderen Windows-Benutzernamens. 

          Wenn Sie keinen gültigen Benutzer angeben, verwendet das Skript standardmäßig die integrierte Windows-Authentifizierung.  
  
    -   Vollständigen Pfad zur CSV-Datei, die Sie in die Datenbank hochladen möchten  
  
        Das Skript sollte die Datei herunterzuladen und sie automatisch in die Datenbank laden. Schlägt dies jedoch fehl, können Sie die Daten auch immer manuell hochladen.  
  
4.  Drücken Sie die EINGABETASTE, um das Skript auszuführen.  
  
## <a name="troubleshooting"></a>Problembehandlung  
 
 Wenn Probleme auftreten sollten, können Sie alle oder beliebige Schritte manuell ausführen und dabei die Zeilen des PowerShell-Skripts als Beispiele verwenden. 
 

### <a name="the-powershell-script-didnt-download-the-data"></a>Das PowerShell-Skript hat die Daten nicht heruntergeladen
  
Um die Daten manuell herunterzuladen, klicken Sie mit der rechten Maustaste auf den folgenden Link, und wählen Sie **Ziel speichern unter** aus.  
  
[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)  
  
Notieren Sie den Pfad zu der heruntergeladenen Datendatei und dem Dateinamen, unter der bzw. dem die Daten gespeichert wurden. Sie benötigen den Pfad zum Laden der Daten in die Tabelle mithilfe von **bcp**.  
  
### <a name="i-was-unable-to-download-the-data"></a>Ich konnte die Daten nicht herunterladen
Die Datendatei ist groß. Verwenden Sie einen Computer mit einer relativ schnellen Internetverbindung, damit beim Download kein Timeout eintritt.  

  
### <a name="could-not-connect-or-script-failed"></a>Fehler bei der Verbindungsherstellung oder Skriptfehler  
  
+ Überprüfen Sie die Schreibweise des Instanznamens. 
+ Überprüfen Sie die vollständige Verbindungszeichenfolge.    
+ Je nach Netzwerkanforderungen muss der Instanzname ggf. mit einem oder mehreren Subnetznamen qualifiziert werden.  Wenn beispielsweise MYSERVER nicht funktioniert, versuchen Sie „myserver.subnet.mycompany.com“.
  
### <a name="network-error-or-protocol-not-found"></a>Netzwerkfehler oder Protokoll nicht gefunden  
  
+ Stellen Sie sicher, dass die Instanz die Remoteverbindungen unterstützt.    
+ Überprüfen Sie, dass der angegebene SQL-Benutzer eine Remoteverbindung zur Datenbank herstellen kann und dass Named Pipes auf der Instanz aktiviert ist.    
+ Überprüfen Sie die Berechtigungen des Kontos. Das Konto, das Sie angegeben haben, verfügt möglicherweise nicht über die Berechtigungen, eine neue Datenbank zu erstellen und Daten hochzuladen.  

### <a name="bcp-did-not-run"></a>bcp wurde nicht ausgeführt  

+ Überprüfen Sie, ob das Hilfsprogramm [bcp](../../tools/bcp-utility.md) auf Ihrem Computer verfügbar ist. Sie können bcp in einem PowerShell-Fenster oder an einer Windows-Befehlszeile ausführen.
+ Wenn Sie eine Fehlermeldung erhalten, fügen Sie den Speicherort des Hilfsprogramms bcp zur Systemumgebungsvariablen PATH hinzu, und versuchen Sie es erneut.  

### <a name="the-table-schema-was-created-but-there-is-no-data-in-the-table"></a>Das Tabellenschema wurde erstellt, aber die Tabelle enthält keine Daten

Wenn der Rest des Skripts ohne Probleme ausgeführt wurde, können Sie die Daten manuell in die Tabelle laden, indem Sie **bcp** über die Befehlszeile wie folgt aufrufen:  


 
**Verwenden einer SQL-Anmeldung**
    
~~~~ 
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password  
~~~~  
  
**Verwenden der Windows-Authentifizierung**  

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T 
~~~~ 
  
  
+ Das Schlüsselwort **in** gibt die Richtung der Datenverschiebung an.  
+ Das Argument **-f** erfordert, dass Sie den vollständigen Pfad einer Formatdatei angeben. Eine Formatdatei ist erforderlich, wenn Sie die Option **in** verwenden.
+ Verwenden Sie die Argumente **-U** und **-P**, wenn bcp mit einer SQL-Anmeldung ausgeführt wird.
+ Verwenden Sie das Argument **-T** bei Verwendung der integrierten Windows-Authentifizierung. 

  
### <a name="how-can-i-run-the-script-without-prompts"></a>Wie kann ich das Skript ohne Eingabeaufforderungen ausführen?  
  
Sie können alle Parameter mithilfe spezifischer Werte für Ihre Umgebung in einer einzigen Befehlszeile angeben. 
  
```  
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>  
```  
  
Geben Sie beispielsweise Folgendes ein, um das Skript mit einer SQL-Anmeldung auszuführen:  
  
```  
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv  
```  
  
In diesem Beispiel werden die folgenden Aufgaben ausgeführt:  
  
-   Stellt eine Verbindung mit der angegebenen Instanz und Datenbank mithilfe der Anmeldeinformationen von *SqlUserName* her.  
-   Ruft Daten aus der Datei *C:\temp\nyctaxi1pct.csv* ab.  
-   Lädt die Daten in die Tabelle *dbo.nyctaxi_sample* in der Datenbank *MyDB* auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz mit dem Namen *MyServer*.  

### <a name="the-data-loaded-but-it-contains-duplicates"></a>Die Daten werden geladen, enthalten aber Duplikate

Wenn eine Tabelle vorhanden ist, die das ordnungsgemäße Schema hat, wird bcp weiterhin ausgeführt. Allerdings wird eine neue Kopie der Daten eingefügt, statt vorhandene Daten zu überschreiben. Dies führt zu doppelten Daten.  Schneiden Sie vorhandene Tabellen unbedingt ab, ehe Sie das Skript erneut ausführen.

## <a name="what-the-download-includes"></a>Umfang des Downloads

Wenn Sie die Dateien aus dem GitHub-Repository herunterladen, erhalten Sie Folgendes:
+ Daten im CSV-Format
+ Ein PowerShell-Skript für die Vorbereitung der Umgebung
+ Eine XML-Formatdatei für das Importieren der Daten mithilfe von bcp in SQL Server
+ Mehrere T-SQL-Skripts
+ Den gesamten R-Code, den Sie in dieser exemplarischen Vorgehensweise ausführen müssen

### <a name="training-and-scoring-data"></a>Trainings- und Bewertungsdaten  
Die Daten stellen einen repräsentativen Querschnitt des Datasets New York City Taxi dar, das Datensätze von über 173 Millionen Fahrten aus dem Jahr 2013 enthält, einschließlich der Fahrpreise und Trinkgelder, die für jede Fahrt gezahlt wurden.  Weitere Informationen darüber, wie diese Daten ursprünglich gesammelt wurden, und wie Sie das vollständige Dataset erhalten, finden Sie unter  
[http://chriswhong.com/open-data/foil_nyc_taxi/](http://chriswhong.com/open-data/foil_nyc_taxi/).  
  
Damit Sie mit den Daten einfacher arbeiten können, hat das Microsoft Data-Science-Team diese verkleinert, damit nur noch 1 % der Daten abgerufen werden.  Diese Daten wurden in einem öffentlichen Blob-Speichercontainer in Azure im CSV-Format freigegeben. Die Quelldaten ist eine unkomprimierte Datei mit einer Größe von nicht ganz 350 MB.  
 
### <a name="files"></a>Dateien

 
+ **RunSQL_R_Walkthrough.ps1** Sie führen dieses Skript zuerst mit PowerShell aus. Es ruft die SQL-Skripts zum Laden von Daten in die Datenbank auf.  
    
+ **taxiimportfmt.xml** Eine Formatdefinitionsdatei, die vom Hilfsprogramm bcp zum Laden von Daten in die Datenbank verwendet wird.
      
+ **RSQL_R_Walkthrough.R**  Dies ist das grundlegende R-Skript, das in den übrigen Lektionen für die Datenanalyse und Modellierung verwendet wird. Es stellt den gesamten R-Code bereit, den Sie zum Durchsuchen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten, zum Erstellen des Klassifizierungsmodells und zum Erstellen von Diagrammen benötigen.   
  
### <a name="sql-scripts"></a>SQL-Skripts  
Dieses PowerShell-Skript führt mehrere [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts auf dem Server aus. Die folgende Tabelle enthält die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skriptdateien.  
  
|Name der SQL-Skriptdatei|Aktion|  
|------------------------|----------------|  
|create-db-tb-upload-data.sql|Erstellt die Datenbank und zwei Tabellen:<br /><br /> *nyctaxi_sample*: Tabelle, in der die trainierten Daten gespeichert sind – ein 1 %-Beispiel des Datasets NYC Taxi. Ein gruppierter Columnstore-Index wird der Tabelle hinzugefügt, um die Speicher- und Abfrageleistung zu verbessern.<br /><br /> *nyc_taxi_models*: Eine leere Tabelle, die Sie später zum Speichern des trainierten Klassifizierungsmodells verwenden.|  
|PredictTipBatchMode.sql|Erstellt eine gespeicherte Prozedur, die ein trainiertes Modell zum Vorhersagen der Bezeichnungen für neue Beobachtungen aufruft. Sie akzeptiert eine Abfrage als Eingabeparameter.|  
|PredictTipSingleMode.sql|Erstellt eine gespeicherte Prozedur, die ein trainiertes Klassifizierungsmodell zum Vorhersagen der Bezeichnungen für neue Beobachtungen aufruft. Variablen der neuen Beobachtungen werden als Inlineparameter übergeben.|  
|PersistModel.sql|Erstellt eine gespeicherte Prozedur, mit der die binäre Darstellung des Klassifizierungsmodells in eine Tabelle in der Datenbank gespeichert werden kann.|  
|fnCalculateDistance.sql|Erstellt eine SQL-Skalarwertfunktion, die die direkte Entfernung zwischen Abhol-und Zielorten berechnet.|  
|fnEngineerFeatures.sql|Erstellt eine SQL-Tabellenwertfunktion, die Funktionen zum Trainieren des Klassifizierungsmodells erstellt|  
  
Alle SQL-Abfragen, die im Rahmen dieser exemplarischen Vorgehensweise verwendet werden, wurden getestet und können unverändert in Ihrem R-Code ausgeführt werden. Wenn Sie jedoch weiter experimentieren oder Ihre eigene Lösung mithilfe von SQL-Abfragen entwickeln möchten, empfiehlt es sich, eine Entwicklungsumgebung wie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zu verwenden, um Ihre Abfragen zunächst zu testen und zu optimieren, bevor Sie sie Ihrem R-Code hinzufügen.  
  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 2: Anzeigen und Durchsuchen der Daten &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Vorherige Lektion  
[Lückenlose exemplarische Data Science-Vorgehensweise](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
  
  
