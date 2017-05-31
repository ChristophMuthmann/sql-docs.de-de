---
title: "Serverberechtigungen für „public“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9ecb6741fae401bd5366e1bf5effdb5bbf0bd969
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="server-public-permissions"></a>Serverberechtigungen für 'public'
  Diese Regel bestimmt, ob die Serverrolle public Serverberechtigung besitzt. Jede Anmeldung, die auf dem Server erstellt wird, ist ein Element der Serverrolle public. Wenn diese Bedingung erfüllt ist, besitzt jede Anmeldung am Server Serverberechtigung.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Gewähren Sie der Serverrolle public keine Serverberechtigung.  
  
> [!IMPORTANT]  
>  Nach Abschluss des Setups verfügt die Rolle **PUBLIC** für alle Endpunkte außer der **dedizierten Administratorverbindung** über eine **CONNECT**-Berechtigung. Dies ist normal und sollte üblicherweise nicht geändert werden. (Der Zugriff wird mit der Berechtigung **CONNECT SQL** gesteuert, die beim Erstellen neuer Anmeldungen automatisch erteilt wird.)  
  
### <a name="for-more-information"></a>Weitere Informationen finden Sie unter  
 [Sichern von SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
  
