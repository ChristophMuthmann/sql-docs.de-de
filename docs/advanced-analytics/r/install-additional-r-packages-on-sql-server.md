---
title: "Installieren zusätzlicher R-Pakete unter SQL Server | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: adc0e5fc229547632759c5702e98d87f4b71cbb3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="install-additional-r-packages-on-sql-server"></a>Installieren zusätzlicher R-Pakete unter SQL Server
In diesem Thema wird beschrieben, wie Sie neue R-Pakete mit einer Instanz von [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] auf einem Computer mit Internetzugang installieren.

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1. Suchen der Windows-Binärdateien im ZIP-Dateiformat

R-Pakete werden auf vielen Plattformen unterstützt. Sie müssen sicherstellen, dass das Paket, das Sie installieren möchten, ein binäres Format für die Windows-Plattform aufweist. Anderenfalls funktioniert das heruntergeladene Paket nicht.

Zum Abrufen des [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) -Pakets von Bioconductor, gehen Sie folgendermaßen vor:  
  
1.  Suchen Sie in der Liste der **Paketarchive** die **Windows-Binärdateiversion** .  
  
2.  Klicken Sie mit der rechten Maustaste auf den Link zur ZIP-Datei, und wählen Sie  **Ziel speichern unter**aus.  
  
3.  Navigieren Sie zum lokalen Ordner, in dem die komprimierten Pakete gespeichert sind, und klicken Sie auf **Speichern**.  
  
 Dieser Vorgang erstellt eine lokale Kopie des Pakets. Sie können anschließend das Paket installieren oder das ZIP-Paket auf einen Server kopieren, der keinen Internetzugang hat.  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2. Öffnen der standardmäßigen R-Paket-Bibliothek für SQL Server R Services 

Navigieren Sie zu dem Ordner auf dem Server, in dem die [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] zugeordneten R-Pakete installiert wurden. Es ist wichtig, dass Sie Pakete in der Standardbibliothek installieren, die der aktuellen Instanz zugeordnet ist. 

Informationen zu dieser Bibliothek finden Sie unter [Installieren und Verwalten von R-Paketen](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).

   Für jede Instanz, in der Sie ein Paket ausführen, müssen Sie eine separate Kopie der Pakete installieren. Derzeit können Pakete zwischen Instanzen nicht freigegeben werden.
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3. Öffnen einer Befehlsaufforderung mit Administratorberechtigung 

Öffnen Sie R als Administrator.  Dies ist mithilfe der Windows-Befehlsaufforderung oder mit einem R-Dienstprogramme möglich.
  
### <a name="using-the-windows-command-prompt"></a>Unter Verwendung der Eingabeaufforderung von Windows 

1. Öffnen Sie eine Windows-Befehlsaufforderung als Administrator, und navigieren Sie zu dem Verzeichnis, in dem sich die Dateien „RTerm.Exe“ oder „RGui.exe“ befinden.  
  
    In einer Standardinstallation ist dies das R-Verzeichnis **\bin** . In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] befinden sich die R-Tools beispielsweise hier: 

    **Standardinstanz**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **Benannte Instanz**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. Führen Sie **R.Exe**aus.  
  
### <a name="using-the-r-command-line-utilities"></a>Unter Verwendung der R-Befehlszeilen-Hilfsprogramme 
  
1. Verwenden Sie Windows Explorer, um zum Verzeichnis mit den R-Tools zu navigieren.  
  
2. Klicken Sie mit der rechten Maustaste auf **RGui.exe** oder **RTerm.exe**, und wählen Sie **Als Administrator ausführen** aus.  
## <a name="4-install-the-package"></a>4. Installieren des Pakets

Welche R-Eingabeaufforderung Sie zum Installieren des Pakets verwenden, ist davon abhängig, ob Sie das Paket aus dem Internet oder aus einer lokalen ZIP-Datei abrufen.  
  
### <a name="install-package-from-internet"></a>Installationspaket aus dem Internet  
  
1.  Im Allgemeinen verwenden Sie den folgenden Befehl,um ein neues Paket aus CRAN oder von einer der gespiegelten Sites installieren.  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    Beachten Sie, dass für den Namen des Pakets immer doppelte Anführungszeichen erforderlich sind.

