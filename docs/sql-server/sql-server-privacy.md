---
title: "Ergänzende Datenschutzbestimmungen zu SQL Server | Microsoft-Dokumentation"
ms.date: 2/19/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: 
helpviewer_keywords: 
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 4ab0d870af9ca795562c1bc9382540e95dfea119
ms.sourcegitcommit: 03021482208259e6c67599b47df23fbbe8f3a393
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
# <a name="sql-server-privacy-supplement"></a>Ergänzende Datenschutzbestimmungen zu SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Dieser Artikel fasst zusammen, wie sich verschiedene Datenobjekte verhalten, die in SQL Server verwendet werden, und wie diese Objekte verwendet werden, um persönliche oder vertrauliche weiterzugeben. Die Datenklassifizierung in diesem Artikel gilt nur für lokale Versionen von SQL Server. Sie gilt nicht für folgende Produkte:

- Azure SQL-Datenbank
- SQL Server Management Studio (SSMS)
- SQL Server Data Tools (SSDT)
- SQL Operations Studio

Definition von *zugelassenen Verwendungsszenarios*. Im Rahmen dieses Artikels werden „zugelassene Verwendungsszenarios“ als Aktionen oder Aktivitäten definiert, die von Microsoft initiiert werden.

***

>## <a name="access-control"></a>Zugriffssteuerung

Informationen, die auf die Anmeldeinformationen bezogen sind, die zum Sichern von Anmeldungen, Benutzern oder Konten in einer Installation von SQL Server verwendet werden.

### <a name="examples-of-access-control"></a>Beispiele für die Zugriffssteuerung

- Kennwörter
- Zertifikate

### <a name="permitted-usage-scenarios"></a>Zugelassene Verwendungsszenarios

|Szenario  |Zugriffseinschränkungen  |Aufbewahrungsanforderungen |
|---------|---------|---------|
|Diese Anmeldeinformationen verlassen den Computer des Benutzers nie über das Nutzungsfeedback.     |-         |-         |
|Absturzabbilder können Zugriffssteuerungsdaten enthalten.     |-         |Absturzabbilder: Maximal 30 Tage.         |
|Diese Anmeldeinformationen verlassen den Computer des Benutzers nie über das Nutzungsfeedback, es sei denn, der Kunde fügt sie manuell ein.    |Der Zugriff ist auf den internen Gebrauch von Microsoft ohne Zugriff von Drittanbietern begrenzt.         |Benutzerfeedback: Maximal 1 Jahr.         |
 |
>## <a name="customer-content"></a>Kundeninhalt

Kundeninhalt bezeichnet Daten, die direkt oder indirekt in Benutzertabellen gespeichert sind. Diese Daten schließen Statistiken und Benutzerliterale in Abfragetexten ein, die in Benutzertabellen gespeichert werden können.

### <a name="examples-of-customer-content"></a>Beispiele für Kundeninhalte

- Datenwerte, die in den Zeilen einer Benutzertabelle gespeichert werden.
- Statistikobjekte, die Kopien von Werten in den Zeilen einer Benutzertabelle enthalten.
- Abfragetexte, die Literalwerte enthalten.

### <a name="permitted-usage-scenarios"></a>Zugelassene Verwendungsszenarios
|Szenario  |Zugriffseinschränkungen  |Aufbewahrungsanforderungen |
|---------|---------|---------|
|Diese Daten verlassen den Computer des Benutzers nicht über das Nutzungsfeedback. |- |- |
|Absturzabbilder können Kundeninhalt enthalten und an Microsoft ausgegeben werden. |- |Absturzabbilder: Maximal 30 Tage. |
|Benutzerfeedback, das Kundeninhalt enthält, kann mit Zustimmung der Kunden an Microsoft gesendet werden. |Der Zugriff ist auf den internen Gebrauch von Microsoft ohne Zugriff von Drittanbietern begrenzt. Microsoft kann die Daten für den ursprünglichen Kunden verfügbar machen. |Benutzerfeedback: Maximal 1 Jahr. |

