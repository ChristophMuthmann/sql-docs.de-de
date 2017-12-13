---
title: Konfiguration (Analysis Services) nach der Installation | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
- setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 7f4417b2-0efb-4361-a79e-fa56e43ee054
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6c35dfdbf2dd4eb9e9cae0c99bfc405fbca27380
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="post-install-configuration-analysis-services"></a>Konfiguration nach der Installation (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Nach der Installation von Analysis Services, sind weitere Konfigurationsschritte erforderlich, den Server vollständig betriebsbereit ist und zur allgemeinen Verwendung verfügbar zu machen. In diesem Abschnitt werden zusätzliche Aufgaben beschrieben, die zum Abschließen der Installation ausgeführt werden. Je nach Verbindungsanforderungen müssen Sie möglicherweise auch die Authentifizierung konfigurieren (siehe [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)).  
  
 Sobald Datenbanken zur Bereitstellung verfügbar sind, müssen zusätzliche Schritte ausgeführt werden. Sie müssen Rollenmitgliedschaften für die Datenbank konfigurieren, um den Benutzerzugriff auf die Daten zu gewähren, eine Sicherungs- und Wiederherstellungsstrategie für Datenbanken entwerfen und entscheiden, ob Daten in regelmäßigen Intervallen nach einem Verarbeitungszeitplan aktualisiert werden sollen. Weitere Informationen zur Bereitstellung und Verwaltung von Datenbanken finden Sie unter den folgenden Links: [Mehrdimensionale Modelldatenbanken &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) und [Tabellarische Modelldatenbanken &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md).  
  
## <a name="instance-configuration"></a>Instanzkonfiguration  
 Analysis Services ist ein replizierbarer Dienst, d. h., Sie können mehrere Instanzen des Diensts auf einem einzelnen Server installieren. Jede zusätzliche Instanz wird mithilfe von SQL Server-Setup separat als benannte Instanz installiert und unabhängig konfiguriert, um ihren jeweiligen Verwendungszweck zu erfüllen. Beispielsweise kann auf einem Entwicklungsserver Flight Recorder ausgeführt werden, oder es werden Standardwerte für die Datenspeicherung verwendet, die auf Servern mit Produktionsarbeitslasten normalerweise geändert werden müssen. Die Anpassung der Systemkonfiguration ist außerdem erforderlich, wenn die Analysis Services-Instanz auf Hardware installiert wird, die von anderen Diensten gemeinsam genutzt wird. Wenn mehrere datenintensive Anwendungen auf derselben Hardware gehostet werden, können Sie die Ressourcenverfügbarkeit anwendungsübergreifend optimieren, indem Sie die Arbeitsspeicherschwellenwerte mithilfe der Servereigenschaften herabsetzen.  
  
## <a name="post-installation-tasks"></a>Aufgaben nach der Installation  
  
|Link|Taskbeschreibung|  
|----------|----------------------|  
|[Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Erstellen Sie eine eingehende Regel für die Windows-Firewall, damit Anforderungen über den von der Analysis Services-Instanz verwendeten TCP-Port weitergeleitet werden können. Diese Aufgabe ist erforderlich. Damit über einen Remotecomputer auf Analysis Services zugegriffen werden kann, muss eine eingehende Regel für die Firewall definiert werden.|  
|[Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)|Während der Installation musste der Administratorrolle der Analysis Services-Instanz mindestens ein Benutzerkonto hinzugefügt werden. Administratorberechtigungen sind für routinemäßige Servervorgänge erforderlich wie die Verarbeitung von Daten aus externen relationalen Datenbanken. Verwenden Sie die Informationen in diesem Thema, um eine Mitgliedschaft zur Administratorrolle hinzuzufügen oder zu ändern.|
|[Konfigurieren von Antivirensoftware auf Computern mit SQL Server](https://support.microsoft.com/kb/309422) |Möglicherweise müssen Sie Softwareanwendungen wie beispielsweise Viren- und Spywarescanner so konfigurieren, dass SQL Server-Ordner und -Dateitypen ausgeschlossen werden. Wenn die Scansoftware ein Programm oder eine Datendatei sperrt, die von Analysis Services benötigt wird, können Dienstunterbrechungen oder Datenbeschädigungen auftreten. |
|[Konfigurieren von Dienstkonten &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)|Während der Installation wurde das Analysis Services-Dienstkonto mit geeigneten Berechtigungen bereitgestellt, um den kontrollierten Zugriff auf ausführbare Programmdateien und Datenbankdateien zu ermöglichen. Nach der Installation sollten Sie abwägen, ob die Verwendung des Dienstkontos zum Ausführen weiterer Aufgaben zulässig sein soll. Sowohl Verarbeitungs- als auch das Abfragearbeitsauslastungen können unter dem Dienstkonto ausgeführt werden. Diese Vorgänge sind nur erfolgreich, wenn das Dienstkonto über entsprechende Berechtigungen verfügt.|  
|[Registrieren einer Analysis Services-Instanz in einer Servergruppe](../../analysis-services/instances/register-an-analysis-services-instance-in-a-server-group.md)|Mit SQL Server Management Studio (SSMS) können Sie Servergruppen zum Organisieren der SQL Server-Instanzen erstellen. Skalierbare Bereitstellungen, die mehrere Serverinstanzen umfassen, sind in Servergruppen einfacher zu verwalten. Verwenden Sie die Informationen in diesem Thema, um Analysis Services-Instanzen in SSMS-Gruppen zu organisieren.|  
|[Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)|Während der Installation wählen Sie einen Servermodus aus, der den Modelltyp (mehrdimensional oder tabellarisch) angibt, unter dem der Server ausgeführt wird. Wenn Sie unsicher sind, welchen Servermodus Sie verwenden sollen, ermitteln Sie den installierten Modus anhand der Informationen in diesem Thema.|  
|[Umbenennen einer Analysis Services-Instanz](../../analysis-services/instances/rename-an-analysis-services-instance.md)|Ein aussagekräftiger Name erleichtert es Ihnen, zwischen mehreren Instanzen mit unterschiedlichen Servermodi oder zwischen Instanzen, die in erster Linie von Abteilungen oder Teams verwendet werden, zu unterscheiden. Wenn Sie den Instanznamen in einen Namen ändern möchten, der die Verwaltung von Installationen vereinfacht, befolgen Sie die Anweisungen in diesem Thema.|  
  
## <a name="next-steps"></a>Nächste Schritte  
 Erfahren Sie, wie Sie von Microsoft-Anwendungen oder benutzerdefinierten Anwendungen, die die Clientbibliotheken verwenden, eine Verbindung mit Analysis Services herstellen. Abhängig von den Anforderungen der Lösung kann es erforderlich sein, den Dienst für die Kerberos-Authentifizierung zu konfigurieren. Für domänenübergreifende Verbindungen ist der HTTP-Zugriff erforderlich. Unter [Connect to Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md) finden Sie Anweisungen zu den nächsten Schritten.  
  
## <a name="see-also"></a>Siehe auch  
 [Installation für SQLServer 2016](../../database-engine/install-windows/installation-for-sql-server-2016.md)   
 [Installieren von Analysis Services im mehrdimensionalen Modus und im Data Mining-Modus](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Installieren von Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)   
 [Installieren von Analysis Services im PowerPivot-Modus](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