2.  Um die Bibliothek angeben, in der das Paket installiert werden soll, verwenden Sie zum Festlegen der Position der Bibliothek einen der folgenden Befehle:
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    Beachten Sie, dass für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] derzeit nur eine Paketbibliothek zulässig ist. Installieren Sie Pakete nicht in einer Benutzerbibliothek, anderenfalls können Sie das Paket nicht von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ausführen.   
     
3.  Nach der Definition des Speicherorts der Bibliothek installiert die folgende Anweisung das gängige e1070-Paket in der Paketbibliothek, die von R Services verwendet wird.  
  
    ```  
    install.packages("e1071", lib = lib.SQL)  
    ```  
  
4.  Sie werden nach einer gespiegelten Site gefragt, von der das Paket abgerufen werden soll. Wählen Sie eine beliebige gespiegelte Site aus, die für Ihren Standort zweckmäßig ist.  
  
    Eine Liste aktueller CRAN-Spiegel finden Sie [auf dieser Website](https://cran.r-project.org/mirrors.html).  
  
    > [!TIP]  
    >  Um nicht jedes Mal, wenn Sie ein neues Paket hinzufügen, eine gespiegelte Site auswählen zu müssen, können Sie die R-Entwicklungsumgebung so konfigurieren, dass immer dasselbe Repository verwendet wird.  
    >   
    >  Hierzu bearbeiten Sie die globale R-Einstellungsdatei (.Rprofile) und fügen die folgende Zeile hinzu:  
    >   
    >  `options(repos=structure(c(CRAN="<mirror site URL>")))`  
    >   
    >  Wenn Sie ausführliche Informationen zu Voreinstellungen und anderen Dateien, die beim Start der R-Laufzeit geladen werden, anzeigen möchten, führen Sie diesen Befehl in einer R-Konsole aus:  
    >   
    >  `?Startup`  
  
5.  Wenn das Zielpaket von weiteren Paketen abhängig ist, werden die Abhängigkeiten vom R-Installationsprogramm automatisch heruntergeladen und installiert.  
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>Manuelle Paketinstallation oder Installation auf einem Computer ohne Internetzugang 

1. Wenn das Paket, das Sie installieren möchten, Abhängigkeiten aufweist, laden Sie die erforderlichen Pakete im Voraus herunter, und fügen Sie sie zum Ordner mit anderen komprimierten Paketdateien hinzu.

    > [!TIP]
    > 
    > Es wird empfohlen, dass Sie ein lokales Repository mithilfe von [MiniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) einrichten, wenn Sie häufig Offlineinstallationen von R-Paketen unterstützen müssen.  
  
2.  Geben Sie an der R-Eingabeaufforderung mit dem folgenden Befehl den Pfad und den Namen des zu installierenden Pakets an:  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    Dieser Befehl extrahiert das R-Paket aus der lokalen ZIP-Datei, sofern Sie die Kopie im Verzeichnis `C:\Temp\Downloaded packages`gespeichert haben, und installiert das Paket (mit seinen Abhängigkeiten) in der R-Bibliothek auf dem lokalen Computer.  
  
3.  Wenn Sie zuvor die R-Umgebung auf dem Computer geändert haben, sollten Sie sicherstellen, die die R-Umgebungsvariable `.libPath` nur einen Pfad verwendet, der auf den Ordner R_SERVICES für die Instanz verweist.  
  
> [!NOTE]
> Wenn Sie Microsoft R Server (eigenständig) zusätzlich zum SQL Server R Services installiert haben, erfolgt auf dem Computer eine separate Installation von R mit allen R-Tools und -Bibliotheken. In der Bibliothek R_SERVER installierte Pakete werden nur von Microsoft R-Server verwendet. Es besteht kein Zugriff durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
> 
>  Achten Sie darauf, dass Sie die R_SERVICES-Bibliothek beim Installieren von Paketen verwenden, die Sie in SQL Server verwenden möchten.

  
## <a name="see-also"></a>Siehe auch  
 [Einrichten von SQL Server R Services &#40;In-Database&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

