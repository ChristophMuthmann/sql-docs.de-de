---
title: Bestimmen des Servermodus einer Analysis Services-Instanz | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f771aec5fa4bfdcb57a471e3f735e2eae9a9cc8a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="determine-the-server-mode-of-an-analysis-services-instance"></a>Bestimmen des Servermodus einer Analysis Services-Instanz
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services kann in einem von drei Servermodi installiert sein: mehrdimensional und Data Mining (Standard), [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint und tabellarisch. Der Servermodus einer Analysis Services-Instanz wird während des Setups bestimmt, wenn Sie die Optionen zum Installieren des Servers auswählen.  
  
 Der Servermodus bestimmt den Typ der Lösung, die Sie erstellen und bereitstellen. Wenn Sie die Serversoftware nicht installiert haben und Sie wissen möchten, in welchem Modus der Server installiert ist, können Sie die Informationen aus diesem Abschnitt nutzen, um den Modus zu bestimmen. Weitere Informationen zu den verfügbaren Funktionen in einem bestimmten Modus finden Sie unter [Vergleichen von tabellarischen und mehrdimensionalen Lösungen ](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md).  
  
 Wenn Sie den Servermodus, den Sie installiert haben, nicht verwenden möchten, müssen Sie die Software deinstallieren und anschließend neu installieren. Wählen Sie dann den Modus aus, den Sie bevorzugen. Alternativ können Sie auf demselben Computer eine zusätzliche Instanz von Analysis Services installieren, damit Sie mehrere Instanzen nutzen, die verschiedene Modi ausführen.  
  
## <a name="server-icons-in-object-explorer"></a>Server-Symbole in Objekt-Explorer  
 Die einfachste Art zur Bestimmung des Servermodus besteht darin, in SQL Server Management Studio eine Verbindung mit dem Server herzustellen und das Symbol neben dem Servernamen in Objekt-Explorer zu erfassen. Die folgende Illustration zeigt drei Instanzen von Analysis Services, die im mehrdimensionalen, tabellarischen oder [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Modus bereitgestellt werden:  
  
 ![Objekt-Explorer-Symbole für jeden Servermodus](../../analysis-services/instances/media/ssas-ssms-servermodes.gif "Objekt-Explorer-Symbole für jeden Servermodus")  
  
## <a name="viewing-deploymentmode-property-in-msmdsrvini-file"></a>Anzeigen der DeploymentMode-Eigenschaft in Datei MSMDSRV.INI  
 Alternativ können Sie die **DeploymentMode** -Eigenschaft in der Datei „msmdsrv.ini“ überprüfen, die in jeder Analysis Services-Instanz enthalten ist. Der Wert dieser Eigenschaft erkennt den Servermodus. Gültige Werte betragen 0 (mehrdimensional), 1 (SharePoint) oder 2 (tabellarisch). Sie müssen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Administrator (Mitglied der Serverrolle) sein, um die Datei „msmdsrv.ini“ öffnen zu können. Diese Datei enthält strukturierte XML. Sie können die Datei mithilfe des Editors oder eines alternativen Text-Editors anzeigen.  
  
> [!CAUTION]  
>  Ändern Sie den Wert für **DeploymentMode** nicht. Die manuelle Änderung der Eigenschaft nach dem Installieren des Servers wird nicht unterstützt.  
  
## <a name="about-the-deploymentmode-property"></a>Informationen zur DeploymentMode-Eigenschaft  
 Die**DeploymentMode** -Eigenschaft bestimmt den operativen Kontext einer Analysis Services-Serverinstanz. Diese Eigenschaft wird in Dialogfeldern, Meldungen und Dokumentation als "Servermodus" bezeichnet. Diese Eigenschaft wird vom Setup auf Grundlage des Installationsmodus von Analysis Services initialisiert. Diese Eigenschaft sollte nur intern berücksichtigt und immer der vom Setup angegebene Wert verwendet werden.  
  
 Für diese Eigenschaften gibt es u. a. folgende gültige Werte:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Dies ist der Standardwert. Der mehrdimensionale Modus wird angegeben. Er dient zur Verwaltung von mehrdimensionalen Datenbanken, die MOLAP, HOLAP und ROLAP-Speicher sowie Data Mining-Modelle verwenden.|  
|1|Gibt Analysis Services-Instanzen an, die als Teil einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung installiert waren. Ändern Sie die Bereitstellungsmoduseigenschaft der Analysis Services-Instanz nicht, die Teil einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installation ist. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten nicht mehr auf dem Server ausgeführt.|  
|2|Gibt den Tabellenmodus an, der zum Hosten von Tabellenmodelldatenbanken dient, die Speicher im Arbeitsspeicher oder DirectQuery-Speicher verwenden.|  
  
 Die Modi schließen sich gegenseitig aus. Ein Server, der für den Tabellenmodus konfiguriert ist, kann keine Analysis Services-Datenbanken ausführen, die Cubes und Dimensionen enthalten. Bei Unterstützung durch die zugrunde liegende Computerhardware können Sie mehrere Instanzen von Analysis Services auf demselben Computer installieren und jede Instanz für einen anderen Bereitstellungsmodus konfigurieren. Beachten Sie, dass Analysis Services eine ressourcenintensive Anwendung ist. Die Bereitstellung mehrerer Instanzen auf demselben System wird nur für High-End-Server empfohlen.  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)   
 [Installieren von Analysis Services im mehrdimensionalen Modus und im Data Mining-Modus](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Installation von PowerPivot für SharePoint 2010](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)   
 [Herstellen einer Verbindung mit Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)   
 [Projektmappen für tabellarische Modelle](../../analysis-services/tabular-models/tabular-models-ssas.md)   
 [Mehrdimensionale Modelllösungen ](../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [Miningmodelle & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
