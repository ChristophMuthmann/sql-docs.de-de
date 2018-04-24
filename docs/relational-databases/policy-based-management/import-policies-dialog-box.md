---
title: Dialogfeld „Richtlinien importieren“ | Microsoft-Dokumentation
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
f1_keywords:
- sql13.swb.dmf.importpolicy.f1
ms.assetid: 78ab5f6e-2f13-4788-937e-8892ef4e2345
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f0a3cfc247a8d3425c7fe9e5b0135f9d5242f4b4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="import-policies-dialog-box"></a>Dialogfeld 'Richtlinien importieren'
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mithilfe dieses Dialogfelds können Sie ein oder mehrere Richtlinien (und deren referenzierte Bedingung), die als XML-Dateien gespeichert sind, in die aktuelle [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz importieren.  
  
## <a name="options"></a>Tastatur  
 **Zu importierende Dateien**  
 Um eine Richtlinie aus einer XML-Datei zu importieren, geben Sie den Pfad und den Namen der Datei ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen (**...**).  
  
 **Duplikate mit importierten Elementen ersetzen**  
 Wählen Sie diese Option aus, um eine vorhandene Richtlinie oder Bedingung mit demselben Namen zu überschreiben, wenn diese bereits in dieser [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz vorhanden ist. Eine Bedingung mit einer abhängigen Richtlinie kann nur überschrieben werden, wenn die abhängige Richtlinie ebenfalls überschrieben wird. Wenn diese Option nicht aktiviert ist, verursacht eine vorhandene Bedingung, die denselben Bedingungsausdruck verwendet, keinen Fehler.  
  
 **Richtlinienstatus**  
 Wählen Sie für die importierte Richtlinie den gewünschten Status aus:  
  
-   **Richtlinienstatus beim Import beibehalten**  
  
-   **Alle Richtlinien beim Import aktivieren**  
  
-   **Alle Richtlinien beim Import deaktivieren**  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Importieren einer Richtlinie der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)   
 [Exportieren einer Richtlinie der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/export-a-policy-based-management-policy.md)  
  
  
