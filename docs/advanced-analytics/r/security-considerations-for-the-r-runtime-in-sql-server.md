---
title: "Sicherheitsüberlegungen für Machine Learning in SQL Server | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b5fba856cc40c11f218faf0a61f66ee5451aa4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>Sicherheitsüberlegungen für Machine Learning in SQL Server

In diesem Artikel werden die Sicherheitsaspekte, die der Administrator oder ein Architekt berücksichtigen, sollten bei Verwendung von Machine Learning Services aufgelistet.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="use-a-firewall-to-restrict-network-access-by-r"></a>Verwenden Sie eine Firewall zum Einschränken des Netzwerkzugriffs mit R

In einer Standardinstallation wird eine Windows-Firewall-Regel verwendet, um alle ausgehenden Netzwerkzugriffe durch R-laufzeitprozesse zu blockieren. Firewallregeln sollten erstellt werden, um den R-Laufzeitprozess daran zu hindern, Pakete herunterzuladen oder andere Netzwerke aufzurufen, die potenziell böswillig sein können.

Wenn Sie ein anderes Firewallprogramm verwenden, können Sie ebenfalls Regeln erstellen, um ausgehende Netzwerkverbindungen für die R-Laufzeit zu blockieren. Sie erreichen dies, indem Sie Regeln für die lokalen Benutzerkonten oder für die durch den Benutzerkontenpool dargestellte Gruppe festlegen.

Es wird dringend empfohlen, dass Sie Windows-Firewall (oder eine andere Firewall Ihrer Wahl) zu verhindern, dass uneingeschränkten Netzwerkzugriff durch R oder Python-Laufzeiten aktivieren.

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>Für remote rechenkontexte unterstützten Authentifizierungsmethoden

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]unterstützt integrierte Windows-Authentifizierung und SQL-Anmeldungen beim Erstellen von Verbindungen zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und eine remote Data Science-Client.

Wenn Sie zum Beispiel eine R-Lösung auf Ihrem Laptop entwickeln und Berechnungen auf dem SQL Server-Computer ausführen möchten, würden Sie eine SQL Server-Datenquelle in R mithilfe der **rx**-Funktionen erstellen und eine Verbindungszeichenfolge basierend auf Ihren Windows-Anmeldeinformationen definieren.

Wenn Sie ändern die _computekontext_ über Ihr Laptop mit dem SQL Server-Computer, wenn Ihr Windows-Konto die erforderlichen Berechtigungen verfügt über alle R-Code wird ausgeführt auf dem SQL Server-Computer. Darüber hinaus werden alle SQL-Abfragen ausgeführt, die als Teil der R-Code unter sowie Ihre Anmeldeinformationen ausgeführt werden.

Die Verwendung von SQL-Anmeldungen wird auch in diesem Szenario unterstützt der erfordert, dass SQL Server-Instanz für die Authentifizierung im gemischten Modus konfiguriert werden.

### <a name="implied-authentication"></a>Implizite Authentifizierung

 Im Allgemeinen die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] startet das externe Skriptlaufzeit und Skripts mit einem eigenen Konto ausgeführt. Jedoch, wenn die externe Laufzeit einen ODBC-Aufruf, übernimmt der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] nimmt die Identität der Anmeldeinformationen des Benutzers, der den Befehl aus, um sicherzustellen, dass der ODBC-Aufruf nicht fehlschlägt gesendet. Dies wird als *implizite Authentifizierung* bezeichnet.
 
 > [!IMPORTANT]
 >
 > Damit die implizite Authentifizierung erfolgreich verlaufen kann, muss die Windows-Benutzergruppe, die die Workerkonten enthält (standardmäßig **SQLRUser**) über ein Konto in der Masterdatenbank für die Instanz verfügen, und dieses Konto muss zur Verbindung mit der Instanz berechtigt sein.
 > 
 > Die Gruppe **SQLRUser** wird auch verwendet werden, wenn Sie Python-Skripts ausführen. 

## <a name="no-support-for-encryption-at-rest"></a>Keine Unterstützung für Verschlüsselung ruhender

Transparente datenverschlüsselung ist für Daten gesendet oder empfangen aus der externen Skript-Laufzeit nicht unterstützt. Daher Verschlüsselung ruhender **nicht** angewendet werden, um alle Daten, die Sie, in R oder Python-Skripts können keine Daten auf Datenträger oder auf jegliche permanente Zwischenergebnisse gespeichert verwenden.

## <a name="resources"></a>Ressourcen

Weitere Informationen zum Verwalten des Diensts und zum Ausführen von R-Skripts verwendeten Benutzerkonten bereitstellen, finden Sie unter [konfigurieren und Verwalten von Advanced Analytics Extensions](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md).

Eine Beschreibung der Sicherheitsarchitektur finden Sie unter:

+ [Übersicht über die Sicherheit für R](security-overview-sql-server-r.md)
+ [Übersicht über die Sicherheit für Python](../python/security-overview-sql-server-python-services.md)

