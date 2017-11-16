---
title: Angeben des Installationszieles | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input files [Analysis Services]
- installation targets [Analysis Services]
- Analysis Services deployments, installation targets
- Analysis Services Deployment Wizard, installation targets
- deploying [Analysis Services], installation targets
- modifying installation targets
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e284ed2df95c56c19ed25cad79f4cf11099902f2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deployment-script-files---specifying-the-installation-target"></a>Bereitstellung Skriptdateien - angeben des Installationszieles
  Die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Bereitstellungsassistent liest die Informationen zum Installationsziel aus der \< *Projektname*> .deploymenttargets-Datei. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erstellt diese Datei, wenn Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellen. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]anhand der Datenbank und auf angegebene Server die **Bereitstellung** auf der Seite der  *\<Projektname >* **Eigenschaftenseiten** Dialogfeld zum Erstellen der \< *Projektname*> .targets-Datei.  
  
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
 [Angeben von Bereitstellungsoptionen für Partitionen und Rollen](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [Angeben der Konfigurationseinstellungen für die Lösungsbereitstellung](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [Angeben von Verarbeitungsoptionen](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  

