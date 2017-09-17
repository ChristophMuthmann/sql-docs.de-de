---
title: "Konfigurieren des ODBC-Treibers für Oracle | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64e6dfe9f31eb983170f08e9fcd3e0705ba9ae62
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Konfigurieren des ODBC-Treibers für Oracle
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Sie können Leistung des ODBC-Treibers für Oracle steuern, indem die datenumgebung kennen und ordnungsgemäß Festlegen der Parameter für die datenquellenverbindung über die [ODBC-Datenquellenadministrator](../../odbc/admin/odbc-data-source-administrator.md) Dialogfeld Feld oder über eine Verbindung herstellen String-Parameter. Das Dialogfeld bietet die folgenden Steuerelemente zum Herstellen einer Verbindung mit einer Datenquelle mithilfe des Dialogfelds aus, oder schließen Sie Zeichenfolgen mit:  
  
-   **Registerkarte "Benutzer-DSN"** Listet die Datenquellennamen, die lokal auf dem Computer sind.  
  
-   **Registerkarte "System-DSN"** ermöglicht es Ihnen, hinzufügen oder entfernen eine Systemdatenquelle. System-Datenquellen können von allen Benutzern auf dem lokalen Computer zugegriffen werden.  
  
-   **Registerkarte "Datei-DSN"** ermöglicht es Ihnen, hinzufügen oder entfernen eine Datei als Datenquelle aus dem lokalen Computer. Dateidatenquellen können von allen Benutzern gemeinsam genutzt werden, die die gleichen Treiber installiert haben.  
  
-   **Registerkarte "Treiber"** installierten ODBC-Treiber aufgeführt.  
  
-   **Registerkarte "Tracing** können Sie angeben, wie die ODBC-Treiber-Manager für Aufrufe an ODBC-Funktionen verfolgt. Sie können die Ablaufverfolgung separat für jeden installierten ODBC-Anwendung konfigurieren.  
  
-   **Registerkarte "Verbindungs-Pooling"** können Sie Verbindungsoptionen für jeden installierten Treiber auswählen.  
  
-   **Zur Registerkarte "** werden die Dateien der installierten ODBC-Komponente aufgeführt.  
  
 Nachdem Sie eine Datenquelle hinzugefügt haben, können Sie die **ODBC-Datenquellenadministrator** (Dialogfeld), um den Zugriff auf die Datenquelle zu konfigurieren. Wählen Sie eine Datenquelle aus, und klicken Sie dann auf eine der Registerkarten bearbeiten, oder überprüfen die Informationen.
