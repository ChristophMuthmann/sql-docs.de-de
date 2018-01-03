---
title: QuickInfo (IntelliSense) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Quick Info option [IntelliSense]
- declarations [IntelliSense]
- IntelliSense [SQL Server], Quick Info
- identifier declarations [IntelliSense]
ms.assetid: 3c8b59f4-1922-4bde-844f-5f2306514d96
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: adcf4b2e0e108a886a3ea24e9b5a225b691dcbcb
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="quick-info-intellisense"></a>QuickInfo (IntelliSense)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Die Option [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense **Quick Info** zeigt die vollständige Deklaration für jeden Bezeichner im Code an. Wenn Sie den Mauszeiger über einen Bezeichner bewegen, wird dessen Deklaration in einem gelben Popupfenster angezeigt. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]steht im Datenbankmodul und in den XML-Abfrage-Editoren **QuickInfo** zur Verfügung.  
  
## <a name="transact-sql-quick-info"></a>Transact-SQL-QuickInfo  
 Mit**QuickInfo** werden zwei Arten von Informationen im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor angezeigt. Wenn der Debugmodus nicht aktiv ist, wird mit **QuickInfo** die Ausdrucksdeklaration angezeigt. Wenn der Debugmodus aktiv ist, werden mit **QuickInfo** stattdessen der Name des Ausdrucks sowie der zugehörige aktuelle Wert angezeigt.  
  
 Im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor steht **Quick Info** nur für die Teile der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Syntax zu Verfügung, die IntelliSense unterstützen. Wenn Sie beispielsweise den Mauszeiger über einen Bezeichner für ein Objekt bewegen, das über einen Datentyp verfügt, der nicht von IntelliSense unterstützt wird, enthält das Popupfenster **Quick Info** eine Meldung, die angibt, dass der Datentyp nicht unterstützt wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Von IntelliSense unterstützte Transact-SQL-Syntax](../../relational-databases/scripting/transact-sql-syntax-supported-by-intellisense.md)  
  
  
