---
title: "&#220;berlegungen zur Sicherheit der R-Laufzeitumgebung in SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# &#220;berlegungen zur Sicherheit der R-Laufzeitumgebung in SQL Server
  Dieses Thema bietet eine Übersicht über Sicherheitsaspekte für die Arbeit mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Weitere Informationen zum Verwalten des Dienstes und dazu, wie Sie die Benutzerkonten, die zum Ausführen von R-Skripts bereitstellen, finden Sie unter [Konfigurieren und Verwalten von Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md).  
  
## Verwenden der Firewall zur Beschränkung des Netzwerkzugriffs mit R  
 Bei der empfohlenen Installationsmethode wird eine Windows-Firewallregel dazu verwendet, alle ausgehenden Netzwerkzugriffe durch R-Laufzeitprozesse zu blockieren. Firewallregeln sollten erstellt werden, um den R-Laufzeitprozess daran zu hindern, Pakete herunterzuladen oder andere Netzwerke aufzurufen, die potenziell böswillig sein können.  
  
 Wir empfehlen Ihnen nachdrücklich, die Windows-Firewall zu aktivieren (oder eine andere Firewall Ihrer Wahl), um den Netzwerkzugriff durch R-Laufzeitprozesse zu blockieren.  
  
 Wenn Sie ein anderes Firewallprogramm verwenden, können Sie ebenfalls Regeln erstellen, um ausgehende Netzwerkverbindungen für die R-Laufzeit zu blockieren. Sie erreichen dies, indem Sie Regeln für die lokalen Benutzerkonten oder für die durch den Benutzerkontenpool dargestellte Gruppe festlegen.   
Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md).  
  
## Für Remote Compute Kontexte unterstützten Authentifizierungsmethoden 
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] unterstützt jetzt die integrierte Windows-Authentifizierung und SQL-Anmeldungen, beim Erstellen von Verbindungen zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und eine remote Data Science-Client. 
  
 Z. B. Wenn Sie eine R-Lösung auf Ihrem Laptop entwickeln und Berechnungen für die SQL Server-Computer ausführen möchten, Sie würden erstellen eine SQL Server-Datenquelle in R mithilfe der **Rx** Funktionen und eine Verbindungszeichenfolge definieren basierend auf Ihren Windows-Anmeldeinformationen. Wenn Sie ändern die _Kontext compute_ auf einem Laptop zu SQL Server-Computers, wenn Ihr Windows-Konto die erforderlichen Berechtigungen hat alle R-Code wird ausgeführt werden auf dem SQL Server-Computer. Darüber hinaus werden alle SQL-Abfragen als Teil der R-Code ausgeführt unter als auch Ihre Anmeldeinformationen ausgeführt werden. 
 
 Obwohl eine SQL-Anmeldung auch in der Verbindungszeichenfolge für eine SQL Server-Datenquelle verwendet werden kann, benötigen Sie eine Anmeldung, dass der SQL Server-Instanz Authentifizierung im gemischten Modus zu ermöglichen.
 
 ### Implizite Authentifizierung
  
 Im Allgemeinen die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] startet die Laufzeit R und R-Skripts unter ihrem eigenen Konto ausgeführt. Jedoch, wenn das R-Skript einen ODBC-Aufruf wird die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] nimmt die Identität der Anmeldeinformationen des Benutzers, der den Befehl aus, um sicherzustellen, dass der ODBC-Aufruf nicht fehlschlägt gesendet. Dies wird als *implizite Authentifizierung*. 
 
 > [!IMPORTANT] 
 >
 > Für die implizite Authentifizierung erfolgreich ist, handelt es sich bei der Windows-Benutzergruppe, die die Konten enthält (standardmäßig **SQLRUser**) ist ein Konto in der master-Datenbank für die Instanz, und dieses Konto muss Berechtigungen für die Verbindung mit der Instanz zugewiesen werden.  
  
## Keine Unterstützung für Verschlüsselung von ruhenden Daten  
 Transparente Datenverschlüsselung wird nicht für an die R-Laufzeit gesendete oder von der R-Laufzeit empfangene Daten unterstützt. Demzufolge ruhende **nicht** angewendet werden, auf die Daten, die auf R-Skripts keine Daten auf Datenträger oder alle beibehaltenen Zwischenergebnisse gespeichert.  
 
 ## Siehe auch
 [Geben Sie hier die linkbeschreibung](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 
  