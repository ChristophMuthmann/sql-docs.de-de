---
title: "Referenz zur Benutzeroberfl&#228;che des Dialogfelds Paketrollen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.dtsserver.packageroles.f1"
helpviewer_keywords: 
  - "Paketrollen (Dialogfeld)"
ms.assetid: 63f13416-c0aa-4480-a336-ef1e6e31a860
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Referenz zur Benutzeroberfl&#228;che des Dialogfelds Paketrollen
  Verwenden Sie das Dialogfeld **Paketrollen**, das in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügbar ist, um die Rollen auf Datenbankebene anzugeben, die Lesezugriff auf das Paket besitzen, sowie die Rollen auf Datenbankebene, die Schreibzugriff auf das Paket besitzen. Rollen auf Datenbankebene gelten nur für Pakete, die in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**-Datenbank gespeichert sind.  
  
 Weitere Informationen zu den Rollen auf Datenbankebene von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und ihren Berechtigungen finden Sie unter [Integration Services-Rollen &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-roles-ssis-service.md).  
  
 Die im Dialogfeld aufgeführten Rollen sind die aktuellen Rollen der **msdb** -Systemdatenbank. Wenn keine Rollen ausgewählt sind, gelten die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Standardrollen. Standardmäßig enthält die Leserolle **db_ssisadmin**, **db_ssisoperator** und den Benutzer, der das Paket erstellt hat. Ein Benutzer, der Mitglied einer dieser Rollen ist oder die Pakete erstellt hat, kann Pakete aufzählen, anzeigen, exportieren und ausführen. Standardmäßig schließt die Schreibrolle **db_ssisadmin** und den Benutzer ein, der das Paket erstellt hat. Ein Benutzer, der Mitglied dieser Rolle ist, und der Benutzer, der die Pakete erstellt hat, kann Pakete importieren, löschen und ändern.  
  
 Die **ownersid** -Spalte in der **sysssispackages** -Tabelle enthält die eindeutige Sicherheits-ID des Benutzers, der das Paket erstellt hat.  
  
## enthalten  
 **Paketname**  
 Gibt den Namen des Pakets an.  
  
 **Leserolle**  
 Auswählen einer Rolle in der Liste.  
  
 **Schreibrolle**  
 Auswählen einer Rolle in der Liste  
  
## Siehe auch  
 [Rollen auf Datenbankebene](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Sicherheitsübersicht &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  