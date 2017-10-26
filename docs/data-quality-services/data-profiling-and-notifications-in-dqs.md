---
title: Datenprofilerstellung und Benachrichtigungen in DQS | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/01/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a778bb5b-8e35-4a7b-b04a-ae2b46dec21b
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 57de348a0ce74aa33b3d19baa60116580ad30b3c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="data-profiling-and-notifications-in-dqs"></a>Datenprofilerstellung und Benachrichtigungen in DQS
  Datenprofilerstellung in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) ist der Prozess des Analysierens der Daten in einer vorhandenen Datenquelle und des Anzeigens von Statistiken zu den Daten in DQS-Aktivitäten. Sie versorgt Sie mit automatischen Messungen der Datenqualität. DQS-Profilerstellung wird in DQS-Wissensverwaltung und Data Quality-Projekte integriert. Sie ist dynamisch und anpassbar. Die Profilerstellung hat zwei Hauptziele: erstens, Sie durch Data Quality-Prozesse zu führen und Ihre Entscheidungen zu unterstützen, und zweitens, die Effektivität der Prozesse zu bewerten. Der DQS-Profilerstellungsprozess hat die folgenden Vorteile:  
  
-   Die Profilerstellung stellt einen Einblick in die Qualität der Quelldaten bereit und hilft Ihnen, Data Quality-Probleme zu identifizieren.  
  
-   Die Profilerstellung bewertet die Effektivität von Data Quality-Prozessen und leitet Sie bei der Wissensermittlung, der Datenbereinigung, der Abgleichsrichtlinie und der Abgleichsarbeit.  
  
-   Die Profilerstellung gibt Ihnen die relevantesten Informationen zum relevantesten Zeitpunkt.  
  
-   Der Profilerstellungsprozess generiert Benachrichtigungen, die wichtige Statistiken oder Ereignisse hervorheben, die möglicherweise Aktionen garantieren. In vielen Fällen geben DQS-Benachrichtigungen eine Bedingung an und empfehlen die Aktion, die Sie ergreifen können, um diese Bedingung zu beheben.  
  
 Die Profilerstellung ermöglicht es Ihnen, Data Quality Services nicht nur zur Wissensermittlung, Bereinigung und zum Abgleich zu verwenden, sondern auch als Analysetool. Möglicherweise möchten Sie eine Wissensdatenbank für die Analyse erstellen und die Wissensermittlung mithilfe dieser Wissensdatenbank ausführen, um aus den Profilerstellungsstatistiken zu bestimmen, ob die Wissensdatenbank Ihren Anforderungen für Ermittlung, Bereinigung und Abgleich gerecht wird.  
  
##  <a name="How"></a> Funktionsweise der Profilerstellung  
 Die Profilerstellung misst nicht die Qualität der Wissensdatenbank. Sie misst die Qualität der Quelldaten. Die Profilerstellung stellt Ihnen Statistiken bereit, die den Effekt des bestimmten Vorgangs angeben, den Sie in der Wissensverwaltung oder einem Data Quality-Projekt für die Quelldaten ausführen. Die Profilerstellung geschieht immer im Kontext der bestimmten Aktivität, die Sie ausführen. Sie können in einem Bildschirm auf die Profilerstellungsregisterkarte klicken, um Profilerstellungsdaten anzuzeigen, ohne die Phase der Aktivität zu verlassen, die Sie ausführen. Die Profilerstellungstabelle wird in Echtzeit aufgefüllt, während der Prozess ausgeführt wird, sodass Sie Data Quality-Aufgaben während des Ausführens bewerten können. Sie können bestimmen, ob Quelldaten nach Bereinigung oder Deduplizierung besser sind und um wie viel besser sie sind.  
  
 Alle Profilerstellungsnummern verweisen auf die Anzahl des Vorkommens eines Werts, und in vielen Fällen auf den Prozentsatz des Gesamtbetrags, mit der Ausnahme der Eindeutigkeitsmetrik. Eindeutigkeitsmetrik verweist auf die absolute Anzahl von Werten, unabhängig davon, wie häufig diese Werte vorkommen.  
  
 Die Profilerstellung ist Teil des wissensgesteuerten DQS-Lösung. Sie stellt Informationen zu einer Wissensdatenbank, einem Abgleichs- oder einem Datenbereinigungsprozess basierend auf der Zuordnung zwischen Datenquellenfeldern und Wissensdatenbankdomänen bereit. Die Profilerstellung wird nur ausgeführt, nachdem die Zuordnung vollständig ist; während der Zuordnungsphase einer Aktivität wird keine Profilerstellung ausgeführt. Die Profilerstellung wird immer an eine Aktivität angefügt. Der Profilerstellungsprozess wird für die Daten ausgeführt, die Domänen zugeordnet sind, nicht für die Daten in den Domänen. Die Profilerstellung wird in die folgenden Schritte von Aktivitäten integriert:  
  
