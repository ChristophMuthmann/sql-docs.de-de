---
title: "Identitätswechsel in tabellarischen Modellen von Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 3ad8bc6b19ab93a75a62134b8b8b9ec51cdb5fdd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="impersonation"></a>Identitätswechsel 

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  In diesem Thema bietet Entwicklern von tabellarischen Modellen einen Überblick über die Anmeldeinformationen von Analysis Services Verwendung beim Herstellen einer Verbindung mit einer Datenquelle zum Importieren und verarbeiten (aktualisieren) von Daten.  

##  <a name="bkmk_conf_imp_info"></a>Konfigurieren des Identitätswechsels  
 Ein Modell vorhanden ist, wo und in welchem Kontext bestimmt, wie die Identitätswechselinformationen konfiguriert ist. Wenn Sie ein neues Modellprojekt erstellen, wird Identitätswechsel beim Herstellen einer Verbindung mit einer Datenquelle zum Importieren von Daten in SQL Server Data Tools (SSDT) konfiguriert. Nachdem ein Modell bereitgestellt wurde, kann Identitätswechsel in Datenbank-Verbindungszeichenfolgeneigenschaft Modell mithilfe von SQL Server Management Studio (SSMS) konfiguriert werden. Für tabellarische Modelle in Azure Analysis Services können Sie SSMS oder die **anzeigen als: Skript** Modus im Designer browserbasierte zum Bearbeiten der Datei Model.bim im JSON-Format.
  
##  <a name="bkmk_how_imper"></a>Wie der Identitätswechsel verwendet wird  
 *Identitätswechsel* ist die Fähigkeit einer Serveranwendung, z.B. Analysis Services, die Identität einer Clientanwendung anzunehmen. Analysis Services wird über ein Dienstkonto, allerdings, wenn der Server eine Verbindung mit einer Datenquelle herstellt Anwendung ein Identitätswechsel verwendet, sodass für den Datenimport und die Verarbeitung zugriffsüberprüfungen kann ausgeführt werden.  
  
 Für den Identitätswechsel verwendeten Anmeldeinformationen unterscheiden sich von den Anmeldeinformationen, denen Sie derzeit angemeldet sind. Angemeldeten Benutzers Anmeldeinformationen werden beim Erstellen eines Modells für bestimmte clientseitige Vorgänge verwendet.  
  
 Es ist wichtig um zu verstehen, wie Identitätswechsel-Anmeldeinformationen angegeben und gesichert, sowie den Unterschied zwischen den Kontexten in welcher sowohl Ihr angemeldetes auf Benutzeranmeldeinformationen verwendet werden, und wenn andere Identitätswechsel-Anmeldeinformationen verwendet werden.  
  
 **Grundlegendes zu serverseitigen Anmeldeinformationen**  
 
Wenn Daten nicht importiert oder verarbeitet werden, werden Identitätswechsel-Anmeldeinformationen verwendet, eine Verbindung mit der Datenquelle und die Daten abzurufen. Dies ist eine *serverseitige* Vorgang im Kontext einer Clientanwendung ausgeführt wird, da das Hosten der arbeitsbereichsdatenbank des Analysis Services-Server eine Verbindung mit der Datenquelle her, und die Daten abruft.  
  
 Wenn Sie ein Modell auf einem Analysis Services-Server bereitstellen und sich die Arbeitsbereichsdatenbank während der Bereitstellung des Modells im Arbeitsspeicher befindet, werden die Anmeldeinformationen an den Analysis Services-Server übergeben, auf dem das Modell bereitgestellt wird. Zu keinem Zeitpunkt werden Benutzeranmeldeinformationen auf dem Datenträger gespeichert.  
  
 Wenn ein bereitgestelltes Modell die Daten aus einer Datenquelle verarbeitet, werden die Identitätswechselinformationen, die in der Datenbank im Arbeitsspeicher beibehalten verwendet, eine Verbindung mit der Datenquelle und die Daten abzurufen. Da dieser Prozess vom Analysis Services-Server, der die Modelldatenbank verwaltet durchgeführt wird, ist dies erneut einen serverseitigen Vorgang.  
  
 **Grundlegendes zu clientseitigen Anmeldeinformationen**  
  
 Wenn ein neues Modell erstellen, oder eine Datenquelle zu einem vorhandenen Modell hinzufügen, Sie Verbindungen mit einer Datenquelle herstellen und Tabellen und Sichten in das Modell importiert werden sollen. In den Tabellenimport-Assistenten oder Abrufen Data\Query Designer Vorschau und Filter-Funktionen sehen Sie ein Beispiel der Daten, die Sie importieren. Sie können auch Filter angeben, um Daten auszuschließen, die im Modell nicht erforderlich sind.  
  
 Auf ähnliche Weise für vorhandene Modelle, die bereits erstellt wurden, verwenden Sie die **Tabelleneigenschaften** Dialogfeld Vorschau und Filtern von Daten in eine Tabelle importiert.  
  
 Die Vorschau und Filter Funktionen **Tabelleneigenschaften**, und **Partitions-Manager** Dialogfelder sind ein in-Process *clientseitige* Vorgang, d. h. welche Aktionen während dieser ausgeführt wird Vorgang unterscheiden sich wie die Datenquelle mit verbunden ist, und Daten aus der Datenquelle abgerufen. ein serverseitiger-Vorgang. Die Anmeldeinformationen, die zum Anzeigen einer Vorschau und Filtern der Daten verwendet werden, sind die Anmeldeinformationen des Benutzers, der zu dem Zeitpunkt angemeldet ist. In der Tat, Ihre Anmeldeinformationen. 
  
 Die Trennung von Anmeldeinformationen verwendet werden, während der serverseitigen und clientseitigen Vorgängen können dazu führen, dass ein Versionskonflikt bei sehen Sie, und welche Daten während eines Imports oder der Prozess (serverseitige Vorgänge) abgerufen werden. Wenn die Anmeldeinformationen Sie derzeit angemeldet sind mit, und die angegebenen Identitätswechselinformationen unterschiedlich sind, die Daten daraufhin in der Vorschau und Filter-Funktionen oder die **Tabelleneigenschaften** Dialogfeld und die Daten abgerufen, die während des Imports oder Prozess kann abhängig von der Datenquelle erforderlichen Anmeldeinformationen unterscheiden.  
  
