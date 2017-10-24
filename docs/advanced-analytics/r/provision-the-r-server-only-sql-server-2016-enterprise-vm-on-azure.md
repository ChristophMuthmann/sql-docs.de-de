---
title: "Bereitstellen eines virtuellen Computers für Machine Learning in Azure | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
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
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: 7cb9e069fc3b537f8aab9d048a152435ad0cc6ac
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>Bereitstellen eines virtuellen Computers für Machine Learning in Azure

Virtuelle Computer in Azure sind eine praktische Möglichkeit für einen vollständigen Server-Umgebung für den Machine learning-Lösungen schnell konfigurieren. Dieser Artikel führt einige Images virtueller Computer, die entweder R-Server, Machine Learning-Server oder SQL Server mit Machine Learning enthalten.

Diese Liste erhebt keinen umfassend, jedoch nur die Namen von Images, die auf Machine Learning-Server oder SQL Server Machine Learning-Services, um die Ermittlung zu ermöglichen beziehen bereitstellen.

> [!TIP]
> Es wird empfohlen, die neue Version der Azure-Portal und Azure Marketplace zu verwenden. Einige Images sind nicht verfügbar, wenn Sie dem Azure-Katalog im klassischen Portal durchsuchen.

## <a name="how-to-provision-a-virtual-machine"></a>Gewusst wie: Bereitstellen eine virtuellen Maschine

Wenn Sie mit der Azure-VMs nicht vertraut sind, wird empfohlen, dass Sie weitere Informationen zu mithilfe des Portals und Konfigurieren eines virtuellen Computers den folgenden Artikeln finden Sie unter.

