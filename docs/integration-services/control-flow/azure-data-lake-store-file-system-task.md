---
title: Azure Data Lake-Speicher-Dateisystemtask | Microsoft Docs
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 303d3b74da3fe370d19b7602c0e11e67b63191e7
ms.openlocfilehash: ce2355de312faed9ab66991d6d0dd344ff315a55
ms.contentlocale: de-de
ms.lasthandoff: 08/29/2017

---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake-Speicher-Dateisystemtask

Die **Azure Data Lake-Speicher-Dateisystemtask** ermöglicht Benutzern das Ausführen von verschiedenen Dateisystemvorgänge auf [Azure Data Lake-Speicher (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

Die **Azure Data Lake-Speicher-Dateisystemtask** ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Um eine Azure Data Lake-Speicher File System Task eines Pakets hinzuzufügen, ziehen Sie es von SSIS-Toolbox auf den designerzeichnungsbereich. Klicken Sie dann doppelklicken Sie auf die Aufgabe oder mit der rechten Maustaste in der Aufgabe und wählen Sie **bearbeiten**, um das Dialogfeld Task-Editor zu öffnen.

Die **Vorgang** Eigenschaft gibt an, das System Dateiübertragungsvorgang ausführen. Die folgenden Vorgänge werden unterstützt.

* **CopyToADLS:** Hochladen von Dateien in ADLS.
* **CopyFromADLS:** Herunterladen von Dateien aus ADLS.

Für jeden Vorgang müssen Sie einen Azure Data Lake-Verbindungs-Manager angeben.

Hier sind die Beschreibungen der Eigenschaften für jeden Vorgang spezifisch.

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:** gibt das Quellverzeichnis der hochzuladenden Dateien enthält.
* **FileNamePattern:** legt einen Dateinamensfilter für Quelldateien. Nur Dateien, deren Name mit das angegebene Muster übereinstimmt, werden hochgeladen werden. Platzhalter `*` und `?` werden unterstützt.
* **SearchRecursively:** gibt an, ob in das Quellverzeichnis für hochzuladenden Dateien rekursiv durchsuchen.
* **AzureDataLakeDirectory:** gibt das Zielverzeichnis ADLS zum Hochladen von Dateien auf.
* **FileExpiry:** ein Ablaufdatum und die Uhrzeit angibt, für die Dateien in ADLS hochgeladen, oder lassen diese Eigenschaft leer, um anzugeben, dass die Dateien nie ablaufen.

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory:** gibt das Verzeichnis der ADLS-Quelle enthält die Dateien heruntergeladen.
* **SearchRecursively:** gibt an, ob in das Quellverzeichnis für Herunterzuladende Dateien rekursiv durchsuchen.
* **LocalDirectory:** gibt das Zielverzeichnis zum Speichern von heruntergeladener Dateien an.
