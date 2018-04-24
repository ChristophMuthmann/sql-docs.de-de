---
title: OLE-Automatisierungsresultsets | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-ole
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data types [SQL Server], OLE Automation
- two-dimensional arrays
- one-dimensional arrays
- result sets [SQL Server], OLE Automation
- OLE Automation [SQL Server], result sets
- arrays [SQL Server]
ms.assetid: b2f99e33-2303-427c-94b9-9d55f8e2a6ab
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8a4890d501c2fc800000ef093ae14aa47d3eacfb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="ole-automation-result-sets"></a>OLE-Automatisierungsresultsets
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Wenn eine OLE-Automatisierungseigenschaft oder -methode Daten in einem ein- oder zweidimensionalen Array zurückgibt, wird das Array als Resultset an den Client zurückgegeben:  
  
-   Ein eindimensionales Array wird dem Client als einzeiliges Resultset zurückgegeben, das so viele Spalten wie Elemente im Array enthält. Ein Array(10) wird z. B. als einzelne Zeile mit 10 Spalten zurückgegeben.  
  
-   Ein zweidimensionales Array wird dem Client als Resultset zurückgegeben, dessen Anzahl an Spalten der Anzahl der Elemente in der ersten Dimension des Arrays entspricht und dessen Anzahl an Zeilen der Anzahl der Elemente in der zweiten Dimension des Arrays entspricht. Ein Array(2,3) wird z. B. als 2 Spalten in 3 Zeilen zurückgegeben.  
  
 Wenn der Rückgabewert für eine Eigenschaft oder eine Methode ein Array ist, geben sp_OAGetProperty oder sp_OAMethod ein Resultset an den Client zurück. (Ausgabeparameter für Methoden können nicht einem Array entsprechen.) Diese Prozeduren durchsuchen alle Datenwerte des Arrays, um die geeigneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen und -Datenlängen für jede Spalte des Resultsets zu ermitteln. Für eine bestimmte Spalte verwenden diese Prozeduren den Datentyp und die -länge, die erforderlich sind, um alle Datenwerte in dieser Spalte darzustellen.  
  
 Wenn alle Datenwerte einer Spalte denselben Datentyp aufweisen, wird dieser Datentyp für die gesamte Spalte verwendet. Wenn Datenwerte in einer Spalte aus unterschiedlichen Datentypen bestehen, wird der Datentyp für die gesamte Spalte entsprechend der folgenden Tabelle ausgewählt. Zum Verwenden der folgenden Tabelle wählen Sie einen Datentyp auf der Achse der linken Zeile und einen zweiten Datentyp auf der Achse der obersten Spalte aus. Der Schnittpunkt von Zeile und Spalte beschreibt den Datentyp der Resultset-Spalte.  
  
||||||||  
|-|-|-|-|-|-|-|  
||**int**|**float**|**money**|**datetime**|**varchar**|**nvarchar**|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Gespeicherte OLE-Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
 [OLE-Automatisierungsprozeduren (Serverkonfigurationsoption)](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
  
