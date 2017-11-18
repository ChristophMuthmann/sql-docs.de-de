---
title: Grundlegendes zu Zeilensperren | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7b41b33aa022bc0a62996e09a713f36bbe04e816
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-row-locking"></a>Grundlegendes zu Zeilensperren
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sperren auf Zeilenebene. Diese implementieren die Parallelitätssteuerung zwischen mehreren Benutzern, die gleichzeitig Änderungen an einer Datenbank vornehmen. Standardmäßig werden Transaktionen und Sperren pro Verbindung verwaltet. Wenn eine Anwendung beispielsweise zwei JDBC-Verbindungen öffnet, können von einer Verbindung erhaltene Sperren nicht mit einer anderen Verbindung gemeinsam verwendet werden. Keine der Verbindungen kann Sperren erhalten, die zu Konflikten mit den Sperren der anderen Verbindung führen.  
  
> [!NOTE]  
>  Wenn Zeilensperren verwendet werden, werden alle Zeilen im Fetchpuffer gesperrt. Das Festlegen eines großen Werts für die Fetchgröße kann daher Auswirkungen auf die Parallelität haben.  
  
 Sperren werden verwendet, um Transaktionsintegrität und Datenbankkonsistenz zu gewährleisten. Sperren verhindern, dass Benutzer Daten lesen, die von anderen Benutzern geändert werden, und dass mehrere Benutzer gleichzeitig die gleichen Daten ändern. Wenn keine Sperren verwendet werden, kann dies dazu führen, dass die Daten in der Datenbank logisch falsch sind. Die für diese Daten ausgeführten Abfragen können dann unerwartete Ergebnisse zurückgeben.  
  
> [!NOTE]  
>  Weitere Informationen zu Zeilensperren in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter "Sperren in der [!INCLUDE[ssDE](../../includes/ssde_md.md)]" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Resultsets mit dem JDBC-Treiber legt diese fest](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  

