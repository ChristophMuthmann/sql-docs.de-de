---
title: JDBC 4.3 Kompatibilität für den JDBC-Treiber | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a943388e1a1a44eb377e9eaa6268733e31c4ef9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 4.3 Kompatibilität für den JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Vorgängerversionen von Microsoft JDBC Driver 6.4 für SQL Server sind für die Java Database Connectivity API 4.2-Spezifikationen kompatibel. Dieser Abschnitt gilt nicht für Versionen vor der Version 6.4.  
  
 Momentan Microsoft JDBC Driver 6.4 für SQL Server ist Java 9 kompatibel, aber es ist nicht vollständig kompatibel mit Java Database Connectivity API 4.3-Spezifikationen. Für die neu eingeführte-APIs in JDBC 4.3, wenn nicht vom Treiber unterstützt, löst der Treiber eine SQLFeatureNotSupportedException.