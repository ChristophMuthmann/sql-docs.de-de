---
title: Erstellen einer Multiserverumgebung | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, multiserver environments
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- multiserver environments [SQL Server]
ms.assetid: edc2b60d-15da-40a1-8ba3-f1d473366ee6
caps.latest.revision: "6"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 65663572c887bc63d0178c8e48cb24beacfec86a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="create-a-multiserver-environment"></a>Erstellen einer Multiserverumgebung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die Multiserververwaltung erfordert, dass Sie einen Masterserver (MSX) und einen oder mehrere Zielserver (TSX) einrichten. Aufträge, die auf allen Zielservern verarbeitet werden, müssen zuerst auf dem Masterserver definiert werden, und dann zu den Zielservern heruntergeladen werden.  
  
Standardmäßig sind die vollständige SSL-Verschlüsselung (Secure Sockets Layer) und die Zertifikatüberprüfung für Verbindungen zwischen Masterservern und Zielservern aktiviert. Weitere Informationen finden Sie unter [Festlegen von Verschlüsselungsoptionen auf Zielservern](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
Wenn Sie eine große Anzahl von Zielservern haben, vermeiden Sie, den Masterserver auf einem Produktionsserver zu definieren, der bedeutende Leistungsanforderungen bezüglich anderer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Funktionalität hat, da der Zielserverdatenverkehr die Leistung auf dem Produktionsserver verlangsamen kann. Wenn Sie auch Ereignisse an einen dedizierten Masterserver weiterleiten, können Sie die Administration auf einem Server zentralisieren. Weitere Informationen finden Sie unter [Verwalten von Ereignissen](../../ssms/agent/manage-events.md).  
  
> [!NOTE]  
> Um die Multiserver-Auftragsverarbeitung verwenden zu können, muss das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstkonto Mitglied der **msdb** -Datenbankrolle **TargetServersRole** auf dem Masterserver sein. Der Masterserver-Assistent fügt dieser Rolle im Rahmen des Eintragungsprozesses automatisch das Dienstkonto hinzu.  
  
## <a name="considerations-for-multiserver-environments"></a>Überlegungen zu Multiserverumgebungen  
  
Beachten Sie die folgenden Punkte, wenn Sie eine Multiserverumgebung erstellen:  
  
-   Verwenden Sie die aktuellste Version als Masterserver. Die aktuelle und die beiden Vorgängerversionen werden unterstützt.

-   Jeder Zielserver berichtet nur einem Masterserver. Sie müssen einen Zielserver aus einem Masterserver austragen, bevor Sie ihn bei einem anderen Masterserver eintragen können.  
  
-   Wenn Sie den Namen eines Zielservers ändern, müssen Sie ihn vor der Namensänderung austragen und danach wieder eintragen.  
  
-   Wenn Sie eine Multiserverkonfiguration auflösen möchten, müssen Sie alle Zielserver aus dem Masterserver austragen.  
  
-   SQL Server Integration Services unterstützt nur Zielserver, die über dieselbe Version wie der Masterserver oder eine höhere Version verfügen.  
  
## <a name="related-tasks"></a>Related Tasks  
In den folgenden Themen werden allgemeine Aufgaben zum Erstellen einer Multiserverumgebung beschrieben.  
  
|Description|Thema|  
|---------------|---------|  
|Beschreibt, wie ein Masterserver erstellt wird.|[Einrichten eines Masterservers](../../ssms/agent/make-a-master-server.md)|  
|Beschreibt, wie ein Zielserver erstellt wird.|[Erstellen eines Zielservers](../../ssms/agent/make-a-target-server.md)|  
|Beschreibt, wie ein Zielserver bei einem Masterserver eingetragen wird.|[Eintragen eines Zielservers bei einem Masterserver](../../ssms/agent/enlist-a-target-server-to-a-master-server.md)|  
|Beschreibt, wie der Austritt eines Zielservers aus einem Masterserver vollzogen wird.|[Vollziehen des Austritts eines Zielservers aus einem Masterserver](../../ssms/agent/defect-a-target-server-from-a-master-server.md)|  
|Beschreibt, wie der Austritt mehrerer Zielserver aus einem Masterserver vollzogen wird.|[Vollziehen des Austritts mehrerer Zielserver aus einem Masterserver](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)|  
|Beschreibt, wie der Status eines Zielservers überprüft wird.|[sp_help_targetserver (Transact-SQL)](http://msdn.microsoft.com/en-us/f841d3bd-901a-4980-ad0b-1c6eeba3f717)<br /><br />[sp_help_targetservergroup (Transact-SQL)](http://msdn.microsoft.com/en-us/ec3a4a68-b591-431c-9518-053ede522d0c)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Problembehandlung von proxybasierten Multiserveraufträgen](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
  
