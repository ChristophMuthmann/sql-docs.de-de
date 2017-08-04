---
title: "Überwachungstransformation | Microsoft Docs"
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
- sql13.dts.designer.audittrans.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c495bd9c116e10877f79f165f0f582938b0347ad
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="audit-transformation"></a>Überwachungstransformation
  Mithilfe der Überwachungstransformation werden in den Datenfluss eines Pakets Daten zur Umgebung, in der das Paket ausgeführt wird, eingeschlossen. Dem Datenfluss kann z. B. der Name des Pakets, Computers und Operators hinzugefügt werden. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] schließt Systemvariablen ein, die diese Informationen bereitstellen.  
  
## <a name="system-variables"></a>Systemvariablen  
 In der folgenden Tabelle sind die Systemvariablen beschrieben, die von der Überwachungstransformation verwendet werden können.  
  
|Systemvariable|Index|Description|  
|---------------------|-----------|-----------------|  
|**ExecutionInstanceGUID**|0|Der GUID, der die Ausführungsinstanz des Pakets identifiziert.|  
|**PackageID**|1|Der eindeutige Bezeichner des Pakets.|  
|**PackageName**|2|Der Paketname.|  
|**VersionID**|3|Die Paketversion.|  
|**ExecutionStartTime**|4|Der Zeitpunkt, zu dem das Paket gestartet wurde.|  
|**MachineName**|5|Der Computername.|  
|**UserName**|6|Der Anmeldename der Person, die das Paket gestartet hat.|  
|**TaskName**|7|Der Name des Datenflusstasks, dem die Überwachungstransformation zugeordnet ist.|  
|**TaskId**|8|Der eindeutige Bezeichner des Datenflusstasks.|  
  
## <a name="configuration-of-the-audit-transformation"></a>Konfiguration der Überwachungstransformation  
 Zum Konfigurieren der Überwachungstransformation stellen Sie den Namen einer neuen Ausgabespalte bereit, die der Transformationsausgabe hinzugefügt werden soll, und ordnen dann der Ausgabespalte die Systemvariable zu. Eine einzelne Systemvariable kann mehreren Spalten zugeordnet werden.  
  
 Diese Transformation weist je eine Eingabe und eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld **Transformations-Editor für Überwachung** festlegen können, finden Sie unter [Audit Transformation Editor](../../../integration-services/data-flow/transformations/audit-transformation-editor.md).  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Informationen zum Festlegen von Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
