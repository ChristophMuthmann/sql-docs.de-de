---
title: Abonnieren und Überprüfen der Richtlinie „Finance Name“ | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6a473677fef460ad5d000c87872255d6b9d9ae8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-2-2---subscribe-to-and-check-the-finance-name-policy"></a>Lektion 2.2: Abonnieren und Überprüfen der Richtlinie „Finance Name“
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In dieser Aufgabe konfigurieren Sie die Datenbank Finanzen, um die Richtlinienkategorie Finanzen zu abonnieren. Anschließend testen Sie die Richtlinie Finanz_Name.  
  
### <a name="to-subscribe-to-the-finance-policy-category"></a>So abonnieren Sie die Richtlinienkategorie 'Finanzen'  
  
1.  Erweitern Sie im Objekt-Explorer **Datenbanken**, klicken Sie mit der rechten Maustaste auf **Finanzen**, zeigen Sie auf **Richtlinien**, und klicken Sie anschließend auf **Kategorien**.  
  
2.  Aktivieren Sie das Kontrollkästchen **Abonniert** für die Kategorie **Finanzen** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-test-the-enforcement-of-the-finance-name-policy"></a>So testen Sie die Durchsetzung der Richtlinie 'Finanz_Name'  
  
1.  Öffnen Sie ein Abfragefenster in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Führen Sie die folgenden Anweisungen aus, mit denen versucht wird, eine Tabelle zu erstellen, die gegen die Richtlinie **Finanz_Name** verstößt. Die Tabelle verstößt gegen die Richtlinie, da der Tabellenname nicht mit den Buchstaben **fintbl**beginnt.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
    Beachten Sie, dass die Richtlinie das Erstellen der Tabelle verhindert und eine Informationsmeldung zurückgibt, die den Richtliniennamen liefert.  
  
2.  Um einen gültigen Namen anzugeben, ändern Sie den Code wie folgt, und führen Sie dann erneut die Anweisung aus.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
    Nun wird die Tabelle erstellt.  
  
### <a name="to-apply-the-policy-to-the-whole-server"></a>So übernehmen Sie die Richtlinie für den ganzen Server  
  
1.  Momentan hat nur die Datenbank Finanzen die Richtlinienkategorie Finanzen abonniert. In vielen Fällen ist es einfacher, die Richtlinienkategorie für den ganzen Server zu übernehmen. Erweitern Sie im Objekt-Explorer **Verwaltung**, klicken Sie mit der rechten Maustaste auf **Richtlinienverwaltung**und anschließend auf **Kategorien verwalten**.  
  
2.  Suchen Sie im Dialogfeld **Richtlinienkategorien verwalten** nach der Kategorie „Finanzen“, und aktivieren Sie das Kontrollkästchen **Datenbankabonnements beauftragen** für die Kategorie „Finanzen“.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Nun gilt die Kategorie „Finanzen“ für alle Datenbanken, aber durch die von Ihnen erstellte Bedingung ist die Richtlinie „Finanz_Name“ nur auf die Datenbank „Finanzen“ beschränkt. Dieses Beispiel zeigt, wie Sie komplexe Kombinationen von Bedingungen verwenden können, um Richtlinien so zuzuweisen, dass sie für viele Server richtig übernommen werden.  
  
## <a name="summary"></a>Zusammenfassung  
Dieses Lernprogramm hat gezeigt, wie Sie Bedingungen, Richtlinien und Richtliniengruppen der richtlinienbasierten Verwaltung erstellen und die Kompatibilität der Ziele der richtlinienbasierten Verwaltung überprüfen können.  
  
## <a name="next"></a>Weiter  
Dieses Lernprogramm ist beendet. Um zum Anfang des Tutorials zurückzukehren, klicken Sie auf [Tutorial: Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md).  
  
Eine Liste der Tutorials finden Sie unter [Tutorials für SQL Server 2016](../../sql-server/tutorials-for-sql-server-2016.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
  
