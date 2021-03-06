---
title: Sys. dm_db_uncontained_entities (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_uncontained_entities
- dm_db_uncontained_entities_TSQL
- sys.dm_db_uncontained_entities_TSQL
- dm_db_uncontained_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_uncontained_entities dynamic management view
ms.assetid: f417efd4-8c71-4f81-bc9c-af13bb4b88ad
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40235280563039493bdd174de1c314809a424336
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694088"
---
# <a name="sysdmdbuncontainedentities-transact-sql"></a>sys.dm_db_uncontained_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt alle nicht enthaltenen Objekte an, die in der Datenbank verwendet werden. Nicht enthaltene Objekte sind Objekte, die die Datenbankbegrenzung in einer eigenständigen Datenbank überschreiten. Auf diese Sicht kann sowohl von einer eigenständigen Datenbank als auch von einer abhängigen Datenbank zugegriffen werden. Wenn Sys. dm_db_uncontained_entities leer ist, verwendet die Datenbank nicht enthaltenen Entitäten.  
  
 Wenn die Datenbankbegrenzung von einem Modul mehrmals überschritten wird, wird nur die erste Überschreitung gemeldet.  
  
||||  
|-|-|-|  
|**Spaltenname**|**Typ**|**Beschreibung**|  
|*class*|**int**|1 = Objekt oder Spalte (einschließlich Modulen, XPs, Sichten, Synonymen und Tabellen).<br /><br /> 4 = Datenbankprinzipal<br /><br /> 5 = Assembly<br /><br /> 6 = Typ<br /><br /> 7 = Index (Volltextindex)<br /><br /> 12 = DDL-Trigger auf Datenbankebene<br /><br /> 19 = Route<br /><br /> 30 = Überwachungsspezifikation|  
|*class_desc*|**nvarchar(120)**|Klassenbeschreibung der Entitätsklasse. Eine der folgenden entsprechend die Klasse:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **DATABASE_PRINCIPAL**<br /><br /> **ASSEMBLY**<br /><br /> **TYPE**<br /><br /> **INDEX**<br /><br /> **DATABASE_DDL_TRIGGER**<br /><br /> **ROUTE**<br /><br /> **AUDIT_SPECIFICATION**|  
|*major_id*|**int**|Die ID der Entität.<br /><br /> Wenn *Klasse* = 1, und klicken Sie dann auf Object_id<br /><br /> Wenn *Klasse* = 4, und klicken Sie dann auf principal_id.<br /><br /> Wenn *Klasse* = 5, und klicken Sie dann auf Sys.Assemblies.<br /><br /> Wenn *Klasse* = 6, und klicken Sie dann auf user_type_id.<br /><br /> Wenn *Klasse* = 7, und klicken Sie dann auf index_id.<br /><br /> Wenn *Klasse* = 12, dann sys.Triggers.<br /><br /> Wenn *Klasse* = 19, Route_ID.<br /><br /> Wenn *Klasse* = 30, und klicken Sie dann auf Sys. database_audit_specifications.databse_specification_id.|  
|*statement_line_number*|**int**|Wenn die Klasse ein Modul ist, wird die Zeilennummer für die nicht enthaltene Verwendung zurückgegeben.  Anderenfalls ist der Wert NULL.|  
|*Statement_ offset_begin*|**int**|Wenn die Klasse ein Modul ist, gibt dies die Startposition der nicht enthaltenen Verwendung in Byte an, beginnend bei 0. Andernfalls ist der Rückgabewert NULL.|  
|*Statement_ offset_end*|**int**|Wenn die Klasse ein Modul ist, gibt dies die Endposition der nicht enthaltenen Verwendung in Byte an, beginnend bei 0. Der Wert -1 gibt das Ende des Moduls an. Andernfalls ist der Rückgabewert NULL.|  
|*statement_type*|**nvarchar(512)**|Der Typ der Anweisung.|  
|*Feature_-name*|**nvarchar(256)**|Gibt den externen Namen des Objekts zurück.|  
|*feature_type_name*|**nvarchar(256)**|Gibt den Typ der Funktion zurück.|  
  
## <a name="remarks"></a>Hinweise  
 Sys. dm_db_uncontained_entities zeigt die Entitäten, die möglicherweise die datenbankbegrenzung überschreiten. Es werden alle Benutzerentitäten zurückgegeben, von denen Objekte außerhalb der Datenbank verwendet werden können.  
  
 Die folgenden Funktionstypen werden gemeldet.  
  
-   Unbekanntes Kapselungsverhalten (dynamisches SQL oder verzögerte Namensauflösung)  
  
-   DBCC-Befehl  
  
-   Gespeicherte Systemprozeduren  
  
-   Skalarsystemfunktion  
  
-   Tabellenwert-Systemfunktion  
  
-   Integrierte Systemfunktion  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Sys. dm_db_uncontained_entities gibt nur Objekte für die der Benutzer eine Art von Berechtigung verfügt. Auszuwertende vollständig die Kapselung der Datenbank diese Funktion werden, von einem Benutzer mit hohen Privilegien wie z. B. ein Mitglied verwendet sollte der **Sysadmin** -Serverrolle sein oder die **Db_owner** Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Prozedur P1 erstellt, und `sys.dm_db_uncontained_entities`wird abgefragt. Die Abfrage meldet, dass **sys.endpoints** von P1 außerhalb der Datenbank verwendet wird.  
  
```sql  
CREATE DATABASE Test;  
GO  
  
USE Test;  
GO  
CREATE PROC P1  
AS   
SELECT * FROM sys.endpoints ;  
GO  
SELECT SO.name, UE.* FROM sys.dm_db_uncontained_entities AS UE  
LEFT JOIN sys.objects AS SO  
    ON UE.major_id = SO.object_id;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Eigenständige Datenbanken](../../relational-databases/databases/contained-databases.md)  
  
  
