---
title: Sichern und Wiederherstellen von Reporting Services SharePoint-dienstanwendungen | Microsoft Docs
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
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: b6dcd64d6f9662ae592474053e6cc9bbce53a83e
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Sichern und Wiederherstellen von Reporting Services SharePoint-dienstanwendungen

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

In diesem Thema wird beschrieben, wie Sichern und Wiederherstellen einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -dienstanwendung mit der SharePoint-Zentraladministration oder PowerShell.

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

## <a name="before-you-begin"></a>Vorbereitungen

### <a name="limitations-and-restrictions"></a>Einschränkungen

> [!NOTE]
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-dienstanwendungen können teilweise gesichert und wiederhergestellt werden sicherungs- und Wiederherstellungsfunktionalität mithilfe der SharePoint. **Zusätzliche Schritte sind erforderlich** , und die Schritte werden in diesem Thema dokumentiert. Derzeit im Rahmen des Sicherungsvorgangs **nicht** Sichern von Verschlüsselungsschlüsseln und Anmeldeinformationen für die unbeaufsichtigte Ausführung Konten (UEA) oder Windows-Authentifizierung für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Datenbank.

### <a name="recommendations"></a>Empfehlungen
  
-   Sichern Sie die Verschlüsselungsschlüssel vor dem Starten der SharePoint-Sicherung aus. Wenn Sie nicht die Verschlüsselungsschlüssel sichern, dann werden Sie nicht auf die verschlüsselten Daten zugreifen nach der Wiederherstellung der dienstanwendung. Sie müssen die verschlüsselten Daten löschen.  
  
-   Überprüfen Sie, ob die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung Konten mit unbeaufsichtigter Ausführung oder Windows-Authentifizierung für den Datenbankzugriff verwendet. Bei Verwendung einer dieser Kontotypen sind die entsprechenden Anmeldeinformationen zu ermitteln, damit Sie die Dienstanwendung nach der Wiederherstellung richtig konfigurieren können.  
  
-   Überprüfen Sie, dass die SharePoint-Sicherungsprotokoll im gleichen Ordner wie die Sicherungsdatei erstellt wird. Die Datei wird in der Regel **spbackup.log**genannt.  
  
## <a name="back-up-the-service-application"></a>Sichern Sie die dienstanwendung

 Führen Sie die folgenden Schritte wie folgt aus:  
  
1.  Sichern der Verschlüsselungsschlüssel  
  
2.  Sichern Sie die dienstanwendung  
  
3.  Überprüfen Sie, ob die Dienstanwendung ein Konto mit unbeaufsichtigter Ausführung oder Windows-Authentifizierung für den Datenbankzugriff verwendet. Bei Verwendung einer dieser Kontotypen müssen Sie sich die Anmeldeinformationen notieren, damit Sie die Dienstanwendung nach der Wiederherstellung konfigurieren können.  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>Sichern der Verschlüsselungsschlüssel mit der SharePoint-Zentraladministration

