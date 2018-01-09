---
title: CLR-Integrationssicherheit | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
caps.latest.revision: "55"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e7045ebaf7ed6b6d9ce3590e8406df34a040584f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="clr-integration-security"></a>Sicherheit der CLR-Integration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Das Sicherheitsmodell von der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Integration in die [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] common Language Runtime (CLR) verwaltet und sichert den Zugriff zwischen verschiedenen Typen von CLR- und nicht-CLR-Objekte, die ausgeführt werden, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Diese Objekte werden möglicherweise durch eine [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung oder ein anderes CLR-Objekt, das im Server ausgeführt wird, aufgerufen. Die Aufrufe zwischen Objekten werden als Links bezeichnet. Die Typen von Sicherheitsüberprüfungen, die für diese Objekte ausgeführt werden, hängen von den betroffenen Linktypen ab.  
  
 Das Sicherheitsmodell der CLR Integration dient folgenden Zielen:  
  
-   Standardmäßig sollte durch die Ausführung von verwaltetem Benutzercode in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die Integrität und Stabilität von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht beeinträchtigt werden. Die Durchführung von Vorgängen, die die Stabilität von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] potenziell beeinträchtigen, sollte durch entsprechende Berechtigungen auf höherer Ebene geschützt werden.  
  
-   Verwalteter Benutzercode sollte keinen unbefugten Zugriff auf Benutzerdaten oder anderen in der Datenbank enthaltenen Benutzercode erhalten. Benutzerdefinierter Code sollte in dem Sicherheitskontext der Benutzersitzung, in der er aufgerufen wurde, und mit den richtigen Berechtigungen für diesen Sicherheitskontext ausgeführt werden.  
  
-   Der Benutzercode sollte durch geeignete Maßnahmen daran gehindert werden, auf Ressourcen außerhalb des Servers zuzugreifen, sodass er ausschließlich für den Zugriff auf lokale Daten und Berechnungen genutzt wird.  
  
-   Benutzerdefinierter Code sollte nicht in der Lage sein, nur deshalb unbefugten Zugriff auf Systemressourcen zu erlangen, weil er im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Prozess ausgeführt wird.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] kombiniert jetzt das benutzerbasierte Sicherheitsmodell von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mit dem auf dem Codezugriff basierenden Sicherheitsmodell der CLR. Einige Vorteile dieses kombinierten Sicherheitsansatzes werden in diesem Abschnitt erläutert.  
  
 In der folgenden Tabelle sind die Themen dieses Abschnitts aufgeführt.  
  
 [CLR-Integration und Codezugriffssicherheit](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
 Erläutert das Codezugriffssicherheitsmodell für verwalteten Code.  
  
 [Hostschutzattribute und Programmierung der CLR-Integration](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 Stellt Informationen zu den Hostschutzattributwerten bereit, die in SAFE-Assemblys und EXTERNAL_ACCESS-Assemblys nicht zulässig sind.  
  
 [Links in Sicherheit der CLR-Integration](http://msdn.microsoft.com/library/168efd01-d12e-4bdf-a1b3-0b5c76474eaf)  
 Beschreibt, wie Teile von Benutzercode in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] einander aufrufen können.  
  
 [Identitätswechsel und Sicherheit der CLR-Integration](http://msdn.microsoft.com/library/1495a7af-2248-4cee-afdb-9269fb3a7774)  
 Erläutert, wie verwalteter Code mithilfe des Identitätswechsels auf externe Ressourcen zugreift.  
  
 [Zulassen von teilweise vertrauenswürdigen Aufrufern](http://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
 Erläutert Probleme, die auftreten, wenn eine verwaltete Methode eine Methode in einer Klasse aufruft, die in einer anderen Assembly enthalten ist.  
  
 [Anwendungsdomänen und Sicherheit der CLR-Integration](http://msdn.microsoft.com/library/54ee904e-e21a-4ee7-b4ad-a6f6f71bd473)  
 Beschreibt, wie Assemblys in Anwendungsdomänen geladen werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwalten von CLR-Integrationsassemblys](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
  
  
