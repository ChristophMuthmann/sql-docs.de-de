---
title: MSSQLSERVER_33027 | Microsoft-Dokumentation
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
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a2d3665c85c42433f8f8c7902946937301719b5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|33027|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SEC_CRYPTOPROV_CANTLOADDLL|  
|Meldungstext|Fehler beim Laden des Kryptografieanbieters ‚%.*ls’ aufgrund einer ungültigen Authenticode-Signatur oder eines ungültigen Dateipfades. Überprüfen Sie vorhergehende Meldungen auf weitere Fehler.|  
  
## <a name="explanation"></a>Erklärung  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] konnte den in der Fehlermeldung aufgelisteten Kryptografieanbieter nicht verwenden, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die DLL nicht laden konnte. Entweder ist der Name ungültig, oder die Authenticode-Signatur ist ungültig.  
  
## <a name="user-action"></a>Benutzeraktion  
Überprüfen Sie, ob die Datei vorhanden ist und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Berechtigung hat, auf diesen Speicherort zuzugreifen. Überprüfen Sie das Fehlerprotokoll auf zusätzliche verwandte Fehlermeldungen. Anderenfalls wenden Sie sich an den Kryptografieanbieter, um weitere Informationen zu erhalten.  
  
