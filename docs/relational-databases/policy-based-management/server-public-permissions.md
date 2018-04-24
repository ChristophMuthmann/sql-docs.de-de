---
title: Serverberechtigungen für „public“ | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c315d0fddc5bc6db3318868d4291e4ab7360e194
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="server-public-permissions"></a>Serverberechtigungen für 'public'
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Diese Regel bestimmt, ob die Serverrolle public Serverberechtigung besitzt. Jede Anmeldung, die auf dem Server erstellt wird, ist ein Element der Serverrolle public. Wenn diese Bedingung erfüllt ist, besitzt jede Anmeldung am Server Serverberechtigung.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Gewähren Sie der Serverrolle public keine Serverberechtigung.  
  
> [!IMPORTANT]  
>  Nach Abschluss des Setups verfügt die Rolle **PUBLIC** für alle Endpunkte außer der **dedizierten Administratorverbindung** über eine **CONNECT**-Berechtigung. Dies ist normal und sollte üblicherweise nicht geändert werden. (Der Zugriff wird mit der Berechtigung **CONNECT SQL** gesteuert, die beim Erstellen neuer Anmeldungen automatisch erteilt wird.)  
  
### <a name="for-more-information"></a>Weitere Informationen finden Sie unter  
 [Sichern von SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
  
