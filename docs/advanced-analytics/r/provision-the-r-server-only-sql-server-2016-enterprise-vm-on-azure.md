---
title: 'Bereitstellen von R Server: Nur SQL Server 2016 Enterprise VM in Azure | Microsoft-Dokumentation'
ms.custom: 
ms.date: 06/05/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3bfca0753984f09220d8ca4e4f6933c949daf2b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-analytics-virtual-machines-on-azure"></a>Advanced Analytics-VMs in Azure

Virtuelle Computer in Azure sind eine praktische Möglichkeit für einen vollständigen Server-Umgebung für den Machine learning-Lösungen schnell konfigurieren. Dieses Thema enthält einige Images virtueller Computer, die R-Server, SQL Server mit Machine Learning oder anderen Data Science-Tools von Microsoft enthalten.

> [!TIP]
> Es wird empfohlen, die neue Version der Azure-Portal und Azure Marketplace zu verwenden. Einige Images sind nicht verfügbar, wenn Sie dem Azure-Katalog im klassischen Portal durchsuchen.

Azure Marketplace enthält mehrere virtuelle Computer, die Data Science unterstützen. Diese Liste erhebt keinen zu umfassend, geben jedoch nur die Namen von Bildern, die Microsoft R Server oder SQL Server-Machine learning-Services, um die Ermittlung zu vereinfachen.

## <a name="how-to-provision-a-vm"></a>Gewusst wie: Bereitstellen ein virtuellen Computers

Wenn Sie mit der Azure-VMs nicht vertraut sind, wird empfohlen, dass Sie weitere Informationen zu mithilfe des Portals und Konfigurieren eines virtuellen Computers den folgenden Artikeln finden Sie unter.

+ [Virtuelle Computer – Erste Schritte](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Erste Schritte mit virtuellen Computern in Windows](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/)

### <a name="find-an-image"></a>Suchen Sie ein Bild

1. Klicken Sie auf der Azure-Dashboard auf **Marketplace**.

    - Klicken Sie auf **Intelligence und Analysen** oder **Datenbanken**, und geben Sie "R" in der **Filter** Steuerelement, um eine Liste der R-Server-Computer anzuzeigen.
    - Weitere mögliche Zeichenfolgen, die für die **Filter** Steuerelement sind *Data Science* und *machine Learning*
    - Verwenden Sie das Platzhalterzeichen % in suchen, um VM-Namen suchen, die eine Zielzeichenfolge, wie z. B. enthalten *R* oder *Julia*.

2. Wählen Sie zum Abrufen von R Server für Windows **R Server nur SQL Server 2016 Enterprise**.
  
    [R Server](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) wie eine Funktion von SQL Server Enterprise Edition, jedoch mit Version 9.1 lizenziert ist. als eigenständiger Server installiert ist und der Supportrichtlinie für moderne Lifecycle bedient.

3. Nachdem der virtuelle Computer erstellt wurde und ausgeführt wird, klicken Sie auf die Schaltfläche **Verbinden** , um eine Verbindung herzustellen und sich auf dem neuen Computer anzumelden.

4. Nachdem Sie eine Verbindung herstellen, müssen Sie möglicherweise zusätzliche R-Tools oder Entwicklungstools installieren.

### <a name="install-additional-r-tools"></a>Zusätzliche R-Tools installieren

Microsoft R Server umfasst standardmäßig alle R-Tools, die mit einer Basisinstallation von R installiert werden, einschließlich RTerm und RGui. Es wurde eine Verknüpfung mit RGui zum Desktop hinzugefügt, falls Sie direkt mit der Verwendung von R beginnen möchten.

