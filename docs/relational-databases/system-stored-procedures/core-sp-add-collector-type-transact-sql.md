---
title: sp_add_collector_type (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_collector_type
- sp_add_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- core.sp_add_collector_type stored procedure
- management data warehouse, data collector stored procedures
- sp_add_collector_type
- data collector [SQL Server], stored procedures
ms.assetid: 1d981037-2147-464e-a456-7d8e479bce89
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7bc16db334b6b8f6538a7ee221beb5fd3ccf2a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727598"
---
# <a name="corespaddcollectortype-transact-sql"></a>core.sp_add_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt der core.supported_collector_types-Sicht in der Datenbank des Verwaltungs-Data Warehouse einen neuen Eintrag hinzu. Die Prozedur muss im Kontext der Verwaltungs-Data Warehouse-Datenbank ausgeführt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
core.sp_add_collector_type [ @collector_type_uid = ] 'collector_type_uid'  
```  
  
## <a name="arguments"></a>Argumente  
 [ @collector_type_uid =] '*Collector_type_uid*"  
 Die GUID für den Sammlertyp. *Collector_type_uid* ist **Uniqueidentifier**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Mdw_admin** (mit EXECUTE-Berechtigung) festen Datenbankrolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der core.supported_collector_types-Sicht der generische T-SQL-Abfragesammlertyp hinzugefügt. Der generische T-SQL-Abfragesammlertyp ist in der Standardeinstellung bereits vorhanden. Wenn Sie diesen Code für eine Standardinstallation ausführen, empfangen Sie daher eine Meldung, dass der Sammlertyp bereits vorhanden ist.  
  
 Dieser Code kann dann erfolgreich ausgeführt werden, wenn Sie den generischen T-SQL-Abfragesammlertyp mithilfe der gespeicherten Prozedur core.sp_remove_collector_type entfernt und anschließend versucht haben, ihn als registrierten Sammlertyp, der Daten in das Verwaltungs-Data Warehouse hochladen kann, hinzuzufügen.  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @RC int;  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = (SELECT collector_type_uid FROM msdb.dbo.syscollector_collector_types WHERE name = N'Generic T-SQL Query Collector Type');  
EXECUTE @RC = core.sp_add_collector_type @collector_type_uid;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Verwaltungs-Data Warehouse](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
