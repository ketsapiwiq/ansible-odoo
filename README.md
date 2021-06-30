# Role Odoo pour Coopaname

## Pour la restauration de base de données

Se fait avec les variables `odoo_db_restore_date` et `odoo_db_restore: yes`.

- `odoo_db_restore`: remplacer la bdd actuelle ou non
- `odoo_db_restore_date`: deux choix
  - ou `immediate`
  - ou une date au format compatible Postgres (±ISO8601)
- `odoo_db_restore_pullonly`: soit la dernière bdd déjà générée (économise environ 20min)

## Pour les autres variables

Voir le fichier `defaults/main.yml`

## Exemple

```yaml
- hosts: test-odoo-gestionsociale
  roles:
    - coopaname.odoo
  vars:
    - odoo_registry_image_version: latest
    - odoo_coopaname_addons_repo_version: main
    - odoo_extra_addons: yes
    - odoo_addons_cae_enabled: yes

    - odoo_filestore_restore: no

    - odoo_db_restore: yes
    - odoo_db_restore_pullonly: no
    - odoo_db_restore_date: immediate

    - odoo_purge_sessions: yes
    - odoo_change_admin_password: yes
    - odoo_random_uuid: yes
    - odoo_remove_mailservers: yes

    - odoo_init_modules: ["example_module"]
```
