---
title: "CLR-fähig (Serverkonfigurationsoption) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 88454574613cf705a3aa209b7d3aaec616a292a4
ms.sourcegitcommit: aebbfe029badadfd18c46d5cd6456ea861a4e86d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="clr-enabled-server-configuration-option"></a>CLR-fähig (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Mithilfe der Option CLR-fähig können Sie angeben, ob Benutzerassemblys von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt werden dürfen. Die Option „CLR-fähig“ stellt folgende Werte bereit: 
  
|value|Description|  
|-----------|-----------------|  
|0|Das Ausführen von Assemblys für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist unzulässig.|  
|1|Das Ausführen von Assemblys für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist zulässig.|  
  
Nur WOW64. Starten Sie WOW64-Server neu, damit die Änderungen an den Einstellungen wirksam werden. Für andere Servertypen ist ein Neustart nicht erforderlich.  

Wenn Sie RECONFIGURE ausführen und der Ausführungswert der Option „CLR-fähig“ von 1 in 0 geändert wird, werden alle Anwendungsdomänen mit Benutzerassemblys sofort entladen.  
  
>  **Die Ausführung der Common Language Runtime (CLR) wird für das Lightweightpooling nicht unterstützt**. Deaktivieren Sie eine der beiden folgenden Optionen: „CLR-fähig“ oder „Lightweightpooling“. Zu den Funktionen, die auf CLR basieren und nicht ordnungsgemäß im Fibermodus arbeiten, gehören der Datentyp **hierarchy** , die Replikation und die richtlinienbasierte Verwaltung.  

>  [!WARNING]
>  CLR verwendet die Codezugriffssicherheit (Code Access Security, CAS) im .NET Framework, die nicht länger als Sicherheitsbegrenzung unterstützt wird. Eine CLR-Assembly, die mit `PERMISSION_SET = SAFE` erstellt wurde, kann womöglich auf externe Systemressourcen zugreifen, nicht verwalteten Code aufrufen und sysadmin-Privilegien erwerben. Ab [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] wird eine `sp_configure`-Option mit der Bezeichnung `clr strict security` eingeführt, um die Sicherheit von CLR-Assemblys zu erhöhen. `clr strict security` ist standardmäßig aktiviert und behandelt `SAFE`- und `EXTERNAL_ACCESS`-Assemblys so, als wären Sie als `UNSAFE` gekennzeichnet. Die Option `clr strict security` kann für die Abwärtskompatibilität deaktiviert werden, es wird jedoch nicht empfohlen. Microsoft empfiehlt, dass alle Assemblys durch ein Zertifikat oder einen asymmetrischen Schlüssel mit einem entsprechenden Anmeldenamen signiert werden, dem `UNSAFE ASSEMBLY`-Berechtigung für die Masterdatenbank gewährt wurde. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Administratoren können auch Assemblys einer Liste von Assemblys hinzufügen, der das Datenbankmodul vertrauen sollte. Weitere Informationen finden Sie unter [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md).
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird zunächst die aktuelle Einstellung der Option CLR-fähig angezeigt und die Option dann aktiviert, indem der Optionswert auf 1 festgelegt wird. Wenn Sie die Option deaktivieren möchten, legen Sie den Wert auf 0 fest.  
  
```sql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Lightweightpooling (Serverkonfigurationsoption)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Lightweightpooling (Serverkonfigurationsoption)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  
