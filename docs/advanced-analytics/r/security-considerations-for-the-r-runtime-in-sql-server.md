---
title: "Sicherheitsüberlegungen für Machine Learning in SQL Server | Microsoft Docs"
ms.date: 02/01/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: c7262b804c1712e7ea962feefd88f3b2f64146a9
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>Sicherheitsüberlegungen für Machine Learning in SQL Server

In diesem Artikel werden die Sicherheitsaspekte, die der Administrator oder ein Architekt berücksichtigen, sollten bei Verwendung von Machine Learning Services aufgelistet.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="use-a-firewall-to-restrict-network-access"></a>Verwenden Sie eine Firewall, um die Einschränkung des Netzwerkzugriffs

In einer Standardinstallation wird eine Windows-Firewall-Regel verwendet, um alle ausgehenden Netzwerkzugriffe durch externe-laufzeitprozesse zu blockieren. Firewallregeln sollten erstellt werden, um zu verhindern, dass die externe-Laufzeitprozessen aus Pakete herunterladen oder andere Netzwerke aufzurufen, die potenziell böswillig sein können.

Wenn Sie ein anderes Firewallprogramm verwenden, können Sie auch Regeln zum Blockieren von ausgehende Netzwerkverbindungen für externen Laufzeiten durch Festlegen von Regeln für den lokalen Benutzerkonten oder für die durch den benutzerkontenpool dargestellte Gruppe erstellen.

Es wird dringend empfohlen, dass Sie Windows-Firewall (oder eine andere Firewall Ihrer Wahl) zu verhindern, dass uneingeschränkten Netzwerkzugriff durch R oder Python-Laufzeiten aktivieren.

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>Für remote rechenkontexte unterstützten Authentifizierungsmethoden

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] unterstützt integrierte Windows-Authentifizierung und SQL-Anmeldungen beim Erstellen von Verbindungen zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und eine remote Data Science-Client.

Angenommen Sie, Sie entwickeln eine R-Lösung auf Ihrem Laptop und Berechnungen auf dem SQL Server-Computer ausführen möchten. Sie würden in R eine SQL Server-Datenquelle erstellen, mit der **Rx** Funktionen und definieren eine Verbindungszeichenfolge basierend auf Ihren Windows-Anmeldeinformationen.

Wenn Sie ändern die _computekontext_ über Ihr Laptop mit dem SQL Server-Computer, wird alle R-Code auf dem SQL Server-Computer ausgeführt, wenn Ihr Windows-Konto die erforderlichen Berechtigungen verfügt. Darüber hinaus werden alle SQL-Abfragen ausgeführt, die als Teil der R-Code unter sowie Ihre Anmeldeinformationen ausgeführt werden.

Die Verwendung von SQL-Anmeldungen wird auch in diesem Szenario unterstützt. Allerdings erfordert dies, dass die SQL Server-Instanz für die Authentifizierung im gemischten Modus konfiguriert werden.

### <a name="implied-authentication"></a>Implizite Authentifizierung

 Im Allgemeinen die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] startet das externe Skriptlaufzeit und Skripts mit einem eigenen Konto ausgeführt. Jedoch, wenn die externe Laufzeit einen ODBC-Aufruf, übernimmt der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] nimmt die Identität der Anmeldeinformationen des Benutzers, der den Befehl aus, um sicherzustellen, dass der ODBC-Aufruf nicht fehlschlägt gesendet. Dies wird als *implizite Authentifizierung* bezeichnet.
 
 > [!IMPORTANT]
 > Für die implizite Authentifizierung erfolgreich ist, handelt es sich bei die Windows-Benutzergruppe, die die Worker-Konten enthält (standardmäßig **SQLRUserGroup**) benötigen ein Konto in der master-Datenbank aus, für die Instanz, und dieses Konto muss Berechtigungen für bestimmte Verbinden Sie mit der Instanz.
 > 
 > Die Gruppe **SQLRUserGroup** wird auch verwendet werden, wenn Sie Python-Skripts ausführen. 

Im Allgemeinen wird empfohlen, dass Sie im Vorfeld größeren Datasets in SQL Server verschieben, anstatt versuchen, Daten mithilfe von RODBC oder einer anderen Bibliothek zu lesen. Verwenden Sie außerdem eine SQL Server-Abfrage oder Sicht als die primäre Datenquelle für eine bessere Leistung. 

Sie können z. B. Trainingsdaten (in der Regel die größte Daten) von SQL Server abgerufen und eine Liste von Faktoren aus einer externen Quelle abzurufen. Sie können einen Verbindungsserver zum Abrufen von Daten aus den meisten ODBC-Datenquellen definieren. Weitere Informationen finden Sie unter [erstellen Sie einen Verbindungsserver](https://docs.microsoft.com/sql/relational-databases/linked-servers/create-linked-servers-sql-server-database-engine).

Um die Abhängigkeit von ODBC-Aufrufe von externen Datenquellen zu minimieren, können Sie auch Daten Engineering als separater Prozess, ausführen und speichern Sie die Ergebnisse in einer Tabelle oder T-SQL verwenden. Finden Sie in diesem Lernprogramm für ein gutes Beispiel der Daten-Entwicklung in Visual Studio die SQL. R: [Erstellen von Data-Funktionen, die mithilfe des T-SQL-](../tutorials/sqldev-create-data-features-using-t-sql.md).

## <a name="no-support-for-encryption-at-rest"></a>Keine Unterstützung für Verschlüsselung ruhender

[Transparente datenverschlüsselung (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption) wird für die Daten gesendet oder empfangen aus der externen Skript-Laufzeit nicht unterstützt. Der Grund hierfür ist, dass R (oder Python) außerhalb von SQL Server-Prozess ausgeführt wird; Daten, die von der externen Laufzeit verwendet werden deshalb nicht durch die Verschlüsselungsfunktionen des Datenbankmoduls geschützt.  Dieses Verhalten unterscheidet sich nicht als andere Clients, die auf dem SQL Server-Computer, der liest Daten aus der Datenbank und erstellt eine Kopie, ausgeführt wird.

Daher TDE **nicht** angewendet wird, können alle Daten, die Sie in R oder Python-Skripts verwenden und alle Daten auf den Datenträger oder auf jegliche permanente Zwischenergebnisse gespeichert. Z. B. das Windows-BitLocker-Verschlüsselung oder Drittanbieter-Verschlüsselung auf der Ebene Datei- oder Ordnernamen angewendet gelten jedoch andere Arten von Verschlüsselung, weiterhin.

Im Fall von [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/overview-of-key-management-for-always-encrypted), externe Laufzeiten haben keinen Zugriff auf die Verschlüsselungsschlüssel; aus diesem Grund können keine Daten gesendet werden, an die Skripts.

## <a name="resources"></a>Ressourcen

Weitere Informationen zum Verwalten des Diensts und zum Ausführen von Machine Learning-Skripts verwendeten Benutzerkonten bereitstellen, finden Sie unter [konfigurieren und Verwalten von Advanced Analytics Extensions](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md).

Eine Erläuterung der Architektur für die allgemeine Sicherheit finden Sie unter:

+ [Übersicht über die Sicherheit für R](security-overview-sql-server-r.md)
+ [Übersicht über die Sicherheit für Python](../python/security-overview-sql-server-python-services.md)
