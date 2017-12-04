---
title: Sichern und Wiederherstellen von Reporting Services-SharePoint-Dienstanwendungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f127627402993c51c64ca3ccaa3a1791da210a53
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Sichern und Wiederherstellen von Reporting Services-SharePoint-Dienstanwendungen

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

In diesem Artikel wird das Sichern und Wiederherstellen einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dienstanwendung mit der SharePoint-Zentraladministration oder mit PowerShell beschrieben.

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

## <a name="before-you-begin"></a>Vorbereitungen

### <a name="limitations-and-restrictions"></a>Einschränkungen

> [!NOTE]
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dienstanwendungen können teilweise mithilfe der SharePoint-Funktionen zum Sichern und Wiederherstellen gesichert und wiederhergestellt werden. **Zusätzliche Schritte sind erforderlich** , und die Schritte werden in diesem Thema dokumentiert. Derzeit lassen sich auf Basis des Sicherungsprozesses **keine** Verschlüsselungsschlüssel und Anmeldeinformationen für Konten mit unbeaufsichtigter Ausführung oder Windows-Authentifizierung für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Datenbank sichern.

### <a name="recommendations"></a>Empfehlungen
  
-   Sichern Sie die Verschlüsselungsschlüssel vor dem Starten der SharePoint-Sicherung. Wenn Sie die Verschlüsselungsschlüssel nicht sichern, ist der Zugriff auf die verschlüsselten Daten nach der Wiederherstellung der Dienstanwendung nicht mehr möglich. Sie müssen die verschlüsselten Daten löschen.  
  
-   Überprüfen Sie, ob die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung Konten mit unbeaufsichtigter Ausführung oder Windows-Authentifizierung für den Datenbankzugriff verwendet. Bei Verwendung einer dieser Kontotypen sind die entsprechenden Anmeldeinformationen zu ermitteln, damit Sie die Dienstanwendung nach der Wiederherstellung richtig konfigurieren können.  
  
-   Überprüfen Sie, ob das SharePoint-Sicherungsprotokoll im gleichen Ordner wie die Sicherungsdatei erstellt wird. Die Datei wird in der Regel **spbackup.log**genannt.  
  
## <a name="back-up-the-service-application"></a>Sichern der Dienstanwendung

 Führen Sie die folgenden Schritte wie folgt aus:  
  
1.  Sichern der Verschlüsselungsschlüssel  
  
2.  Sichern der Dienstanwendung  
  
3.  Überprüfen Sie, ob die Dienstanwendung ein Konto mit unbeaufsichtigter Ausführung oder Windows-Authentifizierung für den Datenbankzugriff verwendet. Bei Verwendung einer dieser Kontotypen müssen Sie sich die Anmeldeinformationen notieren, damit Sie die Dienstanwendung nach der Wiederherstellung konfigurieren können.  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>Sichern der Verschlüsselungsschlüssel mithilfe der SharePoint-Zentraladministration

