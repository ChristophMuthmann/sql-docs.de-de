---
title: "Identität und Zugriffssteuerung (Replikation) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- access controls [SQL Server replication]
- security [SQL Server replication], identity and access control
- authentication [SQL Server replication]
- identity [Replication]
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7773af28acb97d0d5b1d84d7ffcfc67b3595bc94
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="identity-and-access-control-replication"></a>Identität und Zugriffssteuerung (Replikation)
  Als Authentifizierung wird der Vorgang bezeichnet, bei dem eine Entität (in diesem Kontext normalerweise ein Computer) überprüft, dass eine andere Entität, die auch als *Prinzipal*bezeichnet wird (normalerweise ein anderer Computer oder Benutzer), tatsächlich das ist, was sie vorgibt. Als Autorisierung wird der Vorgang bezeichnet, bei dem einem authentifizierten Prinzipal Zugriff auf Ressourcen gewährt wird, beispielsweise auf eine Datei in einem Dateisystem oder eine Tabelle in einer Datenbank.  
  
 Für die Replikationssicherheit wird mithilfe von Authentifizierung und Autorisierung der Zugriff auf replizierte Datenbankobjekte sowie auf die Computer und Agents gesteuert, die in die Replikationsverarbeitung involviert sind. Hierzu werden drei Mechanismen herangezogen:  
  
-   Agentsicherheit  
  
     Das Sicherheitsmodell des Replikations-Agents ermöglicht die präzise Steuerung der Konten, unter denen Replikations-Agents ausgeführt werden und Verbindungen herstellen. Ausführliche Informationen zum agentbezogenen Sicherheitsmodell finden Sie unter [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md). Informationen zum Festlegen von Anmeldungen und Kennwörtern für Agents finden Sie unter [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Verwaltungsrollen  
  
     Stellen Sie sicher, dass für Replikationsinstallation, -wartung und -verarbeitung die richtigen Server- und Datenbankrollen verwendet werden. Weitere Informationen finden Sie unter [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md).  
  
-   Veröffentlichungszugriffsliste (Publication Access List, PAL)  
  
     Gewähren Sie den Zugriff auf Veröffentlichungen über die PAL. Die PAL funktioniert ähnlich wie eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Zugriffssteuerungsliste. Wenn ein Abonnent eine Verbindung mit dem Verleger oder Verteiler herstellt und den Zugriff auf eine Veröffentlichung anfordert, werden die vom Agent übermittelten Authentifizierungsinformationen anhand der PAL überprüft. Weitere Informationen und bewährte Methoden hinsichtlich der PAL finden Sie unter [Sichern des Verlegers](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## <a name="filtering-published-data"></a>Filtern von veröffentlichten Daten  
 Neben der Verwendung von Authentifizierung und Autorisierung zur Steuerung des Zugriffs auf replizierte Daten und Objekte bietet die Replikation zwei Optionen, mit denen gesteuert werden kann, welche Daten auf einem Abonnenten zur Verfügung stehen: die Filterung von Spalten und die Filterung von Zeilen. Weitere Informationen zur Filterung finden Sie unter [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md).  
  
 Bei der Definition eines Artikels können Sie lediglich die Spalten veröffentlichen, die für die Veröffentlichung relevant sind, und diejenigen auslassen, die nicht relevant sind oder vertrauliche Daten enthalten. Wenn Sie beispielsweise die **Customer** -Tabelle aus der Adventure Works-Datenbank für Vertriebsmitarbeiter im Außendienst veröffentlichen, können Sie die **AnnualSales** -Spalte auslassen, die möglicherweise nur für leitende Mitarbeiter im Unternehmen relevant ist.  
  
 Durch das Filtern von veröffentlichten Daten können Sie den Zugriff auf Daten einschränken und die Daten angeben, die auf dem Abonnenten zur Verfügung stehen. Sie können beispielsweise die **Customer** -Tabelle so filtern, dass Geschäftspartner nur die Informationen zu den Kunden erhalten, deren **ShareInfo** -Spalte den Wert "yes" aufweist. Im Fall von Mergereplikationen gelten besondere Sicherheitsüberlegungen, wenn Sie einen parametrisierten Filter verwenden, der HOST_NAME() einschließt. Weitere Informationen finden Sie im Abschnitt über das Filtern mit HOST_NAME() unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheit und Schutz &#40;Replikation&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Sicherheitsübersicht &#40;Replikation&#41;](../../../relational-databases/replication/security/security-overview-replication.md)   
 [Mindern von Bedrohungen und Sicherheitsrisiken &#40;Replication&#41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md)  
  
  
