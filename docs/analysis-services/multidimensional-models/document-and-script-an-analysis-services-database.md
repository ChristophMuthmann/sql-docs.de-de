---
title: Dokumentieren und Skripterstellung eine Analysis Services-Datenbank | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 645499bc5311f74ba689b3cd48d2516c01d384fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="document-and-script-an-analysis-services-database"></a>Dokumentieren und Skripterstellung einer Analysis Services-Datenbank
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Nachdem eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank bereitgestellt ist, können Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] die Metadaten der Datenbank oder eines in der Datenbank enthaltenen Objekts als XML for Analysis-Skript (XMLA) ausgeben. Sie können dieses Skript in ein neues **XMLA-Abfrage-Editor** -Fenster, in eine Datei oder die Zwischenablage exportieren. Weitere Informationen zu XMLA finden Sie unter [Analysis Services Scripting Language &#40;ASSL for XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md) (Analysis Services Scripting Language (ASSL für XMLA)).  
  
 Das generierte XMLA-Skript verwendet Elemente der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Skriptsprache (ASSL), um im Skript enthaltene Objekte zu definieren. Wenn Sie ein CREATE-Skript generiert haben, enthält das entstandene XMLA-Skript einen XMLA **Create** -Befehl und ASSL-Elemente, die verwendet werden können, um die gesamte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankstruktur auf einer Instanz zu erstellen. Wenn Sie ein ALTER-Skript generiert haben, enthält das resultierende XMLA-Skript den XMLA-Befehl **Alter** und ASSL-Elemente, mit denen die Struktur einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank wieder in dem Zustand wiederhergestellt werden kann, den sie zum Zeitpunkt der Skripterstellung innehatte.  
  
 Sie können das aus einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank generierte XMLA-Skript auf viele verschiedene Weisen verwenden, so z. B. wie folgt:  
  
-   Verwalten eines Sicherungsskripts, mit dem Sie alle Datenbankobjekte und -berechtigungen neu erstellen können.  
  
-   Erstellen oder Aktualisieren von Datenbankentwicklungscode.  
  
-   Erstellen eines Testes oder einer Entwicklungsumgebung aus einem vorhandenen Schema heraus.  
  
## <a name="see-also"></a>Siehe auch  
 [Ändern oder Löschen einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Alter-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [Create-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  
