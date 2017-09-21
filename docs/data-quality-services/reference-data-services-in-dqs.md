---
title: Reference Data Services in DQS | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/01/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 201f30b4b5fd5ff6de06274a83fa62967498db2e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="reference-data-services-in-dqs"></a>Reference Data Services in DQS
  Verweisdaten beziehen sich auf einen genauen und vollständigen Satz verwandter oder kategorisierter globaler Daten (jenseits der Begrenzungen eines Unternehmens), die auf vertrauenswürdigen öffentlichen Domänen oder von erstklassigen kommerziellen Inhaltsanbietern verfügbar sind.  
  
 Die Funktion Reference Data Service in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) ermöglicht es Ihnen, Reference Data Service-Drittanbieter zu abonnieren und Ihre Geschäftsdaten durch das Überprüfen gegen hochwertige Daten dieser Anbieter leicht zu bereinigen und zu erweitern. Sie können Dienste von führenden Data Quality Service-Anbietern innerhalb von DQS verwenden, um Ihre Daten während des Bereinigungsprozesses zu standardisieren, zu korrigieren und zu erweitern. Sie können z. B. eine Liste mit Postleitzahlen gegen die Verweisdaten abgleichen, um Adressen Ihrer Kunden zu überprüfen.  
  
 Die Funktion Reference Data Service hat die folgenden Vorteile:  
  
-   Verweisdaten ermöglichen es Ihnen, die Qualität der Daten sicherzustellen, indem Sie sie mit den garantierten Daten eines Drittanbieters vergleichen.  
  
-   Der Verweisdatenprozess wird in die Erstellung einer DQS-Wissensdatenbank und in ein Data Quality-Projekt integriert und ermöglicht es Ihnen, einen umfassenden Data Quality-Prozess einzuführen.  
  
-   Unterstützt das Verwenden von Verweisdaten von Windows Azure Marketplace sowie direkt von Reference Data Service-Drittanbietern.  
  
##  <a name="Marketplace"></a> Verwenden von Verweisdaten von Windows Azure Marketplace  
 DQS unterstützt das Verwenden von Referenzdaten von Windows Azure Marketplace, um es Inhaltsanbietern zu ermöglichen, Verweisdatendienste durch Marketplace bereitzustellen. Marketplace ist ein Dienst von Microsoft, der einen Marketplace und einen Bereitstellungskanal für hochwertige Daten und Anwendungen als Clouddienste bereitstellt. Weitere Informationen zum Marketplace finden Sie in den [Informationen zum Windows Azure Marketplace](http://go.microsoft.com/fwlink/?LinkId=211291) (http://go.microsoft.com/fwlink/?LinkId=211291).  
  
 Die nahtlose Integration zwischen Marketplace und DQS vereinfacht die Schritte, die für das Ermitteln, Untersuchen und Abrufen von Informationen für Data Quality-Projekte innerhalb von DQS erforderlich sind. Die Daten werden von DQS genutzt und helfen DQS-Benutzern dabei, eine hohe Datenqualität durch das Kombinieren von DQS, Marketplace und Verweisdaten-Dienstanbietern auf innovative Weise zu erreichen.  
  
 Um Verweisdaten vom Marketplace in DQS für die Bereinigungsaktivität zu verwenden, müssen Sie über einen Marketplace-Kontoschlüssel verfügen. Das Erstellen eines Marketplace-Kontoschlüssels ist kostenlos. Sie bezahlen nur, wenn Sie kostenpflichtige Datasets abonnieren. Kostenlose Datasets können ohne anfallende Gebühren abonniert und verwendet werden. Weitere Informationen zum Erstellen eines Marketplace-Kontoschlüssels finden Sie im Thema zum [Erstellen Ihres Kontos](http://go.microsoft.com/fwlink/?LinkId=212936) (http://go.microsoft.com/fwlink/?LinkId=212936).  
  
 Darüber hinaus können Sie die folgenden Marketplace-Aktivitäten innerhalb von DQS ausführen:  
  
-   Durchsuchen von Datasets im Marketplace  
  
-   Erstellen eines Marketplace-Kontoschlüssels  
  
-   Verwalten Ihrer Marketplace-Kontodetails, wie z. B. Kontoschlüssel und Abonnements für Datenanbieter  
  
 Sie können diese Aktivitäten auf der Registerkarte **Verweisdaten** des Bildschirms **Konfiguration** in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]ausführen.  
  
##  <a name="Direct"></a> Verwenden von Verweisdaten direkt von Reference Data Service-Drittanbietern  
 Wenn Sie nicht mit dem Internet verbunden sind und daher keinen Marketplace verwenden können, unterstützt DQS auch die direkte Verbindung zu Datenanbietern, die innerhalb des Netzwerks Ihrer Organisation verfügbar sind. Um Verweisdaten von direkten Reference Data Service-Onlinedrittanbietern zu verwenden, müssen Sie in DQS einen Datensatz für den Datenanbieter erstellen.  
  
##  <a name="HowToCleanse"></a> So bereinigen Sie Daten mithilfe der Verweisdaten  
 Das Bereinigen der Daten in DQS mithilfe von Verweisdaten umfasst die folgenden drei Schritte:  
  
1.  **Konfigurieren der Verweisdatenanbieterdetails in DQS**: Bevor Sie Verweisdaten in DQS verwenden können, müssen Sie Verweisdatendienstdetails in DQS konfigurieren.  
  
    1.  Wenn Sie Marketplace verwenden, stellen Sie einen gültigen Marketplace-Kontoschlüssel bereit, wechseln Sie im Marketplace zur Datenkategorie [Data Quality Services](http://go.microsoft.com/fwlink/?LinkId=227587) , und abonnieren Sie die erforderlichen Anbieter.  
  
    2.  Wenn Sie einen direkten Onlineverweisdatenanbieter verwenden, müssen Sie direkte Verweisdatenanbieterdetails in DQS hinzufügen, bevor Sie den Anbieter verwenden können.  
  
     Das Konfigurieren der Verweisdatenanbieterdetails in DQS muss für jeden Datenanbieter nur ein Mal erfolgen. Nur DQS-Administratoren können Verweisdateneinstellungen in DQS konfigurieren.  
  
2.  **Eine Domäne/Verbunddomäne in einer Wissensdatenbank dem Verweisdatendienst zuordnen**: Ordnen Sie eine Domäne/Verbunddomäne dem entsprechenden Verweisdatendienst zu, den Sie in Schritt 1 abonniert/hinzugefügt haben.  
  
3.  **Die zugeordneten Domänen für die Bereinigungsaktivität in einem Data Quality-Projekt verwenden**: Wählen Sie während des Erstellens eines Data Quality-Projekts für die **Bereinigungsaktivität** die Wissensdatenbank aus, die Domänen/Verbunddomänen enthält, die in Schritt 2 Verweisdatendiensten zugeordnet wurden, und führen Sie die Bereinigungsaktivität aus.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie DQS zum Verwenden von Verweisdatendiensten vom Marketplace oder von direkten Reference Data Service-Onlinedrittanbietern konfiguriert wird.|[Konfigurieren von DQS zum Verwenden von Verweisdaten](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Beschreibt, wie einem Verweisdatendienst eine Domäne/Verbunddomäne in einer Wissensdatenbank zugeordnet wird.|[Anfügen einer Domäne oder Verbunddomäne an Verweisdaten](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|Beschreibt, wie Daten mithilfe des Verweisdatendienstes bereinigt werden.|[Bereinigen von Daten mit Wissen über &#40;externe&#41; Verweisdaten](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
  
