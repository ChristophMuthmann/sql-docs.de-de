---
title: "Zeitplaneigenschaften (Registerkarte Allgemein) | Microsoft Docs"
ms.custom: ""
ms.date: "06/11/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.reportserver.scheduleproperties.general.f1"
ms.assetid: 20e43966-6caf-4972-a2e2-0d9131ac8f51
caps.latest.revision: 36
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 36
---
# Zeitplaneigenschaften (Registerkarte Allgemein)
  Auf dieser Seite [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] können Sie einen freigegebenen Zeitplan anzeigen oder ändern. Feigegebene Zeitpläne können anstelle berichts- oder abonnementspezifischer Zeitpläne verwendet werden. Änderungen am Zeitplan werden übernommen, nachdem Sie den Zeitplan gespeichert haben. Die Bearbeitung eines Zeitplans hat keine Auswirkungen auf Aufträge, die gerade ausgeführt werden. Wenn Sie einen Zeitplan bearbeiten, der gerade verwendet wird, wird allen aktuell verarbeiteten Berichten und Abonnements, die durch den Zeitplan ausgelöst wurden, die Fertigstellung ermöglicht.  
  
 Nicht alle Kombinationen der Häufigkeit können in einem einzelnen Zeitplan unterstützt werden. Wenn ein Bericht z. B. um 00:00 Uhr und um 16:00 Uhr an jedem Freitag ausgeführt werden soll, müssen Sie zwei Tageszeitpläne erstellen, in denen der Freitag als Ausführungstag angegeben ist. Der erste Zeitplan hat eine Startzeit von 00:00 Uhr, und für den zweiten ist eine Startzeit von 16:00 Uhr festgelegt.  
  
 Die Verarbeitung von Zeitplänen basiert auf der Ortszeit des Berichtsservers, auf dem der Zeitplan gehostet und verarbeitet wird.  
  
 So öffnen Sie diese Seite:
 1) Starten Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Stellen Sie eine Verbindung mit einem Berichtsserver her.
 3) Erweitern Sie den Ordner **Freigegebene Zeitpläne**.
 4) Klicken Sie mit der rechten Maustaste auf einen freigegebenen Zeitplan, und wählen Sie **Eigenschaften** aus.  
  
> [!NOTE]  
>Diese Funktion ist nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar, und diese Seite wird nicht angezeigt, wenn Sie eine Edition ausführen, die nicht über diese Funktion verfügt. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
## enthalten  
 **Name**  
 Gibt den Namen des freigegebenen Zeitplans an.  
  
 **Diesen Zeitplan ausführen ab**  
 Gibt ein Startdatum für diesen Zeitplan an.  
  
 **Dieser Zeitplan endet am**  
 Gibt ein Ablaufdatum für diesen Zeitplan an.  
  
 **Typ**  
 Gibt an, ob die Wiederholungsoption hauptsächlich auf Stunden, Tagen, Wochen oder Monaten basiert oder nur einmal ausgeführt wird.  
  
 **Stunde (Serienmuster)**  
 Gibt die Optionen zum Ausführen eines geplanten Vorgangs in Intervallen von einer Stunde an (z. B., dass ein Bericht alle 6 Stunden ausgeführt wird). Das Intervall kann in Stunden und Minuten angegeben werden.  
  
 **Tag (Serienmuster)**  
 Gibt die Optionen zum Ausführen eines geplanten Vorgangs in Intervallen von Tagen an (z. B., dass ein Bericht alle 2 Tage ausgeführt wird). Sie können das Intervall in Tagen und mit der Stunde und Minute der Ausführung des Zeitplans angeben.  
  
 **Woche (Serienmuster)**  
 Gibt die Optionen zum Ausführen eines geplanten Vorgangs in Intervallen von einer Woche oder gemäß einem zu wiederholenden Muster an, das auf Wochenangaben basiert (z. B., dass ein Bericht jede zweite Woche ausgeführt wird). Sie können bei einem wöchentlichen Zeitplan den Tag, die Stunde und die Minute für die Ausführung des Zeitplans angeben.  
  
 **Monat (Serienmuster)**  
 Gibt die Optionen zum Ausführen eines geplanten Vorgangs in Intervallen von einem Monat oder gemäß einem zu wiederholenden Muster an, das auf Monatsangaben basiert. Sie können bei einem monatlichen Zeitplan den Tag, die Stunde und die Minute für die Ausführung des Zeitplans angeben. Sie können im Zeitplan bestimmte Monate auslassen.  
  
 **Einmal**  
 Gibt einen Zeitplan an, der nur einmal an einem bestimmten Datum und zu einer bestimmten Uhrzeit ausgeführt wird.  
  
## Siehe auch  
 [Berichtsserver im Management Studio (F1-Hilfe)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Vorgehensweise: Herstellen einer Verbindung mit einem Berichtsserver in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Erstellen, Ändern oder Löschen von Zeitplänen](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [Zeitpläne](../../reporting-services/subscriptions/schedules.md)  
  
  