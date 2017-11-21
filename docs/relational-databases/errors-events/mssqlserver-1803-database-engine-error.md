---
title: MSSQLSERVER_1803 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f14c8fb9f7ec553478ad378764265a13b783a0c5
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1803"></a>MSSQLSERVER_1803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1803|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|NO_SPACE|  
|Meldungstext|Fehler bei CREATE DATABASE. Die primäre Datei muss mindestens %d MB haben, um eine Kopie der model-Datenbank aufnehmen zu können.|  
  
## <a name="explanation"></a>Erklärung  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt eine Datenbank aus einer Kopie der Modelldatenbank. Die Kopie wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] umbenannt, und die neue Datenbank wird auf die angeforderte Größe vergrößert. In diesem Fall versuchte der Benutzer, eine Datenbank zu erstellen, die kleiner als die Modelldatenbank war. Der Vorgang ist fehlgeschlagen, da die Kopie der Modelldatenbank nicht in die primäre Datendatei gepasst hat, da die Datei kleiner als die Modelldatenbank war.  
  
## <a name="user-action"></a>Benutzeraktion  
Erstellen Sie die Datenbank, und geben Sie eine größere Datenbankdateigröße an. Verkleinern Sie dann ggf. die Datenbank mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder der DBCC SHRINKDATABASE-Anweisung.  
  

