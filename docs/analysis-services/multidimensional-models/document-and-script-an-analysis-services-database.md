---
title: Dokumentieren und Skripterstellung eine Analysis Services-Datenbank | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf7f3de5da4b7477ba27fd3f46a8627ac94aedb2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="document-and-script-an-analysis-services-database"></a>Dokumentieren und Skripterstellung einer Analysis Services-Datenbank
  Nachdem eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank bereitgestellt ist, können Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] die Metadaten der Datenbank oder eines in der Datenbank enthaltenen Objekts als XML for Analysis-Skript (XMLA) ausgeben. Sie können dieses Skript in ein neues **XMLA-Abfrage-Editor** -Fenster, in eine Datei oder die Zwischenablage exportieren. Weitere Informationen zu XMLA finden Sie unter [Analysis Services Scripting Language &#40;ASSL for XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md) (Analysis Services Scripting Language (ASSL für XMLA)).  
  
 Das generierte XMLA-Skript verwendet Elemente der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Skriptsprache (ASSL), um im Skript enthaltene Objekte zu definieren. Wenn Sie ein CREATE-Skript generiert haben, enthält das entstandene XMLA-Skript einen XMLA **Create** -Befehl und ASSL-Elemente, die verwendet werden können, um die gesamte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankstruktur auf einer Instanz zu erstellen. Wenn Sie ein ALTER-Skript generiert haben, enthält das resultierende XMLA-Skript den XMLA-Befehl **Alter** und ASSL-Elemente, mit denen die Struktur einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank wieder in dem Zustand wiederhergestellt werden kann, den sie zum Zeitpunkt der Skripterstellung innehatte.  
  
 Sie können das aus einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank generierte XMLA-Skript auf viele verschiedene Weisen verwenden, so z. B. wie folgt:  
  
-   Verwalten eines Sicherungsskripts, mit dem Sie alle Datenbankobjekte und -berechtigungen neu erstellen können.  
  
-   Erstellen oder Aktualisieren von Datenbankentwicklungscode.  
  
-   Erstellen eines Testes oder einer Entwicklungsumgebung aus einem vorhandenen Schema heraus.  
  
## <a name="see-also"></a>Siehe auch  
 [Ändern oder Löschen einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Alter-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [Erstellen Sie-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  
