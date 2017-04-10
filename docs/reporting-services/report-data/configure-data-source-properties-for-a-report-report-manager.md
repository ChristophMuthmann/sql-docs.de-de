---
title: "Konfigurieren von Datenquelleneigenschaften f&#252;r einen Bericht (Berichts-Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenquellen [Reporting Services], eingebettet"
ms.assetid: 27af5195-c845-40e0-9a9c-efe569424022
caps.latest.revision: 44
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 44
---
# Konfigurieren von Datenquelleneigenschaften f&#252;r einen Bericht (Berichts-Manager)
  Bei der Ausführung eines Berichts ruft der Berichtsserver Eigenschaftsinformationen ab, um festzulegen, wie die Verbindung mit einer Datenquelle hergestellt werden soll. Dabei werden der Typ der Datenquelle, die Verbindungszeichenfolge sowie Anmeldeinformationen auf den Eigenschaftenseiten für die Datenquelle des veröffentlichten Berichts angegeben. Sie können die Eigenschaften festlegen, um andere Informationen für die Verbindungsherstellung mit der Datenquelle anzugeben als bei der Erstellung des Berichts genannt wurden.  
  
 Alternativ können Sie stattdessen die freigegebene Datenquelle angeben, wenn Sie über eine vordefinierte freigegebene Datenquelle verfügen, in der bereits die gewünschten Verbindungsinformationen festgelegt sind. Klicken Sie zur Verwendung einer freigegebenen Datenquelle auf der Eigenschaftenseite für die Datenquelle des Berichts auf **Eine freigegebene Datenquelle** .  
  
### So konfigurieren Sie eine eingebettete Datenquelle  
  
1.  Starten Sie den [Berichts-Manager im einheitlichen SSRS-Modus](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  Navigieren Sie im Berichts-Manager zur Seite **Inhalt** . Navigieren Sie zu dem Bericht, für den Sie eine berichtsspezifische Datenquelle konfigurieren möchten, und öffnen Sie den Bericht.  
  
3.  Klicken Sie auf die Registerkarte **Eigenschaften** . Die Eigenschaftenseite **Allgemein** wird geöffnet.  
  
4.  Klicken Sie auf die Registerkarte **Datenquellen** . Hiermit wird die Eigenschaftenseite der Datenquelle des Berichts aufgerufen.  
  
5.  Klicken Sie auf **Eine benutzerdefinierte Datenquelle** , um Verbindungsinformationen für die Datenquelle innerhalb des Berichts anzugeben.  
  
6.  Geben Sie in der Liste **Verbindungstyp** die Datenverarbeitungserweiterung an, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
7.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. Es wird empfohlen, dass Sie keine Anmeldeinformationen in der Verbindungszeichenfolge angeben.  
  
     Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung zur lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank hergestellt wird:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  Geben Sie für **Verbindung herstellen über**an, wie die Anmeldeinformationen bei Ausführung des Berichts abgerufen werden:  
  
    -   Wenn der Benutzer zur Eingabe eines Anmeldenamens und eines Kennworts aufgefordert werden soll, klicken Sie auf **Bereitgestellte Anmeldeinformationen vom Benutzer, der den Bericht ausführt**.  
  
    -   Wenn Sie die Datenquelle mit Berichten verwenden möchten, die Abonnements oder andere geplante Vorgänge (z.B. automatisierte Berichtsverlaufgenerierung) unterstützen, klicken Sie auf **Anmeldeinformationen, die sicher auf dem Berichtsserver gespeichert sind**.  
  
    -   Wenn der Berichtsserver die Anmeldeinformationen des auf den Bericht zugreifenden Benutzers an den Server übergeben soll, der die externe Datenquelle hostet, klicken Sie auf **Integrierte Sicherheit von Windows**. In diesem Fall wird der Benutzer nicht aufgefordert, einen Benutzernamen oder ein Kennwort einzugeben.  
  
    -   Klicken Sie auf **Anmeldeinformationen sind nicht erforderlich**, wenn Sie eine Datenquelle verwenden, die nicht mit Anmeldeinformationen arbeitet (z.B. wenn es sich bei der Datenquelle um eine XML-Datei handelt, auf die vom Dateisystem zugegriffen wird). Diesen Typ Anmeldeinformationen sollten Sie nur dann angeben, wenn er von der Datenquelle unterstützt wird. Wenn Sie diese Option für eine Datenquelle aktivieren, die Authentifizierung erfordert, schlägt die Verbindungsherstellung fehl. Vergewissern Sie sich bei der Auswahl dieser Option, dass Sie das unbeaufsichtigte Ausführungskonto konfigurieren, mit dem der Berichtsserver eine Verbindung zu anderen Computern herstellen kann, um Daten oder Dateien abzurufen, wenn keine Anmeldeinformationen zur Verfügung stehen.  
  
 Weitere Informationen zum Konfigurieren von Anmeldeinformationen finden Sie unter [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). Weitere Informationen zum Konto für die unbeaufsichtigte Ausführung finden Sie unter [Konfigurieren des Kontos für die unbeaufsichtigte Ausführung &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## Siehe auch  
 [Inhalt &#40;Seite, Berichts-Manager&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [Neue Datenquelle &#40;Seite, Berichts-Manager&#41;](../Topic/New%20Data%20Source%20Page%20\(Report%20Manager\).md)   
 [Erstellen, Ändern und Löschen von freigegebenen Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Verwalten von Berichtsdatenquellen](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Erstellen, Löschen oder Ändern einer freigegebenen Datenquelle &#40;Berichts-Manager&#41;](../Topic/Create,%20Delete,%20or%20Modify%20a%20Shared%20Data%20Source%20\(Report%20Manager\).md)   
 [Datenquellen (Eigenschaftenseite) &#40;Berichts-Manager&#41;](../Topic/Data%20Sources%20Properties%20Page%20\(Report%20Manager\).md)  
  
  