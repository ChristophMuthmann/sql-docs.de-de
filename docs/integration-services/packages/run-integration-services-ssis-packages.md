---
title: "Ausf&#252;hren von Integration Services-Paketen (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services-Pakete, Ausführen"
  - "SSIS-Pakete, ausführen"
  - "Pakete [Integration Services], ausführen"
  - "SQL Server Integration Services-Pakete, ausführen"
  - "Ausführen von Paketen [Integration Services]"
  - "Ausführen von Paketen [Integration Services]"
  - "Integration Services (siehe auch: Integration Services-Pakete)"
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
caps.latest.revision: 65
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Ausf&#252;hren von Integration Services-Paketen (SSIS)
  Zum Ausführen eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets können Sie, abhängig vom Speicherort dieser Pakete, unterschiedliche Tools verwenden. Die Tools werden in der Tabelle unten aufgeführt.  
  
 Zum Speichern eines Pakets auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server verwenden Sie das Projektbereitstellungsmodell, um das Projekt auf dem Server bereitzustellen. Weitere Informationen finden Sie unter [Deploy Projects to Integration Services Server](../../integration-services/packages/deploy-projects-to-integration-services-server.md).  
  
 Zum Speichern eines Pakets im SSIS-Paketspeicher, in der MSDB-Datenbank oder im Dateisystem verwenden Sie das Paketbereitstellungsmodell. Weitere Informationen finden Sie unter [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
|Tool|Pakete, die auf dem Integration Services-Server gespeichert werden|Im SSIS-Paketspeicher oder in der MSDB-Datenbank gespeicherte Pakete|Pakete, die im Dateisystem außerhalb des Speicherorts, der Teil des SSIS-Paketspeichers ist, gespeichert werden|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|Nein|Nein<br /><br /> Sie können jedoch einem Projekt ein vorhandenes Paket aus dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher hinzufügen, der die msdb-Datenbank enthält. Wenn ein vorhandenes Paket auf diese Weise dem Projekt hinzugefügt wird, wird im Dateisystem eine lokale Kopie des Pakets erstellt.|ja|  
|**SQL Server Management Studio, wenn eine Verbindung mit einer Instanz des Datenbankmoduls besteht, das den Server Integration Services hostet**<br /><br /> Weitere Informationen finden Sie unter [Execute Package Dialog Box](../../integration-services/packages/execute-package-dialog-box.md).|Ja|Nein<br /><br /> Pakete können jedoch von diesen Speicherorten auf den Server importiert werden.|Nein<br /><br /> Pakete können jedoch aus dem Dateisystem auf den Server importiert werden.|
|**SQL Server Management Studio, wenn eine Verbindung mit einer Instanz des Datenbankmoduls besteht, das den Integration Services-Server hostet, der als Master für horizontales Hochskalieren aktiviert ist**<br /><br /> Weitere Informationen finden Sie unter [Ausführen von Paketen in horizontaler Hochskalierung für Integration Services (SSIS)](../../integration-services/run-packages-in-integration-services-ssis-scale-out.md).|Ja|Nein|Nein|
|**SQL Server Management Studio, wenn eine Verbindung mit dem Integration Services-Dienst besteht, der den SSIS-Paketspeicher verwaltet**|Nein|Ja|Nein<br /><br /> Pakete können jedoch aus dem Dateisystem in den [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher importiert werden.|  
|**dtexec**<br /><br /> Weitere Informationen finden Sie unter [dtexec Utility](../../integration-services/packages/dtexec-utility.md).|Ja|Benutzerkontensteuerung|ja|  
|**dtexecui**<br /><br /> Weitere Informationen finden Sie unter [Paketausführungshilfsprogramm &#40;DtExecUI&#41; – Referenz zur Benutzeroberfläche](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md).|Nein|Benutzerkontensteuerung|Ja|  
|**SQL Server-Agent**<br /><br /> Mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag können Sie ein Paket planen.<br /><br /> Weitere Informationen finden Sie unter [SQL Server Agent Jobs for Packages](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).|Ja|Benutzerkontensteuerung|Ja|  
|**Integrierte gespeicherte Prozedur**<br /><br /> Weitere Informationen finden Sie unter [catalog.start_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).|Ja|Nein|Nein|  
|**Verwaltete API, mit Typen und Elementen im** <xref:Microsoft.SqlServer.Management.IntegrationServices> -Namespace|Ja|Nein|Nein|  
|**Verwaltete API, mit Typen und Elementen im** <xref:Microsoft.SqlServer.Dts.Runtime> -Namespace|Gegenwärtig nicht|Ja|Ja|  
  
## <a name="execution-and-logging"></a>Ausführung und Protokollierung  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete können für die Protokollierung aktiviert werden, und Sie können die Laufzeitinformationen in Protokolldateien erfassen. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Mit Vorgangsberichten können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete überwachen, die auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt und ausgeführt werden. Die Berichte sind in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verfügbar. Weitere Informationen finden Sie unter [Berichte für den Integration Services-Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Planen eines Pakets mit dem SQL Server-Agent](../../integration-services/packages/schedule-a-package-by-using-sql-server-agent.md)  
  
-   [Ausführen eines Pakets in SQL Server Data Tools](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md)  
  
-   [Ausführen eines Pakets auf dem SSIS-Server mit SQL Server Management Studio](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Siehe auch  
 [dtexec (Hilfsprogramm)](../../integration-services/packages/dtexec-utility.md)   
[Starten des SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  