---
title: 'MSSQLSERVER: Datenbankmodul-Fehler | Microsoft Dokumentation'
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71201690ad1a47bdd400ad878a8faab9a158dd65
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver---database-engine-error"></a>MSSQLSERVER: Datenbankmodul-Fehler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|823|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|B_HARDERR|  
|Meldungstext|Das Betriebssystem hat während eines %S_MSG bei Offset %#016I64x in der Datei '%4!s!' den Fehler '%ls' an SQL Server zurückgegeben. Weitere Informationen finden Sie möglicherweise in zusätzlichen Meldungen im SQL Server-Fehlerprotokoll und im Systemereignisprotokoll. Dieser Fehler kann die Datenbankintegrität beeinträchtigen und muss behoben werden. Führen Sie eine vollständige Datenbankkonsistenzprüfung (DBCC CHECKDB) aus. Dieser Fehler kann viele Ursachen haben. Weitere Informationen finden Sie in der SQL Server-Onlinedokumentation.|  
  
## <a name="explanation"></a>Erklärung  
Fehler bei einer Lese- oder Schreibanforderung in Windows. Der von Windows zurückgegebene Fehlercode und der entsprechende Text werden in die Meldung eingefügt. Im Fall des Lesevorgangs hat [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereits viermal versucht, die Leseanforderung zu wiederholen. Dieser Fehler beruht oft auf einem Hardwarefehler, wird jedoch möglicherweise durch den Gerätetreiber verursacht. Weitere Informationen zu Fehlermeldung 823 finden Sie unter [http://support.microsoft.com/kb/828339](http://support.microsoft.com/kb/828339). Weitere Informationen zu E/A-Fehlern finden Sie unter [Microsoft SQL Server I/O Basics, Chapter 2 (E/A-Grundlagen von Microsoft SQL Server, Kapitel 2)](http://go.microsoft.com/fwlink/?LinkId=69370).  
  
## <a name="user-action"></a>Benutzeraktion  
Überprüfen Sie, ob zusätzliche Informationen im Systemereignisprotokoll vorhanden sind. Wenden Sie sich an den Hardwarehersteller oder an Microsoft Support Services, um Unterstützung bei der Bestimmung der Ursache zu erhalten und diese Ursache zu beheben. Nachdem der Hardwarefehler behoben wurde, stellen Sie alle Datenbanken wieder her, und führen Sie DBCC CHECKDB aus.  
  
