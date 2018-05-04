---
title: Hosten Sie Schutzattribute und CLR-Integrationsprogrammierung | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
caps.latest.revision: 28
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8c844f2f5a3491c7eea71b6d3ffab7efff254a97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Hostschutzattribute und Programmierung der CLR-Integration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die CLR (Common Language Runtime) stellt Mechanismen zur Verfügung, um verwaltete Anwendungsprogrammierschnittstellen (Application Programming Interfaces, APIs), die Teil von .NET Framework sind, mit Anmerkungen in Form von bestimmten Attributen zu versehen, die für einen Host der CLR, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], von Interesse sein können. Beispiele für solche Hostschutzattribute sind:  
  
-   **SharedState**, der angibt, ob die-API bietet die Möglichkeit zum Erstellen oder Verwalten des Freigabezustand (z. B. statische Klassenfelder).  
  
-   **Synchronisierung**, der angibt, ob die API die Fähigkeit zum Ausführen der Synchronisierung zwischen Threads verfügbar macht.  
  
-   **ExternalProcessMgmt**, der angibt, ob die API eine Möglichkeit zur Kontrolle des Hostprozesses verfügbar macht.  
  
 Anhand dieser Attribute gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Liste mit Hostschutzattributen an, die in der gehosteten Umgebung von der Codezugriffssicherheit (CAS) nicht zugelassen werden. Die CAS-Anforderungen sind von einem von drei angegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Berechtigungssätze: **sichere**, **EXTERNAL_ACCESS**, oder **UNSAFE**. Einer dieser drei Sicherheitsebenen wird angegeben, wenn die Assembly, auf dem Server registriert ist mithilfe der **CREATE ASSEMBLY** Anweisung. Ausführen von Code in der **sichere** oder **EXTERNAL_ACCESS** Berechtigungssätze müssen eine bestimmte Typen oder Member mit vermeiden der **System.Security.Permissions.HostProtectionAttribute** Attribut angewendet. Weitere Informationen finden Sie unter [Creating an Assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md) und [CLR Integration Programming Model Einschränkungen](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 Die **HostProtectionAttribute** ist eine Sicherheitsberechtigung als eine Möglichkeit zur Verbesserung der Zuverlässigkeit, insofern, dass es bestimmte Codekonstrukte Typen oder Methoden erstellt, dass der Host möglicherweise nicht zulässig. Die Verwendung der **HostProtectionAttribute** erzwingt ein Programmiermodell, das die Stabilität des Hosts besser geschützt.  
  
## <a name="host-protection-attributes"></a>Hostschutzattribute  
 Hostschutzattribute geben die Typen oder Elemente an, die sich nicht für das Hostprogrammiermodell eignen und die folgenden Zuverlässigkeitsrisiken darstellen (ansteigende Gefährdung):  
  
-   Sie sind andernfalls ohne Auswirkung.  
  
-   Sie können zur Destabilisierung von serververwaltetem Benutzercode führen.  
  
-   Sie können zur Destabilisierung des Serverprozesses führen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lässt einen Typ oder Member mit einer **HostProtectionAttribute** , die angibt, eine **System.Security.Permissions.HostProtectionResource** -Enumeration mit dem Wert des  **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**,  **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **Synchronisierung**, oder **UI**. Dies verhindert, dass Assemblys Elemente aufrufen, die die Freigabe des Zustands aktivieren, Synchronisierungen durchführen, einen Ressourcenverlust bei der Beendigung hervorrufen oder die Integrität des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozesses beeinträchtigen.  
  
### <a name="disallowed-types-and-members"></a>Unzulässige Typen und Member  
 In den folgenden Themen zu identifizieren, Typen und Membern, deren **HostProtectionResource** Werte nicht zulässig sind, indem Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Die Listen in diesen Themen wurden von den unterstützten Assemblys generiert.  Weitere Informationen finden Sie unter [unterstützt .NET Framework-Bibliotheken](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Unzulässige Typen und Member in "Microsoft.VisualBasic.dll"](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Listet die Typen und Elemente in Microsoft.VisualBasic.dll auf, deren Hostschutzattributwerte nicht zugelassen werden.  
  
 [Unzulässige Typen und Member in "mscorlib.dll"](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 Listet die Typen und Elemente in mscorlib.dll auf, deren Hostschutzattributwerte nicht zugelassen werden.  
  
 [Unzulässige Typen und Member in "System.dll"](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 Listet die Typen und Elemente in System.dll auf, deren Hostschutzattributwerte nicht zugelassen werden.  
  
 [Unzulässige Typen und Member in "System.Data.dll"](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 Listet die Typen und Elemente in System.Data.dll auf, deren Hostschutzattributwerte nicht zugelassen werden.  
  
 [Unzulässige Typen und Member in "System.Core.dll"](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 Listet die Typen und Elemente in System.Core.dll auf, deren Hostschutzattributwerte nicht zugelassen werden.  
  
## <a name="see-also"></a>Siehe auch  
 [CLR Integration Code Access Security](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR-Integration Einschränkungen des Programmiermodells](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Erstellen einer Assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
