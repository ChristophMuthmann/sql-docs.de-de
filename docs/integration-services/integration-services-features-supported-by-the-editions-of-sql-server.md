---
title: "Von den SQL Server 2016-Editionen unterst&#252;tzte Integration Services-Funktionen | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Von den SQL Server 2016-Editionen unterst&#252;tzte Integration Services-Funktionen
 Dieses Thema bietet detaillierte Informationen zu den von den verschiedenen [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]-Editionen unterstützten SQL Server Integration Services-Funktionen (SSIS).  

Informationen über Funktionen, die von den Evaluation- und Developer-Editionen unterstützt werden, finden Sie unter „SQL Server Enterprise Edition“. 
  
Die neuesten Versionsanmerkungen und Informationen zu Neuerungen finden Sie über die folgenden Links:
-   [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
-   [Neuigkeiten in Integration Services in SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [What's New in Integration Services in SQL Server vNext (Neuigkeiten in Integration Services in SQL Server vNext)](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md)
    
**Probieren Sie SQL Server 2016 aus!**    

Die SQL Server Evaluation Edition steht für einen Testzeitraum von 180 Tagen zur Verfügung.  
    
> [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Virtueller Azure-Computer (klein)](../analysis-services/media/azure-virtual-machine-small.png) **[Starten eines virtuellen Computers, auf dem SQL Server 2016 bereits installiert ist](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

##  <a name="a-nameisanew-integration-services-features-in-sql-server-vnext"></a><a name="IS"></a>Neue Integration Services-Funktionen in SQL Server vNext
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Horizontale Hochskalierung|Ja||||||Ja|
|Unterstützung für Microsoft Dynamics AX und Microsoft Dynamics CRM in OData-Komponenten <sup>1</sup>|ja|Benutzerkontensteuerung|||||Ja|

<sup>1</sup> Diese Funktion wird auch in SQL Server 2016 mit Service Pack 1 unterstützt.

##  <a name="a-nameisa-integration-services"></a><a name="IS"></a> Integration Services  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Integrierte Datenquellenkonnektoren|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja|  
|Azure-Datenquellenkonnektoren und Tasks|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja|  
|SQL Server-Import/Export-Assistent|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Benutzerkontensteuerung|Ja|  
|Hadoop-/HDFS-Connectors und -Tasks|Ja|Benutzerkontensteuerung|Benutzerkontensteuerung||||Ja|  
|SSIS-Designer und Laufzeit|Ja|Benutzerkontensteuerung|||||Ja|  
|Integrierte Tasks und Transformationen|Ja|Benutzerkontensteuerung|||||Ja|  
|Grundlegende Datenprofilerstellungs-Tools|Ja|Benutzerkontensteuerung|||||Ja|  
|Change Data Capture Service für Oracle von Attunity|Ja||||||Ja|  
|Change Data Capture Designer für Oracle von Attunity|Ja||||||ja| 

##  <a name="a-nameisaaa-integration-services---advanced-adapters"></a><a name="ISAA"></a> Integration Services – Erweiterte Adapter  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|High-Performance-Oracle-Ziel|Ja||||||Ja|  
|High-Performance-Teradata-Ziel|Ja||||||Ja|  
|SAP BW-Quelle und -Ziel|Ja||||||Ja|  
|Zieladapter des Data Mining-Modelltrainings|Ja||||||Ja|  
|Zieladapter für Dimensionsverarbeitung|Ja||||||Ja|  
|Zieladapter für Partitionsverarbeitung|Ja||||||Ja|  
|Change Data Capture-Komponenten von Attunity|Ja||||||Ja|  
|Konnektor für Open Database Connectivity (ODBC) von Attunity|Ja||||||ja|  
  
##  <a name="a-nameisata-integration-services---advanced-transforms"></a><a name="ISAT"></a> Integration Services – Erweiterte Transformationen  
  
|Funktion|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Persistente Suchen (hohe Leistungsfähigkeit)|Ja||||||Ja|  
|Transformation für Data Mining-Abfragen|Ja||||||Ja|  
|Transformationen für Fuzzygruppierung und -suche|Ja||||||Ja|  
|Transformationen für Ausdrucksextrahierung und -suche|Ja||||||Ja|  
  