---
title: "Installation von R-Komponenten ohne Internetzugang | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 21
---
# Installation von R-Komponenten ohne Internetzugang
  Das Setup der von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verwendeten R-Komponenten setzt eine Internetverbindung für den Zugriff auf die im Microsoft Download Center oder auf einer anderen vertrauenswürdigen Website bereitgestellten Dateien voraus. Möglich ist allerdings auch die Installation dieser Komponenten auf einem Server ohne Internetzugang von lokalen Kopien, die Sie, wie in diesem Thema beschrieben, erstellen können.  
  
  > [!TIP]
  > 
  > Eine ausführliche exemplarische Vorgehensweise für die Offline-Installation wird im folgenden Blog des [SQL Server-Kundenberatungsteams](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/) beschrieben.
  
## <a name="installation-on-computers-with-no-internet-access"></a>Installation auf Computern ohne Internetzugang  
 Bei einer Offline-Installation kann [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nicht auf die Links für die Installation der erforderlichen R-Komponenten zugreifen. Um dieses Problem zu vermeiden, können Sie eine Kopie des Installationsprogramms herunterladen und das Setup wie hier beschrieben ausführen.
 
 Beachten Sie, dass es zwei Installationsprogramme für R-Komponenten gibt: eines für Microsoft R Open und eines für Microsoft R Server. Sie müssen beide Programme herunterladen und installieren, um SQL Server R Services verwenden zu können. Der Setup-Assistent für SQL Server stellt sicher, dass sie in der richtigen Reihenfolge installiert werden.


Release  |Downloadlink  
---------|---------
**SQL Server 2016 RTM**     |           
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)     
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)      
**SQL Server 2016 CU 1**     |           
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)     
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)      
**SQL Server 2016 CU 2**     |           
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)     
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)  
**SQL Server 2016 CU 3**     |           
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)     
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |           
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)     
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)  
**SQL Server 2016 SP 1 GDR**     |           
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)     
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)  

  
**Vorgehensweise beim Aktualisieren von R-Komponenten in einer Offline-Installation**     

1. Verwenden Sie die obigen Links, um die entsprechende Version herunterzuladen.
2. Kopieren Sie die CAB-Dateien in einen Ordner auf dem Computer, auf dem Sie das Update installieren.
3. Wenn Sie den Setup-Assistenten für SQL Server ausführen, klicken Sie auf der Lizenzierungsseite von Microsoft R auf **Annehmen**.  Es wird ein Dialogfeld angezeigt, in dem die Links zu den Downloads aufgeführt werden. Geben Sie den Pfad zum Speicherort der Dateien ein, die Sie heruntergeladen haben. 
4. Klicken Sie auf **Weiter**, um anzugeben, dass die Komponenten verfügbar sind, und schließen Sie den Setup-Assistenten für SQL Server ab.
5. Optional können Sie auch den archivierten Quellcode für die Open-Source-Komponenten herunterladen. Weitere Informationen finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).


> [!IMPORTANT] Wenn Sie die CAB-Dateien als Teil des SQL Server-Setups auf einen Computer mit Internetzugang herunterladen, erkennt der Setup-Assistent die lokale Sprache und ändert automatisch die Sprache des Installationsprogramms. 
> 
> Wenn Sie jedoch eine der lokalisierten Versionen von SQL Server auf einem Computer ohne Internetzugang installieren und die R-Installationsprogramme auf eine lokale Freigabe herunterladen, müssen Sie manuell den Namen der heruntergeladenen Dateien bearbeiten und die korrekte Sprach-ID für die von Ihnen installierte Sprache einfügen. 
> 
> Wenn Sie beispielsweise die japanische Version von SQL Server installieren, würden Sie den Namen der Datei von SRS_8.0.3.0_1033.cab in SRS_8.0.3.0_1041.cab ändern.    
 
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [Troubleshooting R Services Setup (Problembehebung beim Setup von R Services)](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  