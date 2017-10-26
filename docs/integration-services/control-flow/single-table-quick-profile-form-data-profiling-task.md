---
title: Single Table Schnellprofil Form (Datenprofilerstellungs-Task) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataprofilingtask.quickprofile.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: d2fac9ce-730e-474e-961a-69406b633778
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 76de0987bec5d7886b41d2d415af2bd00e187f87
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="single-table-quick-profile-form-data-profiling-task"></a>Schnellprofilformular für eine einzelne Tabelle (Datenprofilerstellungs-Task)
  Verwenden Sie das **Schnellprofilformular für eine einzelne Tabelle** , um den Datenprofilerstellungs-Task schnell mithilfe der Standardeinstellungen so zu konfigurieren, dass er ein Profil für eine einzelne Tabelle oder Sicht erstellt.  
  
 Weitere Informationen zum Verwenden des Datenprofilerstellungs-Tasks finden Sie unter [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Weitere Informationen zum Verwenden des Datenprofil-Viewers zum Analysieren der Ausgabe des Datenprofilerstellungs-Tasks finden Sie unter [Datenprofil-Viewer](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="options"></a>enthalten  
 **Verbindung**  
 Wählen Sie einen vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager aus, der den .NET-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) verwendet, um eine Verbindung zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herzustellen, die die Tabelle oder Sicht enthält, für die ein Profil erstellt werden soll.  
  
 **Tabelle oder Sicht**  
 Wählen Sie eine vorhandene Tabelle oder Sicht in der Datenbank aus, mit der der ausgewählte Verbindungs-Manager eine Verbindung herstellt.  
  
 **Compute**  
 Wählen Sie aus, welche Profile berechnet werden sollen.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**Profil für Spalten-NULL-Verhältnis**|Berechnen Sie ein Profil für Spalten-NULL-Verhältnis anhand der Standardeinstellungen für alle anwendbaren Spalten in der ausgewählten Tabelle oder Sicht.<br /><br /> Dieses Profil meldet den Prozentwert der NULL-Werte in der ausgewählten Spalte. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. ein unerwartet hohes Verhältnis an NULL-Werten in einer Spalte. Weitere Informationen zu den Einstellungen für dieses Profil finden Sie unter [Optionen für die Anforderung für Profil für NULL-Verhältnis der Spalte &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md).|  
|**Spaltenstatistikprofil**|Berechnen Sie ein Spaltenstatistikprofil anhand der Standardeinstellungen für alle anwendbaren Spalten in der ausgewählten Tabelle oder Sicht.<br /><br /> Dieses Profil meldet Statistiken, wie minimale, maximale, durchschnittliche und standardmäßige Abweichung für numerische Spalten und den Mindest- und Höchstwert für **datetime** -Spalten. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. ungültige Datumsangaben. Weitere Informationen zu den Einstellungen für dieses Profil finden Sie unter [Optionen für die Anforderung für Spaltenstatistikprofil &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md).|  
|**Verteilungsprofil für Spaltenwerte**|Berechnen Sie ein Verteilungsprofil für Spaltenwerte anhand der Standardeinstellungen für alle anwendbaren Spalten in der ausgewählten Tabelle oder Sicht.<br /><br /> Dieses Profil meldet alle eindeutigen Werte in der ausgewählten Spalte sowie den Prozentsatz der Zeilen in der Tabelle, die jeder Wert repräsentiert. Dieses Profil kann auch Werte melden, die mehr als einen angegebenen Prozentwert der Zeilen in der Tabelle darstellen. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. eine falsche Anzahl eindeutiger Werte in einer Spalte. Weitere Informationen zu diesem Profil finden Sie unter [Optionen für Anforderung für Verteilungsprofil für Spaltenwert &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md).|  
|**Verteilungsprofil für Spaltenlänge**|Berechnen Sie ein Verteilungsprofil für Spaltenlänge anhand der Standardeinstellungen für alle anwendbaren Spalten in der ausgewählten Tabelle oder Sicht.<br /><br /> Dieses Profil dokumentiert alle eindeutigen Längen von Zeichenfolgenwerten in der ausgewählten Spalte sowie den Prozentsatz der Zeilen in der Tabelle, die jede Länge darstellt. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. Werte, die nicht gültig sind. Weitere Informationen zu den Einstellungen dieses Profils finden Sie unter [Optionen für Anforderung für Verteilungsprofil für Spaltenlänge &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md).|  
|**Spaltenmusterprofil**|Berechnen Sie ein Spaltenmusterprofil anhand der Standardeinstellungen für alle anwendbaren Spalten in der ausgewählten Tabelle oder Sicht.<br /><br /> Dieses Profil meldet einen Satz von regulären Ausdrücken, die die Werte in einer Zeichenfolgenspalte abdecken. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. ungültige Zeichenfolgen. Dieses Profil kann außerdem reguläre Ausdrücke vorschlagen, die künftig zur Überprüfung neuer Werte verwendet werden können. Weitere Informationen zu den Einstellungen dieses Profils finden Sie unter [Optionen für die Anforderung für Spaltenmusterprofil &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md).|  
|**Kandidatenschlüsselprofil**|Berechnen Sie ein Kandidatenschlüsselprofil für Spaltenkombinationen, die maximal die in **für bis zu N Spaltenschlüssel**angegebene Anzahl an Spalten enthalten.<br /><br /> Dieses Profil meldet, ob eine Spalte oder eine Gruppe von Spalten geeignet ist, um als Schlüssel für die ausgewählte Tabelle zu fungieren. Dieses Profil hilft Ihnen auch, Probleme bei den Daten zu identifizieren, z. B. doppelte Werte in einer potenziellen Schlüsselspalte. Weitere Informationen zu den Einstellungen dieses Profils finden Sie unter [Optionen für die Anforderung für Kandidatenschlüsselprofil &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md).|  
|**für bis zu N Spaltenschlüssel**|Wählen Sie die maximale Anzahl von Spalten aus, die in möglichen Kombinationen als Schlüssel für die Tabelle oder Sicht getestet werden sollen. Der Standardwert ist 1. Der Maximalwert ist 1000. Wenn Sie beispielsweise "3" auswählen, werden Schlüsselkombinationen mit einer, zwei oder drei Spalten getestet.|  
|**Funktionales Abhängigkeitsprofil**|Berechnen Sie ein funktionales Abhängigkeitsprofil für Kombinationen aus bestimmenden Spalten, die maximal die in **für bis zu N Spalten als bestimmende Spalten**angegebene Anzahl an Spalten enthalten.<br /><br /> Dieses Profil meldet, in welchem Ausmaß die Werte in einer Spalte (die abhängige Spalte) von den Werten in einer anderen Spalte oder Gruppe von Spalten (der determinanten Spalte) abhängig sind. Dieses Profil hilft Ihnen auch, Probleme mit den Daten zu identifizieren, z. B. ungültige Werte. Weitere Informationen zu den Einstellungen dieses Profils finden Sie unter [Optionen für die Anforderung für funktionales Abhängigkeitsprofil &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md).|  
|**für bis zu N Spalten als bestimmende Spalten**|Wählen Sie die maximale Anzahl von Spalten aus, die in möglichen Kombinationen als determinante Spalten getestet werden sollen. Der Standardwert ist 1. Der Maximalwert ist 1000. Wenn Sie beispielsweise "2" auswählen, werden Kombinationen getestet, in denen einzelne Spalten oder Kombinationen aus zwei Spalten die bestimmenden Spalten für eine andere (abhängige) Spalte sind.|  
  
> [!NOTE]  
>  Der Typ „Wertinklusionsprofil“ ist im **Schnellprofilformular für eine einzelne Tabelle**nicht verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenprofilerstellungs-Task-Editor &#40; Seite "Allgemein" &#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Datenprofilerstellungs-Task-Editor &#40; Profile Requests Page &#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
  
  