-   In die Schritte **Ermitteln** und **Domänenwerte verwalten** der Wissensermittlungsaktivität  
  
-   In die Schritte **Bereinigen** und **Ergebnisse verwalten und anzeigen** der Bereinigungsaktivität  
  
-   In die Schritte **Abgleichsrichtlinie** und **Abgleichsergebnisse** der Abgleichsrichtlinienaktivität  
  
-   In die Schritte **Abgleich** und **Exportieren** der Abgleichsaktivität  
  
 DQS stellt keine Profilerstellungsstatistiken für die Domänenverwaltungsaktivität bereit.  
  
##  <a name="Activity"></a> Profilerstellungsdaten nach Aktivität  
 DQS-Profilerstellung verwendet standardmäßige Data Quality-Dimensionen, um die Qualität der Daten darzustellen: Vollständigkeit (das Ausmaß des Vorhandenseins von Daten), Genauigkeit (das Ausmaß, in dem Daten für den beabsichtigten Zweck verwendet werden können) und Eindeutigkeit (das Ausmaß, in dem verschiedene Werte verschiedene Entitäten darstellen). Standardmäßig werden NULL-Werte und leere Werte als fehlend betrachtet oder verringern den Vollständigkeitsprozentsatz. Sie können jedoch auch andere Werte so definieren, dass sie NULL entsprechen. In diesem Fall werden sie ebenfalls als fehlend betrachtet.  
  
 Die Profilerstellung stellt Ihnen die Statistiken bereit, die Sie benötigen, um die Prozesse zu bewerten. Die Statistiken müssen Sie allerdings interpretieren. Verstehen Sie, was Ihnen die Profilerstellung mitteilt, indem Sie sich die Statistiken spaltenweise ansehen.  
  
 Die DQS-Aktivitäten verfügen über andere Sätze von Profilerstellungsstatistiken, nämliche folgende:  
  
-   Nur die Bereinigungsaktivität weist Profilerstellungsstatistiken für Genauigkeit (in Prozent nach Domäne) auf. Genauigkeit wird durch Gültigkeit, Konsistenz, Syntaxfehler und Domänenregeln beeinflusst.  
  
-   Nur die Bereinigungsaktivität weist Profilerstellungsstatistiken für richtig, korrigiert und vorgeschlagen in der Quelle sowie für korrigierte und vorgeschlagene Werte nach Domäne (Zahlen und Prozentwerte) auf.  
  
-   Die Bereinigungs und Wissensermittlungsaktivitäten weisen Profilerstellungsstatistiken für Gültigkeit (Reinigen nach Datensatz, Wissensermittlung nach Datensatz und Domäne) auf. Die Abgleichsrichtlinie und die Abgleichsaktivitäten weisen keine Statistiken für Gültigkeit auf.  
  
-   Die Bereinigungsaktivität weist keine Profilerstellungsstatistiken für Eindeutigkeit auf. Die Wissensermittlungs-, Abgleichsrichtlinien- und Abgleichsaktivitäten weisen Profilerstellungsstatistiken für Eindeutigkeit in Zahlen und Prozent für die Quelle und die Domäne auf.  
  
 Weitere Informationen zu den speziellen Profilerstellungsstatistiken, die sich auf eine Aktivität beziehen, finden Sie in den Abschnitten zur Profilerstellung in den folgenden Themen:  
  