>## <a name="end-user-identifiable-information-euii"></a>Personenbezogene Endbenutzerinformationen (End-User Identifiable Information, EUII)

Daten, die von einem Benutzer stammen oder durch die Verwendung des Produkts erstellt wurden.
- Auf einen individuellen Benutzer zurückführbar.
- Enthält keinen Inhalt.

### <a name="examples-end-user-identifiable-information"></a>Beispiele für personenbezogene Endbenutzerinformationen

- Schnittstellenidentifikation Die vollständige IP-Adresse
- Computername
- Anmelde- oder Benutzernamen
- Lokaler Teil der E-Mail-Adresse (joe@contoso.com)
- Informationen zum Speicherort
- Kundenidentifikation

### <a name="permitted-usage-scenarios"></a>Zugelassene Verwendungsszenarios

|Szenario  |Zugriffseinschränkungen  |Aufbewahrungsanforderungen|
|---------|---------|---------|
|Diese Daten verlassen den Computer des Benutzers nicht über das Nutzungsfeedback. |- |- |
|Absturzabbilder können personenbezogene Endbenutzerinformationen enthalten und an Microsoft ausgegeben werden. |- |Absturzabbilder: Maximal 30 Tage. |
|Die Kunden-ID kann an Microsoft ausgegeben werden, um neue Hybrid- und Cloudfeatures bereitzustellen, die Benutzer abonniert haben. |- |Zurzeit existieren solche Hybrid- oder Cloudfeatures nicht.|
|Benutzerfeedback, das Kundeninhalt enthält, kann mit Zustimmung der Kunden an Microsoft gesendet werden.|Der Zugriff ist auf den internen Gebrauch von Microsoft ohne Zugriff von Drittanbietern begrenzt. Microsoft kann die Daten für den ursprünglichen Kunden verfügbar machen. |Benutzerfeedback: Maximal 1 Jahr. |

>## <a name="internet-based-services-data"></a>Internetbasierte Dienstdaten

Daten, die gemäß der SQL Server-Lizenzbedingungen für die Bereitstellung von internetbasierten Diensten benötigt werden.

### <a name="examples-of-internet-based-services-data"></a>Beispiele für internetbasierte Dienstdaten

- Informationen über die Computerspezifikationen
- Name oder Version des Browsers
- SQL Server-Version
- Sprachcode
- Eine IP-Adresse mit bestimmten Oktetten entfernt
- Kartendaten

### <a name="permitted-usage-scenarios"></a>Zugelassene Verwendungsszenarios

|Szenario  |Zugriffseinschränkungen  |Aufbewahrungsanforderungen|
|---------|---------|---------| 
|Können von Microsoft verwendet werden, um Features zu verbessern und bzw. oder Fehler in aktuellen Features zu beheben. |Der Zugriff ist auf den internen Gebrauch von Microsoft ohne Zugriff von Drittanbietern begrenzt. Microsoft kann die Daten für den ursprünglichen Kunden verfügbar machen.  Zum Beispiel Dashboards. |Mindestens 90 Tage bis maximal 3 Jahre. |
|Benutzerfeedback, das Kundeninhalt enthält, kann mit Zustimmung der Kunden an Microsoft gesendet werden. |Der Zugriff ist auf den internen Gebrauch von Microsoft ohne Zugriff von Drittanbietern begrenzt. |Benutzerfeedback, das Kundeninhalt enthält, kann mit Zustimmung der Kunden an Microsoft gesendet werden. |
|Power View und Kartenelemente von SQL Reporting Services können Daten für die Verwendung von Bing Maps freigeben. |Der Zugriff ist auf Sitzungsdaten begrenzt. |- |

>## <a name="system-metadata"></a>Systemmetadaten

Daten, die generiert werden, während der Server ausgeführt wird.  Diese Daten enthalten keinen Kundeninhalt.

### <a name="examples-of-system-metadata"></a>Beispiele für Systemmetadaten

Folgende Daten gelten als Systemmetadaten, wenn sie keine Kundeninhalte, Kundenzugriffssteuerung oder personenbezogene Endbenutzerinformationen enthalten.

