---
title: Analysis Services-Verarbeitungstask | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.asprocessingtask.f1
- sql13.dts.designer.asprocessingtask.general.f1
- sql13.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 1a5107d988014807892ec405dadf61656c7606a5
ms.contentlocale: de-de
ms.lasthandoff: 08/11/2017

---
# <a name="analysis-services-processing-task"></a>Analysis Services-Verarbeitungstask
  Der Verarbeitungstask [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verarbeitet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte, beispielsweise tabellarische Modelle, Cubes, Dimensionen und Miningmodelle.  
  
 Beim Verarbeiten von tabellarischen Modellen müssen Sie Folgendes berücksichtigen:  
  
-   Sie können keine Auswirkungsanalyse auf tabellarische Modelle ausführen.  
  
-   Einige Verarbeitungsoptionen für den tabellarischen Modus werden nicht verfügbar gemacht, z. B. "Defragmentierung verarbeiten" und "Neuberechnung verarbeiten". Sie können diese Funktionen mithilfe des Execute DDL-Tasks ausführen.  
  
-   Die Optionen "Index verarbeiten" und "Update verarbeiten" eignen sich nicht für tabellarische Modelle und sollten daher nicht verwendet werden.  
  
-   Batcheinstellungen werden für tabellarische Modelle ignoriert.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] schließt eine Reihe von Tasks ein, die Business Intelligence-Vorgänge ausführen, wie das Ausführen von DDL-Anweisungen (Data Definition Language, Datendefinitionssprache) und Data Mining-Vorhersageabfragen. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu verwandten Business Intelligence-Tasks zu erhalten:  
  
