---
title: Unbekannter Dienst (Registerkarte Anmelden) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: af938c13a7c647b28b2afc8776244a1dcae2823f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="unknown-service-log-on-tab"></a>Unbekannter Dienst (Registerkarte Anmelden)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager kann diesen Dienst nicht identifizieren.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager werden Dienstinformationen vom WMI-Anbieter auf dem Computer empfangen, auf dem der Dienst ausgeführt wird. Entweder ist beim Lesen der Diensteigenschaften ein Fehler aufgetreten, oder die Diensteigenschaften sind nicht vollständig. Eine mögliche Problemlösung besteht darin, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager zu schließen und erneut zu öffnen, oder den WMI-Anbieter auf dem Computer zu überprüfen, auf dem der Dienst ausgeführt wird.  
  
 Der WMI-Anbieter ist eine Windows-Komponente. Informationen zum Prüfen von Berechtigungen für den WMI-Anbieter finden Sie unter "Vorgehensweise: Konfigurieren von WMI zum Anzeigen des Serverstatus in SQL Server-Tools" in der SQL Server-Onlinedokumentation.  
  
 Verwenden Sie im Dialogfeld **Eigenschaften von Unbekannter Dienst** die Registerkarte **Anmelden** , um das von diesem Dienst verwendete Konto anzugeben und den Dienst zu starten und zu beenden, falls Sie davon ausgehen, dass Sie den richtigen Dienst angezeigt bekommen.  
  
## <a name="options"></a>Tastatur  
 **Lokales System**  
 Geben Sie ein lokales Systemkonto an, das kein Kennwort erfordert. Das lokale Systemkonto kann die Zusammenarbeit mit anderen Servern verhindern. Dies hängt von den Privilegien ab, die dem Konto erteilt wurden.  
  
 **Dieses Konto**  
 Geben Sie ein lokales oder ein Domänenbenutzerkonto an, das die Windows-Authentifizierung verwendet. Das Verwenden eines Domänenbenutzerkontos mit minimalen Berechtigungen für Dienste wird empfohlen. Informationen zum Auswählen eines Kontos finden Sie unter "Einrichten von Windows-Dienstkonten" in der SQL Server-Onlinedokumentation.  
  
 **Kontoname**  
 Geben Sie den Kontonamen des lokalen oder Domänenbenutzers an.  
  
 **Kennwort**  
 Geben Sie das Kennwort des Kontos ein.  
  
 **Kennwort bestätigen**  
 Geben Sie das Kennwort des Kontos erneut ein.  
  
 **Start**  
 Starten Sie den Dienst.  
  
 **Beenden**  
 Beenden Sie den Dienst.  
  
 **Anhalten**  
 Halten Sie den Dienst an.  
  
 **Fortsetzen**  
 Setzen Sie einen angehaltenen Dienst fort.  
  
  
