---
title: "Bereitstellen von R Server – Nur SQL Server 2016 Enterprise VM in Azure | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# Bereitstellen von R Server – Nur SQL Server 2016 Enterprise VM in Azure

„Bereitstellen von R Server – Nur SQL Server 2016 Enterprise VM in Azure“ ist eine neue Option zur schnellen und einfachen Konfiguration einer Serverumgebung, um R-Lösungen zu unterstützen. Dieser virtuelle Azure-Computer wurde mit Microsoft R Server (eigenständige Version) vorkonfiguriert. 

Dieser neue virtuelle Computer ersetzt die RRE für virtuelle Windows-Computer, die zuvor in Azure Marketplace verfügbar war. 

Dieser virtuelle Computer umfasst auch DeployR Enterprise zum Bereitstellen von R-Analysen in Anwendungen und Back-End-Systemen. Weitere Informationen finden Sie unter [Informationen zu DeployR](https://msdn.microsoft.com/microsoft-r/deployr-about).


## Bereitstellen des virtuellen R Server-Computers

Wenn Sie mit der Verwendung von virtuellen Azure-Computern nicht vertraut sind, wird empfohlen, dass Sie diesen Artikel lesen, um weitere Informationen zum Verwenden des Portals und zum Konfigurieren eines virtuellen Computers zu erhalten.
[Virtuelle Computer – Erste Schritte](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)

So erstellen Sie den virtuellen R Server-Computer über Microsoft Azure Marketplace 
1. Klicken Sie auf **Virtuelle Computer**, und geben Sie *R Server* in das Suchfeld ein.
2. Wählen Sie **R Server – Nur SQL Server 2016 Enterprise** aus.
3. Fahren Sie mit der Bereitstellung des virtuellen Computers gemäß der Beschreibung in diesem Artikel fort: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/) 
7. Nachdem der virtuelle Computer erstellt wurde und ausgeführt wird, klicken Sie auf die Schaltfläche **Verbinden**, um eine Verbindung herzustellen und sich auf dem neuen Computer anzumelden.
8. Wenn Sie eine Verbindung herstellen, wird der **Server-Manager** standardmäßig geöffnet, es ist jedoch keine zusätzliche Serverkonfiguration erforderlich. Schließen Sie den **Server-Manager**, um zum Desktop zu wechseln, und fahren Sie dann mit den nächsten Schritten fort:
    + Installieren zusätzlicher R-Tools oder Entwicklungstools
    + Konfigurieren von DeployR  

So finden Sie den virtuellen R Server-Computer im klassischen Azure-Portal
1. Klicken Sie auf **Virtuelle Computer** und dann auf **NEU**.
2. Im Bereich **Neu** sollten **Compute** und **Virtueller Computer** bereits ausgewählt sein. 
3. Klicken Sie auf **Aus Galerie**, um die VM-Images zu suchen. Sie können *R Server* in das Suchfeld eingeben, oder klicken Sie auf **Microsoft**, und scrollen Sie dann nach unten, bis **R Server – Nur SQL Server 2016 Enterprise** angezeigt wird.


## Installieren der R-Tools
Microsoft R Server umfasst standardmäßig alle R-Tools, die mit einer Basisinstallation von R installiert werden, einschließlich RTerm und RGui. Es wurde eine Verknüpfung mit RGui zum Desktop hinzugefügt, falls Sie direkt mit der Verwendung von R beginnen möchten.

Möglicherweise möchten Sie jedoch zusätzliche R-Tools installieren, z. B. RStudio, R-Tools für Visual Studio oder Microsoft R Client. Speicherorte und Anweisungen zum Herunterladen finden Sie über die folgenden Links:
+ [R-Tools für Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio für Windows](https://www.rstudio.com/products/rstudio/download/)

Nachdem Sie diese Tools installiert haben, achten Sie darauf, dass Sie die Tools auf die R Server-Bibliotheken verweisen.

## Verwenden von DeployR auf dem virtuellen Computer

Es sind einige zusätzliche Schritte erforderlich, um die DeployR-Instanz verwenden, die auf diesem virtuellen Computer installiert ist. 

So konfigurieren Sie die DeployR-Instanz

1. Öffnen Sie auf dem virtuellen Computer das **Hilfsprogramm DeployR Administrator**.
2. Legen Sie das Administratorkennwort für DeployR gemäß der folgenden Beschreibung fest: [Schritte nach der Installation](https://msdn.microsoft.com/microsoft-r/deployr-install-on-windows)
3. Legen Sie den DeployR Web-Kontext fest. Weitere Informationen finden Sie unter [Installation von DeployR Administrator in der Cloud](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud). 
4. Öffnen Sie auf dem virtuellen Computer die entsprechenden Ports gemäß der folgenden Beschreibung: [Konfigurieren von Azure-Endpunkten](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#configuring-azure-endpoints). 
4. Aktualisieren Sie die Windows-Firewall gemäß der folgenden Beschreibung: [Aktualisieren der Firewall](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#updating-the-firewall). 

## Zugreifen auf Daten in einem Azure-Speicherkonto 

Wenn Sie Daten aus Ihrem Azure-Konto verwenden möchten, stehen mehrere Optionen für den Zugriff auf die Daten oder zum Verschieben der Daten zur Verfügung:


+ Kopieren Sie die Daten aus dem Speicherkonto mit einem Hilfsprogramm wie [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only) in das lokale Dateisystem. 

+ Fügen Sie die Dateien zu einer Dateifreigabe des Speicherkontos hinzu, und binden Sie anschließend die Dateifreigabe als Netzlaufwerk auf Ihrem virtuellen Computer ein.  Weitere Informationen finden Sie unter [Einbinden von Azure-Dateien](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

## Verwenden von Daten in einem ADLS-Konto (Azure Data Lake Storage)

Sie können Daten mithilfe von ScaleR aus einem ADLS-Speicher lesen, wenn Sie auf das Speicherkonto auf dieselbe Weise verweisen, wie Sie bei einem HDFS-Dateisystem mit webHDFS vorgehen würden.  Weitere Informationen finden Sie in diesem [Einrichtungsleitfaden](http://go.microsoft.com/fwlink/?LinkId=723452).

## Ressourcen

Weitere Dokumentationen zu Microsoft R finden Sie in der MSDN Library: [R-Server und Scale R](https://msdn.microsoft.com/microsoft-r)  


Allgemeine Informationen zu R finden Sie in den folgenden zusätzlichen Ressourcen: 
+ [DataCamp](http://www.datacamp.com): Bietet eine kostenlose Einführung und einen fortgeschrittenen Kurs zu R sowie einen Kurs zum Arbeiten mit Big Data mit Revolution R.
+ [Stack Overflow](http://www.stackoverflow.com): Eine geeignete Ressource für die R-Programmierung und Fragen zu ML-Tools. 
+ [Cross Validated](https://stats.stackexchange.com/): Website für Fragen zu statistischen Machine Learning-Problemen.
+ [Adressenlistenarchive für R Help](https://www.r-project.org/mail.html): Geeignete Ressource für Verlaufsinformationen. 
+ [MRAN-Website](https://mran.microsoft.com/documents/getting-started/): Viele weitere R-Ressourcen.  

## Siehe auch
[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)
