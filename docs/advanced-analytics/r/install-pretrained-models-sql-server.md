---
title: Installieren Sie vortrainierte Machine Learning-Modellen in SQL Server | Microsoft Docs
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5d9f60684cc749c35674233fbdaaa222953396d9
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>Installieren Sie vortrainierte Machine learning-Modelle mit SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt, wie vortrainierte Modelle mit einer Instanz von SQL Server hinzufügen, die bereits über R Services oder Machine Learning-Dienste installiert.

Die Option zum Installieren von vortrainierte Modelle ist verfügbar, wenn Sie separaten Windows Installer für Microsoft R Server "oder" Machine Learning-Server verwenden. Können Sie dieses Installationsprogramm nur das vortrainierte Modelle erhalten, oder können Sie es auf [Aktualisieren des Machine learning Komponenten](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) in einer Instanz von SQL Server 2016 oder SQL Server-2017.

Nach dem Sie die vortrainierte Modelle durch Ausführen des Installationsprogramms heruntergeladen haben, sind einige zusätzliche Schritte erforderlich, um die Modelle für die Verwendung mit SQL Server zu konfigurieren. Dieser Artikel beschreibt den Prozess.

Ein Beispiel dafür, wie mithilfe der vortrainierte Modelle mit SQL Server-Daten finden Sie in diesem Blogbeitrag vom SQL Server-Machine Learning-Team: 