-   [DDL ausführen (Analysis Services-Task)](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Data Mining-Abfragetask](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="object-processing"></a>Objektverarbeitung  
 Mehrere Objekte können gleichzeitig verarbeitet werden. Wenn mehrere Objekte verarbeitet werden, definieren Sie Einstellungen, die für die Verarbeitung aller Objekte im Batch gelten.  
  
 Objekte in einem Batch können nacheinander oder parallel verarbeitet werden. Falls der Batch keine Objekte enthält, für die die Verarbeitungssequenz eine Rolle spielt, kann die parallele Verarbeitung den Vorgang beschleunigen. Wenn Objekte im Batch parallel verarbeitet werden, können Sie den Task so konfigurieren, dass er ermittelt, wie viele Objekte parallel verarbeitet werden, oder Sie können manuell angeben, wie viele Objekte gleichzeitig verarbeitet werden sollen. Falls Objekte nacheinander verarbeitet werden, können Sie ein Transaktionsattribut für den Batch festlegen, indem Sie alle Objekte in einer Transaktion auflisten oder indem Sie für jedes Objekt im Batch eine separate Transaktion verwenden.  
  
 Wenn Sie analytische Objekte verarbeiten, können Sie auch die abhängigen Objekte verarbeiten. Der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verarbeitungstask enthält eine Option, um neben den ausgewählten Objekten alle abhängigen Objekte zu verarbeiten.  
  
 Normalerweise werden Dimensionstabellen vor den Faktentabellen verarbeitet. Möglicherweise treten Fehler auf, wenn Sie versuchen, Faktentabellen vor den Dimensionstabellen zu verarbeiten.  
  
 Mit diesem Task können Sie auch die Fehlerbehandlung in Dimensionsschlüsseln konfigurieren. Beispielsweise kann der Task Fehler ignorieren oder nach einer bestimmten Anzahl von Fehlern beendet werden. Der Task kann die Standardfehlerkonfiguration verwenden. Sie können aber auch eine benutzerdefinierte Fehlerkonfiguration erstellen. Bei einer benutzerdefinierten Fehlerkonfiguration geben Sie an, wie der Task Fehler und die Fehlerbedingungen behandelt. Beispielsweise können Sie angeben, dass der Task nach dem vierten Fehler beendet werden soll oder wie der Task **NULL** -Schlüsselwerte behandeln soll. Die benutzerdefinierte Fehlerkonfiguration kann auch den Pfad eines Fehlerprotokolls einschließen.  
  
> [!NOTE]  
>  Mit dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verarbeitungstask können nur analytische Objekte verarbeitet werden, die mit den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tools erstellt wurden.  
  
 Dieser Task wird häufig zusammen mit einem Masseneinfügungstask verwendet, der Daten in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle lädt, oder mit einem Datenflusstask, der einen Datenfluss zum Laden von Daten in eine Tabelle implementiert. Beispielsweise könnte der Datenflusstask einen Datenfluss aufweisen, der Daten aus einer OLTP-Datenbank (Online Transactional Database) extrahiert und in eine Faktentabelle in einem Data Warehouse lädt. Anschließend wird der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verarbeitungstask aufgerufen, um den im Data Warehouse erstellten Cube zu verarbeiten.  
  
 Der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verarbeitungstask stellt mithilfe eines Verbindungs-Managers von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Verbindung mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her. Weitere Informationen finden Sie unter [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
## <a name="error-handling"></a>Fehlerbehandlung  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Konfiguration des Analysis Services-Verarbeitungstasks  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Programmgesteuerte Konfiguration des Analysis Services-Verarbeitungstasks  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
## <a name="analysis-services-processing-task-editor-general-page"></a>Editor für den Analysis Services-Verarbeitungstask (Seite Allgemein)
  Mithilfe der Seite **Allgemein** des Dialogfelds **Editor für den Analysis Services-Verarbeitungstask** können Sie den Analysis Services-Verarbeitungstask benennen und beschreiben.  
  
### <a name="options"></a>enthalten  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Analysis Services-Verarbeitungstask an. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung des Analysis Services-Verarbeitungstasks ein.  
  
## <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Editor für den Analysis Services-Verarbeitungstask (Seite Analysis Services)
  Auf der Seite **Analysis Services** des Dialogfelds **Editor für den Analysis Services-Verarbeitungstask** können Sie den Analysis Services-Verbindungs-Manager angeben, die zu verarbeitenden Analyseobjekte auswählen und die Verarbeitungs- und Fehlerbehandlungsoptionen festlegen.  
  
 Beim Verarbeiten von tabellarischen Modellen müssen Sie Folgendes berücksichtigen:  
  
1.  Sie können keine Auswirkungsanalyse auf tabellarische Modelle ausführen.  
  
2.  Einige Verarbeitungsoptionen für den tabellarischen Modus werden nicht verfügbar gemacht, z. B. "Defragmentierung verarbeiten" und "Neuberechnung verarbeiten". Sie können diese Funktionen mithilfe des Execute DDL-Tasks ausführen.  
  
3.  Einige bereitgestellte Verarbeitungsoptionen, beispielsweise Verarbeitungsindizes, eignen sich nicht für tabellarische Modelle und sollten daher nicht verwendet werden.  
  
4.  Batcheinstellungen werden für tabellarische Modelle ignoriert.  
  
### <a name="options"></a>enthalten  
 **Analysis Services-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Analysis Services-Verbindungs-Manager aus der Liste aus, oder klicken Sie auf **Neu** , um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Neu**  
 Erstellen Sie einen neuen Analysis Services-Verbindungs-Manager.  
  
 **Verwandte Themen:** [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md), [Referenz zur Benutzeroberfläche des Dialogfelds „Analysis Services-Verbindungs-Manager hinzufügen“](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Objektliste**  
 |Eigenschaft|Description|  
|--------------|-----------------|  
|**Objektname**|Listet die angegebenen Objektnamen auf.|  
|**Typ**|Listet die Typen der angegebenen Objekte auf.|  
|**Verarbeitungsoptionen**|Wählen Sie eine Verarbeitungsoption in der Liste aus.<br /><br /> **Verwandte Themen:** [Verarbeiten eines mehrdimensionalen Modells &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)|  
|**Einstellungen**|Listet die Verarbeitungseinstellungen für die angegebenen Objekte auf.|  
  
 **Hinzufügen**  
 Fügen Sie der Liste ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekt hinzu.  
  
 **Entfernen**  
 Wählen Sie ein Objekt aus, und klicken Sie auf **Löschen**.  
  
 **Auswirkungsanalyse**  
 Führen Sie für das ausgewählte Objekt eine Auswirkungsanalyse aus.  
  
 **Verwandte Themen:** [Dialogfeld „Auswirkungsanalyse“ &#40;Analysis Services – Mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/208268eb-4e14-44db-9c64-6f74b776adb6)  
  
 **Zusammenfassung der Batcheinstellungen**  
 |Eigenschaft|Description|  
|--------------|-----------------|  
|**Verarbeitungsreihenfolge**|Gibt an, ob die Objekte nacheinander oder als Batch verarbeitet werden; bei Verwendung der parallelen Verarbeitung wird die Anzahl der gleichzeitig verarbeiteten Objekte angegeben.|  
|**Transaktionsmodus**|Gibt den Transaktionsmodus für die sequenzielle Verarbeitung an.|  
|**Dimensionsfehler**|Gibt das Verhalten des Tasks bei Auftreten eines Fehlers an.|  
|**Fehlerprotokollpfad für Dimensionsschlüssel**|Gibt den Pfad der Datei an, in der Fehler protokolliert werden.|  
|**Betroffene Objekte verarbeiten**|Kennzeichnet, ob abhängige oder betroffene Objekte auch verarbeitet werden.|  
  
 **Einstellungen ändern**  
 Ändern Sie die Verarbeitungsoptionen und die Fehlerbehandlung bei Dimensionsschlüsseln.  
  
 **Verwandte Themen:** [Dialogfeld „Einstellungen ändern“ &#40;Analysis Services – Mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/0041e042-d7ce-48f9-a690-a6dc65471ff3)  
  

