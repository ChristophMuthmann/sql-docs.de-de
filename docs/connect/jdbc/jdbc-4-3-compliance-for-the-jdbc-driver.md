---
title: "JDBC 4.3 Kompatibilität für den JDBC-Treiber | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
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
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3f678f33ec8f2c844bce14daa150f6c135744ff
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 4.3 Kompatibilität für den JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Vorgängerversionen von Microsoft JDBC Driver 6.4 für SQL Server sind für die Java Database Connectivity API 4.2-Spezifikationen kompatibel. Dieser Abschnitt gilt nicht für Versionen vor der Version 6.4.  
  
 Momentan Microsoft JDBC Driver 6.4 für SQL Server ist Java 9 kompatibel, aber es ist nicht vollständig kompatibel mit Java Database Connectivity API 4.3-Spezifikationen. Für die neu eingeführte-APIs in JDBC 4.3, wenn nicht vom Treiber unterstützt, löst der Treiber eine SQLFeatureNotSupportedException.