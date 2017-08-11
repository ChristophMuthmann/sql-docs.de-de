---
title: "Problembehandlung bei Reporting Services-Abonnements und Übermittlung | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae1775f7-9919-48ca-8bd7-cc16df274e2c
caps.latest.revision: 16
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2c3031036636e8c2ba2e2a0487ea2092c882c3e0
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-reporting-services-subscriptions-and-delivery"></a>Behandlung von Problemen bei Abonnements und Übermittlung in Reporting Services
  
    
Dieses Thema soll Ihnen beim Behandeln von Problemen helfen, die beim Arbeiten mit Berichtsabonnements, -plänen und -übermittlung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] auftreten können.  
## <a name="log-information"></a>Protokollinformationen
 
Die Abonnementseite in [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] enthält den Status eines Abonnements. Wenn jedoch ein Problem mit dem Abonnement auftritt, befinden sich die detaillierten Informationen in den [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Protokollen. 
![ssrs_tutorial_datadriven_subscription_status_ReportManager](../../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png)

**Ablaufverfolgungsprotokolle** : Die Ablaufverfolgungsprotokolle sind Textdateien, die in diesen Pfad geschrieben werden: `\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`

Im Folgenden sehen Sie ein Beispiel für einen Protokolleintrag:

```
   subscription WindowsService_10   4c7c    05/24/2016-01:05:06  e ERROR     Failure writing file \\ServerName\SalesReports\so71949.xls : Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider+NetworkErrorException: An impersonation error occurred using the security context of the current user. ---> System.ArgumentException: Value does not fall within the expected range.  05/24/2016
```
Weitere Informationen zu [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Ablaufverfolgungsprotokollen finden Sie hier: 
+ [Ablaufverfolgungsprotokoll des Berichtsservers](../../reporting-services/report-server/report-server-service-trace-log.md).
+ [Reporting Services-Protokolldateien](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).

**Sichten des Ausführungsprotokolls:**

Die Ausführungsprotokolle stellen in der SQL-Server-Datenbank ReportServer Sichten dar. Weitere Informationen zu [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] finden Sie unter [Reporting Services-Sichten ExecutionLog und ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

----------
## <a name="unable-to-send-reports-using-e-mail-with-windows-server-2003-and-pop3"></a>Berichte können unter Windows Server 2003 nicht über POP3 per E-Mail gesendet werden  
Wenn Sie eine E-Mail-Anwendung ausführen und dafür Post Office Protocol Version 3 (POP3) unter Microsoft Windows Server 2003 verwenden, ist es eventuell nicht möglich, Berichte mithilfe des lokalen POP3-Servers zu senden. Falls Sie den Berichtsserver so konfiguriert haben, dass E-Mail-Nachrichten über den lokalen POP3-Server gesendet werden, und ein Abonnement erstellen, das einen Bericht sendet, wird möglicherweise die folgende Fehlermeldung angezeigt:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Failure sending mail: <error message>`  
  
wobei \<Fehlermeldung > wird ersetzt durch zusätzliche Fehlermeldungsinformationen, die von Collaboration Data Objects (CDO) zurückgegeben.  
  
### <a name="to-resolve-this-problem"></a>So lösen Sie dieses Problem  
* Legen Sie den Wert des `SendUsing` -Elements in der Datei **Rsreportserver.config** auf 1 fest.  
* Löschen Sie den Wert der `SMTPServer` -Eigenschaft, sodass diese leer ist. Darüber hinaus müssen Sie einen Wert für die `SMTPServerPickupDirectory` -Eigenschaft angeben.   
  
Weitere Informationen zum Verwenden eines lokalen SMTP-Dienstes für die E-Mail-Übermittlung von Berichten finden Sie unter "Konfigurieren eine Berichtsservers für die E-Mail-Übermittlung".  
  
## <a name="failure-sending-mail-the-server-rejected-the-sender-address-the-server-response-was-454-573-client-does-not-have-permission-to-submit-mail-to-this-server"></a>Fehler beim Senden von E-Mail: Der Server hat die Absenderadresse zurückgewiesen. Die Serverantwort lautet: 454 5.7.3. Client ist nicht berechtigt, Mail an diesen Server zu übermitteln.  
Dieser Fehler tritt auf, wenn die Sicherheitsrichtlinieneinstellungen auf dem SMTP-Server nur authentifizierten Benutzern das Senden von E-Mails für die nachfolgende Übermittlung ermöglichen. Falls der SMTP-Server keine E-Mail-Sendungen von anonymen Benutzern akzeptiert, wenden Sie sich an den Systemadministrator, um die Berechtigung für die Verwendung des Servers zu erhalten.  
> Dieser Fehler kann außerdem auftreten, wenn Sie einen Exchange-Servernamen als SMTP-Server angeben. Wenn Sie einen Server mit Exchange für die E-Mail-Übermittlung verwenden möchten, müssen Sie den Namen des für den Server mit Exchange konfigurierten SMTP-Gateways angeben. Diese Informationen erhalten Sie von Ihrem Exchange-Administrator.  
  
## <a name="subscriptions-are-not-processing"></a>Abonnements werden nicht verarbeitet  
Abonnements können unter diesen Bedingungen einen Fehler erzeugen:   
* Der Zeitplan zum Auslösen des Berichts ist abgelaufen. Für Abonnements, die das Update einer Berichtsmomentaufnahme auslösen, ist möglicherweise der Zeitplan zum Aktualisieren der Momentaufnahme abgelaufen.  
  
* Der Berichtsserver, der SQL Server-Agent oder die E-Mail-Serveranwendung wird nicht ausgeführt.  
* Der Bericht ist unzustellbar (z. B. zu groß). Um festzustellen, ob die Übermittlung fehlschlägt, weil der Bericht zu groß ist, speichern Sie den Bericht in einer Datei und senden diese per E-Mail. Achten Sie darauf, dass Sie das gleiche Renderingformat wie im Abonnement auswählen. Wenn Sie eine Übermittlungsfehlermeldung erhalten, verwenden Sie als Übermittlungserweiterung Dateifreigabe anstelle von Berichtsserver-E-Mail.  
* Der Computer, der für die Dateifreigabeübermittlung verwendet wird, wird nicht ausgeführt, oder für die Dateifreigabe ist der Nur-Lese-Zugriff konfiguriert.  
* Die im Abonnement angegebene Übermittlungserweiterung wurde deinstalliert oder deaktiviert.  
* Die Einstellungen für Anmeldeinformationen wurden von gespeicherten auf integrierte oder eingegebene Werte geändert.  
* Der Parametername oder Datentyp in der Berichtsdefinition wurde geändert, und der Bericht wurde wieder veröffentlicht. Enthält ein Abonnement einen Parameter, der nicht mehr gültig ist, wird das Abonnement deaktiviert.  
  
Weitere Informationen finden Sie im TechNet-Wiki [Troubleshoot issues and errors with Reporting Services](http://social.technet.microsoft.com/wiki/contents/articles/1633.ssrs-troubleshoot-issues-and-errors-with-reporting-services.aspx).  
  
  
    
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