+ [Virtuelle Computer – Erste Schritte](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Erste Schritte mit virtuellen Computern in Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

## <a name="find-a-machine-learning-image"></a>Suchen Sie ein Machine Learning-Bild

1. Klicken Sie auf der Azure-Portal (portal.azure.com) auf **VMs**, oder klicken Sie auf **neu**.

2. Suchen Sie das Suchfeld am oberen Rand der Seite, die Sie verwenden können, um Ressourcen nach Namen filtern. 

3. Geben Sie "R-Server" (oder "ML-Server") in der **Filter** Steuerelement, um eine Liste der zugehörigen Ressourcen anzuzeigen. Klicken Sie auf **Suche im Marketplace** auf virtuellen Computern finden Sie unter.

    > [!TIP]
    > 
    > Andere möglichen Zeichenfolgen für das Steuerelement Filter sind "Data Science" und "Machine Learning" auf.
    > 
    > Verwenden der `%` Platzhalter in die Suche der Namen von virtuellen Computern zu suchen. Sie können z. B. eingeben `"`% Julia %` or `%R % ".

4. Wählen Sie zum Abrufen von R Server für Windows **R Server nur SQL Server 2016 Enterprise**.
  
    [R Server](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) lizenziert ist, als eine Funktion, die SQL Server Enterprise Edition jedoch Version 9.1 als eigenständiger Server installiert ist und der Supportrichtlinie für moderne Lifecycle bedient wird.

    > [!NOTE] 
    > 
    > Dies fallen, schauen für die Version von einer neuen virtuellen Maschine, die SQL Server-2017 und die 9.2.1 enthält Machine Learning-Server-Version.
    > Bis dahin können Sie die Version von SQL Server auf diesem virtuellen Computer mithilfe von SQL Server-Installationscenter und Auswählen der Aktualisierungsoption aktualisieren. Weitere Informationen finden Sie unter [Aktualisieren von SQL Server mithilfe des Installations-Assistenten](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup).

5. Nachdem die virtuelle Maschine erstellt wurde und ausgeführt wird, klicken Sie auf die **verbinden** Schaltfläche, um eine Verbindung zu öffnen, und melden Sie sich mit dem neuen Computer.

5. Nachdem Sie eine Verbindung herstellen, können Sie zusätzliche R-Paket oder Ihrem bevorzugten Entwicklungstool installieren.

### <a name="install-additional-r-tools"></a>Zusätzliche R-Tools installieren

Microsoft R Server umfasst standardmäßig alle R-Tools, die mit einer Basisinstallation von R installiert werden, einschließlich RTerm und RGui. Das Verfahren abzukürzen, "rgui.exe" wurde auch auf dem Desktop hinzugefügt.

Möglicherweise möchten Sie jedoch zusätzliche R-Tools, z. B. RStudio, R-Tools für Visual Studio (RTVS) oder Microsoft R-Client installieren. Speicherorte und Anweisungen zum Herunterladen finden Sie über die folgenden Links:

+ [R-Tools für Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio für Windows](https://www.rstudio.com/products/rstudio/download/)

Nach Abschluss der Installation müssen Sie den Standardspeicherort für die R-Laufzeit ändern, sodass alle R-Entwicklungstools die Microsoft R Server-Bibliotheken verwenden.

### <a name="configure-r-server-to-support-web-services"></a>Konfigurieren von R-Server zur Unterstützung von Webdiensten

Zusätzliche Konfiguration ist erforderlich, um Web Service-Bereitstellung, Remoteausführung, verwenden oder R-Server als Deployment Server in Ihrer Organisation zu nutzen. Anweisungen hierzu finden Sie unter [R-Server konfigurieren, Analysen operationalisieren von](https://docs.microsoft.com/machine-learning-server/install/operationalize-r-server-one-box-config).

> [!NOTE]
> Wenn Sie nur Pakete, z. B. "revoscaler" oder MicrosoftML verwenden möchten, ist keine zusätzliche Konfiguration erforderlich.

## <a name="other-virtual-machines"></a>Andere virtuelle Maschinen

Die folgenden Bilder sind im Azure Marketplace verfügbar und enthalten vollständig konfiguriertes machine Learning-Tools, jedoch nicht notwendigerweise SQL Server.

### <a name="data-science-virtual-machine"></a>Data Science Virtual Machine

Dieses Image ist mit Microsoft R Server als auch Python (Anaconda-Verteilung), einem Jupyter Notebook-Server, Visual Studio Community Edition, Power BI Desktop, das Azure SDK und SQL Server Express Edition vorkonfiguriert.

Die Windows-Version unter Windows Server 2012 ausgeführt wird, und enthält viele spezielle Tools zum Modellieren und Analysen, einschließlich [CNTK](https://www.microsoft.com/cognitive-toolkit/), [MxNet](https://mxnet.incubator.apache.org/), und beliebte R-Pakete wie **Xgboost**.

Linux-Editionen werden für Ubuntu CentOS- und Centos CSP bereitgestellt und enthalten viele gängige Tools für Data Science und Entwicklung Aktivitäten.

Weitere Informationen finden Sie unter [Einführung zu Azure Data Science Virtual Machine für Linux und Windows](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-vm).

Dieses Image wurde vor kurzem aktualisiert, um einzuschließen: 

+ Unterstützung für Julia, die skalierbare, leistungsstarke Data Science-Sprache der Zukunft 
+ JupyterHub, die eine Option hilfreich ist, wenn Sie möchten, führen Sie eine Schulung und alle Studenten auf den gleichen Server freigeben, aber separate Notizbücher und Verzeichnisse verwenden möchten.

Weitere Informationen zu unterstützten Tools und Machine Learning-Frameworks finden Sie unter [Kennenlernen von Ihrem Data Science Virtual Machine](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-tools-overview)

### <a name="r-server-virtual-machines"></a>R Server-Maschinen

Zusätzlich zu den **R Server nur SQL Server 2016 Enterprise** Image, Sie können eigenständige virtuelle Maschinen mit R-Server abrufen. Images stehen für CentOS Linux-Version 7.2 Linux RedHat Version 7.2 und Ubuntu, Version 16.04.

Weitere Informationen finden Sie unter [Machine Learning-Server in der Cloud](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

 > [!NOTE]
 > Dieser virtuellen Computer ersetzen die **RRE für virtuelle Windows-Computer**, die zuvor in Azure Marketplace verfügbar waren.

### <a name="sql-server-virtual-machines"></a>SQL Server-Maschinen

Es gibt zwei Optionen für die Verwendung von SQL Server-Machine learning-in Azure:

+ Erhalten Sie eine der Abbilder der virtuellen Maschine, die SQL Server R Services vorinstalliert enthält.
+ Erstellen Sie virtueller Azure-Computer und installieren Sie SQL Server Enterprise oder Developer Edition, die mit Ihren eigenen Lizenzschlüssel. 
  
    Führen Sie Setup erneut aus, um hinzufügen und Machine learning-Dienst aktivieren, wie hier beschrieben: [Installing SQL Server R Services auf einem virtuellen Azure-Computer](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).
+ Erstellen einer Azure SQL-Datenbank mit einer Dienstebene, die Machine Learning unterstützen kann, und verwenden das neue Feature für R Services derzeit in der Vorschau an. Weitere Informationen finden Sie unter [Azure SQL-Datenbank](../r/using-r-in-azure-sql-database.md).

> [!NOTE]
> Derzeit wird SQL Server-Machine Learning-Services nicht auf die virtuelle Linux-Computer für SQL Server-2017 unterstützt. Allerdings können Sie die Bewertung auf einem trainierten Modell mit der VORHERSAGE von T-SQL-Funktion ausführen. Weitere Informationen finden Sie unter [in SQl Server Native Bewertung](../sql-native-scoring.md). 

### <a name="virtual-machines-for-deep-learning"></a>Virtuelle Computer für umfassenden lernen 

Zuvor bereitgestellten Microsoft Tiefe Learning-Toolkit für die Data Science Virtual Machine, die Sie zu einer vorhandenen Data Science Virtual Machine hinzufügen konnte. Dieses Toolkit wird nun von der Tiefe Learning virtuelle Maschine ersetzt, die beliebte umfassenden Lerntools enthält:

+ GPU-Editionen von umfassenden lernen Frameworks wie z. B. Microsoft Cognitive Toolkit, TensorFlow Keras und Caffe
+ Integrierte GPU-Treiber
+ Eine Sammlung von Tools, Bild und Textverarbeitung
+ Enterprise-Entwicklungstools wie z. B. Microsoft R Server Developer Edition, Anaconda-Python Jupyter Notebooks für Python und R
+ Entwicklungstools für Python, R, SQL Server und vieles mehr
+ End-to-End-Beispiele für Bild und Text-Kenntnisse

Die Tiefe Learning-Computer ist entweder auf dem Windows 2016 oder Ubuntu Linux-Plattformen verfügbar. Weitere Informationen finden Sie unter [umfassenden lernen und AI-Frameworks](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-deep-learning-ai-frameworks).

> [!IMPORTANT]
> 
> Bereitstellen von dieser virtuellen Maschine müssen Images virtueller Computer Azure GPU NC-Serie, die in Azure-Regionen beschränkt zur Verfügung stehen. Informationen zur Verfügbarkeit finden Sie unter [verfügbaren Produkte nach Region](https://azure.microsoft.com/en-us/regions/services/). Wenn Sie die virtuelle Maschine bereitstellen, achten Sie darauf, verwenden **HDD** als den Datenträgertyp nicht **SSD**.

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

Dieser Abschnitt enthält einige häufig gestellte Fragen zu den Machine learning-virtuellen Computern von Microsoft.

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>Kann ich einen virtuellen Computer mit SQL Server-2017 installieren?

Eine Windows-basierte virtuelle Maschine für SQL Server 2017 Enterprise Edition, die Machine Learning Services umfasst wird bald verfügbar sein. Suchen Sie nach Ankündigungen an diesen Standorten Blogs:

+ [Cortana Intelligence und machine Learning](https://blogs.technet.microsoft.com/machinelearning/)
+ [Data Platform-Insider](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>Wie greife ich auf Daten im Azure Storage-Konto zu?

Wenn Sie Daten aus Ihrem Azure-Konto verwenden möchten, stehen mehrere Optionen für den Zugriff auf die Daten oder zum Verschieben der Daten zur Verfügung:

+ Kopieren Sie die Daten aus dem Speicherkonto mit einem Hilfsprogramm wie [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)in das lokale Dateisystem. 

+ Fügen Sie die Dateien zu einer Dateifreigabe des Speicherkontos hinzu, und binden Sie anschließend die Dateifreigabe als Netzlaufwerk auf Ihrem virtuellen Computer ein.  Weitere Informationen finden Sie unter [Einbinden von Azure-Dateien](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>Wie verwende ich Daten aus Azure Data Lake Storage (ADLS)?

ADLS-Speicher mithilfe des "revoscaler", können Daten gelesen werden, wenn Sie auf das Speicherkonto, das die gleiche Weise wie würden Sie eine HDFS-Dateisystem, mithilfe von WebHDFS verweisen.  Weitere Informationen finden Sie im Artikel: [mithilfe von R für FileSystem-Vorgänge auf Azure Data Lake-Speicher](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/).



