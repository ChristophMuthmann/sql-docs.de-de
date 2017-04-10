---
title: "Schritt 1: Herunterladen der Beispieldaten (Tutorial f&#252;r datenbankinterne Advanced Analytics) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
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
  - "TSQL"
ms.assetid: 32a5d5ad-c58a-4669-a90d-ef296b48fcd8
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Schritt 1: Herunterladen der Beispieldaten (Tutorial f&#252;r datenbankinterne Advanced Analytics)
In diesem Schritt laden Sie das Beispieldataset sowie die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skriptdateien herunter, die in dieser exemplarischen Vorgehensweise verwendet werden. Die Daten- und die Skriptdateien werden jeweils auf Github freigegeben, doch das PowerShell-Skript lädt die Daten und Skriptdateien in ein lokales Verzeichnis Ihrer Wahl herunter.  
  
## Herunterladen der Daten und Skripts  
  
1.  Öffnen Sie eine Windows PowerShell-Befehlskonsole.  
  
    Verwenden Sie die Option **Als Administrator ausführen**, wenn Administratorrechte erforderlich sind, um das Zielverzeichnis zu erstellen oder Dateien in das angegebene Ziel zu schreiben.  
  
2.  Führen Sie die folgenden PowerShell-Befehle aus, die den Wert des Parameters *DestDir* auf jedem beliebigen lokalen Verzeichnis ändern.  Wir haben in diesem Fall **TempRSQL** verwendet.  
  
    ```  
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’  
  
    ```  
  
    Wenn der von Ihnen angegebene Ordner in *DestDir* nicht existiert, wird er vom PowerShell-Skript erstellt.  
  
    > [!TIP]  
    > Wenn Sie eine Fehlermeldung erhalten, können Sie für diese exemplarische Vorgehensweise die Richtlinie für die Ausführung von PowerShell-Skripts auf **Uneingeschränkt** festlegen, indem Sie das Bypass-Argument verwenden, und die Gültigkeit der Änderungen auf die aktuelle Sitzung beschränken.  
    >   
    >````  
    > Set\-ExecutionPolicy Bypass \-Scope Process  
    >````   
    > Das Ausführen dieses Befehls führt zu keiner Konfigurationsänderung.  
  
    Abhängig von Ihrer Internetverbindung kann der Download eine Weile dauern.  
  
3.  Wenn alle Dateien heruntergeladen wurden, wechselt PowerShell in das mithilfe des Parameters *DestDir* angegebene Verzeichnis. Führen Sie den folgenden Befehl in der PowerShell-Eingabeaufforderung aus, und überprüfen Sie die Dateien, die heruntergeladen wurden.  
  
    ```  
    ls  
    ```  
  
    **Ergebnisse:**  
  
    ![list of files downloaded by PowerShell script](../../advanced-analytics/r-services/media/rsql-devtut-filelist.PNG "list of files downloaded by PowerShell script")  
  
## Nächster Schritt  
[Schritt 2: Importieren von Daten in SQL Server mithilfe von PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## Vorheriger Schritt  
[In-Database Advanced Analytics for SQL Developers &#40;Tutorial&#41; (Datenbankinterne Advanced-Analytics für SQL-Entwickler (Tutorial))](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
## Siehe auch  
[SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
