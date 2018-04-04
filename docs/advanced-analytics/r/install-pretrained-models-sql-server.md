---
title: Installieren von Pre-tained Machine Learning-Modellen in SQL Server | Microsoft Docs
ms.date: 03/14/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: c9895584e53f488c0db15ad533ba4a2230ae60c4
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Installieren Sie Pre-tained Machine learning-Modelle mit SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Artikel wird beschrieben, wie Pre-tained Modelle mit einer Instanz von SQL Server hinzufügen, die bereits über R Services oder SQL Server-Machine Learning-Services installiert. 

Pre-tained Modelle, die zum Unterstützen von Kunden, die Aufgaben wie das Sentiment Analysis "oder" Image merkmalbereitstellung müssen, jedoch nicht die Ressourcen zum Abrufen großer Datasets oder ein komplexes Modell trainieren besitzen, vorhanden sein. Das Team Machine Learning-Server erstellt und trainiert diese Modelle können Sie den ersten Schritten für Text- und effizient verarbeiten. Weitere Informationen finden Sie unter der [Ressourcen](#bkmk_resources) Abschnitt dieses Artikels.

Ein Beispiel dafür, wie mithilfe der Pre-tained Modelle mit SQL Server-Daten finden Sie unter diesem Blogbeitrag vom SQL Server-Machine Learning-Team: [stimmungsanalyse mit Python in SQL Server-Machine Learning-Services](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="pre-trained-model-availability"></a>Pre-trained Model-Verfügbarkeit

Pre-tained Modelle werden mithilfe des Installationsmediums Microsoft Machine Learning-Server (oder Microsoft R Server, wenn Sie Modelle auf eine SQL Server 2016-Installation hinzufügen) installiert. Die kostenlose Developer Edition können Sie um die Modelle zu installieren. Es ist keine zusätzliche Kosten mit Model-Installation. 

Pre-tained Modelle funktionieren mit der folgenden Produkte und Sprachen. Das Setup-Programm erkennt Sprache Integration, die MicrosoftML oder Microsoftml-Bibliothek und fügt dann die vorab trainierten Modelle in der jeweiligen-Bibliothek. Beim Modell-Installation abgeschlossen ist, können Sie die Modelle über Bibliotheksfunktionen.

+ SQL Server 2016 R Services (Datenbankintern) - R nur mit der [MicrosoftML-Bibliothek](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ SQL Server 2016 R Server (eigenständig) - R nur mit der [MicrosoftML-Bibliothek](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ SQL Server 2017 Machine Learning Services (Datenbankintern) - R mit [MicrosoftML Bibliothek] (https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), Python, mit der [Microsoftml-Bibliothek](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
+ SQL Server 2017 Machine Learning-Server (eigenständig) - R mit [MicrosoftML Bibliothek] (https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), Python, mit der [Microsoftml-Bibliothek](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)

Während des Installationsvorgangs unterscheidet sich abhängig von Ihrer Version von SQL Server. Finden Sie unter den folgenden Abschnitten Anweisungen für die einzelnen Versionen.

> [!NOTE]
> Es ist nicht möglich, zu lesen oder ändern die vorab trainierten Modelle. Sie werden komprimiert, ein systemeigenes Format verwenden, um die Leistung zu verbessern.

## <a name="obtain-files-for-an-offline-installation"></a>Dateien für eine Offlineinstallation abrufen

Um die vorab trainierten Modelle auf einem Server installieren, die nicht über Internetzugriff verfügt, müssen Sie die entsprechenden Installationsprogramme im Voraus herunterladen und kopieren Sie den Installer in einen lokalen Ordner auf dem Server. 

Finden Sie auf dieser Seite die Downloadlinks für alle R-Server und Machine Learning Server Installationsprogramme: [Offline-Installation](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

## <a name="install-pre-trained-models-on-sql-server-2016-r-services"></a>Installieren Sie vorab trainierten Modelle auf SQL Server 2016 R Services

Mit SQL Server 2016 können Sie installieren und verwenden Sie Pre-tained R-Modelle aus, nur dann, wenn upgrade Machine learning-Komponenten in einem Vorgang namens **Bindung**. 

Hierzu separaten Windows Installer für Microsoft R Server "oder" Machine Learning-Server auf einem Computer, eine SQL Server 2016-R-Services-Installation und in der Auswahl einer Instanz oder Instanzen ausgeführt **binden**. Binden eine Instanz bedeutet, die die Support-Richtlinie mit der Instanz verknüpft wird geändert, um r häufiger Updates zulassen 

1. Starten Sie den separaten Windows-basierten Installer entweder [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) oder [Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Wählen Sie die Instanz zu aktualisieren, und wählen Sie dann die Option aus, um die vorab trainierten Modelle abzurufen.

    Weitere Informationen finden Sie unter [Aktualisieren des Machine Learning-Komponenten von SQL Server verwendeten](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

    Wenn Sie zuvor ausgeführt, haben Bindung zum Aktualisieren der R-Komponenten und nur die Pre-tained Modelle hinzufügen möchten, lassen Sie alle vorherigen Auswahl **als**, und wählen Sie die Option vorab trainierten Modelle. 
    
    Deaktivieren Sie alle zuvor ausgewählten Optionen nicht; Wenn Sie dies tun, entfernt das Installationsprogramm die Komponenten an.

3. Es wird empfohlen, dass Sie die Standardeinstellungen für die Modell-Speicherorte akzeptieren.

4. Akzeptieren Sie alle anderen aufforderungen, einschließlich der Lizenzverträge.

Nach Abschluss der Bindung werden die R-Version und Bibliotheken, die der Instanz zugeordneten mit neueren Versionen bereitgestellten in R-Server "oder" Machine Learning-Server ersetzt. 

Mit SQL Server 2016 müssen Sie einige zusätzliche Schritte zum Registrieren die Modelle mit der SQL Server 2016-Instanz-Bibliothek ausführen. Wiederholen Sie diese Schritte für jede Instanz, auf dem die Pre-tained Modelle installiert.

1. Öffnen Sie Windows-Eingabeaufforderung **als Administrator**.

2. Navigieren Sie zu dem Ordner "Setup bootstrap", für SQL Server, die auch vom Microsoft-R-Installationsprogramm enthält. In einer Standardinstanz von SQL Server 2016 wäre die Ordner:
    
    `C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\SQL2017\x64\`

3. Führen Sie `RSetup.exe` und geben Sie an die Komponente zu installieren, die Version und den Ordner, der der Quelldateien für das Modell mithilfe dieser Syntax enthält:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`installiert haben. 

    Die folgenden Werte sind für den "Version"-Parameter unterstützt:

    + Release Candidate-0: **9.1.0.0**
    + Release Candidate 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + Kumulatives Update 1: **9.2.0.24**
    + Kumulatives Update 4: **9.3.0**

    > [!NOTE]
    > Die entsprechenden SQL Server-Versionen sind aufgeführt, um Ihnen einen Überblick über die Zeit zu geben, die das Update veröffentlicht wurde. Wenn Sie nicht genau wissen, die Version, die mit SQL Server installiert sind, öffnen Sie den Ordner R_SERVICES für die Instanz, und öffnen Sie "rgui.exe" (`~\R_SERVICES\bin\x64`). Der erste Bildschirm Listet die Versionen für die Version von Microsoft R Open und Machine Learning-Server. 

    Z. B. mithilfe von Pre-tained R-Modelle mit einer Standardinstanz von **R_SERVICES**, würden Sie diesen Befehl ausführen:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Auf einer benannten Instanz wäre der Befehl etwa wie folgt:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

4. Wenn die Installation erfolgreich ist, sollte der folgenden Modelle hinzugefügt werden, auf Ihre `R_SERVICES` Ordner:

    + AlexNet\_Updated.model
    + ImageNet1K\_mean.xml
    + pretrained.Model
    + ResNet\_101\_Updated.model
    + ResNet\_18\_Updated.model
    + ResNet\_50\_Updated.model

## <a name="install-pre-trained-models-on-sql-server-machine-learning-services-in-database"></a>Installieren Sie vorab trainierten Modelle auf SQL Server Machine Learning-Services (Datenbankintern)

Wenn Sie SQL Server-2017 bereits installiert haben, können Sie die vorab trainierten Modelle auf zwei Arten abrufen:

+ Aktualisieren Sie die Python- und R-Komponenten mithilfe der Bindung, und installieren Sie die vorab trainierten Modelle zur gleichen Zeit
+ Installieren Sie nur die Pre-tained Modelle

Die folgenden Anweisungen beschreiben das Verfahren zum Aktualisieren der Machine Learning-Komponenten und Abrufen von Pre-tained Modelle zur gleichen Zeit.

1. Führen Sie das Windows-basierten-Installationsprogramm für Machine Learning-Server. Sie können das Installationsprogramm unter den Links auf dieser Seite herunterladen: [Machine Learning-Server für Windows installieren](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Wenn Sie die Modelle auf einem Server, der nicht über Internetzugriff verfügt installieren, stellen Sie sicher, dass das Installationsprogramm für die Pre-tained Modelle auch auf dieser Seite herunterladen: [Offline-Installation für Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline).

3. Führen Sie das Installationsprogramm an.

4. Wählen Sie die Sprache (R, Python oder beides), die Sie aktualisieren möchten, um die R oder Python-Komponenten zur gleichen Zeit zu aktualisieren.

    Wenn Sie zuvor Machine Learning-Server installiert und aktualisiert R oder Python-Komponenten, die die Bindung verwenden, lassen Sie alle vorherigen Auswahl **als**, und wählen Sie die Optionen für die Pre-tained Modelle. Deaktivieren Sie alle zuvor ausgewählten Optionen nicht; Wenn Sie dies tun, entfernt das Installationsprogramm die Komponenten an.

5. Akzeptieren Sie alle anderen aufforderungen, einschließlich der Lizenzverträge.

Mit SQL Server 2017 ist keine zusätzliche Konfiguration erforderlich.

> [!NOTE]
> 
> Für Python-Modelle erhalten Sie möglicherweise einen Fehler, wenn die Modelldatei aus Python-Code aufrufen. Dies ist eine Einschränkung in der aktuellen Python-Implementierung, die beschränkt der Länge des Pfads der Modelldatei. Dieses Problem wurde behoben, und wird in einer bevorstehenden Dienstversion verfügbar sein.

## <a name="install-pre-trained-models-with-sql-server-standalone-r-server"></a>Installieren Sie vorab trainierten Modelle mit SQL Server-eigenständigen R-server

Wenn Sie eine frühere Version von R Server (eigenständig) mithilfe des SQL Server 2016-Setups installiert haben, können Sie die Möglichkeit, mithilfe der Pre-tained Modelle, durch ein Upgrade mit dem neueren Windows-basierten Installer R-Server hinzufügen. 

Das Pre-tained Modelle wurde zuerst als Option mit verfügbar [Microsoft R Server 9.1](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/), jedoch Upgrades mit jeder Version hinzugefügt wurden. Es wird empfohlen, die neueste Version möglich abrufen, aber frühere Versionen sind hier aufgeführt [R Server-Versionen](https://docs.microsoft.com/machine-learning-server/install/r-server-install)

Die folgenden Anweisungen wird beschrieben, wie Aktualisieren von R-Komponenten und gleichzeitig die Pre-tained Modelle hinzufügen.

1. Starten Sie den separaten Windows-basierten Installer entweder [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) oder [Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Wählen Sie die Sprachen, die Sie verwenden möchten, aktualisieren, und wählen Sie die **Pre-trained Modelle** Option.

    > [!TIP]
    > Wenn Sie zuvor ausgeführt, haben die Installer zum Aktualisieren von R Server (eigenständig), und nur die Pre-tained Modelle hinzufügen möchten, lassen Sie alle vorherigen Auswahl **als**, und wählen Sie nur am vorkonfigurierten**-Modelle trainiert** Option . **Nicht** deaktivieren Sie alle zuvor ausgewählten Optionen; in diesem Fall wird das Installationsprogramm Komponenten entfernt.

    Es wird empfohlen, dass Sie die Standardeinstellungen für die Modell-Speicherorte akzeptieren.

3. Klicken Sie auf **Weiter**. 

4. Akzeptieren Sie alle anderen aufforderungen, einschließlich der Lizenzverträge.

Nachdem die Installation abgeschlossen ist, müssen Sie einige zusätzliche Schritte zum Registrieren der vorab trainierten Modelle ausführen.

1. Öffnen Sie Windows-Eingabeaufforderung **als Administrator**.

2. Navigieren Sie zu dem Ordner "Setup bootstrap", für R Server (eigenständig), die auch vom Microsoft-R-Installationsprogramm enthält. 

3. Führen Sie `RSetup.exe` und geben Sie an die Komponente zu installieren, die Version und den Ordner, der der Quelldateien für das Modell mithilfe dieser Syntax enthält:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    Die folgenden Werte sind für den "Version"-Parameter unterstützt:

    + Release Candidate-0: **9.1.0.0**
    + Release Candidate 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + Kumulatives Update 1: **9.2.0.24**
    + Kumulatives Update 4: **9.3.0**

    Um die neueste Version der Pre-tained Modelle für R, in einer Standardinstallation von R Server (eigenständig), aktivieren ausführen Sie beispielsweise diese Anweisung:

    `RSetup.exe /install /component MLM /version 9.3.0 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`

## <a name="install-pre-trained-models-with-sql-server-2017-standalone-server"></a>Installieren Sie Pre-tained Modelle mit SQL Server-2017 eigenständiger server

Wenn Sie Machine Learning-Servers mit 2017 von SQL Server-Setup installiert, fügen Sie der vorab trainierten Modelle durch Ausführen des Windows-basierten hinzu. Sie können die Option zum Aktualisieren der R oder Python-Komponenten und gleichzeitig die Pre-tained Modelle hinzufügen. 

Nachdem die Installation abgeschlossen ist, ist keine weitere Konfiguration erforderlich.

## <a name="bkmk_resources"></a> Forschung und Ressourcen

Aktuell sind die Modelle, die verfügbar sind, Tiefe neuronale Netzwerkmodelle (DNNS) für Sentiment Analysis und bildklassifizierung. Alle zuvor trainierten Modelle mithilfe des Microsoft trainiert wurden [Berechnung Netzwerk Toolkit](https://cntk.ai/Features/Index.html), oder **CNTK**.

Jede Netzwerkkonfiguration wurde basierend auf den folgenden referenzimplementierungen:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Weitere Informationen zu den Algorithmen in diesen Modellen umfassenden lernen und wie sie implementiert werden und mithilfe von CNTK trainiert, finden Sie in diesen Artikeln:

+ [Microsoft-Forschern Algorithmus legt ImageNet Herausforderung Meilenstein](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft rechnerischen Netzwerk Toolkit bietet effizienteste verteilte Deep learning rechenbetonte Leistung](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-use-pre-trained-models-for-text-analysis"></a>Verwenden Sie vorab trainierten Modelle für Textanalyse

Siehe das folgende Beispiel zeigt, wie die Pre-tained merkmalbereitstellung Textmodell für textklassifizierung verwendet:

[Mithilfe von Text Featurizer Stimmungsanalyse](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

## <a name="how-to-use-pre-trained-models-for-image-detection"></a>Verwenden Sie vorab trainierten Modelle für Image-Erkennung

Das vortrainierte Modell für Bilder unterstützt merkmalbereitstellung von Bildern, die Sie angeben. Um das Modell zu verwenden, rufen Sie die **FeaturizeImage** transformieren. Das Bild geladen wird, geändert, und die merkmalerstellung durch das trainierte Modell. Die Ausgabe der DNNS Featurizer wird dann zum Trainieren eines linearen Modells, für die bildklassifizierung verwendet.

Verwenden Sie dieses Modell müssen alle Abbilder Größe geändert werden, um den Anforderungen des trainierten Modells. Z. B. Wenn Sie ein Modell AlexNet verwenden, das Bild geändert werden soll, 227 x 227 px.

Weitere Informationen finden Sie unter [vorab trainierten Modelle für Stimmungslage Analysen und Image](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)
