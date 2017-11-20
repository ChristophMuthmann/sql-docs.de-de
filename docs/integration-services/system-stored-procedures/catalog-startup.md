---
title: Catalog.Startup | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3a8c89be0541be1861f45240b891d349019a8935
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogstartup"></a>catalog.startup
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Führt eine Wartung des Status von Vorgängen für den SSISDB-Katalog aus.  
  
 Durch die gespeicherte Prozedur wird der Status aller Pakete korrigiert, die während des Ausfalls (falls zutreffend) der [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Serverinstanz ausgeführt wurden.  
  
 Sie haben die Möglichkeit, aktivieren die gespeicherte Prozedur automatisch jedes Mal ausführen der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Serverinstanz neu gestartet wird, indem Sie auswählen der **aktivieren die automatische Ausführung von Integration Services gespeicherter Prozeduren beim Starten von SQL Server** -Option in der **Katalog erstellen** (Dialogfeld).  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.startup  
```  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung und MODIFY-Berechtigung für die Instanz der Ausführung, READ-Berechtigung und EXECUTE-Berechtigung für das Projekt und ggf. READ-Berechtigungen für die Umgebung, auf die verwiesen wird  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
  

