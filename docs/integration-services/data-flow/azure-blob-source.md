---
title: "Azure-Blob-Quelle | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpblobsrc.f1"
  - "sql14.dts.designer.afpblobsrc.f1"
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Azure-Blob-Quelle
  Die **Azure-Blobquelle** ermöglicht es einem SSIS-Paket, Daten aus einem Azure-Blob zu lesen. Die unterstützten Dateiformate sind CSV und AVRO.
  
>   [!NOTE] Um sicherzustellen, dass der Azure Storage-Verbindungs-Manager und die Komponenten, die ihn verwenden – Blobquelle, Blobziel, Blobupload- und Blobdownloadtask – sowohl Verbindungen mit allgemeinen Speicherkonten als auch mit Blobspeicherkonten herstellen können, laden Sie unbedingt die [hier](https://www.microsoft.com/download/details.aspx?id=49492) neueste Version von Azure Feature Pack herunter. Weitere Informationen zu diesen beiden Arten von Speicherkonten finden Sie unter [Einführung in Microsoft Azure Storage](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).
  
  Um den Editor für die Azure-Blobquelle aufzurufen, ziehen Sie die **Azure-Blobquelle** auf den Datenfluss-Designer, und doppelklicken Sie darauf, um den Editor zu öffnen.  
  
 Die **Azure-Blobquelle** ist eine Komponente des SQL Server Integration Services (SSIS) Feature Pack für Azure für SQL Server 2016. Laden Sie das Feature Pack [hier](http://go.microsoft.com/fwlink/?LinkID=626967) herunter.  
  
1.  Geben Sie für den **Azure Storage-Verbindungs-Manager** einen vorhandenen Azure Storage-Verbindungs-Manager an, oder erstellen Sie einen neuen, der auf ein Azure-Speicherkonto verweist.  
  
2.  Geben Sie im Feld **Blobcontainername** den Namen des Blobcontainers an, der die Quelldateien enthält.  
  
3.  Geben Sie im Feld **Blobname** den Pfad für das Blob an.  
  
4.  Geben Sie im Feld **Blobdateiformat** das gewünschte Blobformat an.  
  
5.  Wenn es sich um das CSV-Dateiformat handelt, geben Sie den Wert für das **Spaltentrennzeichen** ein. Aktivieren Sie außerdem **Spaltennamen in der ersten Datenzeile**, wenn die erste Zeile in der Datei Spaltennamen enthält.  
  
6.  Nachdem Sie die Verbindungsinformationen angegeben haben, wechseln Sie zur Seite **Spalten**, um Quellspalten zu den Zielspalten für den SSIS-Datenfluss zuzuordnen.  
  
  