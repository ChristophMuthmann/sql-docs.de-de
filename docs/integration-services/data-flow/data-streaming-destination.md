---
title: Datenstreamingziel | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f6b5a6b41776010d957f149a28cd74d51a3b35b3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="data-streaming-destination"></a>Konfigurieren des Datenstreamingziels
  Das **Datenstreamingziel** ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Zielkomponente (SSIS), die es dem **OLE DB-Anbieter für SSIS** ermöglicht, die Ausgabe eines SSIS-Pakets als ein tabellarisches Resultset zu verwenden. Sie können einen Verbindungsserver erstellen, der den OLE DB-Anbieter für SSIS verwendet und anschließend eine SQL-Abfrage auf den Verbindungsserver ausführen, um die Daten anzuzeigen, die vom SSIS-Paket zurückgegeben wurden.  
  
 Im folgenden Beispiel gibt die nachfolgende Abfrage eine Ausgabe aus dem Paket „Package.dtsx“ im Projekt SSISPackagePublishing zurück, das sich im Power BI-Ordner des SSIS-Katalogs befindet. Diese Abfrage verwendet den Verbindungsserver mit dem Namen [Standardverbindungsserver für Integration Services], der wiederum den neuen OLE DB-Anbieter für SSIS verwendet. Die Abfrage umfasst den Ordnernamen, den Projektnamen und den Paketnamen im SSIS-Katalog. Der OLE DB-Anbieter für SSIS führt das Paket aus, das Sie in der Abfrage angegeben haben, und gibt das tabellarische Resultset zurück.  
  
```sql
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
  
## <a name="configure-data-streaming-destination"></a>Konfigurieren des Datenstreamingziels
  Konfigurieren Sie das Datenstreamingziel mithilfe des Dialogfelds **Erweiterter Editor für das Datenstreamingziel** . Öffnen Sie das Dialogfeld, indem Sie auf die Komponente doppelklicken oder indem Sie im Datenfluss-Designer mit der rechten Maustaste auf die Komponente und anschließend auf **Bearbeiten**klicken.  
  
 Dieses Dialogfeld enthält drei Registerkarten: **Komponenteneigenschaften**, **Eingabespalten**und **Eingabe- und Ausgabeeigenschaften**.  
  
## <a name="component-properties-tab"></a>Registerkarte „Komponenteneigenschaften“  
 Auf dieser Registerkarte können die folgenden Elemente bearbeitet werden:  
  
|Feld|Description|  
|-----------|-----------------|  
|Name|Name der Datenstreamingziel-Komponente im Paket.|  
|ValidateExternalMetadata|Gibt an, ob die Komponente zur Entwurfszeit mit externen Datenquellen überprüft wird. Ist diese Option auf „false“ festgelegt, wird die Überprüfung anhand externer Datenquellen bis zur Laufzeit verzögert.|  
|IDColumnName|Die vom Assistenten für das Veröffentlichen von Datenfeeds generierte Ansicht umfasst diese zusätzliche ID-Spalte. Die ID-Spalte dient als EntityKey für die Ausgabedaten aus dem Datenfluss, wenn die Daten als OData-Feed von einer anderen Anwendung genutzt werden.<br /><br /> Der Standardname für diese Spalte lautet „_ID“. Sie können einen anderen Namen für die ID-Spalte angeben.|  
  
## <a name="input-columns-tab"></a>Registerkarte „Eingabespalten“  
 Im oberen Bereich dieser Registerkarte sind alle verfügbaren Eingabespalten aufgeführt. Wählen Sie die Spalten, die in der Ausgabe dieser Komponente enthalten sein sollen. Die ausgewählten Spalten werden in einer Liste im unteren Bereich angezeigt. Sie können den Namen der Ausgabespalte ändern, indem Sie den neuen Namen für das Feld **Ausgabealias** in der Liste eingeben.  
  
## <a name="input-output-properties-tab"></a>Registerkarte „Eingabe- und Ausgabeeigenschaften“  
 Ähnlich wie bei der Registerkarte „Eingabespalten“ können Sie auf dieser Registerkarte die Namen von Ausgabespalten ändern. Erweitern Sie in der Strukturansicht auf der linken Seite den Eintrag **Eingabe des Datenstreamingziels** , und erweitern Sie dann **Eingabespalten**. Klicken Sie auf den Namen der Eingabespalte, und ändern Sie im rechten Bereich den Namen der Ausgabespalte.  
  
## <a name="see-also"></a>Siehe auch  
 [Publish SSIS Packages as OData Feed Sources](http://go.microsoft.com/fwlink/?LinkID=317367)  
  
  
