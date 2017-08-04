---
title: Datenstreamingziel | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e95b4d887bea5783be935a40877d590b8e8dcff
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="data-streaming-destination"></a>Konfigurieren des Datenstreamingziels
  Das **Datenstreamingziel** ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Zielkomponente (SSIS), die es dem **OLE DB-Anbieter für SSIS** ermöglicht, die Ausgabe eines SSIS-Pakets als ein tabellarisches Resultset zu verwenden. Sie können einen Verbindungsserver erstellen, der den OLE DB-Anbieter für SSIS verwendet und anschließend eine SQL-Abfrage auf den Verbindungsserver ausführen, um die Daten anzuzeigen, die vom SSIS-Paket zurückgegeben wurden.  
  
 Im folgenden Beispiel gibt die nachfolgende Abfrage eine Ausgabe aus dem Paket „Package.dtsx“ im Projekt SSISPackagePublishing zurück, das sich im Power BI-Ordner des SSIS-Katalogs befindet. Diese Abfrage verwendet den Verbindungsserver mit dem Namen [Standardverbindungsserver für Integration Services], der wiederum den neuen OLE DB-Anbieter für SSIS verwendet. Die Abfrage umfasst den Ordnernamen, den Projektnamen und den Paketnamen im SSIS-Katalog. Der OLE DB-Anbieter für SSIS führt das Paket aus, das Sie in der Abfrage angegeben haben, und gibt das tabellarische Resultset zurück.  
  
```  
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>Datenfeedveröffentlichungs-Komponenten  
 Die Datenfeedveröffentlichungs-Komponenten beinhalten Folgendes: den OLE DB-Anbieter für SSIS, das Datenstreamingziel und den SSIS-Assistenten für das Veröffentlichen von Paketen (SSIS Package Publish Wizard). Der Assistent ermöglicht es Ihnen, ein SSIS-Paket als SQL-Ansicht in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankinstanz zu veröffentlichen. Der Assistent unterstützt Sie bei der Erstellung eines Verbindungsservers, der den OLE DB-Anbieter für SSIS verwendet, und einer SQL-Ansicht, die eine Abfrage auf dem Verbindungsserver darstellt. Führen Sie die Ansicht aus, um Ergebnisse auf dem SSIS-Paket als tabellarisches Dataset abzufragen.  
  
 Erweitern Sie in SQL Server Management Studio die **Serverobjekte**, die **Verbindungsserver**und die **Anbieter**, und vergewissern Sie sich, dass die **SSISOLEDB** -Anbieter angezeigt werden. So stellen Sie sicher, dass der SSISOLEDB-Anbieter installiert ist. Führen Sie einen Doppelklick auf **SSISOLEDB**aus, aktivieren Sie **InProcess zulassen** , falls es nicht aktiviert ist, und klicken Sie auf **OK**.  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>Veröffentlichen eines SSIS-Pakets als eine SQL-Ansicht  
 Das folgende Verfahren beschreibt die Schritte zum Veröffentlichen eines SSIS-Pakets als eine SQL-Ansicht.  
  
1.  Erstellen Sie ein SSIS-Paket mit einer **Datenstreamingziel** -Komponente, und stellen Sie das Paket im SSIS-Katalog bereit.  
  
2.  Führen Sie den **SSIS-Assistenten für das Veröffentlichen von Paketen** aus, indem Sie „ISDataFeedPublishingWizard.exe“ in „C:\Programme\Microsoft SQL Server\130\DTS\Binn“ ausführen. Alternativ können Sie den Datenfeedveröffentlichungs-Assistent über das Startmenü ausführen.  
  
     Der Assistent erstellt einen Verbindungsserver mithilfe des OLE DB-Anbieters für SSIS (SSISOLEDB) und anschließend eine SQL-Ansicht, die aus einer Abfrage auf den Verbindungsserver besteht. Diese Abfrage umfasst den Ordnernamen, den Projektnamen und den Paketnamen im SSIS-Katalog.  
  
3.  Führen Sie die SQL-Ansicht in SQL Server Management Studio aus, und überprüfen Sie die Ergebnisse aus dem SSIS-Paket. Diese Ansicht sendet eine Abfrage an den OLE DB-Anbieter für SSIS, über den Verbindungsserver, den Sie erstellt haben. Der OLE DB-Anbieter für SSIS führt das Paket aus, das Sie in der Abfrage angegeben haben und gibt das tabellarische Resultset zurück.  
  
> [!IMPORTANT]  
>  Weitere Informationen finden Sie unter [Exemplarische Vorgehensweise: Veröffentlichen eines SSIS-Pakets als eine SQL-Ansicht](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md).  
  
## <a name="expose-output-data-from-an-ssis-package-as-an-odata-feed-by-using-the-power-bi-admin-center"></a>Verfügbarmachen von Ausgabedaten von einem SSIS-Paket als ein OData-Feed mithilfe des Power BI Admin Centers  
 Mithilfe von Power BI Admin Center können IT-Administratoren Daten aus lokalen Datenquellen, als OData-Feeds für Benutzer, verfügbar machen. Das Power BI Admin Center erlaubt Ihnen standardmäßig nur die Registrierung von SQL Server-Datenquellen. Sie können jedoch SSIS-Pakete als Datenquellen im Portal registrieren, indem Sie **Datenstreamingziel** und **Microsoft OLE DB-Anbieter für SQL Server Integration Services (SSISOLEDB)** verwenden und die Ergebnisdaten vom SSIS-Paket als ein OData-Feed für die Benutzer verfügbar machen.  
  
 Das Admin Center ermöglicht Ihnen die Veröffentlichung von Ansichten in einer SQL Server-Datenbank. Daher können Sie den SSIS-Assistent für das Veröffentlichen von Paketen (SSIS Package Publish Wizard), um ein SSIS-Paket als SQL-Ansicht zu veröffentlichen. Anschließend können Sie die Ansicht auswählen, die im OData-Feed im Power BI Admin Center enthalten sein soll. Ein Data Steward kann den Feed aus dem SSIS-Paket mithilfe des Power Query-Add-Ins für Excel verwenden.  
  
 Eine ausführliche exemplarische Vorgehensweise finden Sie unter [Publish SSIS Packages as OData Feed Sources](http://go.microsoft.com/fwlink/?LinkID=317367)(Veröffentlichen von SSIS-Paketen als OData-Feedquellen).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Exemplarische Vorgehensweise: Veröffentlichen eines SSIS-Pakets als eine SQL-Ansicht](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
-   [Konfigurieren des Datenstreamingziels](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Publish SSIS Packages as OData Feed Sources](http://go.microsoft.com/fwlink/?LinkID=317367)  
  
  
