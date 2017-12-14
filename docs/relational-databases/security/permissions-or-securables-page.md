---
title: "Seite „Berechtigungen“ oder „Sicherungsfähige Elemente“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/07/2016
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.common.permissions.f1
- sql13.swb.SecurableAndEffectPermissions.f1
- sql13.swb.common.columnperm.f1
- sql13.swb.availabilitygroupproperties.permission.f1
- sql13.swb.SecurableAndEffectivePermission.f1
ms.assetid: b3bf077a-bec2-4161-ac0c-460586199906
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bcdb1f8d446c5cadf94718f2ae7f59c9c0624caf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="permissions-or-securables-page"></a>Seite 'Berechtigungen' oder 'Sicherungsfähige Elemente'
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Auf der Seite **Berechtigungen** oder **Sicherungsfähige Elemente** können die Berechtigungen für sicherungsfähige Elemente angezeigt oder festgelegt werden. Diese Seite kann von vielen Orten aus geöffnet werden. Der Inhalt der Seite kann sich geringfügig ändern, je nachdem, wie die Seite geöffnet wird und was sie enthält. Das obere Raster der Seite ist u. U. aufgefüllt, wenn die Seite geöffnet wird, oder es ist leer. Klicken Sie auf **Suchen**, um dem oberen Raster Elemente hinzuzufügen. Wählen Sie im oberen Raster ein Element aus, und legen Sie dann auf der Registerkarte **Explizit** die entsprechenden Berechtigungen fest. Verwenden Sie zum Anzeigen von aggregierten Berechtigungen die Registerkarte **Effektiv** .  
  
 Weitere Informationen zu möglichen Kombinationen aus sicherungsfähigen Elementen und Prinzipalen finden Sie bei den Links zur spezifischen Syntax für sicherungsfähige Elemente im Thema [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md). Weitere Informationen finden Sie unter [Securables](../../relational-databases/security/securables.md).  
  
## <a name="page-header"></a>Seitenheader  
 Der Header der Seite **Berechtigungen** oder **Sicherungsfähige Elemente** variiert je nach sicherungsfähigem Element oder Prinzipal. Er zeigt für das Element relevante Informationen an, z. B. den Namen.  
  
## <a name="upper-grid"></a>Oberes Raster  
 Das obere Raster enthält ein oder mehrere Elemente, für die Berechtigungen festgelegt werden können. Das Dialogfeld enthält die Schaltfläche **Suchen** , über die Sie Objekte oder Prinzipale auswählen können, die Sie dem oberen Raster hinzufügen können. Der Name des Rasters enthält u. U. **Sicherungsfähige Elemente** oder einen oder mehrere Typen an sicherungsfähigen Elementen oder Prinzipalen. Die im oberen Raster angezeigten Spalten variieren je nach Prinzipal oder sicherungsfähigem Element.  
  
 **Name**  
 Die Namen der Prinzipale oder sicherungsfähigen Elemente, die dem Raster hinzugefügt werden.  
  
 **Typ**  
 Beschreibt den Typ jedes Elements.  
  
## <a name="explicit-tab"></a>Registerkarte 'Explizit'  
 Die Registerkarte **Explizit** enthält die möglichen Berechtigungen für die im oberen Raster ausgewählten sicherungsfähigen Elemente. Um die Berechtigungen zu konfigurieren, aktivieren oder deaktivieren Sie die Kontrollkästchen **Erteilen** (oder **Zulassen**), **Mit Erteilung**und **Verweigern** . Für einige explizite Berechtigungen sind nicht alle Optionen verfügbar.  
  
 **Berechtigungen**  
 Der Name der Berechtigung.  
  
 **Grantor**  
 Der Prinzipal, der die Berechtigung erteilt.  
  
 **Erteilen**  
 Aktivieren Sie diese Option, um der Anmeldung diese Berechtigung zu erteilen. Deaktivieren Sie diese Option, um diese Berechtigung aufzuheben.  
  
 **Mit Erteilung**  
 Zeigt den Status der WITH GRANT-Option für die angezeigte Berechtigung an. Dieses Feld ist schreibgeschützt. Verwenden Sie die [GRANT](../../t-sql/statements/grant-transact-sql.md) -Anweisung, um diese Berechtigung anzuwenden.  
  
 **Verweigern**  
 Aktivieren Sie diese Option, um der Anmeldung diese Berechtigung zu verweigern. Deaktivieren Sie diese Option, um diese Berechtigung aufzuheben.  
  
 **Spaltenberechtigungen**  
 Bei Objekten, die Spalten enthalten (z.B. Tabellen, Sichten oder Tabellenwertfunktionen), wird mit der Schaltfläche **Spaltenberechtigungen** das Dialogfeld **Spaltenberechtigungen** geöffnet. In diesem Dialogfeld können Sie für einzelne Spalten einer Tabelle oder Sicht die Berechtigungen **Erteilen**, **Zulassen**oder **Verweigern** festlegen. Diese Option ist nicht für alle Objekttypen bzw. Berechtigungen verfügbar.  
  
## <a name="effective-tab"></a>Registerkarte 'Effektiv'  
 Die Berechtigungen, die ein Prinzipal einem sicherungsfähigen Element zuordnet, stammen möglicherweise aus Berechtigungen, die für mehrere unterschiedliche Prinzipale festgelegt wurden. Einer Anmeldung könnten beispielsweise einzeln oder als Gruppenmitglied Berechtigungen erteilt werden. Die Registerkarte **Effektiv** zeigt das Ergebnis einer Kombination aus expliziten Berechtigungen und den Berechtigungen, die aus Gruppen- oder Rollenmitgliedschaften empfangen werden. Erteilen-Berechtigungen sind aggregiert. Eine Verweigern-Berechtigung überschreibt alle Erteilen-Berechtigungen.  
  
 **Berechtigungen**  
 Der Name der Berechtigung.  
  
 **Column**  
 Die Namen der Spalten, auf die sich die Berechtigung auswirkt.  
  
## <a name="see-also"></a>Siehe auch  
 [Rollen auf Datenbankebene](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
