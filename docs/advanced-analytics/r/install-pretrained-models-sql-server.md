---
title: Installieren Sie vortrainierte Machine Learning-Modellen in SQL Server | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14789bafd555a4980875de78c85b32f535a8c0fe
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>Installieren Sie vortrainierte Machine learning-Modelle mit SQL Server

Dieses Thema beschreibt, wie vortrainierte Modelle mit einer Instanz von SQL Server hinzufügen, die bereits über R Services oder Machine Learning-Dienste installiert.

Vortrainierte Modelle werden mit dem Update für Microsoft R Server (oder das Update, Microsoft Machine Learning-Server) bereitgestellt. Informationen zum upgrade Ihrer Instanz und Abrufen der neuesten Version von Microsoft R finden Sie unter [aktualisieren Sie die R-Komponenten in einer Instanz von R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

Sie können diese Modelle nur durch Ausführen von separaten Windows-basierten Installationsprogramm für R-Server installieren.
Es gibt jedoch einige zusätzliche Schritte zum verwenden, wenn die Modelle auf SQL Server zu installieren. Dieses Thema beschreibt den Prozess.

## <a name="benefits-of-using-pretrained-models"></a>Vorteile der Verwendung von vortrainierte Modelle

Pre-tained Modelle wurden zur Unterstützung von Kunden, die Aufgaben wie stimmungsanalyse oder image merkmalbereitstellung müssen, aber keine Ressourcen zum Abrufen großer Datasets oder ein komplexes Modell trainieren verfügbar. Verwendung von vorab trainierten Modelle können Sie die ersten Schritten für Text- und Bilddateitypen, die am effizientesten verarbeiten.

Aktuell sind die Modelle, die verfügbar sind, Tiefe neuronale Netzwerkmodelle (DNNS) für Sentiment Analysis und bildklassifizierung. Alle vier vortrainierte Modelle wurden CNTK trainiert. Jede Netzwerkkonfiguration wurde basierend auf den folgenden referenzimplementierungen:

+ Resnet 18
+ Resnet 50
+ ResNet 101
+ AlexNet

Weitere Informationen zu tief residual Netzwerken und ihre Implementierung mit CNTK finden Sie in diesen Artikeln:

+ [Microsoft-Forschern Algorithmus legt ImageNet Herausforderung Meilenstein](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft rechnerischen Netzwerk Toolkit bietet effizienteste verteilte Deep learning rechenbetonte Leistung](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>Installieren Sie die Modelle auf SQL Server

   > [!NOTE]
   > 
   > Wenn Sie separate Windows-basierten Installationsprogramm mit Microsoft R Server installieren oder aktualisieren Sie Ihre Instanz von SQL Server verwenden, sind die vortrainierte Modelle über den Installer verfügbar. Finden Sie unter [R Installationsserver für Windows](https://docs.microsoft.com/en-us/r-server/install/r-server-install-windows).
   > 
   > Mithilfe der Modelle mit Microsoft R Server, können einige zusätzliche Schritte erforderlich sein. Weitere Informationen finden Sie unter [zum Installieren und Bereitstellen von trainiert vorab Machine Learning-Modellen mit MicrosoftML](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)

1. Vortrainierte Modelle werden nicht standardmäßig installiert, bei der Installation von SQL Server; Sie müssen diese hinzufügen, indem eine befehlszeilensetups-Dienstprogramm ausführen, nachdem SQL Server-Setup abgeschlossen ist.

2. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und navigieren Sie zum Ordner "Setup bootstrap" für SQL Server, die auch vom Microsoft-R-Installationsprogramm enthält.

    In einer Standardinstanz von SQL Server 2017 RC 1 wäre dies:
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017RC1\x64\`

3. Geben Sie die Komponente zum Installieren und den Ordner, in dem die vortrainierte Modelle hinzugefügt werden soll, mithilfe der folgenden Argumente, ein:

  + Verwenden von Modellen mit **R_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\R_SERVICES`

    Um die Verwendung der vortrainierte Modelle mithilfe von R in einer Standardinstanz von SQL Server-2017 aktivieren, würden Sie beispielsweise diese Anweisung ausführen:

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES"`

  + Verwenden von Modellen mit **PYTHON_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\PYTHON_SERVICES`

    Verwendung von vortrainierte Modelle mithilfe von Python, für eine Standardinstanz von SQL Server-2017, würden Sie beispielsweise diese Anweisung ausführen:

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"`

4. Für den Versionsparameter werden die folgenden Werte unterstützt:

    + Release Candidate-0: **9.1.0.0**
    + Release Candidate 1: **9.2.0.22**
    + Abschließende Versionsnummer (nicht veröffentlicht): **9.2.0.100**

5. Wenn die Installation erfolgreich ist, sollte der folgenden Modelle hinzugefügt werden, an Ihre R\_Dienste oder PYTHON\_SERVICES-Ordner:

    - AlexNet_Updated.model
    - ImageNet1K_mean.xml
    - pretrained.Model
    - ResNet_101_Updated.model
    - ResNet_18_Updated.model
    - ResNet_50_Updated.model

## <a name="examples"></a>Beispiele

Nachdem Sie die Modelle installiert haben, können Sie die Modelle durch Aufruf aus R-Code verwenden.

### <a name="image-featurization-example"></a>Die merkmalerstellung Beispiel Bild

Das vortrainierte Modell für Bilder unterstützt merkmalbereitstellung von Bildern, die Sie angeben. Um das Modell zu verwenden, rufen Sie die **FeaturizeImage** transformieren.

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
> 
> Es ist nicht möglich, zu lesen oder ändern das vortrainierte Modell selbst. Dieses bestimmte Modell basiert auf [CNTK](https://docs.microsoft.com/cognitive-toolkit/) zu modellieren, aber wurde mit einem systemeigenen Format aus Leistungsgründen komprimiert.

### <a name="text-analysis-example"></a>Beispiel für die Analyse von Text

Dieses Beispiel zeigt die Verwendung von das vortrainierte Modell für die Klassifizierung:

[Mithilfe von Text Featurizer Stimmungsanalyse](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)