+ [Stimmungsanalyse mit Python in SQL Server-Machine Learning-Services](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="benefits-of-using-pretrained-models"></a>Vorteile der Verwendung von vortrainierte Modelle

Diese vorab trainierten Modelle wurden zum Unterstützen von Kunden, die Aufgaben wie das Sentiment Analysis "oder" Image merkmalbereitstellung müssen, jedoch nicht die Ressourcen zum Abrufen großer Datasets oder ein komplexes Modell trainieren besitzen, erstellt. Verwendung von vorab trainierten Modelle können Sie die ersten Schritten für Text- und effizient verarbeiten.

Aktuell sind die Modelle, die verfügbar sind, Tiefe neuronale Netzwerkmodelle (DNNS) für Sentiment Analysis und bildklassifizierung. Alle vortrainierte Modelle trainiert wurden, mithilfe des Microsoft [Berechnung Netzwerk Toolkit](https://cntk.ai/Features/Index.html), oder **CNTK**.

Jede Netzwerkkonfiguration wurde basierend auf den folgenden referenzimplementierungen:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Weitere Informationen zu diesen Modellen finden Sie unter [vortrainiertes Machine learning-Modellen für Stimmungslage Analysen und Image](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)

Weitere Informationen zu umfassenden lernen Netzwerken und ihre Implementierung mit CNTK finden Sie in diesen Artikeln:

+ [Microsoft-Forschern Algorithmus legt ImageNet Herausforderung Meilenstein](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft rechnerischen Netzwerk Toolkit bietet effizienteste verteilte Deep learning rechenbetonte Leistung](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>Installieren Sie die Modelle auf SQL Server

1. Führen Sie separate Windows-basierten Installationsprogramm für Machine Learning-Server. Speicherorte für den Download finden Sie unter:

    + [Installieren Sie Machine Learning-Server für Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [Installieren von R Server 9.1 für Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows)

2. Die Auswahl der zu installierenden Funktionen hängt davon ab, ob Sie erhalten nur die Modelle oder andere Updates, die mit dem Installer ausführen werden.
 
    + Wenn dies eine Neuinstallation von Machine Learning-Server ist, und Sie keine R oder Python-Komponenten, wählen Sie andere Änderungen vornehmen möchten **nur** vortrainierte Modelle-Option. Akzeptieren Sie alle anderen aufforderungen, einschließlich der Lizenzverträge.

    + Um die R oder Python-Komponenten zur gleichen Zeit zu aktualisieren, wählen Sie die Sprache (R, Python oder beides), die Sie aktualisieren möchten, und wählen Sie die Option vortrainierte Modelle. Wählen Sie eine oder mehrere Instanzen, die diese Änderungen angewendet werden sollen.

    + Wenn Sie zuvor Machine Learning-Server installiert und aktualisiert R oder Python-Komponenten, die die Bindung verwenden, lassen Sie alle vorherigen Auswahl **als**, und wählen Sie die Optionen vortrainierte Modelle. Deaktivieren Sie alle zuvor ausgewählten Optionen nicht; Wenn Sie dies tun, entfernt das Installationsprogramm die Komponenten an.

3. Wenn die Installation abgeschlossen ist, öffnen Sie eine Windows-Eingabeaufforderung **als Administrator**, und navigieren Sie zum Ordner "Setup bootstrap" für SQL Server, die auch vom Microsoft-R-Installationsprogramm enthält. In einer Standardinstanz von SQL Server-2017 wäre die Ordner:
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017\x64\`

4. Führen Sie RSetup.exe, und anzugeben Sie die Komponente zu installieren, die Version und den Ordner mit den Quelldateien für das Modell verwenden Sie die Befehlszeilenargumente, die in diesen Beispielen gezeigte:

    + Verwenden von Modellen mit **R_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Um die neueste Version der vortrainierte Modelle für R in einer Standardinstanz von SQL Server-2017, aktivieren ausführen Sie z. B. diese Anweisung:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Auf einer benannten Instanz wäre der Befehl etwa wie folgt:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + So verwenden vortrainierte Modelle mit R-Server (eigenständig) oder Machine Learning-Server (eigenständig):

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    Zum Aktivieren der Verwendung der neuesten Version der vortrainierte Modelle für R, in einer Standardinstallation von R-Server mit SQL Server 2016, würden Sie beispielsweise diese Anweisung ausführen:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir ‘C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`
    
    + Mithilfe vortrainierte Modelle mit **PYTHON_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Zum Aktivieren der Verwendung der neuesten Version der vortrainierte Modelle für Python, in einer Standardinstanz von SQL Server-2017, würden Sie beispielsweise diese Anweisung ausführen:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Auf einer benannten Instanz wäre der Befehl etwa wie folgt:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + Verwendung von Python pretrained Modelle mit Machine Learning-Server (eigenständig):

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    Beispielsweise wenn eine Standardinstallation von Machine Learning-Server (eigenständig) 2017 von SQL Server-Setup, diese Anweisung ausführen:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. Die folgenden Werte sind für den "Version"-Parameter unterstützt:

    + Release Candidate-0: **9.1.0.0**
    + Release Candidate 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + Kumulatives Update 1: **9.2.0.24**

6. Wenn die Installation erfolgreich ist, sollte der folgenden Modelle hinzugefügt werden, an Ihre R\_Dienste oder PYTHON\_SERVICES-Ordner:

    - AlexNet\_Updated.model
    - ImageNet1K\_mean.xml
    - pretrained.Model
    - ResNet\_101\_Updated.model
    - ResNet\_18\_Updated.model
    - ResNet\_50\_Updated.model


> [!NOTE]
> 
> Wenn Sie der Pfad zu der Modelldatei zu lang ist, erhalten Sie möglicherweise einen Fehler, beim Aufrufen der Modelldatei aus Python-Code. Dies ist eine Einschränkung in der aktuellen Python-Implementierung. Dieses Problem wird in einer bevorstehenden Dienstversion behoben werden.

## <a name="examples"></a>Beispiele

Nachdem Sie die Modelle installiert haben, können Sie die Modelle, indem sie aus dem Code aufgerufen werden.

### <a name="image-featurization-example"></a>Die merkmalerstellung Beispiel Bild

Das vortrainierte Modell für Bilder unterstützt merkmalbereitstellung von Bildern, die Sie angeben. Dieses bestimmte Modell trainiert wurde, mithilfe von [CNTK](https://docs.microsoft.com/cognitive-toolkit/). 

Um das Modell zu verwenden, rufen Sie die **FeaturizeImage** transformieren.

+ [FeaturizeImage: Transformieren der Machine Learning Bilds Merkmalbereitstellung](https://docs.microsoft.com/r-server/r-reference/microsoftml/featurizeimage)

Finden Sie in diesem Beispiel in der zweiten Codeblock. Das Bild geladen wird, geändert, und die merkmalerstellung durch das vortrainierte convolutional DNNS-Modell. Die Ausgabe der DNNS Featurizer wird dann zum Trainieren eines linearen Modells, für die bildklassifizierung verwendet.

Das Bild entsprechend den Anforderungen des trainierten Modells geändert werden muss: die Bilder, die für das Training verwendet wurden 224 x 224 px. Wenn Sie ein Modell AlexNet verwendet haben, würde das Bild geändert werden, um 227 x 227 px.

```R
 model <- rxFastLinear(
     Label ~ Features,
     data = train,
     mlTransforms = list(
         loadImage(vars = list(Features = "Path")),
         resizeImage(vars = "Features", width = 224, height = 224), 
         extractPixels(vars = "Features"),
         featurizeImage(var = "Features")
         ),
     mlTransformVars = "Path")
```

> [!NOTE]
> Es ist nicht möglich, zu lesen oder ändern die vortrainierte Modelle, da sie über ein systemeigenes Format zum Verbessern der Leistung komprimiert werden.

### <a name="text-analysis-example"></a>Beispiel für die Analyse von Text

Siehe das folgende Beispiel zeigt, wie Sie das vortrainierte merkmalbereitstellung Textmodell für textklassifizierung verwenden:

[Mithilfe von Text Featurizer Stimmungsanalyse](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)
