---
title: "Editor für den Datenprofilerstellungs-Task (Seite „Profilanforderungen“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataprofilingtask.profilerequests.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c72acb3d-380e-436e-8041-ed364eddfabd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e6883b8ec802392c0ae4d3a92a41f54433d403f8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="data-profiling-task-editor-profile-requests-page"></a>Editor für den Datenprofilerstellungs-Task (Seite 'Profilanforderungen')
  Verwenden Sie die Seite **Profilanforderungen** im **Editor für den Datenprofilerstellungs-Task** , um die Profile auszuwählen und zu konfigurieren, die Sie berechnen möchten. In einem Datenprofilerstellungs-Task können Sie mehrere Profile für mehrere Spalten oder Kombinationen von Spalten in mehreren Tabellen oder Sichten berechnen.  
  
 Weitere Informationen zum Verwenden des Datenprofilerstellungs-Tasks finden Sie unter [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Weitere Informationen zum Verwenden des Datenprofil-Viewers zum Analysieren der Ausgabe des Datenprofilerstellungs-Tasks finden Sie unter [Datenprofil-Viewer](../../integration-services/control-flow/data-profile-viewer.md).  
  
 **So öffnen Sie die Seite 'Profilanforderungen' des Editors für den Datenprofilerstellungs-Task**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, das den Datenprofilerstellungs-Task enthält.  
  
2.  Doppelklicken Sie auf der Registerkarte **Ablaufsteuerung** auf den Datenprofilerstellungs-Task.  
  
3.  Klicken Sie im **Editor für den Datenprofilerstellungs-Task**auf **Profilanforderungen**.  
  
## <a name="using-the-requests-pane"></a>Verwenden des Anforderungsbereichs  
 Der Anforderungsbereich ist der Bereich, der oben auf der Seite angezeigt wird. In diesem Bereich werden alle Profile aufgelistet, die für den aktuellen Datenprofilerstellungs-Task konfiguriert wurden. Wenn keine Profile konfiguriert wurden, ist der Anforderungsbereich leer. Um ein neues Profil hinzuzufügen, klicken Sie in einen leeren Bereich unter der Spalte **Profiltyp** , und wählen Sie einen Profiltyp aus der Liste aus. Zum Konfigurieren eines Profils wählen Sie das Profil im Anforderungsbereich aus und legen dann die Eigenschaften des Profils im Bereich **Anforderungseigenschaften** fest.  
  
### <a name="requests-pane-options"></a>Optionen im Anforderungsbereich  
 Der Anforderungsbereich enthält die folgenden Optionen:  
  
 **Ansicht**  
 Wählen Sie aus, ob alle für den Task konfigurierten Profile oder nur eines der Profile angezeigt werden soll.  
  
 Die Spalten im Anforderungsbereich haben sich je nach der ausgewählten **Sicht** geändert. Weitere Informationen über jede dieser Spalten finden Sie im nächsten Abschnitt, "Spalten im Anforderungsbereich".  
  
### <a name="requests-pane-columns"></a>Spalten im Anforderungsbereich  
 Welche Spalten im Anforderungsbereich angezeigt werden, hängt von der **Sicht** ab, die Sie ausgewählt haben:  
  
-   Wenn Sie **Alle Anforderungen**auswählen, enthält der Anforderungsbereich zwei Spalten: **Profiltyp** und **Anforderungs-ID**.  
  
-   Wenn Sie die Sicht eines der fünf Spaltenprofile wählen, enthält der Anforderungsbereich vier Spalten: **Profiltyp**, **Tabelle oder Sicht**, **Spalte**und **Anforderungs-ID**.  
  
-   Wenn Sie die Sicht eines Kandidatenschlüsselprofils auswählen, enthält der Anforderungsbereich vier Spalten: **Profiltyp**, **Tabelle oder Sicht**, **Schlüsselspalten**und **Anforderungs-ID**.  
  
-   Wenn Sie ein funktionales Abhängigkeitsprofil anzeigen, enthält der Anforderungsbereich fünf Spalten: **Profiltyp**, **Tabelle oder Sicht**, **Bestimmende Spalten**, **Abhängige Spalte**und **Anforderungs-ID**.  
  
-   Wenn Sie ein Wertanschlussprofil anzeigen, enthält der Anforderungsbereich sechs Spalten: **Profiltyp**, **Untergeordnete Tabelle oder Sicht**, **Übergeordnete Tabelle oder Sicht**, **Untergeordnete Spalten**, **Übergeordnete Spalten**und **Anforderungs-ID**.  
  
 In den folgenden Abschnitten wird jede dieser Spalten beschrieben.  
  
#### <a name="columns-common-to-all-views"></a>Spalten, die allen Sichten gemeinsam sind  
 **Profiltyp**  
 Wählen Sie ein Datenprofil aus folgenden Optionen:  
  
|value|Description|  
|-----------|-----------------|  
|**Anforderung für Kandidatenschlüsselprofil**|Berechnen Sie ein Kandidatenschlüsselprofil.<br /><br /> Dieses Profil meldet, ob eine Spalte oder eine Gruppe von Spalten ein Schlüssel oder ein ungefährer Schlüssel für die ausgewählte Tabelle ist. Dieses Profil hilft Ihnen auch, Probleme bei den Daten zu identifizieren, z. B. doppelte Werte in einer potenziellen Schlüsselspalte.|  
|**Anforderung für Verteilungsprofil für Spaltenlänge**|Berechnen Sie ein Verteilungsprofil für Spaltenlänge.<br /><br /> Das Verteilungsprofil für Spaltenlänge dokumentiert alle eindeutigen Längen von Zeichenfolgenwerten in der ausgewählten Spalte sowie den Prozentsatz der Zeilen in der Tabelle, die jede Länge darstellt. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. Werte, die nicht gültig sind. Beispiel: Sie erstellen ein Profil einer Spalte mit den Codes der US-amerikanischen Bundesstaaten, die zwei Zeichen lang sind, und entdecken Werte, die länger als zwei Zeichen sind.|  
|**Anforderung für Profil für NULL-Verhältnis der Spalte**|Berechnen Sie ein Profil für NULL-Verhältnis der Spalte.<br /><br /> Das Profil für NULL-Verhältnis der Spalte dokumentiert den Prozentwert der NULL-Werte in der ausgewählten Spalte. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. ein unerwartet hohes Verhältnis an NULL-Werten in einer Spalte. Beispiel: Sie erstellen ein Profil der Spalte für die Postleitzahl und entdecken einen unerwartet hohen Prozentsatz an fehlenden Codes.|  
|**Anforderung für Spaltenmusterprofil**|Berechnen Sie ein Spaltenmusterprofil.<br /><br /> Das Spaltenmusterprofil meldet einen Satz von regulären Ausdrücken, die den angegebenen Prozentsatz der Werte in einer Zeichenfolgenspalte abdecken. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. ungültige Zeichenfolgen. Dieses Profil kann außerdem reguläre Ausdrücke vorschlagen, die künftig zur Überprüfung neuer Werte verwendet werden können. Beispiel: Ein Musterprofil einer Spalte mit Postleitzahlen kann folgende reguläre Ausdrücke erstellen: \d{5}-\d{4}, \d{5} und \d{9}. Wenn Sie andere reguläre Ausdrücke erhalten, enthalten Ihre Daten wahrscheinlich ungültige oder falsch formatierte Werte.|  
|**Anforderung für Spaltenstatistikprofil**|Wählen Sie diese Option, um anhand der Standardeinstellungen für alle anwendbaren Spalten in der ausgewählten Tabelle oder Sicht ein Spaltenstatistikprofil zu berechnen.<br /><br /> Das Spaltenstatistikprofil meldet Statistiken, wie minimale, maximale, durchschnittliche und standardmäßige Abweichung für numerische Spalten und den Mindest- und Höchstwert für **datetime** -Spalten. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. ungültige Datumsangaben. Beispiel: Sie erstellen ein Profil einer Spalte mit historischen Daten und entdecken einen Maximalwert, der in der Zukunft liegt.|  
|**Anforderung für Verteilungsprofil für Spaltenwert**|Berechnen Sie ein Verteilungsprofil für Spaltenwert.<br /><br /> Das Verteilungsprofil für Spaltenwert dokumentiert alle eindeutigen Längen von Zeichenfolgenwerten in der ausgewählten Spalte sowie den Prozentsatz der Zeilen in der Tabelle, die jeder Wert darstellt. Dieses Profil kann auch Werte melden, die mehr als einen angegebenen Prozentwert in der Tabelle darstellen. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. eine falsche Anzahl eindeutiger Werte in einer Spalte. Beispiel: Sie erstellen ein Profil einer Spalte, die die US-amerikanischen Bundesstaaten enthält, und entdecken mehr als 50 eindeutige Werte.|  
|**Anforderung für funktionales Abhängigkeitsprofil**|Berechnen Sie ein funktionales Abhängigkeitsprofil.<br /><br /> Das funktionale Abhängigkeitsprofil dokumentiert das Ausmaß, in dem die Werte in einer Spalte (der abhängigen Spalte) von den Werten in einer anderen Spalte oder einer Gruppe von Spalten (der determinanten Spalte) abhängen. Dieses Profil hilft Ihnen auch, Probleme mit den Daten zu identifizieren, z. B. ungültige Werte. Beispiel: Sie erstellen ein Profil der Abhängigkeit zwischen einer Spalte mit US-amerikanischen Postleitzahlen und einer Spalte mit US-amerikanischen Bundesstaaten. Die gleiche Postleitzahl sollte immer denselben Bundesstaat aufweisen, doch das Profil entdeckt Verstöße gegen dieses Abhängigkeitsverhältnis.|  
|**Anforderung für Wertinklusionsprofil**|Berechnen Sie ein Wertinklusionsprofil.<br /><br /> Das Wertinklusionsprofil berechnet die Überschneidung in den Werten zwischen zwei Spalten oder Gruppen von Spalten. Dieses Profil kann auch ermitteln, ob eine Spalte oder eine Gruppe von Spalten geeignet ist, um als Fremdschlüssel zwischen den ausgewählten Tabellen zu fungieren. Dieses Profil hilft Ihnen auch, Probleme mit den Daten zu identifizieren, z. B. ungültige Werte. Beispiel: Sie erstellen ein Profil der Spalte ProductID einer Vertriebstabelle und stellen fest, dass die Spalte Werte enthält, die nicht in der Spalte ProductID der Produkttabelle enthalten sind.|  
  
 **RequestID**  
 Zeigt den Bezeichner für die Anforderung an. In der Regel müssen Sie den automatisch generierten Wert nicht ändern.  
  
#### <a name="columns-common-to-all-individual-profiles"></a>Spalten, die allen einzelnen Profilen gemeinsam sind  
 **Verbindungs-Manager**  
 Zeigt den [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager an, der eine Verbindung mit der Quelldatenbank herstellt.  
  
 **Anforderungs-ID**  
 Zeigt einen Bezeichner für die Anforderung an. In der Regel müssen Sie den automatisch generierten Wert nicht ändern.  
  
#### <a name="columns-common-to-the-five-individual-column-profiles"></a>Spalten, die den fünf einzelnen Spaltenprofilen gemeinsam sind  
 **Tabelle oder Sicht**  
 Zeigt die Tabelle oder Sicht an, die die ausgewählte Spalte enthält.  
  
 **Spalte**  
 Zeigt die für die Profilerstellung ausgewählte Spalte an.  
  
#### <a name="columns-specific-to-the-candidate-key-profile"></a>Spezifische Spalten des Kandidatenschlüsselprofils  
 **Tabelle oder Sicht**  
 Zeigt die Tabelle oder Sicht an, die die ausgewählten Spalten enthält.  
  
 **Schlüsselspalten**  
 Zeigt die für die Profilerstellung ausgewählten Spalten an.  
  
#### <a name="columns-specific-to-the-functional-dependency-profile"></a>Spezifische Spalten des funktionalen Abhängigkeitsprofils  
 **Tabelle oder Sicht**  
 Zeigt die Tabelle oder Sicht an, die die ausgewählten Spalten enthält.  
  
 **Bestimmende Spalten**  
 Zeigt die Spalten an, die für die Profilerstellung als determinante Spalte(n) ausgewählt wurden. In dem Beispiel, in die US-amerikanische Postleitzahl den US-Bundesstaat festlegt, ist die Spalte mit den Postleitzahlen die determinante Spalte.  
  
 **Dependent column**  
 Zeigt die Spalte an, die für die Profilerstellung als abhängige Spalte ausgewählt wurde. In dem Beispiel, in dem die US-amerikanische Postleitzahl den US-Bundesstaat festlegt, ist die Spalte mit dem Bundesstaat die abhängige Spalte.  
  
#### <a name="columns-specific-to-the-value-inclusion-profile"></a>Spezifische Spalten des Wertinklusionsprofils  
 **Untergeordnete Tabelle oder Sicht**  
 Zeigt die Tabelle oder die Sicht an, die die Spalte oder Spalten enthält, die als untergeordnete Spalten ausgewählt wurden.  
  
 **Übergeordnete Tabelle oder Sicht**  
 Zeigt die Tabelle oder die Sicht an, die die Spalte oder Spalten enthält, die als übergeordnete Spalten ausgewählt wurden.  
  
 **Untergeordnete Spalten**  
 Zeigt die Spalte oder Spalten an, die für die Profilerstellung als untergeordnete Spalten ausgewählt wurden. In dem Beispiel, in dem Sie prüfen möchten, dass die Werte in einer Spalte mit US-Bundesstaaten in einer Verweistabelle mit aus zwei Zeichen bestehenden Codes für US-Bundesstaaten gefunden werden, ist die untergeordnete Spalte die Spalte mit den Bundesstaaten in der Quelltabelle.  
  
 **Übergeordnete Spalten**  
 Zeigt die Spalte oder Spalten an, die für die Profilerstellung als übergeordnete Spalten ausgewählt wurden. In dem Beispiel, in dem Sie prüfen möchten, dass die Werte in einer Spalte mit US-Bundesstaaten in einer Verweistabelle mit aus zwei Zeichen bestehenden Codes für US-Bundesstaaten gefunden werden, ist die übergeordnete Spalte die Spalte mit den Bundesstaatencodes in der Verweistabelle.  
  
## <a name="using-the-request-properties-pane"></a>Verwenden des Bereichs 'Anforderungseigenschaften'  
 Der Bereich **Anforderungseigenschaften** wird unter dem Anforderungsbereich angezeigt. Dieser Bereich zeigt die Optionen für das Profil an, das Sie im Anforderungsbereich ausgewählt haben.  
  
> [!NOTE]  
>  Wenn Sie einen **Profiltyp**ausgewählt haben, müssen Sie das Feld **Anforderungs-ID** auswählen, um die Eigenschaften für die Profilanforderung im Bereich **Anforderungseigenschaften** anzuzeigen.  
  
 Diese Optionen hängen vom ausgewählten Profil ab. Informationen zu den Optionen für einzelne Profiltypen finden Sie in den folgenden Themen:  
  
-   [Optionen für die Anforderung für Kandidatenschlüsselprofil &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [Optionen für die Anforderung für Profil für NULL-Verhältnis der Spalte &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [Optionen für die Anforderung für Spaltenstatistikprofil &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [Optionen für Anforderung für Verteilungsprofil für Spaltenwert &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Optionen für Anforderung für Verteilungsprofil für Spaltenlänge &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Optionen für die Anforderung für Spaltenmusterprofil &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [Optionen für die Anforderung für funktionales Abhängigkeitsprofil &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [Optionen für Anforderung für Wertinklusionsprofil &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Editor für den Datenprofilerstellungs-Task &#40;Seite "Allgemein"&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Schnellprofilformular für eine einzelne Tabelle &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
