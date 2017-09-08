---
title: Data Mining-Abfragetasks | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataminingquerytask.f1
- sql13.dts.designer.dmquerytask.miningmodel.f1
- sql13.dts.designer.dmquerytask.query.f1
- sql13.dts.designer.dmquerytask.output.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: efffacb30616a880c628894dac2f49201c2b8e24
ms.contentlocale: de-de
ms.lasthandoff: 08/11/2017

---
# <a name="data-mining-query-task"></a>Data Mining-Abfragetask
  Der Data Mining-Abfragetask führt Vorhersageabfragen basierend auf in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erstellten Data Mining-Modellen aus. Die Vorhersageabfrage erstellt mithilfe von Miningmodellen eine Vorhersage für neue Daten. Beispielsweise kann eine Vorhersageabfrage vorhersagen, wie viele Segelboote in den Sommermonaten voraussichtlich verkauft werden, oder sie kann eine Liste potenzieller Kunden generieren, die mit hoher Wahrscheinlichkeit ein Segelboot kaufen werden.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt Tasks bereit, die andere Business Intelligence-Vorgänge ausführen, z.B. das Ausführen von DDL-Anweisungen (Data Definition Language, Datendefinitionssprache) und das Verarbeiten analytischer Objekte.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu weiteren Business Intelligence-Tasks zu erhalten:  
  
