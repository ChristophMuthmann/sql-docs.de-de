---
title: "Integration Services-Funktionen, die von den Editionen von SQLServer unterstützte | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: e9d1b8851f113fa44264230a79d0e496007ed96b
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>Unterstützt von den Editionen von SQL Server Integration Services-Funktionen
 Dieses Thema bietet detaillierte Informationen zu den von den verschiedenen [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]-Editionen unterstützten SQL Server Integration Services-Funktionen (SSIS).  

Finden Sie von Evaluation und Developer-Editionen unterstützte Funktionen in der Enterprise Edition in den folgenden Tabellen aufgeführten Funktionen.
  
Die neuesten Versionshinweise und Neuigkeiten neue Informationen finden Sie in den folgenden Artikeln:
-   [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Neuigkeiten in Integration Services in SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [Neues in Integration Services in SQL Server 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**SQL Server 2016 R2 ausprobieren!**    

Die SQL Server Evaluation Edition steht für einen Testzeitraum von 180 Tagen zur Verfügung.  
    
> [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a>Neues Integration Services-Funktionen in SQL Server-2017
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Dezentrales Skalieren Master|ja|||||
|Dezentrales Skalieren Worker|ja|Ja <sup>1</sup>|TBD|TBD|TBD|
|Unterstützung für Microsoft Dynamics AX und Microsoft Dynamics CRM OData-Komponenten <sup>2</sup>|ja|ja||||

<sup>1</sup> , wenn Sie Pakete, die nur Enterprise-Features in horizontal skalieren ist erforderlich ausführen, muss die Skalierung Out Worker auch auf Instanzen von SQL Server Enterprise ausführen.

<sup>2</sup> dieses Feature wird auch in SQL Server 2016 mit Service Pack 1 unterstützt.

## <a name="IEWiz"></a>SQL Server-Import / Export-Assistent

|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Server-Import/Export-Assistent|Ja|ja|ja|ja|ja|  

## <a name="IS"></a> Integration Services  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Integrierte Datenquellenkonnektoren|Ja|Ja|||| 
|Integrierte Tasks und Transformationen|Ja|ja||||  
|ODBC-Quelle und Ziel von Attunity|ja|Ja|||| 
|Azure-Datenquellenkonnektoren und Tasks|Ja|ja||||  
|Hadoop/HDFS-Konnektoren und tasks|ja|Ja||||  
|Grundlegende Datenprofilerstellungs-Tools|Ja|ja|||| 

## <a name="ISAA"></a>Integration Services – erweiterte Quellen und Ziele  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|High-Performance-Oracle-Quelle und Ziel von Attunity|ja|||||  
|High-Performance-Teradata-Quelle und Ziel von Attunity|ja|||||  
|SAP BW-Quelle und -Ziel|ja|||||  
|Ziel des Datamining-modelltrainings|ja|||||  
|Ziel für dimensionsverarbeitung|ja|||||  
|Ziels für partitionsverarbeitung|ja|||||  
  
## <a name="ISAT"></a>Integration Services – erweiterte Tasks und Transformationen  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Change Data Capture-Komponenten von Attunity <sup>1</sup>|ja|||||  
|Transformation für Data Mining-Abfragen|ja|||||  
|Fuzzygruppierung und die Transformationen für Fuzzysuche|ja|||||  
|Ausdrucksextrahierung und Transformationen für Suche Begriff|ja|||||  

<sup>1</sup> der Change Data Capture-Komponenten von Attunity erfordern, Enterprise Edition. Die Change Data Capture Service und Change Data Capture Designer ist die Enterprise Edition nicht jedoch erforderlich. Können Sie den Designer und dem Dienst auf einem Computer, auf dem SSIS nicht installiert.

