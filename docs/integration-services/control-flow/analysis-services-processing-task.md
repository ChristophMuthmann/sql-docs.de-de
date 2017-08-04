---
title: Analysis Services-Verarbeitungstask | Microsoft Docs
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
- sql13.dts.designer.asprocessingtask.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2f607edcad955a4d0a22cc246a13d9d97a06fe24
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

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
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Analysis Services-Verarbeitungstask &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/analysis-services-processing-task-editor-general-page.md)  
  
-   [Editor für den Analysis Services-Verarbeitungstask &#40;Seite „Analysis Services“&#41;](../../integration-services/control-flow/analysis-services-processing-task-editor-analysis-services-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Programmgesteuerte Konfiguration des Analysis Services-Verarbeitungstasks  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften zu erhalten:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
  
