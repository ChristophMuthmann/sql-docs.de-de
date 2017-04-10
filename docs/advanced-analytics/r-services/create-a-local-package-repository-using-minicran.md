---
title: "Erstellen Sie ein lokales Repository mithilfe miniCRAN | Microsoft Docs"
ms.custom: ""
ms.date: "05/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 4
---
# Erstellen Sie ein lokales Repository mithilfe miniCRAN
In diesem Thema wird beschrieben, wie Sie ein lokales R-Paket-Repository mit dem R-Paket erstellen können **MiniCRAN**. 

Da [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanzen in der Regel befinden sich auf einem Server, die nicht über Internetkonnektivität, die Standardmethode für die Installation von R-Pakete (R-Befehl `install.packages()`) funktioniert möglicherweise nicht, wie der Paketinstaller CRAN oder beliebige andere Spiegelung Standorte zugreifen kann.

Es gibt zwei Optionen zum Installieren von Paketen aus einer lokalen Freigabe oder einem Repository:

+ Verwenden Sie das MiniCRAN-Paket, um ein lokales Repository der Pakete zu erstellen, müssen Sie von diesem Repository installieren. Dieses Thema beschreibt die MiniCRAN-Methode.

+ Herunterladen, Sie müssen, Pakete und ihre Abhängigkeiten, als Zip-Dateien und in einem lokalen Ordner zu speichern, und kopieren Sie diesen Ordner auf den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer. Weitere Informationen für die manuelle Methode finden Sie unter [Installieren zusätzlicher Pakete in SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).


## Schritt 1: Installieren von MiniCRAN und Herunterladen von Paketen 


1. Installieren Sie das MiniCRAN-Paket auf einem Computer, der Zugang zum Internet hat.

   ~~~~
   # Install miniCRAN ---------------------------------------------------

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. Herunterladen Sie oder installieren Sie die Pakete, die Sie benötigen für diesen Computer. Dadurch wird die Ordnerstruktur, die Sie benötigen, kopieren Sie die Pakete erstellt die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] später.

   ~~~~
   # List the packages you need 
   # Do not specify dependencies
   pkgs_needed <- c("ggplot2", "ggdendro")
   ~~~~

3. Kopieren Sie das Repository MiniCRAN in die R_SERVICES-Bibliothek auf die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanz.

## Schritt 2: Installieren Sie die Pakete auf dem SQL Server-computer 

4. Auf der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer führen Sie den Befehl R  `install.packages()`. Verwenden Sie eine der R-Tools, die mit installiert werden [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], wie z. B. Rgui.exe, oder Sie den Befehl als Teil des ausführen können eine [!INCLUDE[tsql_md](../../includes/tsql-md.md)] gespeicherte Prozedur.
5. Aufgefordert werden, geben Sie ein Repository wählen Sie den Ordner mit den Dateien, die Sie gerade kopiert haben. also das lokale MiniCRAN-Repository.

   ~~~~
   pkgs_needed <- c("ggplot2", "ggdendro")
   local_repo  <- "~/miniCRAN"
   
   .libPaths()[1]
   "C:/Program Files/Microsoft SQL Server/130/R_SERVER/library"

   lib <- .libPaths()[1]

   install.packages(pkgs_needed, 
                 repos = file.path("file://", normalizePath(local_repo, winslash = "/")),
                 lib = lib,
                 type = "win.binary",
                 dependencies = TRUE
                 )
   ~~~~

6. Stellen Sie sicher, dass die Pakete durch Ausführen dieses Codes R installiert wurden.
   ~~~~
   installed.packages()
   ~~~~



## Bestätigungen

Die Quelle dieser Informationen ist in diesem Artikel von Andre de Vries, auch das Paket MiniCRAN entwickelt hat. Weitere Informationen und eine vollständige Exemplarische Vorgehensweise finden Sie unter  [R Installieren von Paketen auf einer Offline-SQL Server 2016-Instanz](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)