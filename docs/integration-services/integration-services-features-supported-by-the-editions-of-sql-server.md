---
title: "Von den SQL Server-Editionen unterstützte Integration Services-Funktionen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bd1193331cc9658a4703a39201219896c0e921d0
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>Von den SQL Server-Editionen unterstützte Integration Services-Funktionen
 Dieses Thema bietet detaillierte Informationen zu den von den verschiedenen [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]-Editionen unterstützten SQL Server Integration Services-Funktionen (SSIS).  

Von Evaluation und Developer Edition unterstützte Funktionen finden Sie in den Funktionen der Enterprise Edition in den folgenden Tabellen.
  
Die neuesten Anmerkungen zu dieser Version und Informationen zu Neuigkeiten finden Sie in folgenden Artikeln:
-   [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Neuigkeiten in Integration Services in SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [Neues in Integration Services in SQL Server 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**SQL Server 2016 R2 ausprobieren!**    

Die SQL Server Evaluation Edition steht für einen Testzeitraum von 180 Tagen zur Verfügung.  
    
> [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a> Neue Integration Services-Funktionen in SQL Server 2017
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Scale Out-Master|ja|||||
|Scale Out-Worker|ja|Ja <sup>1</sup>|TBD|TBD|TBD|
|Unterstützung für Microsoft Dynamics AX und Microsoft Dynamics CRM in OData-Komponenten <sup>2</sup>|ja|ja||||

<sup>1</sup> Wenn Sie Pakete ausführen, für die nur Enterprise-Funktionen in Scale Out erforderlich ist, müssen die Scale Out-Worker ebenfalls auf Instanzen von SQL Server Enterprise ausgeführt werden.

<sup>2</sup> Diese Funktion wird auch in SQL Server 2016 mit Service Pack 1 unterstützt.

## <a name="IEWiz"></a> SQL Server-Import/Export-Assistent

|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Server-Import/Export-Assistent|ja|ja|ja|ja|ja|  

## <a name="IS"></a> Integration Services  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Integrierte Datenquellenkonnektoren|ja|ja|||| 
|Integrierte Tasks und Transformationen|ja|ja||||  
|ODBC-Quelle und -Ziel |ja|ja|||| 
|Azure-Datenquellenkonnektoren und Tasks|ja|ja||||  
|Hadoop-/HDFS-Connectors und -Tasks|ja|ja||||  
|Grundlegende Datenprofilerstellungs-Tools|ja|ja|||| 

## <a name="ISAA"></a>Integration Services – Erweiterte Quellen und Ziele  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Oracle-Quelle und -Ziel für eine leistungsstarke Ausführung von Attunity|ja|||||  
|Teradata-Quelle und -Ziel für eine leistungsstarke Ausführung von Attunity|ja|||||  
|SAP BW-Quelle und -Ziel|ja|||||  
|Ziel für Data Mining-Modelltraining|ja|||||  
|Ziel für Dimensionsverarbeitung|ja|||||  
|Ziel für Partitionsverarbeitung|ja|||||  
  
## <a name="ISAT"></a> Integration Services – Erweiterte Tasks und Transformationen  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Change Data Capture-Komponenten von Attunity <sup>1</sup>|ja|||||  
|Transformation für Data Mining-Abfragen|ja|||||  
|Transformationen für Fuzzygruppierung und Fuzzysuche|ja|||||  
|Transformationen für Ausdrucksextrahierung und Ausdruckssuche|ja|||||  

<sup>1</sup> Für die Change Data Capture-Komponenten von Attunity ist Enterprise Edition erforderlich. Die Enterprise Edition ist jedoch nicht für den Change Data Capture Service und Change Data Capture-Designer notwendig. Sie können den Designer und den Dienst auf einem Computer verwenden, auf dem SSIS nicht installiert ist.
