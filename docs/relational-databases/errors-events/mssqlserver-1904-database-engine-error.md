---
title: MSSQLSERVER_1904 | Microsoft-Dokumentation
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
- 1904 (Database Engine error)
ms.assetid: 2a35d57d-74e2-45a2-8f67-3f2e51d69712
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 872d941d58892089cadbe0e2254b4c63854ad3b0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1904"></a>MSSQLSERVER_1904
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1904|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|KEYCOUNT|  
|Meldungstext|Das %S_MSG-Objekt '%.*ls' in der '%.\*ls'-Tabelle weist %d Spaltennamen in der %S_MSG-Schlüsselliste auf. Die maximale Anzahl für Spaltenlisten von Index- oder Statistikschlüsseln beträgt % d.|  
  
## <a name="explanation"></a>Erklärung  
Die Schlüsselspaltenliste für den angegebenen Index bzw. die angegebenen Statistiken überschreitet die maximal zulässige Anzahl von Spalten.  
  
## <a name="user-action"></a>Benutzeraktion  
Ändern Sie die Schlüsselspaltenliste, sodass nur die maximal zulässige Anzahl von Spalten eingeschlossen wird.  
  
Ziehen Sie bei nicht gruppierten Indizes die Verwendung der INCLUDE-Klausel in der CREATE INDEX-Anweisung in Betracht, um dem Index Spalten als Nichtschlüsselspalten hinzuzufügen. Auf diese Weise können Sie vermeiden, dass die aktuelle Größenbeschränkung des Indexes von maximal 16 Schlüsselspalten überschritten wird. Weitere Informationen finden Sie unter [Create Indexes with Included Columns](~/relational-databases/indexes/create-indexes-with-included-columns.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[CREATE STATISTICS &#40;Transact-SQL&#41;](~/t-sql/statements/create-statistics-transact-sql.md)  
  
