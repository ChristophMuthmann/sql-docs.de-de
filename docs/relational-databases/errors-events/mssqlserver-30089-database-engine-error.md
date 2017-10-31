---
title: MSSQLSERVER_30089 | Microsoft-Dokumentation
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
- 9992 (Database Engine error)
ms.assetid: 188e5bde-6865-4740-a2b2-582be8f55c77
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c42bbbb05ba2cb78628433815effb5ef7ce48132
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver30089"></a>MSSQLSERVER_30089
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|30089|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|IFTS_FDHOST_TERMINATEDABNORMAL|  
|Meldungstext|Der Hostprozess des Volltextfilterdaemons (FDHost) wurde fehlerbedingt beendet. Dieser Fehler kann auftreten, wenn eine falsch konfigurierte oder nicht ordnungsgemäß funktionierende linguistische Komponente, wie z. B. eine Wörtertrennung, eine Wortstammerkennung oder ein Filter, bei der Volltextindizierung oder Abfrageverarbeitung einen nicht behebbaren Fehler verursacht hat. Der Prozess wird automatisch neu gestartet.|  
  
## <a name="explanation"></a>Erklärung  
Der Host des Volltextfilterdaemons hat ein Problem erkannt, wodurch der Prozess fehlerbedingt beendet wurde. Die Ursache des Problems kann ein falsch formatiertes Dokument, ein Fehler im Filter oder in der Wörtertrennung oder ein Fehler im Filterdaemon sein.  
  
## <a name="user-action"></a>Benutzeraktion  
Normalerweise wird der Daemon wiederhergestellt. Wenn der Fehler weiterhin auftritt, ist eine Problembehandlung erforderlich. Versuchen Sie Folgendes, um das Problem zu isolieren:  
  
1.  Wenn kürzlich eine neue linguistische Komponente installiert wurde, entfernen Sie diese vom System.  
  
2.  Suchen Sie im Durchforstungsprotokoll nach neuen Dokumenten, bei deren Volltextindizierung ein Fehler aufgetreten ist, und entfernen Sie diese Dokumente.  
  
## <a name="see-also"></a>Siehe auch  
[sp_help_fulltext_system_components &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
[Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](~/relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
[Konfigurieren und Verwalten von Filtern für die Suche](~/relational-databases/search/configure-and-manage-filters-for-search.md)  
  

