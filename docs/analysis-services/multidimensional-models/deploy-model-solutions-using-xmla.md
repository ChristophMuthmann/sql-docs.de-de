---
title: "Bereitstellen von Modelllösungen mit XMLA | Microsoft Docs"
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
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML scripts [Analysis Services]
- scripts [Analysis Services], deployment
- deploying [Analysis Services], XML scripts
- Analysis Services deployments, XML scripts
ms.assetid: a8cb1837-fcac-4730-bea4-a72cf94d9f7c
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b8315642255f95211c8e9bc2fd7e540351cdd3fb
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deploy-model-solutions-using-xmla"></a>Bereitstellen von Modelllösungen mit XMLA
  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]bewirkt die Option **CREATE in** des Befehls **Skript für Datenbank als** das Erstellen eines XML-Skripts für eine gesamte [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank oder für eines der in ihr enthaltenen Objekte. Das dabei entstehende Skript kann dann auf einem anderen Computer ausgeführt werden, um das Schema (die Metadaten) der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank neu zu erstellen. Das Skript generiert die gesamte Datenbank, und es gibt beim Verwenden des Skripts keine Mechanismen zum inkrementellen Aktualisieren bereits bereitgestellter Objekte. Nach dem Ausführen des Skripts und dem Bereitstellen der Datenbank muss die neu erstellte Datenbank verarbeitet werden, bevor Benutzer diese Datenbank durchsuchen können.  
  
 Weitere Informationen zum Befehl **Skript für Datenbank als** finden Sie unter [Dokumentieren und Skripterstellung einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md).  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>Ändern der Objekteigenschaften im XML-Skript  
 Beim Verwenden des Befehls **Skript für Datenbank als** können Sie keine bestimmten Eigenschaften der Datenbankobjekte ändern (z.B. den Datenbanknamen, die Datenquellenverbindungszeichenfolgen und die Sicherheitseinstellungen). Diese Eigenschaften müssen entweder manuell im Skript geändert werden, nachdem das Skript generiert wurde, oder sie müssen nach dem Ausführen des Skripts in der bereitgestellten Datenbank geändert werden.  
  
> [!IMPORTANT]  
>  Das XML-Skript enthält das Kennwort nicht, wenn dies in der Verbindungszeichenfolge für eine Datenquelle oder für Identitätswechsel angegeben ist. Da das Kennwort in diesem Szenario für Verarbeitungszwecke erforderlich ist, müssen Sie es dem XML-Skript entweder vor oder nach dem Ausführen des XML-Skripts manuell hinzufügen.  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)   
 [Synchronisieren von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
  