-   [DDL ausführen (Analysis Services-Task)](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services-Verarbeitungstask](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>Vorhersageabfragen  
 Bei der Abfrage handelt es sich um eine DMX-Anweisung (Data Mining Extensions). Die DMX-Sprache ist eine Erweiterung der SQL-Sprache, die das Arbeiten mit Miningmodellen unterstützt. Weitere Informationen zum Verwenden der DMX-Sprache finden Sie unter [Data Mining-Erweiterungen &#40;DMX&#41; – Referenz](../../dmx/data-mining-extensions-dmx-reference.md).  
  
 Der Task kann mehrere Miningmodelle abfragen, die auf der gleichen Miningstruktur basieren. Ein Miningmodell wird mithilfe eines der Data Mining-Algorithmen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellt. Die Miningstruktur des Data Mining-Abfragetasks kann mehrere Miningmodelle einschließen, die mit verschiedenen Algorithmen erstellt wurden. Weitere Informationen finden Sie unter [Miningstrukturen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md) und [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 Die Vorhersageabfrage, die der Data Mining-Abfragetask ausführt, gibt als Ergebnis eine einzelne Zeile oder ein Dataset zurück. Eine Abfrage, die eine einzelne Zeile zurückgibt, wird als SINGLETON-Abfrage bezeichnet: Beispielsweise gibt die Abfrage zur Vorhersage, wie viele Segelboote in den Sommermonaten verkauft werden, eine Zahl zurück. Weitere Informationen zu Vorhersageabfragen, die eine einzelne Zeile zurückgeben, finden Sie unter [Data Mining-Abfragetools](../../analysis-services/data-mining/data-mining-query-tools.md).  
  
 Die Abfrageergebnisse werden in Tabellen gespeichert. Falls eine Tabelle mit dem vom Data Mining-Abfragetask angegebenen Namen bereits vorhanden ist, kann der Task eine neue Tabelle erstellen, wobei der gleiche Name verwendet und eine Zahl angefügt wird, oder der Tabelleninhalt kann überschrieben werden.  
  
 Wenn die Ergebnisse eine Schachtelung einschließen, wird das Ergebnis vor dem Speichern vereinfacht. Durch das Vereinfachen eines Ergebnisses wird das geschachtelte Resultset in eine Tabelle geändert. Beispielsweise werden durch das Vereinfachen eines geschachtelten Ergebnisses mit einer **Customer** -Spalte und einer geschachtelten **Product** -Spalte der **Customer** -Spalte Zeilen hinzugefügt, um eine Tabelle zu erstellen, die Produktdaten für jeden Kunden enthält. Beispielsweise wird ein Kunde mit drei verschiedenen Produkten zu einer Tabelle mit drei Zeilen, wobei der Kunde in jeder Zeile wiederholt und in jeder Zeile ein anderes Produkt hinzugefügt wird. Falls das FLATTENED-Schlüsselwort ausgelassen wird, enthält die Tabelle nur die **Customer** -Spalte und nur eine einzige Zeile pro Kunde. Weitere Informationen finden Sie unter [SELECT &#40;DMX&#41;](../../dmx/select-dmx.md).  
  
## <a name="configuration-of-the-data-mining-query-task"></a>Konfiguration des Data Mining-Abfragetasks  
 Der Data Mining-Abfragetask erfordert zwei Verbindungen. Die erste Verbindung ist ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verbindungs-Manager, der eine Verbindung mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder mit einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt herstellt, die bzw. das die Miningstruktur und das Miningmodell enthält. Die zweite Verbindung ist ein OLE DB-Verbindungs-Manager, der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herstellt, die die Tabelle enthält, in die der Task schreibt. Weitere Informationen finden Sie unter [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md) und [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
> [!NOTE]  
>  Der Transformations-Editor für Data Mining-Abfragen weist keine Seite mit Ausdrücken auf. Verwenden Sie stattdessen das Fenster **Eigenschaften** für den Zugriff auf die Tools zum Erstellen und Verwalten von Eigenschaftsausdrücken für Eigenschaften des Data Mining-Abfragetasks.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>Programmgesteuerte Konfiguration des Data Mining-Abfragetasks  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften zu erhalten:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
## <a name="data-mining-query-task-editor-mining-model-tab"></a>Editor für Data Mining-Abfragetasks (Registerkarte Miningmodell)
  Mithilfe der Registerkarte **Miningmodell** des Dialogfelds **Editor für Data Mining-Abfragetasks** können Sie die zu verwendende Miningstruktur sowie das Miningmodell angeben.  
  
 Weitere Informationen zur Implementierung von Data Mining in Paketen finden Sie unter [Data Mining-Abfragetask](../../integration-services/control-flow/data-mining-query-task.md) und [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md).  
  
### <a name="general-options"></a>Allgemeine Optionen  
 **Name**  
 Geben Sie einen eindeutigen Namen für die Data Mining-Abfragetasks ein. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung für den Data Mining-Abfragetask ein.  
  
### <a name="mining-model-tab-options"></a>Optionen der Registerkarte Miningmodell  
 **Verbindung**  
 Wählen Sie einen vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verbindungs-Manager aus der Liste aus, oder klicken Sie auf **Neu** , um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:**  [Analysis Services-Verbindungs-Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **Neu**  
 Erstellt einen neuen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verbindungs-Manager.  
  
 **Verwandte Themen:** [Referenz zur Benutzeroberfläche des Dialogfelds Analysis Services-Verbindungs-Manager hinzufügen](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Miningstruktur**  
 Wählt eine Miningstruktur in der Liste aus.  
  
 **Miningmodelle**  
 Wählt ein auf der ausgewählten Miningstruktur aufgebautes Miningmodell aus.  

## <a name="data-mining-query-task-editor-query-tab"></a>Editor für Data Mining-Abfragetasks (Registerkarte Abfrage)
  Mithilfe der Registerkarte **Abfrage** des Dialogfelds **Data Mining-Abfragetask** können Sie Vorhersageabfragen auf der Grundlage eines Miningmodells erstellen. In diesem Dialogfeld können Sie auch Parameter und Resultsets an Variablen anbinden.  
  
 Weitere Informationen zur Implementierung von Data Mining in Paketen finden Sie unter [Data Mining-Abfragetask](../../integration-services/control-flow/data-mining-query-task.md) und [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md).  
  
### <a name="general-options"></a>Allgemeine Optionen  
 **Name**  
 Geben Sie einen eindeutigen Namen für die Data Mining-Abfragetasks ein. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung für den Data Mining-Abfragetask ein.  
  
### <a name="build-query-tab-options"></a>Optionen der Registerkarte Abfrage erstellen  
 **Data Mining-Abfrage**  
 Geben Sie eine Data Mining-Abfrage ein.  
  
 **Verwandte Themen:** [Data Mining-Erweiterungen &#40;DMX&#41; – Referenz](../../dmx/data-mining-extensions-dmx-reference.md)  
  
 **Neue Abfrage erstellen**  
 Erstellt die Data Mining-Abfrage mithilfe eines grafischen Tools.  
  
 **Verwandte Themen:** [Data Mining Query](../../integration-services/control-flow/data-mining-query.md)  
  
### <a name="parameter-mapping-tab-options"></a>Optionen der Registerkarte Parameterzuordnung  
 **Parametername**  
 Sie können optional den Parameternamen aktualisieren. Ordnen Sie den Parameter einer Variable zu, indem Sie in der Liste **Variablenname** eine Variable auswählen.  
  
 **Variablenname**  
 Wählen Sie in der Liste eine Variable aus, um sie dem Parameter zuzuordnen.  
  
 **Hinzufügen**  
 Fügt der Liste einen Parameter hinzu.  
  
 **Entfernen**  
 Wählen Sie einen Parameter aus, und klicken Sie anschließend auf **Entfernen**.  
  
### <a name="result-set-tab-options"></a>Optionen der Registerkarte Resultset  
 **Ergebnisname**  
 Sie können optional den Resultsetnamen aktualisieren. Ordnen Sie das Resultset einer Variable zu, indem Sie in der Liste **Variablenname** eine Variable auswählen.  
  
 Nachdem Sie das Ergebnis durch Klicken auf **Hinzufügen**hinzugefügt haben, geben Sie einen eindeutigen Namen für das Ergebnis an.  
  
 **Variablenname**  
 Wählen Sie in der Liste eine Variable aus, um sie dem Resultset zuzuordnen.  
  
 **Ergebnistyp**  
 Gibt an, ob eine einzelne Zeile oder ein vollständiges Resultset zurückgegeben werden soll.  
  
 **Hinzufügen**  
 Fügt ein Resultset zur Liste hinzu.  
  
 **Entfernen**  
 Wählen Sie ein Ergebnis aus, und klicken Sie anschließen auf **Entfernen**.  
## <a name="data-mining-query-task-editor-output-tab"></a>Editor für Data Mining-Abfragetasks (Registerkarte Ausgabe)
  Mithilfe der Registerkarte **Ausgabe** des Dialogfelds **Editor für Data Mining-Abfragetasks** können Sie das Ziel der Vorhersageabfrage angeben.  
  
 Weitere Informationen zur Implementierung von Data Mining in Paketen finden Sie unter [Data Mining-Abfragetask](../../integration-services/control-flow/data-mining-query-task.md) und [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md).  
  
### <a name="general-options"></a>Allgemeine Optionen  
 **Name**  
 Geben Sie einen eindeutigen Namen für die Data Mining-Abfragetasks ein. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung für den Data Mining-Abfragetask ein.  
  
### <a name="output-tab-options"></a>Optionen der Registerkarte Ausgabe  
 **Verbindung**  
 Wählen Sie einen Verbindungs-Manager aus der Liste aus, oder klicken Sie auf **Neu** , um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Neu**  
 Erstellt einen neuen Verbindungs-Manager. Sie können nur die ADO.NET- und OLE DB-Verbindungsmanagertypen verwenden.  
  
 **Ausgabetabelle**  
 Geben Sie die Tabelle an, in die die Vorhersageabfrage ihre Ergebnisse schreiben soll.  
  
 **Ausgabetabelle löschen und erneut erstellen**  
 Gibt an, ob die Vorhersageabfrage den Inhalt in der Zieltabelle überschreiben soll, indem die Tabelle gelöscht und anschließend erneut erstellt wird.  
  

