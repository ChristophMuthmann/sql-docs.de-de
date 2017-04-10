---
title: "Gesch&#228;ftsregeln (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Geschäftsregeln [Master Data Services], Informationen zu Geschäftsregeln"
  - "Geschäftsregeln [Master Data Services]"
ms.assetid: a9f9e41a-2461-4845-b947-58b3a205543f
caps.latest.revision: 16
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 16
---
# Gesch&#228;ftsregeln (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ist eine Geschäftsregel ist eine Regel, mit der Sie die Qualität und Genauigkeit der Masterdaten sicherstellen. Sie können eine Geschäftsregel zum automatischen Aktualisieren von Daten, zum Senden von E-Mails oder zum Starten eines Geschäftsprozesses oder Workflows verwenden.  
  
 Beispiele für Geschäftsregeln finden Sie unter [Beispiele für Business & #40; Master Data Services & #41;](../master-data-services/business-rule-examples-master-data-services.md).  
  
## Erstellen und Veröffentlichen von Geschäftsregeln  
 Geschäftsregeln sind **If/Then/Else** -Anweisungen, die Sie in erstellen [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Wenn ein Attributwert eine angegebene Bedingung erfüllt, wird eine Aktion ausgeführt. Andernfalls erfolgt eine Else-Aktion. Zu den möglichen Aktionen zählen das Festlegen eines Standardwerts oder Ändern eines Werts. Diese Aktionen können mit dem Senden einer E-Mail-Benachrichtigung kombiniert werden.  
  
 Geschäftsregeln können auf bestimmten Attributwerten (z. B. Aktion, wenn Color=Blue) oder Attributwertänderungen basieren (z. B. Aktion, wenn der Wert des Color-Attributs geändert wird). Weitere Informationen zum Nachverfolgen von nicht-spezifische Änderungen finden Sie unter [Change Tracking & #40; Master Data Services & #41;](../master-data-services/change-tracking-master-data-services.md).  
  
 Um Geschäftsregeln zu verwenden, müssen Sie zuerst die Regeln erstellen und veröffentlichen und dann die veröffentlichten Regeln auf die Daten anwenden. Sie können Regeln auf eine Teilmenge der Daten oder auf alle Daten für eine Version anwenden, indem Sie die Version überprüfen. Ein Commit kann erst dann für eine Version ausgeführt werden, wenn alle Attribute die Geschäftsregelüberprüfung bestanden haben.  
  
 Wenn ein Benutzer versucht, einen Attributwert hinzuzufügen, der die Geschäftsregelüberprüfung nicht bestanden hat, kann der Wert dennoch gespeichert werden. Sie können die Überprüfungsprobleme, die in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] angezeigt werden, analysieren und korrigieren.  
  
 Wenn Sie ein Modellbereitstellungspaket erstellen und Geschäftsregeln einschließen möchten, müssen Sie Daten aus der Version in das Paket einschließen.  
  
 Wenn Sie eine Geschäftsregel erstellen, verwendet die **oder** -Operator, erstellen Sie eine separate Regel für jede bedingungsanweisung, die unabhängig ausgewertet werden kann. Sie können dann Regeln nach Bedarf ausschließen und so mehr Flexibilität und eine einfachere Problembehandlung bereitstellen.  
  
## So werden Geschäftsregeln übernommen  
 Sie können die Priorität der Regelausführung festlegen, indem Sie Geschäftsregeln nach oben oder unten verschieben. Bevor die Priorität jedoch berücksichtigt wird, werden Geschäftsregeln auf Grundlage des Aktionstyps der Regel angewendet. Die Reihenfolge ist die Folgende:  
  
1.  **Standardwert**  
  
2.  **Wert ändern**  
  
3.  **Überprüfung**  
  
4.  **Externe Aktion**  
  
5.  **Benutzerdefiniertes Aktionsskript**  
  
 Innerhalb dieser Gruppen werden Aktionen in der Prioritätsreihenfolge übernommen, von der niedrigsten zur höchsten. Z. B. vier separate Regeln möglicherweise **Standardwert** Aktionen. Die **Standardwert** Aktion, das zuerst auftritt, hängt von der Reihenfolge ihrer Priorität in der Webbenutzeroberfläche angegeben.  
  
 Andere wichtige Hinweise zum Anwenden von Regeln:  
  
-   Wenn eine Geschäftsregel ausgeschlossen oder nicht mit dem Status veröffentlicht **Active**, die Regel ist weiterhin verfügbar, jedoch nicht enthalten ist, wenn Geschäftsregeln angewendet werden.  
  
-   Geschäftsregeln werden auf die Attributwerte für alle Blattelemente oder alle konsolidierten Elemente angewendet, jedoch nicht auf beide.  
  
-   Geschäftsregeln können auf eine beliebige Version eines Modells, die angewendet werden **Öffnen** oder **gesperrt**.  
  
-   Änderungen an Daten bei der Anwendung von Geschäftsregeln werden nicht als Transaktionen protokolliert.  
  
-   Eine Geschäftsregel dürfen nicht mehr als eine **Workflow starten** Aktion.  
  
## Systemeinstellungen  
 Es gibt zwei Einstellungen in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], die sich auf Geschäftsregeln auswirken. Sie können diese Einstellungen in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] oder direkt in der Tabelle Systemeinstellungen anpassen. Weitere Informationen finden Sie unter [Systemeinstellungen & #40; Master Data Services & #41;](../master-data-services/system-settings-master-data-services.md).  
  
## Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen und veröffentlichen Sie eine neue Geschäftsregel.|[Erstellen Sie und veröffentlichen Sie einer Geschäftsregel & #40. Master Data Services & #41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|Fügen Sie einer Geschäftsregel mehrere Bedingungen hinzu.|[Fügen Sie mehrerer Bedingungen zu einer Geschäftsregel & #40 hinzu; Master Data Services & #41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)|  
|Erstellen Sie eine Geschäftsregel, damit Attribute über Werte verfügen müssen.|[Erfordern Sie Attributwerte & #40. Master Data Services & #41;](../master-data-services/require-attribute-values-master-data-services.md)|  
|Erstellen Sie eine Geschäftsregel, um eine Aktion auf der Grundlage der Änderungen an Attributwerten auszuführen.|[Initiieren von Aktionen auf Grundlage von Attributwertänderungen & #40; Master Data Services & #41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
|Erstellen Sie eine Geschäftsregel, um ein benutzerdefiniertes Skript als Bedingung zu verwenden.|[Geschäftsregel-Erweiterung & #40; Master Data Services & #41;](../master-data-services/business-rules-extension-master-data-services.md)|  
|Erstellen Sie eine Geschäftsregel, um ein benutzerdefiniertes Skript als Aktion zu verwenden.|[Geschäftsregel-Erweiterung & #40; Master Data Services & #41;](../master-data-services/business-rules-extension-master-data-services.md)|  
|Ändern Sie den Namen einer vorhandenen Geschäftsregel.|[Ändern von Namen einer Geschäftsregel & #40. Master Data Services & #41;](../master-data-services/change-a-business-rule-name-master-data-services.md)|  
|Konfigurieren Sie [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], um Benachrichtigungen zu senden, wenn Geschäftsregeln angewendet werden.|[Konfigurieren von Geschäftsregeln zum Senden von Benachrichtigungen & #40; Master Data Services & #41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|Wenden Sie Geschäftsregeln auf bestimmte Elemente an.|[Überprüfen von bestimmten Elementen auf Geschäftsregeln & #40; Master Data Services & #41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|Schließen Sie eine Geschäftsregel aus, damit sie nicht verwendet wird.|[Ausschließen einer Geschäftsregel & #40; Master Data Services & #41;](../master-data-services/exclude-a-business-rule-master-data-services.md)|  
|Löschen Sie eine vorhandene Geschäftsregel.|[Löschen einer Geschäftsregel & #40. Master Data Services & #41;](../master-data-services/delete-a-business-rule-master-data-services.md)|  
  
## Verwandte Inhalte  
  
-   [Übersicht über Master Data Services & #40; MDS & #41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Versionen & #40; Master Data Services & #41;](../master-data-services/versions-master-data-services.md)  
  
-   [Überprüfung & #40; Master Data Services & #41;](../master-data-services/validation-master-data-services.md)  
  
-   [Versionsvergleich & #40; Master Data Services & #41;](../master-data-services/change-tracking-master-data-services.md)  
  
  