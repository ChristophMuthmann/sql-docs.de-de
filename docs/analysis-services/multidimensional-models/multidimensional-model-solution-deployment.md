---
title: "Mehrdimensionale Modelllösungsbereitstellung | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services deployments, planning
- deploying [Analysis Services]
- deploying [Analysis Services], planning
ms.assetid: 7259c201-ff54-43e8-bda5-a6d51474e0e6
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d09db4ead5f0b05d82c40a16aed31a070b16250c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="multidimensional-model-solution-deployment"></a>Mehrdimensionale Modelllösungsbereitstellung
  Nachdem Sie die Entwicklung eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts abgeschlossen haben, können Sie die Datenbank auf einem Analysis Services-Server bereitstellen. Analysis Services bietet sechs mögliche Bereitstellungsmethoden, die zum Umlagern der Datenbank auf einen Test- oder Produktionsserver verwendet werden können. Die Methoden werden nach ihren Vorteilen aufgelistet: AMO-Automatisierung, XMLA, Bereitstellungs-Assistent, Bereitstellungshilfsprogramm, Synchronisations-Assistent sowie Sicherung und Wiederherstellung.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Bereitstellungsmethoden](#bkmk_meth)  
  
 [Überlegungen zur Bereitstellung](#bkmk_considerations)  
  
 [Verwandte Aufgaben](#bkmk_rel)  
  
##  <a name="bkmk_meth"></a> Bereitstellungsmethoden  
  
|Methode|Description|Link|  
|------------|-----------------|----------|  
|**Analysis Management Objects (AMO)-Automatisierung**|AMO stellt eine programmgesteuerte Schnittstelle für den vollständigen Befehlssatz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]bereit, einschließlich Befehlen zur Bereitstellung von Projektmappen. Die AMO-Automatisierung bietet die flexibelste Möglichkeit zur Bereitstellung von Projektmappen, impliziert jedoch gleichzeitig einen gewissen Programmieraufwand.  Ein wichtiger Vorteil bei der Verwendung von AMO besteht darin, dass der SQL Server-Agent mit der AMO-Anwendung zum Ausführen einer Bereitstellung nach einem festgelegten Zeitplan verwendet werden kann.|[Entwickeln mit Analysis Management Objects &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|**XMLA**|Verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , um ein XMLA-Skript der Metadaten einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank zu erstellen, und führen Sie dieses Skript dann auf einem anderen Server aus, um die ursprüngliche Datenbank erneut zu erstellen. XMLA-Skripts können in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] einfach erstellt werden, indem Sie den Bereitstellungsprozess definieren, anschließend codieren und in einem XMLA-Skript speichern. Nachdem Sie das XMLA-Skript in einer Datei gespeichert haben, können Sie das Skript einfach gemäß einem Zeitplan ausführen oder das Skript in eine Anwendung einbetten, die eine direkte Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]herstellt.<br /><br /> Sie können auch XMLA-Skripts auf einer vordefinierten Basis mithilfe des SQL Server-Agents ausführen, aber dabei bieten Ihnen XMLA-Skripts nicht dieselbe Flexibilität wie AMO. AMO stellt eine größere Bandbreite an Funktionalität bereit, indem es das gesamte Spektrum von Verwaltungsbefehlen hostet.|[Bereitstellen von Modelllösungen mit XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**Bereitstellungs-Assistent**|Verwenden Sie den Bereitstellungs-Assistenten, um mithilfe der durch ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt generierten XML-Ausgabedateien die Metadaten des Projekts auf einem Zielserver bereitzustellen. Mit dem Bereitstellungs-Assistenten können Sie die Bereitstellung direkt in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datei ausführen, die während der Projekterstellung im Ausgabeverzeichnis erstellt wurde.<br /><br /> Der Hauptvorteil bei der Verwendung des Bereitstellungs-Assistenten von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] besteht in der Benutzerfreundlichkeit. Genauso wie ein XMLA-Skript zur späteren Verwendung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]gespeichert werden kann, können Skripts des Bereitstellungs-Assistenten gespeichert werden. Der Bereitstellungs-Assistent kann sowohl interaktiv als auch mit dem Bereitstellungshilfsprogramm über die Eingabeaufforderung ausgeführt werden.|[Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**Bereitstellungshilfsprogramm**|Mit dem Bereitstellungshilfsprogramm kann das Analysis Services-Bereitstellungsmodul über die Eingabeaufforderung gestartet werden.|[Bereitstellen von Modelllösungen mit dem Bereitstellungshilfsprogramm](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**Assistent zum Synchronisieren einer Datenbank**|Verwenden Sie den Assistenten zum Synchronisieren einer Datenbank, um die Metadaten und Daten zwischen zwei [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken zu synchronisieren.<br /><br /> Mithilfe des Synchronisations-Assistenten können Sie sowohl Daten als auch Metadaten von einem Quellserver auf einen Zielserver kopieren. Wenn der Zielserver keine Kopie der Datenbank enthält, die Sie bereitstellen möchten, wird eine neue Datenbank auf den Zielserver kopiert. Wenn auf dem Zielserver bereits eine Kopie derselben Datenbank vorhanden ist, wird die Datenbank auf dem Zielserver aktualisiert, damit sie die Metadaten und Daten der Quelldatenbank verwendet.|[Synchronisieren von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)|  
|**Sichern und Wiederherstellen**|Das Sichern stellt die einfachste Vorgehensweise zum Übertragen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken dar. Im Dialogfeld **Sichern** können Sie die Konfiguration der Optionen festlegen und anschließend die Sicherung über das Dialogfeld ausführen. Alternativ können Sie ein Skript erstellen, das Sie speichern und so oft wie nötig ausführen können.<br /><br /> Sichern und Wiederherstellen wird nicht so häufig verwendet wie die anderen Bereitstellungsmethoden, aber diese Methode stellt eine Möglichkeit zum schnellen Abschließen einer Bereitstellung mit minimalen Infrastrukturanforderungen dar.|[Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_considerations"></a> Überlegungen zur Bereitstellung  
 Bevor Sie ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt bereitstellen, sollten Sie überlegen, welche der folgenden Fragen auf Ihre Projektmappe zutreffen, und sich dann anhand der angegebenen Links über die richtige Vorgehensweise informieren:  
  
|Aspekt|Link zu weiteren Informationen|  
|-------------------|------------------------------|  
|Welche Hardware- und Softwareressourcen sind für diese Projektmappe erforderlich?|[Anforderungen und Überlegungen für die Bereitstellung von Analysis Services](../../analysis-services/multidimensional-models/requirements-and-considerations-for-analysis-services-deployment.md)|  
|Wie sollen verbundene Objekte außerhalb des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projektbereichs, wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete, Berichte oder relationale Datenbankschemas, bereitgestellt werden?||  
|Wie werden die Daten in der bereitgestellten [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank geladen und aktualisiert?<br /><br /> Wie werden die Metadaten (z.B. Berechnungen) in der bereitgestellten [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank aktualisiert?|[Bereitstellungsmethoden](#bkmk_meth) in diesem Thema.|  
|Sollen Benutzer über das Internet auf [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Daten zugreifen können?|[Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|  
|Soll ein kontinuierlicher Abfragezugriff auf [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Daten möglich sein?|[Anforderungen und Überlegungen für die Bereitstellung von Analysis Services](../../analysis-services/multidimensional-models/requirements-and-considerations-for-analysis-services-deployment.md)|  
|Sollen Objekte mithilfe von verknüpften Objekten oder Remotepartitionen in einer verteilten Umgebung bereitgestellt werden?|[Erstellen und Verwalten einer lokalen Partition &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md), [Erstellen und Verwalten einer Remotepartition &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md) und [Verknüpfte Measuregruppen](../../analysis-services/multidimensional-models/linked-measure-groups.md).|  
|Wie sollen die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Daten gesichert werden?|[Autorisieren des Zugriffs auf Objekte und Vorgänge &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)|  
  
##  <a name="bkmk_rel"></a> Verwandte Aufgaben  
 [Anforderungen und Überlegungen für die Bereitstellung von Analysis Services](../../analysis-services/multidimensional-models/requirements-and-considerations-for-analysis-services-deployment.md)  
  
 [Bereitstellen von Modelllösungen mit XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)  
  
 [Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
 [Bereitstellen von Modelllösungen mit dem Bereitstellungshilfsprogramm](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  
