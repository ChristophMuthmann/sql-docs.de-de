---
title: "Wichtige Änderungen an Funktionen des Datenbankmoduls in SQL Server 2017 | Microsoft-Dokumentation"
description: "Wichtige Änderungen an Funktionen des Datenbankmoduls in SQL Server 2017"
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-engine
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: breaking changes 2017 [SQL Server]
ms.assetid: 
caps.latest.revision: "1"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b560ce9771f1ce93a3dc4b6269d636e5e66df99
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="breaking-changes-to-database-engine-features-in-includesssqlv14-mdincludessssqlv14-mdmd"></a>Wichtige Änderungen an Funktionen des Datenbankmoduls in [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


  In diesem Thema werden fehlerhafte Änderungen im [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] beschrieben. Diese Änderungen können u. U. zur Funktionsunfähigkeit von Anwendungen, Skripts oder Funktionen führen, die auf früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]basieren. Diese Probleme können nach einem Upgrade auftreten.  
  
## <a name="breaking-changes-in-includesssqlv14-mdincludessssqlv14-mdmdincludessdeincludesssde-mdmd"></a>Wichtige Änderungen in [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-  CLR verwendet die Codezugriffssicherheit (Code Access Security, CAS) im .NET Framework, die nicht länger als Sicherheitsbegrenzung unterstützt wird. Ab [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] wird eine `sp_configure`-Option mit der Bezeichnung `clr strict security` eingeführt, um die Sicherheit von CLR-Assemblys zu erhöhen. CLR Strict Security ist standardmäßig aktiviert und behandelt `SAFE`- und `EXTERNAL_ACCESS`-Assemblys so, als wären Sie als `UNSAFE` gekennzeichnet. Die `clr strict security`-Option kann für die Abwärtskompatibilität deaktiviert werden, es wird jedoch nicht empfohlen. Wenn `clr strict security` deaktiviert ist, kann eine CLR-Assembly, die mit `PERMISSION_SET = SAFE` erstellt wurde, möglicherweise auf externe Systemressourcen zugreifen, nicht verwalteten Code aufrufen und **sysadmin**-Privilegien erwerben. Nachdem Sie Strict Security aktiviert haben, können Assemblys, die nicht signiert sind, nicht geladen werden. Wenn eine Datenbank über `SAFE`- oder `EXTERNAL_ACCESS`-Assemblys verfügt, können `RESTORE`- oder `ATTACH DATABASE`-Anweisungen abgeschlossen werden, aber die Assemblys können möglicherweise nicht geladen werden.   
  Um die Assemblys zu laden, müssen Sie jede Assembly entweder bearbeiten, ablegen oder neu erstellen, damit sie mit einem Zertifikat oder asymmetrischen Schlüssel signiert ist, der über einen entsprechenden Anmeldenamen mit der `UNSAFE ASSEMBLY`-Berechtigung auf dem Server verfügt. Weitere Informationen finden Sie unter [CLR Strict Security](../database-engine/configure-windows/clr-strict-security.md). 


  
## <a name="previous-versions"></a>Vorgängerversionen  

-   [Fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)  
  
-   [Fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2014](https://msdn.microsoft.com/library/ms143179\(v=sql.120\))  
  
-   [Fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2012](https://msdn.microsoft.com/library/ms143179\(v=sql.110\))  
  
-   [Fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2008](https://msdn.microsoft.com/library/ms143179\(v=sql.100\))  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Als veraltet markierte Funktionen des Datenbankmoduls in SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Nicht mehr unterstützte Datenbankmodul-Funktionalität in SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Abwärtskompatibilität des SQL Server-Datenbankmoduls](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
