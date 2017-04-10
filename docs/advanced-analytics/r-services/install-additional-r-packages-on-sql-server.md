---
title: "Installieren zus&#228;tzlicher R-Pakete unter SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# Installieren zus&#228;tzlicher R-Pakete unter SQL Server
In diesem Thema wird beschrieben, wie zum Installieren von neuen R-Pakete mit einer Instanz von [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] auf einem Computer, der Zugriff auf das Internet hat.

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1. Suchen Sie die Windows-Binärdateien im ZIP-Dateiformats

R-Pakete werden auf vielen Plattformen unterstützt. Sie müssen sicherstellen, dass das Paket, das Sie installieren möchten, ein binäres Format für die Windows-Plattform verfügt. Andernfalls kann das heruntergeladene Paket nicht ausgeführt werden.

Zum Abrufen des [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) -Pakets von Bioconductor, gehen Sie folgendermaßen vor:  
  
1.  Suchen Sie in der Liste der **Paketarchive** die **Windows-Binärdateiversion** .  
  
2.  Klicken Sie mit der rechten Maustaste auf den Link zur ZIP-Datei, und wählen Sie  **Ziel speichern unter**aus.  
  
3.  Navigieren Sie zum lokalen Ordner, in dem die komprimierten Pakete gespeichert sind, und klicken Sie auf **Speichern**.  
  
 Dieser Prozess wird eine lokale Kopie des Pakets erstellt. Sie können anschließend installieren Sie das Paket, oder kopieren das ZIP-Paket auf einen Server, die über keinen Zugriff auf das Internet.  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2. Öffnen Sie die Standard-R-Paket-Bibliothek für SQL Server R Services 

Navigieren Sie zu dem Ordner auf dem Server, auf dem die R-Pakete zugeordneten [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert wurde. Es ist wichtig, dass Sie in der Standardbibliothek Pakete installieren, die der aktuellen Instanz zugeordnet ist. 

Informationen zu dieser Bibliothek finden Sie unter [Installieren und Verwalten von R-Pakete](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).

   Für jede Instanz, in dem Sie ein Paket ausgeführt wird, müssen Sie eine separate Kopie der Pakete installieren. Derzeit können keine Pakete über Instanzen freigegeben werden.
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3. Öffnen Sie eine administratoreingabeaufforderung 

Öffnen Sie R als Administrator.  Dies ist mithilfe der Windows-Befehl p Ropt, oder mithilfe einer R-Hilfsprogrammen möglich.
  
### <a name="using-the-windows-command-prompt"></a>Unter Verwendung der Eingabeaufforderung von Windows 

1. Öffnen Sie eine Windows-Eingabeaufforderung als Administrator, und navigieren Sie zu dem Verzeichnis, in dem die RTerm.Exe "oder" RGui.exe-Dateien gespeichert sind.  
  
    In einer Standardinstallation ist dies das R-Verzeichnis **\bin** . Beispielsweise ist in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], R-Tools befinden sich hier: 

    **Standardinstanz**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **Benannte Instanz**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. Führen Sie **R.Exe**aus.  
  
### <a name="using-the-r-commandline-utilities"></a>Unter Verwendung der R-Befehlszeilen-Hilfsprogramme 
  
1. Verwenden Sie Windows Explorer, um zum Verzeichnis mit den R-Tools zu navigieren.  
  
2. Mit der rechten Maustaste **RGui.exe** oder **RTerm.exe**, und wählen Sie **als Administrator ausführen**.  
## <a name="4-install-the-package"></a>4. Installieren Sie das Paket

Der R-Befehl zum Installieren des Pakets, hängt davon ab, ob Sie das Paket aus dem Internet oder aus einer lokalen ZIP-Datei ausgegeben werden.  
  
### <a name="install-package-from-internet"></a>Installieren des Pakets aus dem Internet  
  
1.  Im Allgemeinen verwenden Sie den folgenden Befehl ein neues Paket aus CRAN oder einem der Spiegelung Standorte zu installieren.  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    Beachten Sie, dass für den Namen des Pakets immer doppelte Anführungszeichen erforderlich sind.

2.  Verwenden Sie einen Befehl wie diese zum Festlegen der Bibliothek, zum Angeben der Bibliotheks, in dem das Paket installiert werden soll:
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    Beachten Sie, dass für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], derzeit nur ein einzelnes Paket Bibliothek ist zulässig. Pakete in einer Benutzerbibliothek nicht installieren, oder Sie werden nicht in der Lage sind, führen Sie das Paket von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
     
3.  Der Speicherort der Bibliothek definieren, installiert die folgende Anweisung das beliebte e1070-Paket in der Paket-Bibliothek, die von R Services verwendete.  
  
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
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>Manuelle Paketinstallation oder auf Computer ohne Internetzugang installieren 

1. Wenn das Paket, das Sie installieren möchten Abhängigkeiten aufweist, erhalten Sie die erforderlichen Pakete voraus, und fügen Sie sie zum Ordner mit anderen Paket ZIP-Dateien.

    > [!TIP]
    > 
    > Es wird empfohlen, dass Sie ein lokales Repository eingerichtet [MiniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) Wenn häufige offline-Installation von R-Paketen unterstützt werden müssen.  
  
2.  Geben Sie an der R-Eingabeaufforderung mit dem folgenden Befehl den Pfad und den Namen des zu installierenden Pakets an:  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    Dieser Befehl extrahiert das R-Paket aus der lokalen ZIP-Datei, sofern Sie die Kopie im Verzeichnis gespeichert ist `C:\Temp\Downloaded packages`, und das Paket (mit seinen Abhängigkeiten) in der R-Bibliothek auf dem lokalen Computer installiert.  
  
3.  Wenn Sie zuvor die R-Umgebung auf dem Computer geändert haben, Sie sollten sicherstellen, dass die R-Umgebungsvariable `.libPath` verwendet nur ein Pfad, die auf den Ordner R_SERVICES für die Instanz verweist.  
  
> [!NOTE]
> Wenn Sie Microsoft R Server (eigenständig) zusätzlich zu SQL Server R Services installiert haben, müssen der Computer eine separate Installation von R mit allen erforderlichen R-Tools und Bibliotheken. Pakete, die in der Bibliothek R_SERVER installiert sind, werden nur von Microsoft R Server verwendet und kann nicht zugegriffen werden, indem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
> 
>  Achten Sie darauf, dass Sie die R_SERVICES-Bibliothek verwenden, Installieren von Paketen, die Sie in SQL Server verwenden möchten.

  
## <a name="see-also"></a>Siehe auch  
 [Einrichten von SQL Server R Services &#40; In-Database &#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  