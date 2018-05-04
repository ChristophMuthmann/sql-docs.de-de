---
title: Angeben des Installationszieles | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ef168e39d162aabeb6cb6eb46ce3ab61216af288
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deployment-script-files---specifying-the-installation-target"></a>Bereitstellung Skriptdateien - angeben des Installationszieles
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Bereitstellungsassistent liest die Informationen zum Installationsziel aus der \< *Projektname*> .deploymenttargets-Datei. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Diese Datei erstellt, beim Erstellen der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekt. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] anhand der Datenbank und auf angegebene Server die **Bereitstellung** auf der Seite der  *\<Projektname >* **Eigenschaftenseiten** Dialogfeld zum Erstellen der \< *Projektname*> .targets-Datei.  
  
## <a name="modifying-the-installation-target-for-deployment"></a>Ändern des Installationszieles für die Bereitstellung  
 In einigen Situationen müssen Sie möglicherweise ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt für eine andere Datenbank oder eine andere Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitstellen, als auf der Seite **Bereitstellung** angegeben ist. Vielleicht möchten Sie das Projekt, bevor Sie es bereitstellen, erst auf einem Server zum Testen bereitstellen und es nach Abschluss der Testes auf einem Produktionsserver bereitstellen. Sie können aber auch ein abgeschlossenes und getestetes Projekt auf mehreren Produktionsservern in einem Netzwerklastenausgleich-Cluster oder auf einem Stagingserver und einem Produktionsserver bereitstellen.  
  
 Sie können mit einer der im Folgenden beschriebenen Methoden das Installationsziel in der Eingabedatei ändern, um ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt auf einer anderen Datenbank oder einer anderen Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitzustellen.  
  
#### <a name="to-change-the-installation-target-after-the-input-files-have-been-generated"></a>So ändern Sie das Installationsziel, nachdem die Eingabedateien erstellt wurden  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interaktiv aus. Geben Sie auf der Seite **Installationsziel** ein neues Ziel für die Instanz und die Datenbank von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an.  
  
     – oder –  
  
-   Führen Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an der Eingabeaufforderung aus, und legen Sie fest, dass der Assistent im Antwortdateimodus ausgeführt wird. Weitere Informationen zum Antwortdateimodus finden Sie unter [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     – oder –  
  
-   Ändern der \< *Projektname*> .deploymenttargets-Datei mit einem beliebigen Texteditor.  
  
## <a name="see-also"></a>Siehe auch  
 [Angeben von Partition und Optionen für die Rollenbereitstellung](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [Angeben der Konfigurationseinstellungen für die Lösungsbereitstellung](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [Angeben von Verarbeitungsoptionen](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