> [!IMPORTANT]  
>  Beim Erstellen eines Modells, stellen Sie die Anmeldeinformationen, mit dem Sie angemeldet sind, und die für einen Identitätswechsel angegebenen Anmeldeinformationen über die erforderlichen Rechte zum Abrufen der Daten aus der Datenquelle.  
  
##  <a name="bkmk_imp_info_options"></a> enthalten  
 Beim Identitätswechsel konfigurieren oder Eigenschaften für eine vorhandene Datenquelle Verbindung bearbeiten, geben Sie eine der folgenden Optionen aus:  
  
**Tabellenmodelle 1400 und höher**
 
|Option|Description|  
|------------|-----------------|  
|**Identitätswechsel**|Gibt an, das Modell ein Windows-Benutzerkonto zum Importieren oder Daten aus der Datenquelle verarbeitet. Die Domäne und den Namen des Benutzerkontos folgen dem folgenden Format:**\<Domänenname >\\< Benutzerkontoname\>**.|  
|**Identität des aktuellen Benutzers**|Gibt an, dass die Daten zugegriffen werden soll, aus der Datenquelle, die mit der Identität des Benutzers, der die Anforderung gesendet. Dieser Modus gilt nur für DirectQuery-Modus.|  
|**Identität annehmen**|Gibt einen Benutzernamen für den Zugriff auf die Datenquelle, jedoch nicht das Kennwort des Kontos angeben müssen. Dieser Modus gilt nur, wenn Kerberos-Delegierung aktiviert ist, und gibt an, dass die S4U-Authentifizierung verwendet werden soll.|  
|**Identität des Dienstkontos**|Gibt an, das Modell die Sicherheitsanmeldeinformationen, die das Modell verwaltet die Analysis Services-Dienstinstanz zugeordnet.|  
|**Identität des Kontos für unbeaufsichtigte**|Gibt an, dass das Analysis Services-Modul ein vorkonfiguriertes unbeaufsichtigtes Konto für den Datenzugriff verwenden soll.|  


**Tabellarische 1200-Modelle**
 
|Option|Description|  
|------------|-----------------|  
|**Bestimmten Windows-Benutzernamen und Kennwort**|Diese Option gibt an das Modell ein Windows-Benutzerkonto zum Importieren oder Daten aus der Datenquelle verarbeitet. Die Domäne und den Namen des Benutzerkontos folgen dem folgenden Format:**\<Domänenname >\\< Benutzerkontoname\>**. Beim Erstellen eines neuen Modells mit dem Tabellenimport-Assistenten ist dies die Standardoption.|  
|**Dienstkonto**|Diese Option gibt an, dass das Modell die Sicherheitsanmeldeinformationen verwendet, die der Analysis Services-Dienstinstanz zugeordnet sind, die das Modell verwaltet.|  
  
##  <a name="bkmk_impers_sec"></a> Sicherheit  
 Identitätswechsel verwendeten Anmeldeinformationen werden dauerhaft im Arbeitsspeicher vom VertiPaq™-Modul. Anmeldeinformationen werden nie geschrieben, auf dem Datenträger. Wenn die arbeitsbereichsdatenbank nicht im Arbeitsspeicher ist, wenn das Modell bereitgestellt wird, der Benutzer wird aufgefordert, die Anmeldeinformationen zur Verbindung mit der Datenquelle und Abrufen der Daten einzugeben.  
  
> [!NOTE]  
>  Es wird empfohlen, ein Windows-Benutzerkonto und ein Kennwort für die Identitätswechselinformationen anzugeben. Ein Windows-Benutzerkonto kann für die mindestens erforderlichen Berechtigungen zum Herstellen einer Verbindung mit und Lesen von Daten aus der Datenquelle konfiguriert werden.  
  

  
## <a name="see-also"></a>Siehe auch  
 [DirectQuery-Modus](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Datenquellen](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [Tabellenmodelllösungsbereitstellung](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