Weitere Informationen zum Sichern der Verschlüsselungsschlüssel für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie im Abschnitt „Verschlüsselungsschlüssel“ in [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>Sichern Sie die dienstanwendung mit der SharePoint-Zentraladministration

So sichern Sie die Dienstanwendung:  
  
1.  Im SharePoint-Zentraladministration auf **führen Sie eine Sicherung** in der **Sicherungs- /** Gruppe.  
  
2.  Erweitern Sie unter dem Knoten **Gemeinsame Dienste** die Option für **gemeinsame Dienstanwendungen** , und wählen Sie die Dienstanwendung aus. Sie weist einen Typ von **SQL Server Reporting Services-Dienstanwendung**auf.  
  
3.  Wählen Sie **Weiter**aus.  
  
4.  Geben Sie den Pfad für die **Sicherungsspeicherort:** , und wählen Sie **Sicherung starten**  
  
5.  Wiederholen Sie den oben beschriebenen Prozess. Erweitern Sie jedoch anstelle der Auswahl der Dienstanwendung den Knoten **Proxys der gemeinsamen Dienste** , und wählen Sie den Dienstanwendungsproxy aus. Er weist einen Typ von **Proxy für die SQL Server Reporting Services-Dienstanwendung**auf.  
  
 Weitere Information finden Sie in den folgenden Themen in der SharePoint-Dokumentation:  
  
 [Sichern einer Dienstanwendung (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748601.aspx)in der SharePoint-Dokumentation.  
  
 [Sichern einer Dienstanwendung (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Überprüfen der Ausführung-Konto und Datenbank-Authentifizierung

 **Ausführungskonto:** So überprüfen Sie, ob die Dienstanwendung ein Ausführungskonto verwendet:  
  
1.  Wählen Sie in der SharePoint-Zentraladministration **Dienstanwendungen verwalten** in der **Anwendungsverwaltung** Gruppe.  
  
2.  Wählen Sie den Namen der dienstanwendung, und wählen Sie dann **verwalten** im SharePoint-Menüband.  
  
3.  Wählen Sie **Ausführungskonto**.  
  
4.  Ist ein Ausführungskonto konfiguriert, müssen Ihnen die Anmeldeinformationen bekannt sein, um die Sicherung der Dienstanwendung wiederherstellen zu können. Fahren Sie erst mit der Sicherungs- und Wiederherstellungsprozedur fort, wenn Sie die richtigen Anmeldeinformationen kennen.  
  
 **Datenbankauthentifizierung** : So überprüfen Sie, ob die Dienstanwendung die Windows-Authentifizierung für die Datenbankauthentifizierung verwendet:  
  
1.  Wählen Sie in der SharePoint-Zentraladministration **Dienstanwendungen verwalten** in der **Anwendungsverwaltung** Gruppe.  
  
2.  Wählen Sie den Namen der dienstanwendung, und wählen Sie dann **Eigenschaften** im SharePoint-Menüband.  
  
3.  Lesen Sie den Abschnitt **Reporting Services-Dienstdatenbank (SSRS)** .  
  
4.  Ist die Windows-Authentifizierung konfiguriert, müssen Ihnen die Anmeldeinformationen bekannt sein, um die Dienstanwendung nach der Wiederherstellung konfigurieren zu können. Fahren Sie erst mit der Sicherungs- und Wiederherstellungsprozedur fort, wenn Sie die richtigen Anmeldeinformationen kennen.  
  
## <a name="restore-the-service-application"></a>Wiederherstellen der dienstanwendung

 Führen Sie die folgenden Schritte wie folgt aus:  
  
1.  Stellen Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung wieder her.  
  
2.  Wiederherstellen der Verschlüsselungsschlüssel  
  
3.  Wurde für die Dienstanwendung ein Ausführungskonto oder die Windows-Authentifizierung für den Datenbankzugriff verwendet, konfigurieren Sie die Anmeldeinformationen.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Wiederherstellen der dienstanwendung mit der SharePoint-Zentraladministration
  
1.  Im SharePoint-Zentraladministration auf **aus einer Sicherung wiederherstellen** in der **Sicherungs- /** Gruppe.  
  
2.  Geben Sie den Pfad für die Sicherungsdatei im **Sicherungsverzeichnisspeicherort** und wählen Sie **aktualisieren**.  
  
3.  Wählen Sie die dienstanwendungssicherung aus der **Komponente der höchsten Ebene** aus, und wählen Sie dann **Weiter**.  
  
4.  Wählen Sie Ihre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Anwendung und wählen Sie dann **Weiter**.  
  
5.  Geben Sie im Abschnitt **Anmeldenamen und Kennwörter** das Kennwort für den Anmeldenamen ein. Feld Anmeldename muss mit der Anmeldung ausgefüllt werden, die der dienstanwendung vor der Sicherung, einrichten verwendet wurde.  
  
6.  Wählen Sie **Wiederherstellung starten**.  
  
7.  Wiederholen Sie den oben beschriebenen Prozess. Erweitern Sie jedoch anstelle der Wiederherstellung der Dienstanwendung den Knoten **Gemeinsame Dienste** , und erweitern Sie anschließend den Knoten für **gemeinsame Dienstanwendungen**.  
  
 Weitere Information finden Sie in den folgenden Themen in der SharePoint-Dokumentation:  
  
 [Wiederherstellen einer Dienstanwendung (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx)  
  
 [Wiederherstellen einer Dienstanwendung (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx)  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>Wiederherstellen der Verschlüsselungsschlüssel mit der SharePoint-Zentraladministration

 Weitere Informationen zum Wiederherstellen der Verschlüsselungsschlüssel für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie im Abschnitt „Verschlüsselungsschlüssel“ in [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="configure-the-execution-account-and-database-authentication"></a>Konfigurieren Sie die Ausführung-Konto und Datenbank-Authentifizierung

 **Ausführungskonto** : Wurde für die Dienstanwendung ein Ausführungskonto verwendet, gehen Sie zum Konfigurieren des Kontos wie folgt vor:  
  
1.  Wählen Sie in der SharePoint-Zentraladministration **Dienstanwendungen verwalten** in der **Anwendungsverwaltung** Gruppe.  
  
2.  Wählen Sie den Namen der dienstanwendung, und wählen Sie dann **verwalten** im SharePoint-Menüband.  
  
3.  Wählen Sie **Ausführungskonto**.  
  
4.  Geben Sie das Konto und Kennwort ein, und wählen Sie das Feld **Ausführungskonto angeben** aus.  
  
5.  Wählen Sie **OK**.  
  
 **Datenbankauthentifizierung** : Wenn für die Dienstanwendung die Windows-Authentifizierung zur Datenbankauthentifizierung verwendet wurde, gehen Sie wie folgt vor:  
  
1.  Im SharePoint-Zentraladministration auf **Dienstanwendungen verwalten** in der **Anwendungsverwaltung** Gruppe.  
  
2.  Wählen Sie den Namen der dienstanwendung, und wählen Sie dann **Eigenschaften** im SharePoint-Menüband.  
  
3.  Lesen Sie den Abschnitt **Reporting Services-Dienstdatenbank (SSRS)** .  
  
4.  Wählen Sie **Windows-Authentifizierung**.  
  
5.  Geben Sie das Konto und Kennwort ein. Wählen Sie ggf. die Option **Windows-Anmeldeinformationen verwenden** aus.  
  
6.  Wählen Sie **Ok**

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

