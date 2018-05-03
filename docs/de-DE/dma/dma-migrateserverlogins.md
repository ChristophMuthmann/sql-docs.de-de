---
title: Migrieren von SQL Server-Anmeldungen (Data Migration Assistant) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 5e4a84b40563b67142170ab65bf38da62ea086a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-sql-server-logins-using-data-migration-assistant"></a>Migrieren von SQL Server-Anmeldungen, die mithilfe des Migrations-Assistenten Daten

Dieser Artikel enthält einen Überblick über die Migration von SQL Server-Anmeldungen, die mit dem Daten Migrations-Assistenten. 

## <a name="key-concepts"></a>Wichtige Konzepte
Im folgenden werden die grundlegenden Konzepte.

- Sie können die Anmeldungen auf Grundlage eines Windows-Prinzipals (z. B. ein Domänenbenutzer oder eine Windows-Domänengruppe) migrieren. Sie können auch basierend auf SQL Server-Anmeldungen so genannte SQL-Authentifizierung erstellte Anmeldungen migrieren.

- Daten-Migrations-Assistent unterstützt derzeit nicht die Benutzernamen, einem eigenständigen Sicherheitszertifikat (Anmeldungen zugeordnet zu Zertifikat), einem eigenständigen asymmetrischen Schlüssel (Anmeldungen zugeordnet zu asymmetrischem Schlüssel) und Anmeldenamen zugeordnet zu Anmeldeinformationen zugeordnet.

- Data Migration Assistant nicht verschieben der **sa** Anmelde- und Server Prinzipien, deren Name von doppelten Nummernzeichen eingeschlossen (\#\#), die sind nur zur internen Verwendung.

- Standardmäßig wählt Daten Migration Assistatn alle qualifizierten Benutzernamen zu migrieren. Optional können Sie die spezifische Anmeldungen Migration auswählen. Wenn Daten Migration Assistant alle qualifizierte Benutzernamen migriert wird, bleiben die Zuordnung für die Anmeldung für Benutzer in den Datenbanken, die migriert werden. 

  Wenn Sie die spezifische Anmeldungen migrieren möchten, stellen Sie sicher, um die Anmeldenamen auszuwählen, die einen oder mehrere Benutzer in den Datenbanken, die für die Migration ausgewählt zugeordnet sind.

- Im Rahmen der Anmeldung Migration Data Migration Assistant außerdem verschiebt benutzerdefinierte Serverrollen und Berechtigungen auf Serverebene, die eine benutzerdefinierte Serverrollen hinzugefügt. Der Besitzer der Rolle festgelegt, um **sa** Prinzipal.

- Im Rahmen der Anmeldung Migration weist Data Migration Assistant die Berechtigungen auf sicherungsfähige Elemente auf dem SQL-Zielserver wie sie auf dem Quellserver mit SQL Server vorhanden sind. 

  Wenn die Anmeldung auf dem SQL-Zielserver bereits vorhanden ist, Data Migration Assistant migriert nur die Berechtigungen für sicherungsfähige Elemente und die gesamte Anmeldung nicht neu erstellt wird.

- Daten-Migrations-Assistent macht die bemüht sich, das Datenbankbenutzern die Anmeldung zuzuordnen, wenn die Anmeldung auf dem Zielserver bereits vorhanden ist.

- Es wird empfohlen, dass Sie die Migrationsergebnisse zum Verständnis des Gesamtstatus der Migration für die Anmeldung und alle empfohlenen Aktionen in der nach der Migration überprüfen.

## <a name="resources"></a>Ressourcen

[Daten-Migrations-Assistenten (DMA)](../dma/dma-overview.md)

[Assistent für die Migration von Daten: Konfigurationseinstellungen](../dma/dma-configurationsettings.md)
