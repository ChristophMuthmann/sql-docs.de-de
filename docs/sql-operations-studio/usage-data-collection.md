---
title: Aktivieren oder deaktivieren Sie die Sammlung von Verwendungsdaten und Absturzberichten für SQL-Vorgänge Studio (Vorschau) | Microsoft Docs
description: In diesem Artikel wird erläutert, wie steuern, wenn die Verwendung und Absturzberichte Daten gesammelt und an Microsoft gesendet werden.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fbf952360599642497c1d7109229cba89728d61
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>Aktivieren Sie oder deaktivieren Sie der Erfassung von Nutzungsdaten für [!INCLUDE[name-sos](../includes/name-sos-short.md)]

## <a name="how-to-disable-telemetry-reporting"></a>Vorgehensweise beim Deaktivieren der Telemetrie reporting

[!INCLUDE[name-sos](../includes/name-sos-short.md)] erfasst Nutzungsdaten und sendet diese an Microsoft zur Verbesserung unserer Produkte und Dienste. Weitere Informationen finden Sie die [Datenschutzbestimmungen](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409).

Wenn Sie keine Nutzungsdaten an Microsoft senden möchten, legen Sie die *telemetry.enableTelemetry* auf *"false"*.

Zu hören alle telemetrieereignisse aus [!INCLUDE[name-sos](../includes/name-sos-short.md)], aus **Datei** > **Voreinstellungen** > **Einstellungen**, fügen Sie die folgende Option:

```json
    "telemetry.enableTelemetry": false
```

**Wichtiger Hinweis**: Diese Option erfordert einen Neustart des [!INCLUDE[name-sos](../includes/name-sos-short.md)] wirksam wird. 

## <a name="how-to-disable-crash-reporting"></a>Gewusst wie: Deaktivieren Sie die berichterstellung von Abstürzen

So deaktivieren Sie die berichterstellung von Abstürzen vom **Datei** > **Voreinstellungen** > **Einstellungen**, fügen Sie die folgende Option:

```json
    "telemetry.enableCrashReporter": false
```

**Wichtiger Hinweis**: Diese Option erfordert einen Neustart des [!INCLUDE[name-sos](../includes/name-sos-short.md)] wirksam wird.

## <a name="additional-resources"></a>Weitere Ressourcen
- [Arbeitsbereich und benutzereinstellungen](settings.md)