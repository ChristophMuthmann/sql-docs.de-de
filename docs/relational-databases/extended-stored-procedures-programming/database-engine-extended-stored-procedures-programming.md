---
title: Programmieren erweiterter gespeicherter Prozeduren | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- gateway applications [SQL Server]
- extended stored procedures [SQL Server], about extended stored procedures
- Open Data Services [SQL Server]
- ODS [SQL Server]
ms.assetid: 561305cd-c803-48af-9eec-2c19f4d311ce
caps.latest.revision: 42
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a372ac6b678903b435c682bcb6bf21c76637488f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="database-engine-extended-stored-procedures---programming"></a>Datenbankmodul erweiterten gespeicherten Prozeduren - Programmierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 In der Vergangenheit wurde Open Data Services verwendet, um Serveranwendungen zu schreiben, z. B. Gateways zu anderen Datenbankumgebungen als SQL Server. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die veraltete Teile der Open Data Services-API unterstützt nicht. Der einzige weiterhin von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützte Bereich der ursprünglichen Open Data Services-API betrifft die Funktionen für erweiterte gespeicherte Prozeduren. Daher wurde die API umbenannt in "API für erweiterte gespeicherte Prozeduren".  
  
 Mit dem Erscheinen neuerer und leistungsfähigerer Technologien wie beispielsweise der verteilten Abfragen oder der CLR-Integration ist der Bedarf an Anwendungen, die auf die API für erweiterte gespeicherte Prozeduren zurückgreifen, weitgehend verschwunden.  
  
> [!NOTE]  
>  Für bereits bestehende Gateway-Anwendungen können Sie die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthaltene Datei opends60.dll nicht verwenden, um die Anwendungen auszuführen. Gateway-Anwendungen werden nicht mehr unterstützt.  
  
## <a name="extended-stored-procedures-vs-clr-integration"></a>Erweiterte gespeicherte Prozeduren und CLR-Integration  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] boten erweiterte gespeicherte Prozeduren (XPs) den einzigen für Datenbankentwickler verfügbaren Mechanismus zum Erstellen serverseitiger Logik, die in [!INCLUDE[tsql](../../includes/tsql-md.md)] entweder schwierig auszudrücken oder unmöglich zu schreiben war. Die CLR-Integration bietet eine robustere Alternative zum Schreiben von solchen gespeicherten Prozeduren. Des Weiteren kann mit der CLR-Integration die Logik, die zuvor in der Form von gespeicherten Prozeduren geschrieben wurde, oft besser in Tabellenwertfunktionen ausgedrückt werden. So können die von der Funktion konstruierten Ergebnisse in SELECT-Anweisungen abgefragt werden, indem sie in die FROM-Klausel eingebettet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Common Language Runtime &#40;CLR&#41; Integration (Übersicht)](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)   
 [CLR-Tabellenwertfunktionen](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
  
  