Möglicherweise möchten Sie jedoch zusätzliche R-Tools, z. B. RStudio, die R-Tools für Visual Studio (RTVS) oder Microsoft R-Client installieren. Speicherorte und Anweisungen zum Herunterladen finden Sie über die folgenden Links:
+ [R-Tools für Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio für Windows](https://www.rstudio.com/products/rstudio/download/)

Nach Abschluss der Installation müssen Sie den Standardspeicherort für die R-Laufzeit ändern, sodass alle R-Entwicklungstools die Microsoft R Server-Bibliotheken verwenden.

### <a name="configure-server-for-web-services"></a>Konfigurieren der Server für Webdienste

Enthält der virtuelle Computer R Server, sind zusätzliche Konfigurationsschritte erforderlich, um die Web Service-Bereitstellung und Remoteausführung, oder den R Server als Bereitstellungsserver in Ihrem Unternehmen zu nutzen. Eine Anleitung hierzu finden Sie unter [Configure R Server for Operationalization](https://msdn.microsoft.com/microsoft-r/operationalize/configuration-initial) (R Serverkonfiguration für Operationalisierung).

> [!NOTE]
> Wenn Sie nur Pakete, z. B. "revoscaler" oder MicrosoftML verwenden möchten, ist keine zusätzliche Konfiguration erforderlich.

## <a name="r-server-images"></a>R Server-Images

### <a name="microsoft-data-science-virtual-machine"></a>Microsoft Data Science Virtual Machine

Ist mit Microsoft R Server als auch Python (Anaconda-Verteilung), einem Jupyter Notebook-Server, Visual Studio Community Edition, Power BI Desktop, das Azure SDK und SQL Server Express Edition konfiguriert.

Die Windows-Version unter Windows Server 2012 ausgeführt wird, und viele spezielle Tools zum Modellieren und Analysen, einschließlich CNTK und Mxnet, z. B. Xgboost und Vowpal Wabbit beliebten R-Pakete enthält.

### <a name="linux-data-science-virtual-machine"></a>Linux Data Science Virtual Machine

Enthält auch die gängigen Tools für Data Science und Entwicklung Aktivitäten, einschließlich Microsoft R Open, Microsoft R Server Developer Edition, Anaconda Python und Jupyter Notebooks für R, Python und Julia.

Dieses VM-Image wurde vor kurzem aktualisiert, um JupyterHub, open Source-Software enthalten, die über verschiedene Authentifizierungsmethoden, einschließlich der Authentifizierung von OS-Konto und die Authentifizierung des Github-Konto von mehreren Benutzern verwendet werden können. JupyterHub ist eine besonders Option aus, wenn Sie verwenden möchten, führen Sie eine Schulung und alle Studenten auf den gleichen Server freigeben, aber separate Notizbücher und Verzeichnisse verwenden möchten.

Bilder werden für Ubuntu CentOS- und Centos CSP bereitgestellt.

### <a name="r-server-only-sql-server-2016-enterprise"></a>R Server nur SQL Server 2016 Enterprise

Diese virtuelle Maschine enthält ein eigenständiges Installationsprogramm für den [R Server 9.1.](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) die das neue Lizenzierungsmodell moderne Softwarelebenszyklus unterstützt.

 R-Server ist auch in Bildern für CentOS Linux-Version 7.2 Linux RedHat Version 7.2 und Ubuntu, Version 16.04 verfügbar.

 > [!NOTE]
 > Dieser virtuellen Computer ersetzen die **RRE für virtuelle Windows-Computer**, die zuvor in Azure Marketplace verfügbar waren.

## <a name="sql-server-images"></a>SQL Server-Images

Wenn R Services (Datenbankintern) "oder" Machine Learning-Dienste verwenden möchten, müssen Sie eine der SQL Server Enterprise oder Developer Edition virtuellen Computer installieren und Machine learning-Dienst hinzufügen, wie hier beschrieben: [Installieren von SQL Server R Services auf einem Virtuellen Azure-Computer](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

> [!NOTE]
> Derzeit werden Machine Learning-Dienste nicht auf die virtuelle Linux-Computer für die SQL Server-2017 oder in Azure SQL-Datenbank unterstützt. Sie müssen SQL Server 2016 SP1 oder SQL Server-2017 für Windows verwenden.

Die Data Science Virtual Machine umfasst auch SQL Server 2016 mit der R-Services-Funktion bereits aktiviert.


## <a name="other-vms"></a>Andere virtuelle Maschinen

### <a name="deep-learning-toolkit-for-the-data-science-virtual-machine"></a>Deep-Toolkit für die Data Science Virtual Machine Learning

Diese virtuelle Maschine enthält die gleichen Machine learning-Tools auf die Data Science Virtual Machine, jedoch mit GPU-Versionen von Mxnet, CNTK TensorFlow und Keras. Dieses Image kann nur auf Azure-GPU-N-Serie Instanzen verwendet werden. 

Die umfassenden lernen Toolkit bietet auch eine Reihe von Tiefen learning-Lösungen, in denen die GPU simulieren, z. B. bilderkennung für die CIFAR-10-Datenbank und ein Zeichen Recognition-Beispiel für die Datenbank MNIST Beispiel. GPU-Instanzen sind derzeit im Süd/Mitte, Osten USA, Westeuropa und Südostasien verfügbar.

> [!IMPORTANT]
> GPU-Instanzen sind derzeit nur in den USA (Süden, Mitte) verfügbar.


## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>Kann ich einen virtuellen Computer mit SQL Server-2017 installieren?

Images sind verfügbar, enthalten SQL Server 2017 CTP 2.0 für Linux-Umgebungen, aber diese Umgebungen unterstützen derzeit keine Machine Learning-Dienste. 

Eine Windows-basierte virtuelle Maschine für SQL Server 2017 Enterprise Edition, die Machine Learning Services umfasst, wird nach der Veröffentlichung verfügbar sein. 

Als Alternative können Sie das Image von SQL Server 2016 verwenden und upgrade Ihrer Instanz von R, wie hier beschrieben: [aktualisieren eine Instanz durch SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). 

Oder Erstellen eines virtuellen Computers und die Vorschau CTP 2.0 herunterladen [SQL Server-2017](https://www.microsoft.com/sql-server/sql-server-2017).

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>Wie greife ich auf Daten im Azure Storage-Konto zu?

Wenn Sie Daten aus Ihrem Azure-Konto verwenden möchten, stehen mehrere Optionen für den Zugriff auf die Daten oder zum Verschieben der Daten zur Verfügung:

+ Kopieren Sie die Daten aus dem Speicherkonto mit einem Hilfsprogramm wie [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)in das lokale Dateisystem. 

+ Fügen Sie die Dateien zu einer Dateifreigabe des Speicherkontos hinzu, und binden Sie anschließend die Dateifreigabe als Netzlaufwerk auf Ihrem virtuellen Computer ein.  Weitere Informationen finden Sie unter [Einbinden von Azure-Dateien](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>Wie verwende ich Daten aus Azure Data Lake Storage (ADLS)?

ADLS-Speicher mithilfe des "revoscaler", können Daten gelesen werden, wenn Sie auf das Speicherkonto, das die gleiche Weise wie würden Sie eine HDFS-Dateisystem, mithilfe von WebHDFS verweisen.  Weitere Informationen finden Sie im Artikel: [mithilfe von R für FileSystem-Vorgänge auf Azure Data Lake-Speicher](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/).

## <a name="see-also"></a>Siehe auch

[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)


