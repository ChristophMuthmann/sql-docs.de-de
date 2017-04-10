---
title: "SQL Server Integration Services-Projekte und Projektmappen (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.importprojectwizard.f1"
helpviewer_keywords: 
  - "Projekte [Integration Services], erstellen"
  - "Ordner [Integration Services], Projekte"
  - "Dateien [Integration Services], Projekte"
  - "Ordner [Integration Services]"
  - "Projekte [Integration Services], Informationen zu Projekten"
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 62
---
# SQL Server Integration Services-Projekte und Projektmappen (SSIS)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] stellt [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] für die Entwicklung von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Paketen bereit.  
  
 Wenn Sie Pakete auf einer [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Datenbank oder im [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paketspeicher bereitstellen, verwenden Sie den [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Dienst, um die Pakete zu verwalten. Der [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Dienst steht nur in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]zur Verfügung. Weitere Informationen über den Dienst finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../integration-services/service/integration-services-service-ssis-service.md). Weitere Informationen zur Paketbereitstellung finden Sie unter [Legacy-Paketbereitstellung &#40;SSIS&#41;](../integration-services/packages/legacy-package-deployment-ssis.md).  
  
 Wenn Sie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekte auf dem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Server bereitstellen, verwenden Sie Transact-SQL-Sichten und gespeicherte Prozeduren in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], um die Projekte zu verwalten. Weitere Informationen zur Projektbereitstellung finden Sie unter [Bereitstellung von Projekten und Paketen](https://msdn.microsoft.com/library/hh213290.aspx). Weitere Informationen über den [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Server finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](https://msdn.microsoft.com/library/ms137731.aspx).  
  
 Eine Übersicht über [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] und [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] finden Sie unter [Integration Services &#40;SSIS&#41; und Verwaltungstools](https://msdn.microsoft.com/library/ms140028.aspx)%20and%20Studio%20Environments.md).  
  
## Integration Services-Projekte enthalten Pakete  
 Ein Projekt ist ein Container, in dem Sie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakete entwickeln.  
  
 In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] werden in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekten die mit dem Paket verknüpften Dateien gespeichert und gruppiert. Beispielsweise enthält ein Projekt die zum Erstellen einer bestimmten ETL-Projektmappe (Extract, Transfer, And Load) erforderlichen Dateien.  
  
 Vor dem Erstellen eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekts sollten Sie sich mit den grundlegenden Inhalten dieser Art von Projekten vertraut machen. Wenn Sie die Inhalte eines Projekts verstanden haben, können Sie ein [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekt erstellen und verwenden.  
  
## Ordner in SQL Server Integration Services-Projekten  
 Im folgenden Diagramm werden die Ordner in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekt in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] veranschaulicht.  
  
 ![Ordner in einem Integration Services-Projekt](../integration-services/media/solutionexplorer.gif "Ordner in einem Integration Services-Projekt")  
  
 In der folgende Tabelle werden die Ordner in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekt beschrieben.  
  
|Ordner|Description|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] Pakete|Enthält Pakete. Weitere Informationen finden Sie unter [Integration Services-Pakete &#40;SSIS&#41;](../integration-services/integration-services-ssis-packages.md).|  
|Sonstiges|Enthält Dateien, die sich von Paketdateien unterscheiden.|  
  
## Dateien in SQL Server Integration Services-Projekten  
 Wenn Sie einer Projektmappe ein neues oder vorhandenes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekt hinzufügen, erstellt [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] Projektdateien mit den Erweiterungen DTPROJ, DTPROJ.USER und DATABASE.  
  
-   Die DTPROJ-Datei enthält Informationen zu Projektkonfigurationen und Elementen wie Pakete.  
  
-   Die DTPROJ.USER-Datei enthält Informationen zu Ihren Einstellungen für das Verwenden dieses Projekts.  
  
-   Die DATABASE-Datei enthält Informationen, die [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] zum Öffnen des [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekts benötigt.  
  
## Versionsauswahl in Integration Services-Projekten  
 In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] können Sie Pakete für SQL Server 2016, SQL Server 2014 oder SQL Server 2012 erstellen, verwalten und ausführen.  
  
 Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf ein Integration Services-Projekt, und wählen Sie **Eigenschaften** aus, um die Eigenschaftsseiten für das Projekt zu öffnen. Klicken Sie in der Registerkarte **Allgemein** in den **Konfigurationseigenschaften**auf die Eigenschaft **TargetServerVersion** , und wählen Sie dann SQL Server 2016, 2014 oder 2012 aus.  
  
 ![TargetServerVersion property in project properties dialog box](../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
  
## Lösungen enthalten Projekte  
 Eine Projektmappe ist ein Container, in dem die Projekte gruppiert und verwaltet werden, die Sie zum Entwickeln von End-to-End-Unternehmenslösungen verwenden. Mithilfe einer Projektmappe können Sie mehrere Projekte als Einheit verwalten und zusammenhängende Projekte für eine Unternehmenslösung zusammenbringen.  
  
 Projektmappen können unterschiedliche Projekttypen enthalten. Wenn Sie [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer zum Erstellen eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakets verwenden, arbeiten Sie in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekt in einer von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] bereitgestellten Projektmappe.  
  
 Wenn Sie eine neue Projektmappe erstellen, fügt [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] dem Projektmappen-Explorer einen Projektmappenordner hinzu und erstellt Dateien mit den Dateierweiterungen „.sln“ und „.suo“.  
  
-   Die SLN-Datei enthält Informationen zur Projektmappenkonfiguration und führt die Projekte in der Projektmappe auf.  
  
-   Die SUO-Datei enthält Informationen zu Ihren Einstellungen für das Verwenden der Projektmappe.  
  
 Zwar wird von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] beim Erstellen eines neuen Projekts automatisch eine Projektmappe erstellt, jedoch können Sie auch eine leere Projektmappe erstellen und später Projekte hinzufügen.  
  
> **HINWEIS:** Wenn Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekt erstellen, wird die Projektmappe standardmäßig nicht im Bereich **Projektexplorer** angezeigt. Um dieses Standardverhalten zu ändern, klicken Sie im Menü **Extras** auf **Optionen**. Erweitern Sie im Dialogfeld **Optionen** den Eintrag **Projekte und Projektmappen**, und klicken Sie dann auf **Allgemein**. Wählen Sie auf der Seite **Allgemein** die Option **Projektmappe immer anzeigen**aus.  
  
## Verwandte Aufgaben  
 [Hinzufügen oder Entfernen eines Integration Services-Projekts in einer Projektmappe](../Topic/Add%20or%20Remove%20an%20Integration%20Services%20Project%20in%20a%20Solution.md)  
  
 [Erstellen eines neuen SQL Server Integration Services-Projekts](../Topic/Create%20a%20New%20Integration%20Services%20Project.md)  
  
 [Hinzufügen eines Elements zu einem Integration Services-Projekt](../Topic/Add%20an%20Item%20to%20an%20Integration%20Services%20Project.md)  
  
 [Kopieren von Projektelementen](../Topic/Copy%20Project%20Items.md)  
  
## Verwandte Inhalte  
 [Entwicklung eines Integration Services-Projekts](../Topic/Development%20of%20an%20Integration%20Services%20Project.md)  
  
  