Weitere Informationen zum Sichern der Verschlüsselungsschlüssel für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie im Abschnitt „Verschlüsselungsschlüssel“ in [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>Sichern der Dienstanwendung mithilfe der SharePoint-Zentraladministration

So sichern Sie die Dienstanwendung:  
  
1.  Klicken Sie in der Gruppe **Sichern und Wiederherstellen** der SharePoint-Zentraladministration auf **Sicherung durchführen**.  
  
2.  Erweitern Sie unter dem Knoten **Gemeinsame Dienste** die Option für **gemeinsame Dienstanwendungen** , und wählen Sie die Dienstanwendung aus. Sie weist einen Typ von **SQL Server Reporting Services-Dienstanwendung**auf.  
  
3.  Wählen Sie **Weiter**aus.  
  
4.  Geben Sie im Feld **Sicherungsspeicherort:** den Pfad für den Speicherort ein, und klicken Sie auf **Sicherung starten**.  
  
5.  Wiederholen Sie den oben beschriebenen Prozess. Erweitern Sie jedoch anstelle der Auswahl der Dienstanwendung den Knoten **Proxys der gemeinsamen Dienste** , und wählen Sie den Dienstanwendungsproxy aus. Er weist einen Typ von **Proxy für die SQL Server Reporting Services-Dienstanwendung**auf.  
  
 Weitere Information finden Sie in den folgenden Themen in der SharePoint-Dokumentation:  
  
 [Sichern einer Dienstanwendung (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748601.aspx)in der SharePoint-Dokumentation.  
  
 [Sichern einer Dienstanwendung (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Überprüfen der Kontoausführung und Datenbankauthentifizierung

 **Ausführungskonto:** So überprüfen Sie, ob die Dienstanwendung ein Ausführungskonto verwendet:  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Anwendungsverwaltung** auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf den Namen der Dienstanwendung und dann im SharePoint-Menüband auf **Verwalten**.  
  
3.  Klicken Sie auf **Ausführungskonto**.  
  
4.  Ist ein Ausführungskonto konfiguriert, müssen Ihnen die Anmeldeinformationen bekannt sein, um die Sicherung der Dienstanwendung wiederherstellen zu können. Fahren Sie erst mit der Sicherungs- und Wiederherstellungsprozedur fort, wenn Sie die richtigen Anmeldeinformationen kennen.  
  
 **Datenbankauthentifizierung** : So überprüfen Sie, ob die Dienstanwendung die Windows-Authentifizierung für die Datenbankauthentifizierung verwendet:  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Anwendungsverwaltung** auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf den Namen Ihrer Dienstanwendung und dann im SharePoint-Menüband auf **Eigenschaften**.  
  
3.  Lesen Sie den Abschnitt **Reporting Services-Dienstdatenbank (SSRS)** .  
  
4.  Ist die Windows-Authentifizierung konfiguriert, müssen Ihnen die Anmeldeinformationen bekannt sein, um die Dienstanwendung nach der Wiederherstellung konfigurieren zu können. Fahren Sie erst mit der Sicherungs- und Wiederherstellungsprozedur fort, wenn Sie die richtigen Anmeldeinformationen kennen.  
  
## <a name="restore-the-service-application"></a>Wiederherstellen der Dienstanwendung

 Führen Sie die folgenden Schritte wie folgt aus:  
  
1.  Stellen Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung wieder her.  
  
2.  Wiederherstellen der Verschlüsselungsschlüssel  
  
3.  Wurde für die Dienstanwendung ein Ausführungskonto oder die Windows-Authentifizierung für den Datenbankzugriff verwendet, konfigurieren Sie die Anmeldeinformationen.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Wiederherstellen der Dienstanwendung mithilfe der SharePoint-Zentraladministration
  
1.  Klicken Sie in der Gruppe **Sichern und Wiederherstellen** der SharePoint-Zentraladministration auf **Wiederherstellen aus einer Sicherung**.  
  
2.  Geben Sie in das Feld **Speicherort des Sicherungsverzeichnisses** den Pfad zur Sicherungsdatei ein, und klicken Sie auf **Aktualisieren**.  
  
3.  Wählen Sie die Dienstanwendungssicherung aus der Liste **Komponente der höchsten Ebene** aus, und klicken Sie dann auf **Weiter**.  
  
4.  Wählen Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Anwendung aus, und klicken Sie dann auf **Weiter**.  
  
5.  Geben Sie im Abschnitt **Anmeldenamen und Kennwörter** das Kennwort für den Anmeldenamen ein. Geben Sie in das Anmeldefeld den Anmeldenamen ein, der von der Dienstanwendung vor der Sicherung verwendet wurde.  
  
6.  Klicken Sie auf **Wiederherstellung starten**.  
  
7.  Wiederholen Sie den oben beschriebenen Prozess. Erweitern Sie jedoch anstelle der Wiederherstellung der Dienstanwendung den Knoten **Gemeinsame Dienste** , und erweitern Sie anschließend den Knoten für **gemeinsame Dienstanwendungen** .  
  
 Weitere Information finden Sie in den folgenden Themen in der SharePoint-Dokumentation:  
  
 [Wiederherstellen einer Dienstanwendung (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx)  
  
 [Wiederherstellen einer Dienstanwendung (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx)  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>Wiederherstellen der Verschlüsselungsschlüssel mithilfe der SharePoint-Zentraladministration

 Weitere Informationen zum Wiederherstellen der Verschlüsselungsschlüssel für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie im Abschnitt „Verschlüsselungsschlüssel“ in [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="configure-the-execution-account-and-database-authentication"></a>Konfigurieren des Ausführungskontos und der Datenbankauthentifizierung

 **Ausführungskonto** : Wurde für die Dienstanwendung ein Ausführungskonto verwendet, gehen Sie zum Konfigurieren des Kontos wie folgt vor:  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Anwendungsverwaltung** auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf den Namen der Dienstanwendung und dann im SharePoint-Menüband auf **Verwalten**.  
  
3.  Klicken Sie auf **Ausführungskonto**.  
  
4.  Geben Sie das Konto und Kennwort ein, und wählen Sie das Feld **Ausführungskonto angeben** aus.  
  
5.  Wählen Sie **OK**.  
  
 **Datenbankauthentifizierung** : Wenn für die Dienstanwendung die Windows-Authentifizierung zur Datenbankauthentifizierung verwendet wurde, gehen Sie wie folgt vor:  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Anwendungsverwaltung** auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf den Namen Ihrer Dienstanwendung und dann im SharePoint-Menüband auf **Eigenschaften**.  
  
3.  Lesen Sie den Abschnitt **Reporting Services-Dienstdatenbank (SSRS)** .  
  
4.  Wählen Sie **Windows-Authentifizierung**.  
  
5.  Geben Sie das Konto und Kennwort ein. Wählen Sie ggf. die Option **Windows-Anmeldeinformationen verwenden** aus.  
  
6.  Klicken Sie auf **OK**.

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
