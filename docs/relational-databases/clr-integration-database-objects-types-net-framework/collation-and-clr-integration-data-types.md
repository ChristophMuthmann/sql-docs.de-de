---
title: Sortierung und CLR-Integrationsdatentypen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ff9f8b52d2b6b9856562a99db288a461a71e0f6b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="collation-and-clr-integration-data-types"></a>Sortierung und Datentypen für die CLR-Integration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]werden Sortierungen vom **CompareInfo** -Objekt gehandhabt. Die Zeichenfolgen-APIs (Application Programming Interface, API) von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] verwenden die **CompareInfo** -Eigenschaft zusammen mit dem **CultureInfo** -Objekt des aktuellen Threads, um Zeichenfolgenvergleiche durchzuführen. Die Standardeinstellung des **CultureInfo** -Objekts basiert auf der Einstellung für das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Gebietsschema des Computers, auf dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Dies bestimmt die Standardvergleichssemantik bei Vergleichen von **CultureInfo** -Werten, wenn **System.String** nicht explizit angegeben wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nimmt keine explizite Änderung der **CompareInfo** Eigenschaft, um die Datenbank- oder serversortierung. Falls erforderlich, müssen Benutzer die entsprechende **CompareInfo** -Eigenschaft in ihren Routinen festlegen.  
  
## <a name="parameter-collation"></a>Parametersortierung  
 Wenn Sie eine CLR-Routine (Common Language Runtime) erstellenaufweist, erstellt und ein an die Routine gebundener Parameter einer CLR-Methode den Typ **SQLString**aufweist, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Instanz des Parameters mit der Standardsortierung der Datenbank, die die aufrufende Routine enthält. Wenn ein Parameter nicht vom Typ **SqlType** ist (beispielsweise **String** , nicht **SQLString**), werden die Sortierungsinformationen der Datenbank nicht mit dem Parameter verknüpft.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Datentypen in .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