- Datenbank-GUID
- Hash des Computernamens
- Hash des Instanznamens
- Hash des Anwendungsnamens
- Verhaltens- oder Nutzungsdaten
- Daten vom SQL-Programm zur Verbesserung der Benutzerfreundlichkeit (SQLCEIP)
- Serverkonfigurationsdaten, zum Beispiel Einstellungen von „sp_configure“
- Featurekonfigurationsdaten
- Ereignisnamen und Fehlercodes

### <a name="permitted-usage-scenarios"></a>Zugelassene Verwendungsszenarios

|Szenario  |Zugriffseinschränkungen  |Aufbewahrungsanforderungen|
|---------|---------|---------|
|Können von Microsoft verwendet werden, um Features zu verbessern und bzw. oder Fehler in aktuellen Features zu beheben.|Der Zugriff ist auf den internen Gebrauch von Microsoft ohne Zugriff von Drittanbietern begrenzt. |Mindestens 90 Tage bis maximal 3 Jahre. |
|Können verwendet werden, um dem Kunden Vorschläge zu machen.  Zum Beispiel „Ziehen Sie das Feature X in Betracht, da es für Ihre Verwendung des Produkts besser geeignet ist.“ |Microsoft kann die Daten für den ursprünglichen Kunden, z.B. über Dashboards, verfügbar machen. |Sicherheitsprotokolle zu Kundendaten: Mindestens 3 Jahre bis maximal 6 Jahre. |
Können von Microsoft für die zukünftige Produktplanung verwendet werden. |Microsoft kann diese Informationen mit anderen Hardware- und Softwareanbietern teilen, um die Ausführung derer Produkte im Zusammenspiel mit Microsoft-Software zu verbessern. |Mindestens 90 Tage bis maximal 3 Jahre.|
|Können von Microsoft verwendet werden, um cloudbasierte Dienste bereitzustellen, die auf dem ausgegebenen Nutzungsfeedback basieren. Zum Beispiel ein Kundendashboard, das die Verwendung von Features in allen Installationen von SQL Server in einer Organisation anzeigt. |Microsoft kann die Daten für den ursprünglichen Kunden, z.B. über Dashboards, verfügbar machen. |Mindestens 90 Tage bis maximal 3 Jahre. |
|Benutzerfeedback, das Kundeninhalt enthält, kann mit Zustimmung der Kunden an Microsoft gesendet werden. |Der Zugriff ist auf den internen Gebrauch von Microsoft ohne Zugriff von Drittanbietern begrenzt. Microsoft kann die Daten für den ursprünglichen Kunden verfügbar machen. |Benutzerfeedback: Maximal 1 Jahr. |

>## <a name="object-metadata"></a>Objektmetadaten

Daten, die zum Beschreiben oder Konfigurieren von Servern, Datenbanken, Tabellen und anderen Ressourcen verwendet werden.  Objektmetadaten schließen Datenbanktabellen und Spaltennamen ein, aber nicht die Inhalte von Datenbankzeilen oder anderen Kundeninhalten. Kunden sollten keine persönlichen Daten, wie z.B. personenbezogene Endbenutzerinformationen, in Objektmetadatenfelder platzieren oder Anwendungen zum Speichern von persönlichen Daten in diesen Feldern erstellen.

### <a name="examples-of-object-metadata"></a>Beispiele für Objektmetadaten

- SQL Server-Datenbanknamen
- Tabellen- und Spaltennamen
- Namen von Statistiken

### <a name="permitted-usage-scenarios"></a>Zugelassene Verwendungsszenarios

|Szenario  |Zugriffseinschränkungen  |Aufbewahrungsanforderungen|
|---------|---------|---------|
|Können von Microsoft verwendet werden, um Features zu verbessern und bzw. oder Fehler in aktuellen Features zu beheben. |Der Zugriff ist auf den internen Gebrauch von Microsoft ohne Zugriff von Drittanbietern begrenzt. |Mindestens 90 Tage bis maximal 3 Jahre.|

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]