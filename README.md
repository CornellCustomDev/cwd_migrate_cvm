# CVM Migration

Upgrade / Migrate the Vet School website from Drupal 7 to Drupal 10.

P.S. If I could start over, I would put the migration configs in modules/custom_cvm/cwd_migrate_cvm, not modules/custom_cvm/cwd_migrate_cvm/config/install 🤦‍♀️  OH WELL!

## Getting started

See also: That Google doc I created during October 2023 prep / proof of concept (not putting a link here because idr if I put anything sensitive in it; worry about it later; if you know, you know).

## misc drush/config commands

```
lando drush cim --partial --source=../config
lando drush cim --partial --source=modules/custom_cvm/cwd_migrate_cvm/config/install

drush migr_cim_cvm
drush migr_cim_normal

lando drush mim upgrade_d7_taxonomy_term_policy_executive
lando drush mr upgrade_d7_taxonomy_term_policy_executive
lando drush ms upgrade_d7_taxonomy_term_policy_executive
lando drush mmsg upgrade_d7_taxonomy_term_policy_executive

terminus drush cornell-cvm.migr-stg -- cim --partial --source=modules/custom_cvm/cwd_migrate_cvm/config/install
```

To import something with a "source ID" that has multiple parts, separate each part with a colon:
```
lando drush mim upgrade_d7_field_formatter_settings --idlist=node:portfolio_project:teaser:field_ess_type
```

### Generate / update migrations
```
lando drush migrate-upgrade --legacy-db-url=mysql://pantheon:pantheon@database.cucvm.internal/pantheon --configure-only
```

Then, some commands for after doing that:
```
sed -i -e 's/migrate_drupal_7/cornell_cvm/g' config/migrate_plus.migration.*
cp -rp config/migrate_plus.migration.* web/modules/custom_cvm/cwd_migrate_cvm/config/install/
```

(I used Migrate Sandbox to figure out some IDs.)
* I'm sure this ^^ note was meant for a different section of this doc...

### More ... stuff ...

Bulk moving migrations into new migration groups:
```
sed -i -e 's/migration_group: cornell_cvm\b/migration_group: cornell_cvm_taxonomy_terms/' web/modules/custom_cvm/cwd_migrate_cvm/config/install/migrate_plus.migration.upgrade_d7_taxonomy_term_*
```

### A few more references...
* https://thinktandem.io/blog/2020/04/28/lando-migration-webinar-part-1-followup/
* https://github.com/thinktandem/migration_boilerplate#setup
* Convo with Dustin on Lando Slack: https://devwithlando.slack.com/archives/C2XBSHX8R/p1615916356008600?thread_ts=1604969491.465700&cid=C2XBSHX8R
  * ...for the migration database, you can start by changing the host to `database.whatevertheappnameoftheoldappis.internal`
* FCS migration -- very VERY old, but I still find useful bits and pieces sometimes: https://github.com/CU-CommunityApps/cwd_migrate_fcs
* Policy migration -- only "very" old: https://github.com/CU-CommunityApps/cwd_migrate_policy

## Steps

Mainly: https://www.drupal.org/docs/upgrading-drupal/upgrading-from-drupal-6-or-drupal-7/customize-migrations#s-create-your-initial-migrations

Also: https://github.com/CU-CommunityApps/cwd_migrate_policy/tree/main#steps

### Pantheon

i.e setting up "secrets" / database connection stuff

HOT TIP: Sometimes, things won't work and it's because the source site is ASLEEP 😑
```
terminus env:wake cucvm.d10
```

#### ...stuff copied from my CLI while doing things on pantheon...

Reference: https://github.com/CU-CommunityApps/cwd_migrate_fcs/blob/main/README.md#notes-from-running-on-pantheon-envs

_NOTE: "later", replace cucvm.d10 with cucvm.live_ (maybe/probably!)<br>
_NOTE: "later", replace cornell-cvm.alison with cornell-cvm.test_<br>
```
terminus self:plugin:install terminus-secrets-plugin
  (^^ if you don't have this plugin installed already)
terminus connection:info cucvm.d10 --field="mysql_url"
  (^^ "just looking")
export D7_MYSQL_URL=$(terminus connection:info cucvm.d10 --field="mysql_url")
terminus secrets:set cornell-cvm.alison migrate_source_db__url $D7_MYSQL_URL
  (^^ create or update secrets file on multidev server)
terminus secrets:list cornell-cvm.alison --format=json
  (^^ "did it work?")
```

### settings.*.php files

For work on Pantheon multidev, do this or something like this:<br>
https://github.com/CU-CommunityApps/cwd_migrate_fcs/blob/main/settings.migrate-fromto-pantheon.php

P.S. For "local" work, add Drupal 7 connection info to `settings.local.php`.
* Copy code from Step 4 here: https://github.com/CU-CommunityApps/cwd_migrate_policy/tree/main#steps

## Epilogue

Review "Post-migration clean-up" from Policy migration: https://github.com/CU-CommunityApps/cwd_migrate_policy/tree/main#post-migration-clean-up

As always, when done, put this module into a private repo on GitHub.

## Special stuff

For this migration, we added a patch and a module to get some cool "conditions" functionality.
* Source conditions are supported by a core patch (MR #849, issue #3069776).
* Process conditions are supported by the Migrate Conditions module.
* See upgrade_d7_block for usage examples.
