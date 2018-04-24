---
title: Festlegen der Datenbankoption AUTO_CLOSE auf OFF | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
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
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1ea25d2198206595048e70501ddc14e1dbedc4b8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-the-autoclose-database-option-to-off"></a>Festlegen der Datenbankoption AUTO_CLOSE auf OFF
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Diese Regel überprüft, ob die AUTO_CLOSE-Option auf OFF festgelegt ist. Wenn AUTO_CLOSE auf ON festgelegt ist, kann diese Option bei Datenbanken, auf die häufig zugegriffen wird, aufgrund des erhöhten Aufwands zum Öffnen und Schließen der Datenbank nach jeder Verbindung zu einer Leistungseinbuße führen. AUTO_CLOSE bewirkt auch die Leerung des Prozedurcaches nach jeder Verbindung.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Wenn auf eine Datenbank häufig zugegriffen wird, legen Sie die AUTO_CLOSE-Option für die Datenbank auf OFF fest.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
