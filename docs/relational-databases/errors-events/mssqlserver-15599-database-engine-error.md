---
title: MSSQLSERVER_15599 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aa0d5c203907702e20ca9c780baad266b3def320
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver15599"></a>MSSQLSERVER_15599
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|15599|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|Meldungstext|Überwachung und Berechtigungen können nicht für lokale temporäre Objekte festgelegt werden.|  
  
## <a name="explanation"></a>Erklärung  
Überwachung und Berechtigungen haben keine Auswirkungen, wenn sie für lokale oder globale temp-Objekte festgelegt werden. Die Anweisungen haben keinem Fehler zur Folge (die Vorgänge geben Erfolg zurück), sie haben lediglich keine Auswirkungen.  
  
Dieses Verhalten hat sich nicht geändert. Seit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] wird der Benutzer jedoch in einer Informationsmeldung hierüber informiert.  
  
## <a name="user-action"></a>Benutzeraktion  
Es ist keine Aktion notwendig. Sie sollten jedoch das Entfernen von Anweisungen in Erwägung ziehen, durch die Überwachung oder Berechtigungen für lokale oder globale temp-Objekte festgelegt werden.  
  

