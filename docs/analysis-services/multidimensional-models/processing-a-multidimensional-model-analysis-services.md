---
title: Verarbeiten eines mehrdimensionalen Modells (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- online mode [Analysis Services]
- processing objects [Analysis Services]
- partitions [Analysis Services], processing
- jobs [Analysis Services]
- objects [Analysis Services], processing
- reprocessing objects
- impact analysis [Analysis Services]
- dimensions [Analysis Services], processing
- project mode [Analysis Services]
- cubes [Analysis Services], processing
ms.assetid: 625aa5a6-aa09-4bac-be8a-778fa81c5a61
caps.latest.revision: 52
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eb063d1667fc3cd3824f2577784278fa46308960
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="processing-a-multidimensional-model-analysis-services"></a>Verarbeiten eines mehrdimensionalen Modells (Analysis Services)
  Die Verarbeitung bezeichnet den Schritt oder eine Abfolge von Schritten, durch die Daten von Analysis Services aus einer relationalen Datenquelle in ein mehrdimensionales Modell geladen werden. Bei Objekten, die die MOLAP-Speicherung verwenden, werden Daten auf dem Datenträger im Datenbankdateiordner gespeichert. In Bezug auf den ROLAP-Speicher ist die Verarbeitung bedarfsbasiert, und zwar als Reaktion auf eine MDX-Abfrage auf einem Objekt. Bei Objekten, die die ROLAP-Speicherung verwenden, bezieht sich "Verarbeitung" auf die Aktualisierung des Caches, bevor Abfrageergebnisse zurückgegeben werden.  
  
 Die Verarbeitung wird standardmäßig ausgeführt, wenn eine Projektmappe auf dem Server bereitgestellt wird. Sie können eine Projektmappe auch vollständig oder teilweise verarbeiten, indem Sie entweder Ad-hoc-Tools wie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oder [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]verwenden oder eine zeitgesteuerte Verarbeitung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und SQL Server-Agent durchführen. Wenn Sie eine strukturelle Änderung am Modell vornehmen, z.. B. eine Dimension entfernen oder den Kompatibilitätsgrad ändern, müssen Sie die Verarbeitung wiederholen, um die physischen und logischen Aspekte des Modells zu synchronisieren.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Erforderliche Komponenten](#bkmk_prereq)  
  
 [Auswählen eines Tools oder eines Ansatzes](#bkmk_tool)  
  
 [Verarbeiten von Objekten](#bkmk_proc)  
  
 [Reprocessing Objects](#bkmk_reproc)  
  
##  <a name="bkmk_prereq"></a> Erforderliche Komponenten  
  
-   Zur Verarbeitung werden Administratorberechtigungen auf der Analysis Services-Instanz benötigt. Bei der interaktiven Verarbeitung von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] oder [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]aus müssen Sie Mitglied der Serveradministratorrolle auf der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz sein. Um eine unbeaufsichtigte Verarbeitung durchzuführen, z. B. über ein SSIS-Paket, das zeitgesteuert vom SQL Server-Agent ausgeführt wird, muss das Konto, unter dem das Paket ausgeführt wird, Mitglied der Serveradministratorrolle sein. Weitere Informationen zur Einstellung von Administratorberechtigungen finden Sie unter [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
-   Das für den Datenempfang verwendete Konto wird im Datenquellenobjekt angegeben, entweder als eine Identitätswechseloption, wenn die Windows-Authentifizierung verwendet wird, oder als Benutzername in der Verbindungszeichenfolge, wenn die Datenbankauthentifizierung verwendet wird. Das Konto muss über Leseberechtigungen für relationale Datenquellen verfügen, die vom Modell verwendet werden.  
  
-   Bevor Objekte verarbeitet werden können, muss das Projekt oder die Lösung bereitgestellt werden.  
  
     In der frühen Phase der Modellentwicklung werden Bereitstellung und Verarbeitung zunächst zusammen ausgeführt. Nachdem Sie die Lösung bereitgestellt haben, können Sie anhand von Optionen jedoch festlegen, dass das Modell zu einem späteren Zeitpunkt verarbeitet wird. Weitere Informationen zur Bereitstellung finden Sie unter [Bereitstellen von Analysis Services-Projekten &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md).  
  
##  <a name="bkmk_tool"></a> Auswählen eines Tools oder eines Ansatzes  
 Sie können Objekte interaktiv verarbeiten, und zwar mithilfe einer Clientanwendung, beispielsweise [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] oder [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], oder einem skriptbasierten Vorgang, der als SQL Server-Agent-Auftrag oder [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paket ausgeführt wird.  
  
 Auf welche Weise Sie eine Datenbank verarbeiten, hängt beachtlich davon ab, ob sich das Modell in einer aktiven Entwicklung oder in der Produktion befindet. Sobald ein Modell auf einem Produktionsserver bereitgestellt wird, muss die Verarbeitung eng gesteuert sein, um die Integrität und die Verfügbarkeit mehrdimensionaler Daten sicherzustellen. Da Objekte untereinander abhängig sind, hat die Verarbeitung in der Regel einen kaskadierenden Effekt über das Modell hinweg, da andere Objekte auch gleichzeitig verarbeitet bzw. nicht verarbeitet werden. Wenn einige Objekte in einem nicht verarbeiteten Status bleiben, werden Anfragen für diese Daten nicht so aufgelöst, dass Berichte oder Anwendungen unterbrochen werden, von denen sie verwendet werden. Wenn Sie eine Strategie zum Verarbeiten einer Produktionsdatenbank entwickeln, verwenden Sie dabei für die Erwägung Skripts oder [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Pakete, die Sie gedebugged und getestet haben, um Operatorfehler oder übersehene Schritte zu vermeiden.  
  
 Weitere Informationen finden Sie unter [Tools und Ansätze für die Verarbeitung &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
##  <a name="bkmk_proc"></a> Verarbeiten von Objekten  
 Die Verarbeitung betrifft die folgenden [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte: Measuregruppen, Partitionen, Dimensionen, Cubes, Miningmodelle, Miningstrukturen und Datenbanken. Wenn ein Objekt mindestens ein Objekt enthält, führt die Verarbeitung des Objekts der höchsten Ebene zum Kaskadieren der Verarbeitung aller Objekte der niedrigeren Ebenen. Beispielsweise enthält ein Cube in der Regel mindestens eine Measuregruppe (von denen jede eine oder mehrere Partitionen enthält) und Dimensionen. Die Verarbeitung eines Cubes bewirkt die Verarbeitung aller im Cube enthaltenen Measuregruppen und deren noch nicht verarbeitete Dimensionen. Weitere Informationen zur Verarbeitung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekten finden Sie unter [Verarbeiten von Analysis Services-Objekten](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md).  
  
 Während der Ausführung des Verarbeitungsauftrags sind die betroffenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte für Abfragen verfügbar. Der Verarbeitungsauftrag erfolgt innerhalb einer Transaktion, welche ihrerseits ein Commit oder ein Rollback der Änderungen durchführt. Wenn der Verarbeitungsauftrag fehlschlägt, wird ein Rollback für die Transaktion ausgeführt. Wenn der Verarbeitungsauftrag erfolgreich ausgeführt wird, wird das Objekt während des Commits der Änderungen exklusiv gesperrt, d. h. das Objekt ist vorübergehend nicht für Abfragen oder andere Verarbeitungen verfügbar. Während der Commitphase der Transaktion können weiterhin Abfragen an das Objekt gesendet werden; diese werden jedoch in eine Warteschlangen gestellt, bis der Commit abgeschlossen ist.  
  
 Ob und wie Objekte von einem Verarbeitungsauftrag verarbeitet werden, ist von den Verarbeitungsoptionen abhängig, die für das Objekt festgelegt wurden. Weitere Informationen zu den spezifischen Verarbeitungsoptionen von Objekten finden Sie unter [Verarbeiten von Optionen und Einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
##  <a name="bkmk_reproc"></a> Reprocessing Objects  
 Cubes, die nicht verarbeitete Elemente enthalten, müssen erneut verarbeitet werden, bevor sie durchsucht werden können. Cubes in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] enthalten Measuregruppen und Partitionen, die verarbeitet werden müssen, bevor der Cube abgefragt werden kann. Die Verarbeitung eines Cubes veranlasst [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , die darin enthaltenen Dimensionen zu verarbeiten, falls sich diese im Status Nicht verarbeitet befinden. Nachdem ein Objekt das erste Mal verarbeitet wurde, ist die erneute Teil- oder vollständige Verarbeitung erforderlich, wenn eine der folgenden Situationen eintritt:  
  
-   Die Struktur des Objekts ändert sich (z. B. wird in einer Faktentabelle eine Spalte gelöscht).  
  
-   Der Aggregationsentwurf für das Objekt wurde geändert.  
  
-   Die Daten im Objekt müssen aktualisiert werden.  
  
 Beim Verarbeiten von Objekten in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]können Sie eine Verarbeitungsoption auswählen, oder Sie können die jeweils geeignete Verarbeitungsart automatisch mithilfe von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bestimmen. Die verfügbaren Verarbeitungsmethoden unterscheiden sich von Objekt zu Objekt und basieren auf dem Objekttyp. Zusätzlich basieren die verfügbaren Methoden auf den Änderungen, die im Objekt seit der letzten Verarbeitung aufgetreten sind. Wenn Sie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwenden, um die Verarbeitungsmethode automatisch auszuwählen, wird die Methode verwendet, die das Objekt in der kürzesten Zeit in einem vollständig verarbeiteten Zustand zurückgibt. Weitere Informationen finden Sie unter [Verarbeitungsoptionen und -einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Logische Architektur &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  

