---
title: Optionen (Designer – Seite „Tabellen- und Datenbank-Designer“) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-menu
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Designers.Table_Designer
ms.assetid: b43f4b97-17b9-4004-a824-f77b9e145741
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c65543f8babf73764a1eca5eba5e61690e0cd910
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="options-designers---table-and-database-designers-page"></a>Optionen (Designer – Seite „Tabellen- und Datenbank-Designer“)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Auf dieser Seite können Sie das Standardverhalten des Designers bestimmen. Um auf die Einstellungen zuzugreifen, klicken Sie im Menü **Extras** auf **Optionen**, erweitern Sie den Ordner **Designer** , und klicken Sie dann auf **Tabellen-Designer**.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
**Timeoutwert für Verbindungszeichenfolge für Tabellen-Designer-Updates überschreiben**  
Lässt zu, dass für die Aktionen des Tabellen-Designers ein neuer Timeoutwert festgelegt wird. Das kann hilfreich sein, wenn der Tabellen-Designer Auswirkungen auf eine große Tabelle hat und für die Änderung der Tabelle zusätzliche Zeit benötigt.  
  
**Transaktionstimeout nach**  
Legt einen Timeoutwert für den Tabellen-Designer fest.  
  
**Automatisches Erstellen von Änderungsskripts**  
Erstellt automatisch ein Skript für die Implementierung der im Tabellen-Designer definierten Änderungen.  
  
**Warnung bei Nullprimärschlüsseln**  
Stellt ein Warndialogfeld bereit, wenn ein für einen Primärschlüssel ausgewähltes Feld Nullwerte enthalten kann.  
  
**Warnung bei Unterschiederkennung**  
Wenn Sie dieses Kontrollkästchen aktivieren, werden beim Speichern der Änderungen in einem Nachrichtenfeld alle Überschneidungen zwischen Ihren Änderungen und den von einem anderen Benutzer vorgenommenen Änderungen aufgelistet.  
  
**Warnung bei betroffenen Tabellen**  
Stellt ein Warndialogfeld bereit, in dem die von der Aktion betroffenen Tabellen aufgeführt sind und zur Bestätigung aufgefordert wird.  
  
**Speichern von Änderungen verhindern, die die Neuerstellung der Tabelle erfordern**  
Verhindert, dass ein Benutzer Änderungen vornimmt, die eine Neuerstellung der Tabelle erfordern. Die folgenden Aktionen können die erneute Erstellung einer Tabelle erfordern:  
  
-   Hinzufügen einer neuen Spalte zur Mitte der Tabelle  
  
-   Löschen einer Spalte  
  
-   Ändern der NULL-Zulässigkeit einer Spalte  
  
-   Ändern der Reihenfolge der Spalten  
  
-   Ändern des Datentyps einer Spalte  
  
**Standardtabellenansicht**  
Wählen Sie aus, wie Tabellen in den Designern angezeigt werden sollen:  
  
-   **Standard**  
  
    Zeigt den Tabellenkopf, alle Spaltennamen, Datentypen und die Einstellung NULL-Werte zulassen an.  
  
-   **Spaltennamen**  
  
    Zeigt die Spaltennamen an.  
  
-   **Key**  
  
    Zeigt den Tabellenkopf und die Primärschlüsselspalten an.  
  
-   **Nur Name**  
  
    Zeigt nur den Tabellenkopf mit seinem Namen an.  
  
-   **Benutzerdefiniert**  
  
    Ermöglicht Ihnen die Auswahl der anzuzeigenden Spalten.  
  
**Tabellendialogfeld hinzufügen bei Neues Diagramm starten**  
Öffnet beim Öffnen der Designer automatisch das Dialogfeld **Tabelle hinzufügen** .  
  
