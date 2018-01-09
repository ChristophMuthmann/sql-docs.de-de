---
title: "Starten oder Beenden eines PowerPivot für SharePoint-Server | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e38e6366-9f20-4db0-b2a8-da7d5adf00eb
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 72fb8e7c0f964fe140082d9aed5748b98440fac3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="start-or-stop-a-power-pivot-for-sharepoint-server"></a>Starten oder Beenden eines Power Pivot für SharePoint-Servers
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst und ein [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] Instanz arbeiten zusammen auf dem gleichen lokalen Anwendungsserver, die koordinierte Anforderungs- und Datenverarbeitung in einer SharePoint-Farm zu unterstützen.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Dienstabhängigkeiten](#dependencies)  
  
 [Starten oder Beenden der Dienste](#startstop)  
  
 [Welche Auswirkungen hat das Beenden eines Power Pivot-Servers?](#effects)  
  
##  <a name="dependencies"></a> Dienstabhängigkeiten  
 Der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst ist von der lokalen Analysis Services-Serverinstanz abhängig, die zusammen mit dem Dienst auf dem gleichen physischen Server installiert ist. Wenn Sie den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst beenden, müssen Sie auch die lokale Analysis Services-Serverinstanz manuell beenden. Wenn ein Dienst ohne den anderen ausgeführt wird, treten Fehler bei der Zuordnung von Anforderungen für die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenverarbeitung auf.  
  
 Der Analysis Services-Server sollte nur zu Diagnosezwecken oder zur Problembehandlung isoliert ausgeführt werden. In allen anderen Fällen erfordert der Server den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst, der lokal auf dem gleichen Server ausgeführt wird.  
  
##  <a name="startstop"></a> Starten oder Beenden der Dienste  
 Verwenden Sie immer die Zentraladministration, um den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst oder die Analysis Services-Serverinstanz zu starten oder zu beenden. Mit der Zentraladministration können Sie die Dienste gleichzeitig auf der gleichen Seite starten oder beenden. Außerdem verwendet die Zentraladministration einen Zeitgeberauftrag namens **Mindestens ein Dienst wurde unerwartet gestartet oder beendet** , um Dienste neu zu starten, von denen sie annimmt, dass sie ausgeführt werden sollen. Wenn Sie den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst oder Analysis Services mit einem Nicht-SharePoint-Tool beenden, werden beim Ausführen des Zeitgeberauftrags die Dienste neu gestartet.  
  
 Das Starten und Beenden von Diensten ist eine Aktion, die sich auf eine physische Dienstinstanz bezieht. Wenn Sie über zusätzliche [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Server in der Farm verfügen, akzeptieren die anderen Server innerhalb der Farm weiterhin Anforderungen für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten.  
  
 In der Farm können nicht alle physischen Dienste gleichzeitig gestartet oder beendet werden. Sie müssen jeden Server auswählen und dann einen bestimmten Dienst starten oder beenden.  
  
 Sie können einen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst nicht für eine bestimmte Webanwendung starten, anhalten oder beenden, Sie können einen Dienst jedoch aus der Standardverbindungsliste entfernen, damit er nicht verfügbar ist. Weitere Informationen finden Sie unter [Verbinden einer PowerPivot-Dienstanwendung mit einer SharePoint-Webanwendung in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
1.  Klicken Sie in der Zentraladministration unter **Systemeinstellungen**auf **Dienste auf dem Server verwalten**.  
  
2.  Klicken Sie oben auf der Seite unter Server auf den Pfeil nach unten und dann auf **Server ändern**.  
  
3.  Wählen Sie den SharePoint-Server mit dem [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst oder der [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] -Instanz aus, den bzw. die Sie starten oder beenden möchten.  
  
4.  Wählen Sie den Dienst aus, und klicken Sie dann auf die Aktion. Denken Sie daran, die Dienste paarweise zu starten oder zu beenden. Wenn Sie den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst starten oder beenden, müssen Sie auch die Analysis Services-Serverinstanz, die auf dem gleichen Computer ausgeführt wird, starten oder beenden.  
  
##  <a name="effects"></a> Welche Auswirkungen hat das Beenden eines Power Pivot-Servers?  
 In der folgenden Tabelle werden die Auswirkungen beschrieben, die das Beenden des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdiensts und des Analysis Services-Diensts auf einem SharePoint-Server hat.  
  
|Auswirkungen auf|Description|  
|---------------|-----------------|  
|Vorhandene Abfragen|Auf einem Analysis Services-Server ausgeführte Abfragen werden sofort beendet. Der Benutzer erhält eine Fehlermeldung, dass keine Daten oder keine Datenquellenverbindung gefunden wurde.|  
|Vorhandene Datenaktualisierungsaufträge, die gerade verarbeitet werden|Auf dem aktuellen Analysis Services-Server ausgeführte Aufträge werden sofort beendet. Die Datenaktualisierung schlägt fehl, und im Datenaktualisierungsverlauf wird ein Fehler protokolliert.<br /><br /> Sie können den Status der aktuellen Aufträge anzeigen, bevor Sie den Dienst mithilfe der Seite Auftragsstatus überprüfen in der SharePoint-Zentraladministration beenden.<br /><br /> Obwohl die derzeit verarbeiteten Aufträge ermittelt werden können, gibt es keine Möglichkeit, die Warteschlange selbst anzuzeigen, um festzustellen, ob andere Aufträge gerade gestartet werden.|  
|Vorhandene Datenaktualisierungsanforderungen in der Warteschlange|Geplante Datenaktualisierungsanforderungen verbleiben während eines vollständigen Zeitplanzyklus (d. h.bis zur nächsten Startzeit) in der Verarbeitungswarteschlange. Wenn der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst bis zu diesem Zeitpunkt nicht wieder gestartet wurde, wird die Datenaktualisierungsanforderung gelöscht und ein Fehler protokolliert.|  
|Neue Abfrage- oder Datenaktualisierungsanforderungen|Wenn Sie den einzigen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Server in der Farm beenden, werden neue Anforderungen für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten nicht verarbeitet, und eine Datenanforderung verursacht den Fehler „Daten wurden nicht gefunden“.<br /><br /> Wenn Sie über zusätzliche [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Server verfügen, wird die Anforderung an einen der verfügbaren Server weitergeleitet.|  
|Verwendungsdaten|Es werden keine Verwendungsdaten gesammelt, während die Dienste beendet sind.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Power Pivot-Dienstkonten](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)  
  
  
