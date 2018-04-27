---
title: Programm zur Verbesserung der Benutzerfreundlichkeit für SQL Server Data Tools | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/21/2016
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: baf3a205-a6bb-4564-8b64-3a0475bb9273
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: beae11de576f8f6c413271ee2b532454d03613fe
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="customer-experience-improvement-program-for-sql-server-data-tools"></a>Programm zur Verbesserung der Benutzerfreundlichkeit für SQL Server Data Tools
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Erfahren Sie, wie das Programm zur Verbesserung der Benutzerfreundlichkeit (Customer Experience Improvement Program; CEIP) uns dabei hilft, unsere Software zu verbessern.  Sie können Tools konfigurieren, um Ihr Einverständnis jederzeit zu widerrufen bzw. neu zu erteilen.  
  
> [!NOTE]  
>  Eine Erklärung der Datensammlungs- und Datennutzungsverfahren der Microsoft SQL Server 2016-Releases sowie anderer Produkte und Dienste finden Sie in diesen [Datenschutzbestimmungen von Microsoft](https://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx).  
  
## <a name="opting-in-and-out-of-ceip-for-sql-server-data-tools"></a>Abonnieren und Kündigen des CEIP für SQL Server Data Tools  
 Das Programm zur Verbesserung der Benutzerfreundlichkeit soll Microsoft dabei helfen, seine Produkte im Lauf der Zeit zu verbessern. Dieses Programm sammelt Informationen zur Computerhardware und dazu, wie Benutzer unser Produkt verwenden, ohne die Benutzer bei ihren Aufgaben am Computer zu unterbrechen. Die gesammelten Informationen helfen Microsoft dabei, zu identifizieren, welche Funktionen verbessert werden müssen. In diesem Dokument wird beschrieben, wie Sie Ihr Einverständnis im CEIP für SQL Server Data Tools (SSDT) in Visual Studio 2017, Visual Studio 2015 und Visual Studio 2013 widerrufen bzw. neu erteilen können.  

### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2017"></a>Auswahl und Kontrolle über das CEIP und SQL Server Data Tools in Visual Studio 2017  
 SSDT für Visual Studio 2017 ist das Datenmodellierungstool, das mit SQL Server 2017 geliefert wird. Es verwendet die CEIP-Optionen, die in Visual Studio 2017 integriert sind. Weitere Informationen zum Übermitteln von Feedback über das CEIP in Visual Studio 2017 finden Sie in diesem [Hilfedokument von Visual Studio](https://www.visualstudio.com/en-us/docs/work/connect/give-feedback).  
  
 In Vorschauversionen von SQL Server 2017 ist das CEIP standardmäßig aktiviert. Sie können es mithilfe der folgenden Anweisungen deaktivieren oder wieder aktivieren.  
  
 **In Visual Studio (gilt für vollständige Sprachinstallationen von Visual Studio 2017)**  
  
 Wenn Sie das SSDT-Setup auf einem Computer ausführen, auf dem Visual Studio bereits installiert ist, werden nur die SQL Server- und Business Intelligence-Projektvorlagen hinzugefügt. In diesem Szenario können von Visual Studio bereitgestellte Kunden-Feedbackoptionen verwendet werden, um das Einverständnis im CEIP zu widerrufen bzw. neu zu erteilen.  
  
1.  Starten Sie Visual Studio.  
  
2.  Wählen Sie im Hilfemenü **Feedback senden** > **Einstellungen**aus.  
  
3.  Um CEIP zu deaktivieren, klicken Sie auf **Nein, ich möchte nicht teilnehmen**, und klicken Sie dann auf **OK**.  
  
     Um CEIP zu aktivieren, klicken Sie auf **Ja, ich möchte teilnehmen**, und klicken Sie dann auf **OK**.  
  

  
 **Verwenden einer registrierungsbasierten Richtlinie oder Gruppenrichtlinie**  
  
 Wenn Sie das SSDT-Setup auf einem Computer ausführen, auf dem Visual Studio 2017 nicht installiert ist, wird nur die Visual Studio-Shell installiert. Die Shell stellt keine Kunden-Feedbackoptionen bereit. In diesem Fall stellt ein Registrierungsupdate die einzige Option zum Konfigurieren des CEIP dar.  
  
 Unternehmenskunden können durch Festlegen einer registrierungsbasierten Richtlinie für SQL Server 2017 eine Gruppenrichtlinie erstellen, um das Einverständnis zu widerrufen bzw. neu zu erteilen.  
  
 Der entsprechende Registrierungsschlüssel und die entsprechenden Einstellungen lauten wie folgt:  
  
 Key = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\15.0\SQM  
  
 RegEntry name = OptIn  
  
 DWORD-Eintrag:  
  
-   0 bedeutet keine Teilnahme  
  
-   1 bedeutet einschalten  
  
> [!CAUTION]  
>  Ein fehlerhaftes Bearbeiten der Registrierung kann möglicherweise eine schwerwiegende Beschädigung des Systems zur Folge haben. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie wichtige Daten auf dem Computer sichern. Sie können auch die Startoption Letzte als funktionierend bekannte Konfiguration verwenden, wenn nach dem Übernehmen manueller Änderungen Probleme auftreten.  
  
 Weitere Informationen zu den vom CEIP gesammelten, verarbeiteten oder übertragenen Informationen finden Sie in den [Datenschutzbestimmungen zum Microsoft-Programm zur Verbesserung der Benutzerfreundlichkeit](http://go.microsoft.com/fwlink/?LinkId=52143).  
 
### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2015"></a>Auswahl und Kontrolle über das CEIP und SQL Server Data Tools in Visual Studio 2015  
 SSDT für Visual Studio 2015 ist das Datenmodellierungstool, das mit SQL Server 2016 geliefert wird. Es verwendet die CEIP-Optionen, die in Visual Studio 2015 integriert sind. Weitere Informationen zum Übermitteln von Feedback über das CEIP in Visual Studio 2015 finden Sie in diesem [Hilfedokument von Visual Studio](http://go.microsoft.com/fwlink/?LinkId=517102).  
  
 In Vorschauversionen von SQL Server 2016 ist das CEIP standardmäßig aktiviert. Sie können es mithilfe der folgenden Anweisungen deaktivieren oder wieder aktivieren.  
  
 **In Visual Studio (gilt für vollständige Sprachinstallationen von Visual Studio 2015)**  
  
 Wenn Sie das SSDT-Setup auf einem Computer ausführen, auf dem Visual Studio bereits installiert ist, werden nur die SQL Server- und Business Intelligence-Projektvorlagen hinzugefügt. In diesem Szenario können von Visual Studio bereitgestellte Kunden-Feedbackoptionen verwendet werden, um das Einverständnis im CEIP zu widerrufen bzw. neu zu erteilen.  
  
1.  Starten Sie Visual Studio.  
  
2.  Wählen Sie im Hilfemenü **Feedback senden** > **Einstellungen**aus.  
  
3.  Um CEIP zu deaktivieren, klicken Sie auf **Nein, ich möchte nicht teilnehmen**, und klicken Sie dann auf **OK**.  
  
     Um CEIP zu aktivieren, klicken Sie auf **Ja, ich möchte teilnehmen**, und klicken Sie dann auf **OK**.  
  

  
 **Verwenden einer registrierungsbasierten Richtlinie oder Gruppenrichtlinie**  
  
 Wenn Sie das SSDT-Setup auf einem Computer ausführen, auf dem Visual Studio 2015 nicht installiert ist, wird nur die Visual Studio-Shell installiert. Die Shell stellt keine Kunden-Feedbackoptionen bereit. In diesem Fall stellt ein Registrierungsupdate die einzige Option zum Konfigurieren des CEIP dar.  
  
 Unternehmenskunden können durch Festlegen einer registrierungsbasierten Richtlinie für SQL Server 2016 eine Gruppenrichtlinie erstellen, um das Einverständnis zu widerrufen bzw. neu zu erteilen.  
  
 Der entsprechende Registrierungsschlüssel und die entsprechenden Einstellungen lauten wie folgt:  
  
 Key = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\14.0\SQM  
  
 RegEntry name = OptIn  
  
 DWORD-Eintrag:  
  
-   0 bedeutet keine Teilnahme  
  
-   1 bedeutet einschalten  
  
> [!CAUTION]  
>  Ein fehlerhaftes Bearbeiten der Registrierung kann möglicherweise eine schwerwiegende Beschädigung des Systems zur Folge haben. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie wichtige Daten auf dem Computer sichern. Sie können auch die Startoption Letzte als funktionierend bekannte Konfiguration verwenden, wenn nach dem Übernehmen manueller Änderungen Probleme auftreten.  
  
 Weitere Informationen zu den vom CEIP gesammelten, verarbeiteten oder übertragenen Informationen finden Sie in den [Datenschutzbestimmungen zum Microsoft-Programm zur Verbesserung der Benutzerfreundlichkeit](http://go.microsoft.com/fwlink/?LinkId=52143).  
  
### <a name="choice-and-control-for-ceip-and-sql-server-data-tools---bi-ssdt-bi"></a>Auswahl und Steuerung für das CEIP und SQL Server Data Tools – BI (SSDT-BI)  
 Falls Sie SSDT-BI verwenden, erhalten Sie während der Installation die Gelegenheit zur Teilnahme am CEIP. Später können Sie die CEIP-Konfiguration für SSDT-BI durch Clienttools oder durch Ändern der Registrierungseinstellungen ändern.  
  
 **In SSDT und SSDT-BI für Visual Studio 2013**  
  
1.  Starten Sie das Tool, und öffnen Sie ein neues oder vorhandenes Projekt für Analysis Services oder Integration Services.  
  
2.  Wählen Sie im Menü „Hilfe“ **Kundenfeedbackoptionen für Microsoft SQL Server**aus.  
  
3.  Zum Deaktivieren des CEIP klicken Sie auf **Nein, ich möchte nicht teilnehmen**.  
  
     Zum Aktivieren des CEIP klicken Sie auf **Ja, ich möchte teilnehmen**.  
  
4.  Klicken Sie auf **OK**.  
  
 **Verwenden einer registrierungsbasierten Richtlinie oder Gruppenrichtlinie**  
  
 Unternehmenskunden können durch Festlegen einer registrierungsbasierten Richtlinie für SQL Server 2014 eine Gruppenrichtlinie erstellen, um das Einverständnis zu widerrufen bzw. neu zu erteilen.  
  
 Der entsprechende Registrierungsschlüssel und die entsprechenden Einstellungen lauten wie folgt:  
  
 Schlüssel = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\120  
  
 Name des Registrierungseintrags = CustomerFeedback  
  
 DWORD-Eintrag:  
  
-   0 bedeutet keine Teilnahme  
  
-   1 bedeutet einschalten  
  
  
