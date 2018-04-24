---
title: Verwalten von Oracle-Tabellenbereichen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d3c63ddd5932e5f97fd0dd2b7b05ab657651af9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="manage-oracle-tablespaces"></a>Verwalten von Oracle-Tabellenbereichen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ein Tabellenbereich ist eine Einheit des Datenbankspeicherplatzes, die in etwa einer Dateigruppe in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]entspricht. Tabellenbereiche ermöglichen das Speichern und Verwalten von Datenbankobjekten innerhalb einzelner Gruppen. Weitere Informationen finden Sie in der Oracle-Dokumentation.  
  
 Wenn Sie eine Tabelle als Teil einer Oracle-Veröffentlichung konfigurieren, können Sie optional einen vorhandenen Oracle-Tabellenbereich angeben, der beim Speichern der Replikations-Protokollinformationen verwendet wird. Wird kein spezifischer Tabellenbereich angegeben, wird für die Replikationsobjekte der Standardtabellenbereich verwendet, der mit dem Schema für den administrativen Replikationsbenutzer verknüpft ist, das beim Konfigurieren des Verlegers konfiguriert wurde.  
  
 **So geben Sie einen Tabellenbereich für eine Artikelprotokolltabelle an**:  
  
-   Geben Sie im Dialogfeld **Artikeleigenschaften** einen Tabellenbereich an. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Verwenden Sie [sp_changearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Soll **sp_changearticle**verwendet werden, geben Sie Folgendes an:  
  
    -   Den Namen des Oracle-Verlegers für den Parameter **@publisher**entspricht.  
  
    -   Den Namen der Oracle-Veröffentlichung für den Parameter **@publication**entspricht.  
  
    -   Den Namen des Artikels für den Parameter **@article**entspricht.  
  
    -   Wert 'tablespace' für den Parameter **@property**entspricht.  
  
    -   Name des Tabellenbereichs für den Parameter **@value**entspricht.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  
