---
title: XMLA-Begriffe | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 429d1bc09714d15cfb8fbd851c72e01dd8ba198b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xmla-concepts"></a>Konzepte von XMLA
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  XML for Analysis (XMLA) beschreibt einen offenen Standard, der Datenzugriff auf Datenquellen unterstützt, die im World Wide Web liegen. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementiert XMLA mithilfe der XMLA 1.1-Spezifikation.  
  
 XML for Analysis (XMLA) ist ein SOAP-basiertes (Simple Object Access Protocol) XML-Protokoll, das speziell auf den universellen Datenzugriff für jede standardmäßige, mehrdimensionale Datenquelle im Web ausgerichtet ist. XMLA umgeht die Notwendigkeit, eine Clientkomponente bereitstellen, das Component Object Model (COM) verfügbar macht oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework-Schnittstellen. XMLA ist für das Internet optimiert, wenn Roundtrips zum Server viel Zeit und Ressourcen verbrauchen und statusbehaftete Verbindungen zu den Daten die Benutzerverbindungen auf der Instanz einschränken.  
  
 XMLA ist das native Protokoll für [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], die für alle Interaktionen zwischen einer Clientanwendung und einer Instanz von verwendet [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] unterstützt XML for Analysis 1.1 vollständig, und stellt auch Erweiterungen bereit, um die Metadatenverwaltung, die Sitzungsverwaltung und Sperrfunktionen zu unterstützen. Sowohl AMO (Analysis Management Objects) als auch ADOMD.NET verwenden das XMLA-Protokoll bei der Kommunikation mit einer Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="handling-xmla-communications"></a>Behandeln von XMLA-Kommunikation  
 Der offene Standard XMLA beschreibt zwei allgemein verfügbare Methoden: **Discover** und **Execute**. Diese Methoden verwenden lose verbundene Client- und Serverarchitektur, die von XML unterstützt wird, um eingehende und ausgehende Informationen auf einer Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] zu behandeln.  
  
 Die **Discover** Methode ruft Informationen und Metadaten von einem Webdienst ab. Diese Informationen können eine Liste verfügbarer Datenquellen und Informationen über jegliche Anbieter von Datenquellen enthalten. Eigenschaften definieren und gestalten die Daten, die aus einer Datenquelle abgerufen werden. Die **Discover** Methode ist eine gängige Methode zur Definition vieler Arten von Informationen, die eine Clientanwendung möglicherweise Daten aus Datenquellen auf [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanzen. Die Eigenschaften und generische Schnittstelle bieten Erweiterbarkeit, ohne dass Sie bestehende Funktionen in einer Clientanwendung neu schreiben müssen.  
  
 Die **Execute** -Methode ermöglicht es Anwendungen, anbieterspezifische Befehle gegen XMLA-Datenquellen auszuführen.  
  
 Obwohl das XMLA-Protokoll für Webanwendungen optimiert ist, kann es auch für LAN-orientierte Anwendungen genutzt werden. Die folgenden Anwendungen können von dieser XML-basierten API profitieren:  
  
-   Client/Server-Anwendungen, die flexible Technologie zwischen Clients und dem Server erfordern  
  
-   Client/Server-Anwendungen, die auf mehrere Betriebssysteme abzielen  
  
-   Clients, die keinen aussagekräftigen Status benötigen, um die Serverkapazität zu erhöhen  
  
## <a name="xmla-and-the-unified-dimensional-model"></a>XMLA und Unified Dimensional Model  
 XMLA ist das Protokoll, das von Business Intelligence-Anwendungen verwendet wird, die das Unified Dimensional Model (UDM) verwenden  
  
  
