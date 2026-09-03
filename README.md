# Project SEKAI: Colorful Stage! Modded server

## Setup
**Config: use_local_assets = True**
* Setup config.
* Get a decompressed copy of the PJSK master data and put it as data/masterdata_{region}.json (`python -m scripts.download_masterdata` in root directory)
* Download all of the sekai assets (`python -m scripts.download_all_assets` in root directory (comment the `continue` if downloading all bundles))
* Setup database (`python -m scripts.database_setup`)
* migrate database if needed

**Config: use_local_assets = False**
* Setup config.
* Setup database (`python -m scripts.database_setup`)
* migrate database if needed

### Finalize Database Setup
for now, these cmds are needed (run these directly in psql console, you can do `psql {dsn}` (DSN is printed on startup, if debug is True))
```sql
DELETE FROM app_versions;
INSERT INTO "app_versions" 
("versionId", "systemProfile", "appVersion", "multiPlayVersion", "assetVersion", "dataVersion", "assetHash", "appHash", "appVersionStatus", "region")  
VALUES
(1, 'production', '6.4.0', 'miku', '6.4.0.20', '6.4.0.22', 'e0ce8719-8790-4f01-b65f-e3bd21d34ce2', '6bad6856-ef61-eb43-47f5-dbc95fc5967c', 'available', 'jp');
INSERT INTO config (id, name, value, type, "updatedAt", region) VALUES
(1, 'sessionLength', '86400000', 'int', 1, 'jp'),
(2, 'isMultiLiveMaintenance', '0', 'bool', 1, 'jp'),
(3, 'isGachaMaintenance', '0', 'bool', 1, 'jp'),
(4, 'isVirtualLiveMaintenance', '0', 'bool', 1, 'jp'),
(5, 'isBillingShopMaintenance', '1', 'bool', 1, 'jp'),
(6, 'isMysekaiMaintenance', '0', 'bool', 1, 'jp'),
(7, 'isMysekaiRoomMaintenance', '0', 'bool', 1, 'jp');
```

### Requirements
- Redis (install redis-server ubuntu, or use https://github.com/redis-windows/redis-windows)
- PSQL
- Python
