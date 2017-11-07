---
title: Datendefinitionsabfragen (Datamining) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49e02de1-4ffa-401c-8eee-471a9c25b86a
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a42d980837958ff2b605eeaac01dd61739bc1078
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="data-definition-queries-data-mining"></a>Datendefinitionsabfragen (Data Mining)
  Beim Data Mining umfasst die Kategorie *Datendefinitionsabfrage* DMX-Anweisungen und XMLA-Befehle, die folgende Operationen ausführen:  
  
-   Erstellen, Ändern oder Bearbeiten von Data Mining-Objekten, z. B. eines Modells.  
  
-   Definieren der Datenquelle, die für das Training oder für Vorhersagen verwendet werden soll.  
  
-   Exportieren oder Importieren von Miningmodellen und Miningstrukturen.  
  
 [Erstellen von Datendefinitionsabfragen](#bkmk_Create)  
  
-   [Datendefinitionsabfragen in SQL Server-Datentools](#bkmk_ssdt)  
  
-   [Datendefinitionsabfragen in SQL Server Management Studio](#bkmk_SSMS)  
  
 [Erstellen von Skripts für Datendefinitionsanweisungen](#bkmk_Scripts)  
  
 [Erstellen von Skripts für Datendefinitionsanweisungen](#bkmk_Export)  
  
##  <a name="bkmk_Create"></a> Erstellen von Datendefinitionsabfragen  
 Sie können Datendefinitionsabfragen (Anweisungen) mit dem Generator für Vorhersageabfragen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellen, oder das DMX-Abfragefenster in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verwenden. Datendefinitionsanweisungen in DMX sind Teil der Datendefinitionssprache (Data Definition Language, DDL) von Analysis Services.  
  
 Informationen zur Syntax bestimmter Datendefinitionsanweisungen finden Sie unter [DMX-Referenz &#40;Data Mining-Erweiterungen&#41;](../../dmx/data-mining-extensions-dmx-reference.md).  
  
###  <a name="bkmk_ssdt"></a> Datendefinitionsabfragen in SQL Server-Datentools  
 Der Data Mining-Assistent in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ist das bevorzugte Tool zum Erstellen und Ändern von Miningmodellen und Miningstrukturen und zum Definieren der Datenquellen, die in Vorhersageabfragen und beim Training verwendet werden.  
  
 Wenn Sie jedoch wissen möchten, welche Anweisungen vom Assistenten an den Server gesendet werden, um Datenstrukturen oder Miningmodelle zu erstellen, können Sie die Datendefinitionsanweisungen mithilfe von SQL Server Profiler aufzeichnen. Weitere Informationen finden Sie unter [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Um die Anweisungen anzuzeigen, die zum Definieren von Datenquellen für Training oder Vorhersagen verwendet werden, können Sie die **SQL-Sicht** im Generator für Vorhersageabfragen verwenden. Manchmal ist es hilfreich, mit dem Generator für Vorhersageabfragen zunächst grundlegende Abfragen für das Training und Testen von Modellen zu erstellen, um so eine richtige Syntax zu erhalten. Anschließend können Sie zur **SQL-Sicht** wechseln und die Abfrage manuell bearbeiten. Weitere Informationen finden Sie unter [Manually Edit a Prediction Query](../../analysis-services/data-mining/manually-edit-a-prediction-query.md).  
  
###  <a name="bkmk_SSMS"></a> Datendefinitionsabfragen in SQL Server Management Studio  
 Bei Data Mining-Objekten können Sie die folgenden Aktionen mithilfe von Datendefinitionsabfragen ausführen:  
  
-   Erstellen bestimmter Modelltypen, z.B. eines Clusteringmodells oder eines Entscheidungsstrukturmodells, mit [CREATE MINING MODEL &#40;DMX&#41;](../../dmx/create-mining-model-dmx.md).  
  
-   Ändern einer vorhandenen Miningstruktur durch Hinzufügen eines Modells oder Ändern der Spalten mit [ALTER MINING STRUCTURE &#40;DMX&#41;](../../dmx/alter-mining-structure-dmx.md). Beachten Sie, dass Sie ein Miningmodell nicht mit DMX ändern können. Sie fügen einer vorhandenen Struktur lediglich neue Modelle hinzu.  
  
-   Erstellen einer Kopie eines Miningmodells und Ändern der Kopie mit [SELECT INTO &#40;DMX&#41;](../../dmx/select-into-dmx.md).  
  
-   Definieren des Datasets für das Training eines Modells mit [INSERT INTO &#40;DMX&#41;](../../dmx/insert-into-dmx.md) und einer Datenquellenabfrage, z.B. OPENROWSET.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] stellt Abfragevorlagen bereit, die Ihnen beim Erstellen von Datendefinitionsabfragen helfen können. Weitere Informationen finden Sie unter [Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md).  
  
 Im Allgemeinen ist in den Vorlagen, die in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] für [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] bereitgestellt werden, nur die allgemeine Syntaxdefinition enthalten, die Sie dann durch Eingaben im Fenster **Abfrage** oder über das Dialogfeld für Parametereingaben anpassen müssen.  
  
 Ein Beispiel zur Eingabe von Parametern über die Benutzeroberfläche finden Sie unter [Erstellen einer SINGLETON-Vorhersageabfrage aus einer Vorlage](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md).  
  
###  <a name="bkmk_Scripts"></a> Erstellen von Skripts für Datendefinitionsanweisungen  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt mehrere Skript- und Programmiersprachen bereit, in denen Sie Data Mining-Objekte erstellen und ändern sowie Datenquellen definieren können.  Obwohl DMX zur schnelleren Verarbeitung von Data Mining-Tasks entworfen wurde, können Sie auch XMLA und AMO verwenden, um in Skripts oder benutzerdefiniertem Code Objekte zu bearbeiten.  
  
 Das Data Mining Add-In für Excel beinhaltet ebenfalls viele Abfragevorlagen und stellt den **Erweiterten Abfrage-Editor**bereit, der Sie beim Erstellen komplexer DMX-Anweisungen unterstützt. Sie können eine Abfrage interaktiv erstellen und dann zur SQL-Sicht wechseln, um die DMX-Anweisung aufzuzeichnen.  
  
##  <a name="bkmk_Export"></a> Exportieren und Importieren von Modellen  
 Sie können die Definition eines Modells und seine erforderliche Struktur sowie die Datenquellen mithilfe der Datendefinitionsanweisungen in DMX exportieren und anschließend diese Definition auf einem anderen Server importieren. Das Exportieren und Importieren ist die schnellste und einfachste Möglichkeit, Data Mining-Modelle und Miningstrukturen zwischen Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]zu verschieben. Weitere Informationen finden Sie unter [Verwaltung von Data Mining-Lösungen und -Objekten](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md).  
  
> [!WARNING]  
>  Wenn das Modell auf Daten aus einer Cubedatenquelle basiert, können Sie das Modell nicht mithilfe von DMX exportieren. Verwenden Sie stattdessen eine Sicherung und anschließende Wiederherstellung.  
  
##  <a name="bkmk_Tasks"></a> Verwandte Aufgaben  
 Die folgende Tabelle enthält Links zu verschiedenen Aufgaben im Zusammenhang mit Datendefinitionsabfragen.  
  
|||  
|-|-|  
|Arbeiten mit Vorlagen für DMX-Abfragen.|[Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|Entwerfen verschiedenster Abfragen mit dem Generator für Vorhersageabfragen.|[Erstellen von Vorhersageabfragen mithilfe des Generators für Vorhersageabfragen](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)|  
|Aufzeichnen von Abfragedefinitionen mit SQL Server Profiler und Verwenden von Ablaufverfolgungen zum Überwachen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)|  
|Erfahren Sie mehr zu den Skriptsprachen und Programmiersprachen, die für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]bereitgestellt werden.|[XML for Analysis-Referenz &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)<br /><br /> [Entwickeln mit Analysis Management Objects &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|Erfahren Sie, wie Modelle in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]verwaltet werden.|[Exportieren und Importieren von Data Mining-Objekten](../../analysis-services/data-mining/export-and-import-data-mining-objects.md)<br /><br /> [EXPORT &#40;DMX&#41;](../../dmx/export-dmx.md)<br /><br /> [IMPORT &#40;DMX&#41;](../../dmx/import-dmx.md)|  
|Erfahren Sie mehr über OPENROWSET und andere Möglichkeiten zum Abfragen von externen Daten.|[&#60;source data query&#62;](../../dmx/source-data-query.md)-Klausel (Quellabfrage-Klausel).|  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Assistent &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)  
  
  

