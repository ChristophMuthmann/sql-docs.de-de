---
title: Common Language Runtime (CLR) Integration Programmierkonzepte | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
caps.latest.revision: 59
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 41c8382d933a02d26ca47bfc76acc4d2563fce62
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>Programmierkonzepte für die Common Language Runtime (CLR)-Integration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]enthält [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Integration der CLR-Komponente (Common Language Runtime) des .NET Framework für [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Das bedeutet, dass Sie jetzt gespeicherte Prozeduren, Trigger, benutzerdefinierte Typen, benutzerdefinierte Funktionen, benutzerdefinierte Aggregate und Streaming-Tabellenwertfunktionen mit einer beliebigen .NET Framework-Sprache schreiben können, einschließlich [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Der Microsoft.SqlServer.Server-Namespace beinhaltet Kernfunktionalität für die CLR-Programmierung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Der Microsoft.SqlServer.Server-Namespace hingegen ist im NET Framework SDK dokumentiert. Diese Dokumentation ist nicht in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] der Onlinedokumentation enthalten.  
  
> [!IMPORTANT]  
>  Standardmäßig ist .NET Framework unter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert; dies gilt jedoch nicht für .NET Framework SDK. Wenn SDK auf Ihrem Computer nicht installiert ist und nicht in der Onlinedokumentation aufgeführt wird, funktionieren die in diesem Abschnitt aufgeführten Links zu SDK-Inhalten nicht. Installieren Sie das .NET Framework SDK. Fügen Sie das SDK nach der Installation der Onlinedokumentation und dem Inhaltsverzeichnis hinzu, indem Sie die Anweisungen unter [Installieren des .NET Framework SDKs](http://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)befolgen.  
  
> [!NOTE]  
>  CLR-Funktionen, z. B. CLR User-Funktionen sind *nicht* für Azure SQL-Datenbank unterstützt.  
  
 In der folgenden Tabelle sind die Themen dieses Abschnitts aufgeführt.  
  
 [Common Language Runtime & #40; CLR & #41; Übersicht über die Integration](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
 Bietet eine kurze Übersicht über CLR und beschreibt die Verwendung dieser Technologie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Beschreibt die Vorteile der Verwendung von CLR zur Erstellung von Datenbankobjekten.  
  
 [Assemblys &#40;Datenbankmodul&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)  
 Beschreibt, wie Assemblys in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden, um Funktionen, gespeicherte Prozeduren, Trigger, benutzerdefinierte Aggregate und benutzerdefinierte Typen bereitzustellen, die in einer der verwalteten Codesprachen geschrieben wurden, die von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework-CLR (Common Language Runtime) gehostet werden, und nicht in [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 [Erstellen von Datenbankobjekten mit Common Language Runtime & #40; CLR & #41; Integration](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 Beschreibt, welche Objekte mit CLR erstellt werden können, sowie die Anforderungen zur Erstellung von CLR-Datenbankobjekten.  
  
 [Datenzugriff von CLR-Datenbankobjekten aus](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
 Beschreibt, wie eine CLR-Routine auf Daten zugreifen kann, die in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeichert sind.  
  
 [Sicherheit der CLR-Integration](../../relational-databases/clr-integration/security/clr-integration-security.md)  
 Beschreibt das Sicherheitsmodell der CLR-Integration.  
  
 [Debuggen von CLR-Datenbankobjekten](../../relational-databases/clr-integration/debugging-clr-database-objects.md)  
 Beschreibt Einschränkungen und Anforderungen des Debuggens von CLR-Datenbankobjekten.  
  
 [Bereitstellen von CLR-Datenbankobjekten](../../relational-databases/clr-integration/deploying-clr-database-objects.md)  
 Beschreibt die Bereitstellung von Assemblys auf Produktionsservern.  
  
 [Verwalten von CLR-Integrationsassemblys](../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
 Beschreibt das Erstellen und Löschen der Assemblys zur CLR-Integration.  
  
 [Überwachung und Problembehandlung von verwalteten Datenbankobjekten](../../relational-databases/clr-integration/monitoring-and-troubleshooting-managed-database-objects.md)  
 Enthält Informationen zu den Tools, die zum Überwachen und zur Problembehandlung von verwalteten Datenbankobjekten und Assemblys in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden können.  
  
 [Verwendungsszenarien und Beispiele für Common Language Runtime & #40; CLR & #41; Integration](http://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
 Beschreibt Verwendungsszenarien und Codebeispiele mit CLR-Objekten.  
  
## <a name="see-also"></a>Siehe auch  
 [Assemblys & #40; Datenbankmodul & #41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Installieren von .NET Framework SDK](http://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
