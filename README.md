# Role Odoo pour Coopaname

## Pour la restauration de base de données
Se fait avec la variable `odoo_db_restore_method` et `odoo_db_restore: yes`.

### Trois méthodes
- juste `odoo_db_restore`: juste switcher la base en cours d'utilisation avec un dump déjà importé (suffixé `_imported_dump`)
- `odoo_db_generate_dump` à `yes` : demander à barman / au serveur `db_backups` un dump tout frais à la date `barman_restore_pitr_date` (`immediate` : la base de prod actuelle), et l'importer comme base actuelle (implique `odoo_db_pull_dump==True` )
- `odoo_db_pull_dump`: récupérer depuis le serveur `db_backups` le dernier dump existant et l'importer comme base actuelle
- Don't restore anything by default

## Pour les autres variables
Voir le fichier `defaults/main.yml`

## Exemple
```yaml
- hosts: test-odoo-gestionsociale
  roles:
  - coopaname.odoo
  vars:
    - odoo_env_repo_version: main
    - odoo_registry_image_version: latest
    - odoo_coopaname_addons_repo_version: main
    - odoo_niboo_addons_rsync: yes
    - odoo_addons_cae_enabled: yes

    - odoo_filestore_restore: no

    - odoo_db_restore: yes
    - odoo_db_pull_dump: yes
    - odoo_db_generate_dump: yes
    - barman_restore_pitr_date: immediate

    - odoo_purge_sessions: yes
    - odoo_change_admin_password: yes
    - odoo_random_uuid: yes
    - odoo_remove_mailservers: yes

    - odoo_init_modules: ["coopaname_custom","coopaname_custom_contracts"]
    - odoo_update_all_modules: yes
```