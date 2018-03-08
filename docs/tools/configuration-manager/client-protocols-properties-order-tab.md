---
title: Clientprotokolle-Eigenschaften (Registerkarte Reihenfolge) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b00026954339af65d3730c91a24ec4f16505c682
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="client-protocols-properties-order-tab"></a>Eigenschaften der Clientprotokolle (Registerkarte Reihenfolge)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
Verwenden der **Reihenfolge** Seite auf die **Eigenschaften der Clientprotokolle** Dialogfeld anzuzeigen und die Clientprotokolle zu aktivieren.  
  
 Klicken Sie auf ein Protokoll, und klicken Sie dann auf **Aktivieren** oder **Deaktivieren** , um das ausgewählte Protokoll in die Liste **Deaktivierte Protokolle** oder **Aktivierte Protokolle** zu verschieben.  
  
 Protokolle werden in der Reihenfolge verwendet, in der sie aufgelistet sind, wobei zunächst das erste Protokoll in der Liste, dann das zweite Protokoll usw. verwendet wird. Verschieben Sie Protokolle in der Liste **Aktivierte Protokolle** nach oben oder nach unten, indem Sie auf die Schaltfläche mit dem Aufwärtspfeil bzw. Abwärtspfeil klicken. Beim Herstellen einer Verbindung zu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einem Client auf diesem Computer wird immer zuerst das **Shared Memory** -Protokoll versucht, falls dieses aktiviert ist.  
  
> [!NOTE]  
>  Diese Einstellungen werden nicht von [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient verwendet. In der Protokollreihenfolge für .NET SqlClient steht TCP an der ersten Stelle, dann folgen Named Pipes. Dies kann nicht geändert werden.  
  
## <a name="options"></a>enthalten  
 **Deaktivierte Protokolle**  
 Listet die Protokolle, die installiert sind, aber derzeit nicht verwendet.  
  
 **Aktivierte Protokolle**  
 Listet die Protokolle, die für die verfügbaren [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Clients auf diesem Computer.  
  
 **>**  
 Aktiviert das aktuell hervorgehobene Protokoll im Feld **Deaktivierte Protokolle** und verschiebt es in das Feld **Aktivierte Protokolle** .  
  
 **\<**  
 Deaktiviert das aktuell hervorgehobene Protokoll im Feld **Aktivierte Protokolle** und verschiebt es in das Feld **Deaktivierte Protokolle** .  
  
 Pfeil nach oben  
 Verschiebt das markierte Protokoll in der Liste nach oben. Damit wird die Priorität erhöht, nach der von der Netzwerkbibliothek versucht wird, das ausgewählte Protokoll für Verbindungen zu verwenden.  
  
 Pfeil nach unten  
 Verschiebt das markierte Protokoll in der Liste nach unten. Damit wird die Priorität herabgesetzt, nach der von der Netzwerkbibliothek versucht wird, das ausgewählte Protokoll für Verbindungen zu verwenden.  
  
 **Shared Memory-Protokoll aktivieren**  
 Aktiviert das Shared Memory-Protokoll. Dieses wird (falls aktiviert) immer zuerst herangezogen, wenn von einem Client eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf diesem Computer hergestellt wird.  
  
> [!NOTE]  
>  Wenn das Protokoll mithilfe eines Präfix oder als Teil der Verbindungszeichenfolge angegeben ist, wird nur das angegebene Protokoll versucht.  
  
## <a name="see-also"></a>Siehe auch  
 [Auswählen eines Netzwerkprotokolls](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
