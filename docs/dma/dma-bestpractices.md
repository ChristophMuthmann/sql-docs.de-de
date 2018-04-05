---
title: Bewährte Methoden für das Data Migration Assistant (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8842ca064494bc7ead99eb34d6ea2cc76bb2679
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Bewährte Methoden für die Ausführung von Data-Migrations-Assistent
Dieser Artikel enthält die folgenden best Practice-Informationen für die Installation, Bewertungen und Migration.

## <a name="installation"></a>Installation

Installieren Sie nicht, und führen Sie direkt auf dem SQL Server-Hostcomputer Data Migration Assistant.

## <a name="assessment"></a>Bewertung

- Führen Sie Bewertungen für Produktionsdatenbanken während Zeiten geringer Netzwerkverwendung.

- Führen Sie die **Kompatibilitätsprobleme** und **neue Funktion Empfehlungen** Bewertungen für die Reduzierung der Dauer Assessment einzeln.

## <a name="migration"></a>Migration

- Migrieren eines Servers während Zeiten geringer Netzwerkverwendung.

- Beim Migrieren einer Datenbank geben Sie einen einzelnen Netzwerkfreigabe, die vom Quellserver und Zielserver zugegriffen werden kann, und eines Kopiervorgangs vermeiden Sie nach Möglichkeit. Ein Vorgang zum Kopieren kann basierend auf der Größe der Sicherungsdatei Verzögerung führen. Der Kopiervorgang auch steigt die Wahrscheinlichkeit, einer Migration aufgrund ein zusätzlicher Schritt fehlschlägt. Bei ein zentralen Ort bereitgestellt wird, umgeht Data Migration Assistant den Kopiervorgang.
 
    Auch Achten Sie darauf, geben Sie die korrekten Berechtigungen für den freigegebenen Ordner, um Migrationsfehler zu vermeiden. Die richtigen Berechtigungen werden im Tool angegeben. Wenn SQL Server-Instanz unter Network Service Anmeldeinformationen ausgeführt wird, geben Sie die richtigen Berechtigungen für den freigegebenen Ordner auf das Computerkonto für den SQL Server-Instanz.

- Verbindung verschlüsseln aktivieren, bei der Verbindung von Quell-und Ziel. Verwendung von SSL-Verschlüsselung erhöht die Sicherheit der Daten, die netzwerkübergreifend zwischen Data Migration Assistant und SQL Server-Instanz. Dies ist auch hilfreich, besonders bei der Migration von SQL-Anmeldungen. Wenn keine SSL-Verschlüsselung verwendet wird, und das Netzwerk von einem Angreifer gefährdet ist, wird die SQL-Anmeldungen, die zu migrierenden konnte abgefangen abrufen und/oder auf dynamisch von der Angreifer geändert.

    Wenn sich aber der gesamte Zugriff innerhalb einer sicheren Intranetkonfiguration abspielt, ist eine Verschlüsselung möglicherweise nicht erforderlich. Aktivieren der Verschlüsselung durch die die Leistung aufgrund des zusätzlichen Verarbeitungsaufwand zum Verschlüsseln und Entschlüsseln von Paketen. Weitere Informationen finden Sie auf [Verschlüsseln von Verbindungen zu SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
