---
title: "Konfigurieren eines Berichtsservers für die Remoteverwaltung | Microsoft-Dokumentation"
ms.date: 09/14/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reporting Services Configuration tool
- WMI provider [Reporting Services], remote configuration
- configuration management [WMI]
- report servers [Reporting Services], configuring
- remote server administration [Reporting Services]
ms.assetid: 8c7f145f-3ac2-4203-8cd6-2a4694395d09
caps.latest.revision: "11"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: aea0b5ff0ec119cc19744220442761ae74e9bf86
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="configure-a-report-server-for-remote-administration"></a>Konfigurieren eines Berichtsservers für die Remoteverwaltung
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]können Sie Berichtsserverinstanzen lokal oder remote konfigurieren. Zum Konfigurieren einer Remote-Berichtsserverinstanz können Sie das Reporting Services-Konfigurationstool verwenden oder benutzerdefinierten Code schreiben, der für den Anbieter der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Windows-Verwaltungsinstrumentation (Windows Management Instrumentation oder WMI) verwendet wird. Das Reporting Services-Konfigurationstool stellt dem WMI-Anbieter eine grafische Benutzeroberfläche bereit, sodass Sie einen Berichtsserver konfigurieren können, ohne Code schreiben zu müssen. Wenn Sie das Tool starten, können Sie einen Remoteserver angeben, zu dem eine Verbindung hergestellt werden soll.  
  
 Bevor Sie das Tool zur Konfiguration eines Remoteberichtsservers verwenden können, müssen Sie die Anweisungen zu diesem Thema befolgen und die Ports in der Windows-Firewall, Remoteverbindungen und Remote-WMI-Anforderungen aktivieren.  
  
 Die richtige Konfiguration hilft Ihnen, den folgenden Fehler zu vermeiden:  
  
 `The machine could not be found.`  
  
 `"The RPC server is unavailable. (Exception from HRESULT: 0x800706BA)".`  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Zum Ändern der Firewalleinstellungen müssen Sie lokal angemeldet und Mitglied der lokalen Administratorengruppe sein. Die Windows-Firewalleinstellungen eines Remotecomputers können nicht über eine Remoteverbindung geändert werden.  
  
 Wenn Sie die Remoteverwaltung für einen Benutzer aktivieren möchten, der kein Administrator ist, müssen Sie dem Konto DCOM-Remoteaktivierungsberechtigungen gewähren (Distributed Component Object Model). Anweisungen zum Konfigurieren des Servers für den Zugriff durch Nichtadministratoren sind in diesem Thema enthalten.  
  
 Einige Organisationen verfügen über Gruppenrichtlinien, durch die die Remoteserververwaltung für bestimmte Betriebssysteme oder Benutzer verhindert wird. Bevor Sie die Firewalleinstellungen ändern, sollten Sie beim Netzwerkadministrator anfragen, ob Einschränkungen für die Remoteverwaltung vorliegen.  
  
 Weitere Informationen finden Sie unter [Connecting Through Windows Firewall](http://go.microsoft.com/fwlink/?LinkId=63615) in der Dokumentation zur Plattform MSDN.  
  
## <a name="tasks"></a>Aufgaben  
 Anhand folgender Tasks kann die Konfiguration des Remoteberichtsservers aktiviert werden:  
  
-   Ports in der Windows-Firewall aktivieren, um Anforderungen in Ports zuzulassen, die vom Berichtsserver und von der Instanz des SQL Server-Datenbankmoduls verwendet werden.  Siehe [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) und [Configure a Windows Firewall for Database Engine Access](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
-   Remoteverbindungen für die Instanz des Datenbankmoduls aktivieren, auf der die Berichtserver-Datenbank gehostet ist. Eine Remoteverbindung ist zum Konfigurieren der Berichtsserver-Datenbankverbindung und zum Verwalten der Verschlüsselungsschlüssel erforderlich.  
  
-   Remote-WMI-Anforderungen aktivieren, sodass diese die [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Windows-Firewall passieren können.  
  
-   Wenn Sie einen Remoteberichtsserver für die Verwaltung durch einen Benutzer konfigurieren, der kein Administrator ist, müssen Sie die DCOM-Berechtigungen so einstellen, dass Remote-WMI-Zugriffe auf ein Standard-Windows-Benutzerkonto möglich sind. Da DCOM von der WMI als Transportmedium für Remoteaufrufe verwendet wird, müssen Sie die DCOM-Berechtigungen so festlegen, dass Benutzer, die nicht als lokaler Administrator angemeldet sind, den Server konfigurieren können.  
  
-   Wenn Sie einen Remoteberichtsserver für die Verwaltung durch einen Benutzer konfigurieren, der kein Administrator ist, müssen Sie außerdem die WMI-Berechtigungen auf den Berichtsserver-WMI-Namespace einstellen. In der Standardeinstellung haben alle Mitglieder der lokalen Administratorgruppe Zugriff auf den WMI-Namespace des Berichtsservers. Wenn Sie Nichtadministratoren Zugriff gewähren möchten, müssen Sie Berechtigungen festlegen.  
  
 Anweisungen zum Ausführen dieser Tasks sind in diesem Thema enthalten.  
  
### <a name="to-configure-remote-connections-to-the-report-server-database"></a>Konfigurieren von Remoteverbindungen für die Berichtsserver-Datenbank  
  
1.  Klicken Sie auf **Start**, zeigen Sie auf **Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], dann auf **Konfigurationstools**, und klicken Sie auf **SQL Server-Konfigurations-Manager**.  
  
2.  Erweitern Sie im linken Bereich den Eintrag **SQL Server-Netzwerkkonfiguration**, und klicken Sie dann für die Instanz von auf **Protokolle** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Aktivieren Sie im Detailbereich die Protokolle TCP/IP und Named Pipes, und starten Sie dann den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst neu.  
  
### <a name="to-enable-remote-administration-in-windows-firewall"></a>Aktivieren der Remoteverwaltung in der Windows-Firewall  
  
1.  Melden Sie sich als lokaler Administrator an dem Computer an, für den Sie die Remoteverwaltung aktivieren möchten.  
  
2.  Öffnen Sie eine Eingabeaufforderung mit Administratorberechtigungen.  
  
3.  Führen Sie den folgenden Befehl aus:  
  
    ```  
    netsh.exe firewall set service type=REMOTEADMIN mode=ENABLE scope=ALL  
    ```  
  
     Für Bereich können Sie verschiedene Optionen angeben. Weitere Informationen finden Sie in der Produktdokumentation zur Windows-Firewall.  
  
4.  Überprüfen Sie, ob die Remoteverwaltung aktiviert ist. Sie können den folgenden Befehl ausführen, um den Status anzuzeigen:  
  
    ```  
    netsh.exe firewall show state  
    ```  
  
5.  Starten Sie den Computer neu.  
  
### <a name="to-set-dcom-permissions-to-enable-remote-wmi-access-for-non-administrators"></a>So legen Sie DCOM-Berechtigungen zum Aktivieren des WMI-Remotezugriffs für Nichtadministratoren fest  
  
1.  Zeigen Sie im Menü Start auf **Verwaltung**, und klicken Sie auf **Komponentendienste**.  
  
     Unter Windows Vista klicken Sie im Startmenü auf **Alle Programme**, auf **Ausführen**, und geben Sie dann **mmc comexp.msc**ein.  
  
2.  Öffnen Sie den Ordner Komponentendienste.  
  
3.  Öffnen Sie den Ordner Computer.  
  
4.  Wählen Sie Arbeitsplatz aus.  
  
5.  Wählen Sie im Menü **Aktion** die Option **Eigenschaften**aus.  
  
6.  Klicken Sie auf **COM-Sicherheit**.  
  
7.  Klicken Sie unter **Start- und Aktivierungsberechtigungen**auf **Limits bearbeiten**.  
  
8.  Wenn Ihr Name unter **Startberechtigung**nicht angezeigt wird, klicken Sie auf **Hinzufügen**.  
  
9. Geben Sie den Namen Ihres Benutzerkontos ein, und klicken Sie dann auf **OK**.  
  
10. Aktivieren Sie unter **Berechtigungen für \<Benutzer oder Gruppe>** in der Spalte **Zulassen** die Optionen **Remotestart** und **Remoteaktivierung**, und klicken Sie dann auf **OK**.  
  
### <a name="to-set-permissions-on-the-report-server-wmi-namespace-for-non-administrators"></a>Festlegen von Berechtigungen für den Berichtsserver-WMI-Namespace für Nichtadministratoren  
  
1.  Zeigen Sie im Menü Start auf **Verwaltung**, und klicken Sie auf **Computerverwaltung**.  
  
2.  Öffnen Sie den Ordner Dienste und Anwendungen.  
  
3.  Klicken Sie mit der rechten Maustaste auf **WMI-Steuerung**, und wählen Sie **Eigenschaften**aus.  
  
4.  Klicken Sie auf **Sicherheit**.  
  
5.  Öffnen Sie den Stammordner.  
  
6.  Öffnen Sie den Ordner Microsoft.  
  
7.  Öffnen Sie den Ordner SQLServer.  
  
8.  Öffnen Sie den Ordner ReportServer.  
  
9. Öffnen Sie den Ordner Instanz. Wenn Sie die Standardinstanz installiert haben, ist der Ordner MSSQLSERVER.  
  
10. Öffnen Sie den Ordner v10  
  
11. Wählen Sie den Ordner Admin aus, und klicken Sie dann auf **Sicherheit**.  
  
12. Klicken Sie auf **Hinzufügen**, und geben Sie anschließend das Benutzerkonto ein, das Sie zum Verwalten des Servers verwenden werden.  
  
13. Aktivieren Sie in der Spalte **Zulassen** die Optionen **Konto aktivieren**, **Remoteaktivierung**und **Sicherheit lesen**, und klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
  
