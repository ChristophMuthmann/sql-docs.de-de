---
title: "Zurückgeben von Ergebnissen aus dem Skripttask | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs: VB
helpviewer_keywords:
- Script task [Integration Services], status information
- ExecutionValue property
- status information [Integration Services]
- TaskResult property
- SSIS Script task, status information
ms.assetid: ac06805b-c2db-44bd-af5c-5a0debe36dd7
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: caf501cc710329cec6f944a6e300a618395b4e40
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="returning-results-from-the-script-task"></a>Zurückgeben von Ergebnissen aus dem Skripttask
  Der Skripttask verwendet die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>- und die optionale <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>-Eigenschaft, um Statusinformationen an die [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]-Laufzeit zurückzugeben, die zur Bestimmung des Pfads des Workflows nach Abschluss des Skripttasks verwendet werden können.  
  
## <a name="taskresult"></a>TaskResult  
 Die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>-Eigenschaft berichtet, ob der Task erfolgreich war oder zu einem Fehler geführt hat. Beispiel:  
  
 `Dts.TaskResult = ScriptResults.Success`  
  
## <a name="executionvalue"></a>ExecutionValue  
 Die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>-Eigenschaft gibt optional ein benutzerdefiniertes Objekt zurück, das das erfolgreiche Ausführen oder Fehlschlagen des Skripttasks misst oder weitere Informationen darüber liefert. Der FTP-Task verwendet beispielsweise die <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>-Eigenschaft, um die Anzahl von übertragenen Dateien zurückzugeben. Der Task „SQL ausführen“ gibt die Anzahl von Zeilen zurück, auf die sich der Task ausgewirkt hat. Der <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> kann auch verwendet werden, um den Pfad des Workflows zu bestimmen. Beispiel:  
  
 `Dim rowsAffected as Integer`  
  
 `...`  
  
 `rowsAffected = 1000`  
  
 `Dts.ExecutionValue = rowsAffected`  
