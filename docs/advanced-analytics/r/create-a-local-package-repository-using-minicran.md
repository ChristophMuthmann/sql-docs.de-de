---
title: Erstellen eines lokalen Paketverzeichnisses mit miniCRAN | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8af93b3e132290eef4b43da568b9381ff8e5a04
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>Erstellen eines lokalen Paketverzeichnisses mit miniCRAN
In diesem Thema wird beschrieben, wie Sie ein lokales R-Paketverzeichnis mit dem R-Paket erstellen können **miniCRAN**. 

Da sich [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanzen in der Regel auf einem Server befinden, der nicht über Internetkonnektivität verfügt, funktioniert die Standardmethode für die Installation von R-Paketen (R-Befehl `install.packages()`) möglicherweise nicht, da der Paketinstaller nicht auf CRAN oder beliebige andere gespiegelte Seiten zugreifen kann.

Es gibt zwei Optionen zum Installieren von Paketen aus einer lokalen Freigabe oder einem Repository:

+ Verwenden Sie das miniCRAN-Paket, um ein lokales Repository der benötigten Pakete zu erstellen und anschließend aus diesem Repository zu installieren. Dieses Thema beschreibt die miniCRAN-Methode.

+ Laden Sie die benötigten Pakete und ihre Abhängigkeiten als ZIP-Dateien herunter, und speichern Sie sie in einem lokalen Ordner. Kopieren Sie diesen Ordner anschließend auf den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Computer. Weitere Informationen für die manuelle Kopiermethode finden Sie unter [Install Additional Packages on SQL Server (Installieren zusätzlicher Pakete in SQL Server)](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).


## <a name="step-1-install-minicran-and-download-packages"></a>Schritt 1: Installieren von miniCRAN und Herunterladen von Paketen 


1. Installieren Sie das miniCRAN-Paket auf einem Computer, der Zugang zum Internet hat.

   ~~~~
   # Install miniCRAN and igraph

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. Laden Sie mithilfe des folgenden R-Skripts die benötigten Pakete auf diesen Computer herunter oder installieren Sie sie. Dadurch wird die Ordnerstruktur erstellt, die Sie benötigen, um die Pakete später in den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zu kopieren.

   ~~~~
   # List the packages to get. Do not specify dependencies.
   pkgs_needed <- c("ggplot2", "ggdendro")
   # Plot the dependency graph 
   plot(makeDepGraph(pkgs_needed)) 
   
   # Create the local repo 
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror) 
   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.2") 

   # List local packages 
   pdb <- as.data.frame( 
     pkgAvail(local_repo, type = "win.binary", Rversion = "3.2"),  
     stringsAsFactors = FALSE) 
   head(pdb) 
   pdb$Package 
   pdb[, c("Package", "Version", "License")] 
   ~~~~


## <a name="step-2-copy-the-minicran-repository-to-the-sql-server-computer"></a>Schritt 2: Kopieren der miniCRAN-Repository auf den SQL-Servercomputer 

Kopieren Sie das miniCRAN-Repository in die R_SERVICES-Bibliothek in die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz.

+ Für SQL Server 2016 ist der Standardordner `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library1`.
+ Für SQL Server 2017 der Standardordner ist `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library1`.

Wenn Sie R-Services mithilfe einer benannten Instanz installiert haben, müssen Sie den Instanznamen im Pfad angeben, um sicherzustellen, dass die Bibliotheken in der richtigen Instanz installiert werden. Wenn die benannte Instanz RTEST02 ist, lauter der Standardpfad für die benannte Instanz folgendermaßen: `C:\Program Files\Microsoft SQL Server\MSSQL13.RTEST02\R_SERVICES\library`.

Wenn Sie SQL Server auf einem anderen Laufwerk installiert haben, oder andere Änderungen im Installationspfad vorgenommen haben, achten Sie darauf, dass Sie auch diese Änderungen übernehmen.

## <a name="step-3-install-the-packages-on-sql-server-using-the-minicran-repository"></a>Schritt 3: Installieren der Pakete auf dem SQL Server mithilfe der miniCRAN-Repository

Öffnen Sie auf dem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Computer eine R-Befehlszeile oder RGui als Administrator. 
  
> [!TIP]
> Sie haben möglicherweise mehrere R-Bibliotheken auf dem Computer. Verwenden Sie daher die Kopie der RGui oder RTerm, die mit der bestimmten Instanz installiert ist, in dem die Pakete installiert werden sollen, um sicherzustellen, dass Pakete in der richtigen Instanz installiert sind.
  
Wenn Sie ein Repository angeben sollen, wählen Sie den Ordner mit den Dateien, die Sie gerade kopiert haben, also das lokale miniCRAN-Repository.

   ~~~~
   # Run this R code as administrator on the SQL Server computer 
   pkgs_needed <- c("ggplot2", "ggdendro") 
   local_repo  <- "~/miniCRAN" 

   # OPTIONAL: If you are not running R from the instance library as recommended, you must specify the path
   #   .libPaths()[1] 
   # "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library " 
   # lib <- .libPaths()[1]
   
   install.packages(pkgs_needed,  
                    repos = file.path("file://", normalizePath(local_repo, winslash = "/")), 
                    lib = lib, 
                    type = "win.binary", 
                    dependencies = TRUE 
                    ) 
   installed.packages() 
   ~~~~

Stellen Sie sicher, dass die Pakete installiert wurden.
   ~~~~
   installed.packages()
   ~~~~



## <a name="acknowledgements"></a>Bestätigungen

Die Quelle dieser Informationen ist dieser Artikel von Andre de Vries, der auch das Paket miniCRAN entwickelt hat. Weitere Informationen und eine vollständige Exemplarische Vorgehensweise finden Sie unter [How to install R packages on an off-line SQL Server 2016 instance (Installieren von R-Paketen auf einer Offline-SQL Server 2016-Instanz)](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html).

