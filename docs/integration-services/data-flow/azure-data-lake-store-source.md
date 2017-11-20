---
title: Azure Data Lake-Speicher-Quelle | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 65b4526b4c83525f61d53807fd21c72de4ee087a
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="azure-data-lake-store-source"></a>Azure Data Lake Store Source
  Die Komponente **Azure Data Lake Store Source** ermöglicht einem SSIS-Paket das Lesen von Daten aus Azure Data Lake Store. Die unterstützten Dateiformate sind: Text und Avro.
  
 Die **Azure Data Lake-Speicher-Quelle** ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
>   [!NOTE]
> Um sicherzustellen, dass der Azure Data Lake Store-Verbindungsmanager und die Komponenten, die ihn verwenden – das bedeutet Azure Data Lake Store Source und Azure Data Lake Store Destination – eine Verbindung zu Diensten herstellen können, stellen Sie sicher, dass Sie die neueste Version von Azure Feature Pack [hier](https://www.microsoft.com/download/details.aspx?id=49492)herunterladen. 
  
## <a name="configure-the-azure-data-lake-store-source"></a>Konfigurieren von Azure Data Lake Store Source
 1. Um den Editor für Azure Data Lake Store Source aufzurufen, ziehen Sie die **Azure Data Lake Store Source** auf den Datenfluss-Designer, und doppelklicken Sie darauf, um den Editor zu öffnen.  
  
2.  Geben Sie im Feld **Azure Data Lake Store connection manager** (Azure Data Lake Store-Verbindungs-Manager) einen vorhandenen Azure Data Lake Store-Verbindungs-Manager an, oder erstellen Sie einen neuen, der auf einen Azure Data Lake Store-Dienst verweist.  
  
    1.  Geben Sie im Feld **Dateipfad** den Dateipfad der Quelldatei in Azure Data Lake Store an.   
  
    2.  Geben Sie im Feld **Dateiformat** das Dateiformat der Quelldatei an.  
  
        Wenn es sich um Textformat handelt, geben Sie den Wert für das **Spaltentrennzeichen** ein. Aktivieren Sie außerdem **Spaltennamen in der ersten Datenzeile** , wenn die erste Zeile in der Datei Spaltennamen enthält.  
  
3.  Nachdem Sie die Verbindungsinformationen angegeben haben, wechseln Sie zur Seite **Spalten** , um Quellspalten zu den Zielspalten für den SSIS-Datenfluss zuzuordnen.   

