---
title: SQL Serverintegration Services-Eigenschaften (Registerkarte Dienst) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 37f0acd9-c96f-48fd-9b53-2ca0097af242
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fdd7b2f7ac6e01b52843e597f50bcbd6939053d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-integration-services-properties-service-tab"></a>Eigenschaften von SQL Server Integration Services (Registerkarte Dienst)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Verwenden der **Service**Registerkarte auf die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] **Eigenschaften** (Dialogfeld), um die folgenden Optionen anzuzeigen oder anzugeben.  
  
## <a name="options"></a>Tastatur  
 **Binärpfad**  
 Zeigt den Speicherort der Programmdateien an, die von diesem Dienst verwendet werden.  
  
 **Fehlersteuerung**  
 1 steht für `SERVICE_ERROR_NORMAL`. Wenn der Dienst nicht zusammen mit dem Computer gestartet werden kann, wird der Fehler vom Startprogramm protokolliert und eine Popupmeldung angezeigt, der Startvorgang aber fortgesetzt. Dieser Wert kann nicht geändert werden.  
  
 **Exitcode**  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Fehlercode, der alle Probleme definiert, die beim Starten oder Beenden des Dienstes aufgetreten sind. Diese Eigenschaft wird auf **ERROR_SERVICE_SPECIFIC_ERROR** (1066) festgelegt, wenn der Fehler in Bezug auf den Dienst eindeutig ist, der durch diese Klasse repräsentiert wird, und Informationen zu dem Fehler stehen in der **ServiceSpecificExitCode** -Eigenschaft zur Verfügung. Vom Dienst wird dieser Wert bei der Ausführung und erneut bei normaler Beendigung auf NO_ERROR (0) festgelegt.  
  
 **HostName**  
 Zeigt den Namen des Computers oder Clusters an, auf dem der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Dienst ausgeführt wird.  
  
 **Name**  
 Zeigt den Anzeigenamen des Dienstes an.  
  
 **Prozess-ID**  
 Zeigt die Prozess-ID von Windows an.  
  
 **SQL-Diensttyp**  
 Zeigt den für aufrufende Prozesse bereitgestellten Diensttyp an. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden mehrere Dienste installiert.  
  
 **Startmodus**  
 Richten Sie den Dienst mit den folgenden Auswahlmöglichkeiten ein:  
  
-   Manuell: Dieser Dienst wird nicht automatisch zusammen mit dem Computer gestartet. Zum Starten des Dienstes verwenden Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager oder ein anderes Tool.  
  
-   Automatisch: Dieser Dienst wird zusammen mit dem Computer gestartet.  
  
-   Deaktiviert: Dieser Dienst kann nicht gestartet werden.  
  
 **Status**  
 Zeigt an, ob dieser Dienst ausgeführt wird, angehalten oder deaktiviert ist. "**…**" gibt einen ausstehenden Statuswechsel an.  
  
  
