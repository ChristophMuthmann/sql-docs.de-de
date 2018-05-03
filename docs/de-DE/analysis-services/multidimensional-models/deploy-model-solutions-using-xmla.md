---
title: Bereitstellen von Modelllösungen mit XMLA | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 70dbd820e0ef1936d60dc1dca3508897c4b6764a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-model-solutions-using-xmla"></a>Bereitstellen von Modelllösungen mit XMLA
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]bewirkt die Option **CREATE in** des Befehls **Skript für Datenbank als** das Erstellen eines XML-Skripts für eine gesamte [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank oder für eines der in ihr enthaltenen Objekte. Das dabei entstehende Skript kann dann auf einem anderen Computer ausgeführt werden, um das Schema (die Metadaten) der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank neu zu erstellen. Das Skript generiert die gesamte Datenbank, und es gibt beim Verwenden des Skripts keine Mechanismen zum inkrementellen Aktualisieren bereits bereitgestellter Objekte. Nach dem Ausführen des Skripts und dem Bereitstellen der Datenbank muss die neu erstellte Datenbank verarbeitet werden, bevor Benutzer diese Datenbank durchsuchen können.  
  
 Weitere Informationen zum Befehl **Skript für Datenbank als** finden Sie unter [Dokumentieren und Skripterstellung einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md).  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>Ändern der Objekteigenschaften im XML-Skript  
 Beim Verwenden des Befehls **Skript für Datenbank als** können Sie keine bestimmten Eigenschaften der Datenbankobjekte ändern (z.B. den Datenbanknamen, die Datenquellenverbindungszeichenfolgen und die Sicherheitseinstellungen). Diese Eigenschaften müssen entweder manuell im Skript geändert werden, nachdem das Skript generiert wurde, oder sie müssen nach dem Ausführen des Skripts in der bereitgestellten Datenbank geändert werden.  
  
> [!IMPORTANT]  
>  Das XML-Skript enthält das Kennwort nicht, wenn dies in der Verbindungszeichenfolge für eine Datenquelle oder für Identitätswechsel angegeben ist. Da das Kennwort in diesem Szenario für Verarbeitungszwecke erforderlich ist, müssen Sie es dem XML-Skript entweder vor oder nach dem Ausführen des XML-Skripts manuell hinzufügen.  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)   
 [Synchronisieren von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
  
