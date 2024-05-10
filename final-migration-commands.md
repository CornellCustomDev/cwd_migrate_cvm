# Command list from semi-final migration
p.s. `tdr` = `terminus drush`

FIRST, delete Elodie's account on Dev:
/admin/people?user=eeg47&status=All&role=All&permission=All
```
tdr cornell-cvm.dev -- mim --update upgrade_d7_user
tdr cornell-cvm.dev -- mim --update upgrade_d7_custom_block

tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_cvmscopes
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_org_codes
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_departments
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_diagnoses
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_health_info_categories
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_hospitals
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_job_position_types
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_membership_departments
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_person_keywords
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_research_areas
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_research_award_types
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_research_categories
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_sections
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_service_areas
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_species
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_canine_embryo
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_canine_parts
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_canine_stages
tdr cornell-cvm.dev -- mim --update upgrade_d7_taxonomy_term_ess_portfolio_project_type

tdr cornell-cvm.dev -- mim --update upgrade_d7_node_ahdc_news_and_announcements
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_ctrial
tdr cornell-cvm.dev -- mim --update upgrade_d7_node__chc_member
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_news
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_page
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_phd_dissertation_award
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_research_award
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_service
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_spotlight
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_webform
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_canine_image
tdr cornell-cvm.dev -- mim --update upgrade_d7_node_portfolio_project

tdr cornell-cvm.dev -- mim --update upgrade_d7_file

tdr cornell-cvm.dev -- migrate:duplicate-file-detection cwd_migrate_cvm_mf2m_canine_image_step1
tdr cornell-cvm.dev -- mim --update cwd_migrate_cvm_mf2m_canine_image_step1
tdr cornell-cvm.dev -- mim --update cwd_migrate_cvm_mf2m_canine_image_step2
tdr cornell-cvm.dev -- migrate:duplicate-file-detection mf2m_ctrial_step1
tdr cornell-cvm.dev -- mim --update mf2m_ctrial_step1
tdr cornell-cvm.dev -- mim --update mf2m_ctrial_step2
tdr cornell-cvm.dev -- migrate:duplicate-file-detection mf2m_news_step1
tdr cornell-cvm.dev -- mim --update mf2m_news_step1
tdr cornell-cvm.dev -- mim --update mf2m_news_step2
tdr cornell-cvm.dev -- migrate:duplicate-file-detection mf2m_page_step1
tdr cornell-cvm.dev -- mim --update mf2m_page_step1
tdr cornell-cvm.dev -- mim --update mf2m_page_step2
tdr cornell-cvm.dev -- migrate:duplicate-file-detection mf2m_phd_dissertation_award_step1
tdr cornell-cvm.dev -- mim --update mf2m_phd_dissertation_award_step1
tdr cornell-cvm.dev -- mim --update mf2m_phd_dissertation_award_step2
tdr cornell-cvm.dev -- migrate:duplicate-file-detection mf2m_portfolio_project_step1
tdr cornell-cvm.dev -- mim --update mf2m_portfolio_project_step1
tdr cornell-cvm.dev -- mim --update mf2m_portfolio_project_step2
tdr cornell-cvm.dev -- migrate:duplicate-file-detection mf2m_service_step1
tdr cornell-cvm.dev -- mim --update mf2m_service_step1
tdr cornell-cvm.dev -- mim --update mf2m_service_step2
tdr cornell-cvm.dev -- migrate:duplicate-file-detection mf2m_spotlight_step1
tdr cornell-cvm.dev -- mim --update mf2m_spotlight_step1
tdr cornell-cvm.dev -- mim --update mf2m_spotlight_step2
tdr cornell-cvm.dev -- migrate:duplicate-file-detection mf2m__chc_member_step1
tdr cornell-cvm.dev -- mim --update mf2m__chc_member_step1
tdr cornell-cvm.dev -- mim --update mf2m__chc_member_step2

# maybe not this one next time ⬇️ I didn't actually mean to -- or maybe it's fine!
tdr cornell-cvm.dev -- mim --update upgrade_d7_webform
tdr cornell-cvm.dev -- mim --update upgrade_d7_webform_submission

tdr cornell-cvm.dev -- mim --update upgrade_d7_menu_links
tdr cornell-cvm.dev -- mim --update upgrade_d7_url_alias
tdr cornell-cvm.dev -- mim --update upgrade_d7_path_redirect

tdr cornell-cvm.dev -- cr

# later, after Bill does private files rsync:
tdr cornell-cvm.dev -- mim --update upgrade_d7_file_private_do_not_rollback
```

(Also)
```
tdr cornell-cvm.dev -- ms upgrade_d7_menu_links --fields=id,total,imported,unprocessed,message_count
```