-   [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [Bereinigen von Daten mit &#40;internem&#41; DQS-Wissen](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md)  
  
-   [Ausführen eines Abgleichsprojekts](../data-quality-services/run-a-matching-project.md)  
  
##  <a name="Monitoring"></a> Profilerstellungsdaten bei der Aktivitätsüberwachung  
 Profilerstellungsinformationen für die Wissensermittlungs, Abgleichsrichtlinien-, Abgleichs- und Bereinigungsaktivitäten sind nicht nur auf den Aktivitätsseiten im Data Quality-Client verfügbar, sondern auch bei der Aktivitätsüberwachung. Die Aktivitätsüberwachung stellt Ihnen eine Übersicht über aktuelle und vergangene Aktivitäten bereit. Zusätzlich zu den Eigenschaften und verknüpften Berechnungsprozessen von Aktivitäten können Sie die für jede Aktivität an einem Speicherort generierten Profilerstellungsinformationen anzeigen. Sie wählen eine Aktivität in der Aktivitätstabelle aus, um Profilerstellungsergebnisse in einer Tabelle weiter unten anzuzeigen. Sie können die Profilerstellungsergebnisse auch exportieren. Weitere Informationen finden Sie unter [DQS Administration](../data-quality-services/dqs-administration.md).  
  
##  <a name="Notifications"></a> Benachrichtigungen  
 Zusätzlich zum Sammeln und Anzeigen von wichtigen Statistiken und wichtiger Metrik durch die Profilerstellung generiert DQS Benachrichtigungen (wenn aktiviert), um anzugeben, wann Sie auf Grundlage der angezeigten Profilerstellungsstatistiken eine Aktion ausführen können. DQS hebt wichtige Fakten zur Datenquelle und die Effektivität der aktuellen Aktivität relativ zum Zweck, für den sie ausgeführt wurde, mithilfe von Benachrichtigungen hervor. Benachrichtigungen stellen Tipps und Empfehlungen bereit, die eine Bedingung angeben und empfehlen, wie Sie eine Wissensermittlungs-, Datenbereinigungs- oder Datenabgleichsaktivität verbessern können.  
  
 Eine DQS-Benachrichtigung wird verwendet, um ein Problem auszulösen, das Sie möglicherweise interessiert, oder um ein potenzielles Problem zu behandeln. Ob Sie auf die Benachrichtigung reagieren, hängt davon ab, ob sie für Ihre Zwecke relevant ist. Nehmen Sie zum Beispiel an, dass DQS eine Benachrichtigung ausgibt, wenn die Datenbereinigung keine korrigierten Werte oder vorgeschlagenen Werte erzeugt, während Vollständigkeit und Genauigkeit beide bei 100 % sind. Diese Benachrichtigung würde angeben, dass die Aktivität möglicherweise nicht ausgeführt werden muss. Ob Sie die Aktivität ausführen, ist jedoch Ihre Entscheidung.  
  
 Eine Benachrichtigung wird von einer QuickInfo mit einem Ausrufezeichen auf der Registerkarte **Profilerstellung** angegeben. Der Benachrichtigung zugeordnete Statistiken werden rot dargestellt, um die statistische Rechtfertigung für die Benachrichtigung anzugeben.  
  
 Sie können Benachrichtigungen auf der Registerkarte **Allgemeine Einstellungen** des Abschnitts **Verwaltung** der Data Quality-Clientstartseite aktivieren (Standard) oder deaktivieren. Wenn die Benachrichtigung deaktiviert wird, werden keine QuickInfos angezeigt, und Statistiken werden nicht rot dargestellt. Durch das Deaktivieren von Benachrichtigungen entsteht keine deutliche Leistungsverbesserung. Die Profilerstellung ist immer noch funktionstüchtig, wenn Sie Benachrichtigungen deaktivieren.  
  
 Informationen zu bestimmten Bedingungen, die Benachrichtigungen für eine Aktivität zugeordnet sind, finden Sie hier:  
  
-   [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md)  
  
-   [Bereinigen von Daten mit &#40;internem&#41; DQS-Wissen](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
-   [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md)  
  
-   [Ausführen eines Abgleichsprojekts](../data-quality-services/run-a-matching-project.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie Benachrichtigungen in DQS aktiviert und deaktiviert werden.|[Aktivieren oder Deaktivieren von Profilerstellungsbenachrichtigungen in DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
  
  

