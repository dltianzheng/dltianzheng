```sql

explain SELECT "internal_app_tvm_manager"."vuln_info_enhance"."id",
       "internal_app_tvm_manager"."vuln_info_enhance"."vul_type",
       "internal_app_tvm_manager"."vuln_info_enhance"."vul_number",
       "internal_app_tvm_manager"."vuln_info_enhance"."vul_category",
       "internal_app_tvm_manager"."vuln_info_enhance"."vul_category_id",
       "internal_app_tvm_manager"."vuln_info_enhance"."data_source",
       "internal_app_tvm_manager"."vuln_info_enhance"."vul_state",
       "internal_app_tvm_manager"."vuln_info_enhance"."vul_tags",
       "internal_app_tvm_manager"."vuln_info_enhance"."affect_assets",
       "internal_app_tvm_manager"."vuln_info_enhance"."detection_mode",
       "internal_app_tvm_manager"."vuln_info_enhance"."create_time",
       "internal_app_tvm_manager"."vuln_info_enhance"."update_time",
       "internal_app_tvm_manager"."vuln_info_enhance"."create_person",
       "internal_app_tvm_manager"."vuln_info_enhance"."update_person",
       "internal_app_tvm_manager"."vuln_info_enhance"."plugin_id",
       "internal_app_tvm_manager"."vuln_info_enhance"."vul_id",
       "internal_app_tvm_manager"."vuln_info_enhance"."cve_id",
       "internal_app_tvm_manager"."vuln_info_enhance"."bugtraq_id",
       "internal_app_tvm_manager"."vuln_info_enhance"."nsfocus_id",
       "internal_app_tvm_manager"."vuln_info_enhance"."osvdb",
       "internal_app_tvm_manager"."vuln_info_enhance"."edb",
       "internal_app_tvm_manager"."vuln_info_enhance"."cvss_base_score",
       "internal_app_tvm_manager"."vuln_info_enhance"."cnnvd",
       "internal_app_tvm_manager"."vuln_info_enhance"."cncve",
       "internal_app_tvm_manager"."vuln_info_enhance"."cnvd",
       "internal_app_tvm_manager"."vuln_info_enhance"."familiar",
       "internal_app_tvm_manager"."vuln_info_enhance"."severity_points",
       "internal_app_tvm_manager"."vuln_info_enhance"."threat_level",
       "internal_app_tvm_manager"."vuln_info_enhance"."date_recorded",
       "internal_app_tvm_manager"."vuln_info_enhance"."date_found",
       "internal_app_tvm_manager"."vuln_info_enhance"."is_banned",
       "internal_app_tvm_manager"."vuln_info_enhance"."is_testonly",
       "internal_app_tvm_manager"."vuln_info_enhance"."is_disabled",
       "internal_app_tvm_manager"."vuln_info_enhance"."i18n_name",
       "internal_app_tvm_manager"."vuln_info_enhance"."i18n_description",
       "internal_app_tvm_manager"."vuln_info_enhance"."i18n_morelinks",
       "internal_app_tvm_manager"."vuln_info_enhance"."i18n_patch",
       "internal_app_tvm_manager"."vuln_info_enhance"."patch",
       "internal_app_tvm_manager"."vuln_info_enhance"."ms_security_bulletin",
       "internal_app_tvm_manager"."vuln_info_enhance"."scan_method",
       "internal_app_tvm_manager"."vuln_info_enhance"."is_dangerous",
       "internal_app_tvm_manager"."vuln_info_enhance"."vendor",
       "internal_app_tvm_manager"."vuln_info_enhance"."reserved1",
       "internal_app_tvm_manager"."vuln_info_enhance"."reserved2",
       "internal_app_tvm_manager"."vuln_info_enhance"."reserved3",
       "internal_app_tvm_manager"."vuln_info_enhance"."reserved4",
       "internal_app_tvm_manager"."vuln_info_enhance"."reserved5",
       "internal_app_tvm_manager"."vuln_info_enhance"."is_update",
       "internal_app_tvm_manager"."vuln_info_enhance"."threshold",
       "internal_app_tvm_manager"."vuln_info_enhance"."publish_organization"
FROM "internal_app_tvm_manager"."vuln_info_enhance"
WHERE "internal_app_tvm_manager"."vuln_info_enhance"."vul_id" IN (SELECT U0."vul_id"
                                                                  FROM "internal_app_tvm_manager"."vuln_category_map_vuln" U0
                                                                  WHERE (vul_category_id in
                                                                         (SELECT "internal_app_tvm_manager"."vuln_category"."vul_category_id"
                                                                          FROM "internal_app_tvm_manager"."vuln_category")))
ORDER BY "internal_app_tvm_manager"."vuln_info_enhance"."create_time" DESC
LIMIT 10
```

```csv

```

Gather  (cost=168871.83..168872.86 rows=10 width=1801)
  Workers Planned: 1
  Single Copy: true
  ->  Limit  (cost=167871.83..167871.86 rows=10 width=1801)
        ->  Sort  (cost=167871.83..167873.89 rows=824 width=1801)
              Sort Key: vuln_info_enhance.create_time DESC
              ->  Hash Semi Join  (cost=156960.43..167854.03 rows=824 width=1801)
                    Hash Cond: ((vuln_info_enhance.vul_id)::text = (u0.vul_id)::text)
                    ->  Seq Scan on vuln_info_enhance  (cost=0.00..137.24 rows=824 width=1801)
                    ->  Hash  (cost=113391.14..113391.14 rows=2655623 width=6)
                          ->  Hash Semi Join  (cost=6957.09..113391.14 rows=2655623 width=6)
                                Hash Cond: (u0.vul_category_id = vuln_category.vul_category_id)
                                ->  Seq Scan on vuln_category_map_vuln u0  (cost=0.00..43225.23 rows=2655623 width=14)
                                ->  Hash  (cost=3765.93..3765.93 rows=194493 width=8)
                                      ->  Seq Scan on vuln_category  (cost=0.00..3765.93 rows=194493 width=8)







```sql
explain SELECT "internal_app_tvm_manager"."vuln_info_enhance"."id", "internal_app_tvm_manager"."vuln_info_enhance"."vul_type", "internal_app_tvm_manager"."vuln_info_enhance"."vul_number", "internal_app_tvm_manager"."vuln_info_enhance"."vul_category", "internal_app_tvm_manager"."vuln_info_enhance"."vul_category_id", "internal_app_tvm_manager"."vuln_info_enhance"."data_source", "internal_app_tvm_manager"."vuln_info_enhance"."vul_state", "internal_app_tvm_manager"."vuln_info_enhance"."vul_tags", "internal_app_tvm_manager"."vuln_info_enhance"."affect_assets", "internal_app_tvm_manager"."vuln_info_enhance"."detection_mode", "internal_app_tvm_manager"."vuln_info_enhance"."create_time", "internal_app_tvm_manager"."vuln_info_enhance"."update_time", "internal_app_tvm_manager"."vuln_info_enhance"."create_person", "internal_app_tvm_manager"."vuln_info_enhance"."update_person", "internal_app_tvm_manager"."vuln_info_enhance"."plugin_id", "internal_app_tvm_manager"."vuln_info_enhance"."vul_id", "internal_app_tvm_manager"."vuln_info_enhance"."cve_id", "internal_app_tvm_manager"."vuln_info_enhance"."bugtraq_id", "internal_app_tvm_manager"."vuln_info_enhance"."nsfocus_id", "internal_app_tvm_manager"."vuln_info_enhance"."osvdb", "internal_app_tvm_manager"."vuln_info_enhance"."edb", "internal_app_tvm_manager"."vuln_info_enhance"."cvss_base_score", "internal_app_tvm_manager"."vuln_info_enhance"."cnnvd", "internal_app_tvm_manager"."vuln_info_enhance"."cncve", "internal_app_tvm_manager"."vuln_info_enhance"."cnvd", "internal_app_tvm_manager"."vuln_info_enhance"."familiar", "internal_app_tvm_manager"."vuln_info_enhance"."severity_points", "internal_app_tvm_manager"."vuln_info_enhance"."threat_level", "internal_app_tvm_manager"."vuln_info_enhance"."date_recorded", "internal_app_tvm_manager"."vuln_info_enhance"."date_found", "internal_app_tvm_manager"."vuln_info_enhance"."is_banned", "internal_app_tvm_manager"."vuln_info_enhance"."is_testonly", "internal_app_tvm_manager"."vuln_info_enhance"."is_disabled", "internal_app_tvm_manager"."vuln_info_enhance"."i18n_name", "internal_app_tvm_manager"."vuln_info_enhance"."i18n_description", "internal_app_tvm_manager"."vuln_info_enhance"."i18n_morelinks", "internal_app_tvm_manager"."vuln_info_enhance"."i18n_patch", "internal_app_tvm_manager"."vuln_info_enhance"."patch", "internal_app_tvm_manager"."vuln_info_enhance"."ms_security_bulletin", "internal_app_tvm_manager"."vuln_info_enhance"."scan_method", "internal_app_tvm_manager"."vuln_info_enhance"."is_dangerous", "internal_app_tvm_manager"."vuln_info_enhance"."vendor", "internal_app_tvm_manager"."vuln_info_enhance"."reserved1", "internal_app_tvm_manager"."vuln_info_enhance"."reserved2", "internal_app_tvm_manager"."vuln_info_enhance"."reserved3", "internal_app_tvm_manager"."vuln_info_enhance"."reserved4", "internal_app_tvm_manager"."vuln_info_enhance"."reserved5", "internal_app_tvm_manager"."vuln_info_enhance"."is_update", "internal_app_tvm_manager"."vuln_info_enhance"."threshold", "internal_app_tvm_manager"."vuln_info_enhance"."publish_organization" FROM "internal_app_tvm_manager"."vuln_info_enhance" WHERE "internal_app_tvm_manager"."vuln_info_enhance"."vul_id" IN (SELECT U0."vul_id" FROM "internal_app_tvm_manager"."vuln_category_map_vuln" U0 WHERE (vul_category_id in (
    WITH RECURSIVE team(vul_category_id, parent_id) AS (
          SELECT vul_category_id, parent_id
          FROM "internal_app_tvm_manager"."vuln_category"
          WHERE parent_id = 0
        UNION ALL
          SELECT sm.vul_category_id, sm.parent_id
          FROM "internal_app_tvm_manager"."vuln_category" AS sm, team AS t
          WHERE sm.parent_id = t.vul_category_id
        )
    SELECT vul_category_id FROM team
    ))) ORDER BY "internal_app_tvm_manager"."vuln_info_enhance"."create_time" DESC LIMIT 10
```

Limit  (cost=326527.47..326527.50 rows=10 width=1801)
  ->  Sort  (cost=326527.47..326529.53 rows=824 width=1801)
        Sort Key: vuln_info_enhance.create_time DESC
        ->  Hash Semi Join  (cost=320803.07..326509.67 rows=824 width=1801)
              Hash Cond: ((vuln_info_enhance.vul_id)::text = (u0.vul_id)::text)
              ->  Seq Scan on vuln_info_enhance  (cost=0.00..137.24 rows=824 width=1801)
              ->  Hash  (cost=299018.42..299018.42 rows=1327812 width=6)
                    ->  Hash Join  (cost=234050.27..299018.42 rows=1327812 width=6)
                          Hash Cond: (u0.vul_category_id = team.vul_category_id)
                          ->  Seq Scan on vuln_category_map_vuln u0  (cost=0.00..43225.23 rows=2655623 width=14)
                          ->  Hash  (cost=234047.77..234047.77 rows=200 width=8)
                                ->  HashAggregate  (cost=234045.77..234047.77 rows=200 width=8)
                                      Group Key: team.vul_category_id
                                      ->  CTE Scan on team  (cost=164513.90..207302.74 rows=2139442 width=8)
                                            CTE team
                                              ->  Recursive Union  (cost=0.00..164513.90 rows=2139442 width=16)
                                                    ->  Seq Scan on vuln_category  (cost=0.00..4252.16 rows=22 width=16)
                                                          Filter: (parent_id = 0)
                                                    ->  Hash Join  (cost=7.15..11747.29 rows=213942 width=16)
                                                          Hash Cond: (sm.parent_id = t.vul_category_id)
                                                          ->  Seq Scan on vuln_category sm  (cost=0.00..3765.93 rows=194493 width=16)
                                                          ->  Hash  (cost=4.40..4.40 rows=220 width=8)
                                                                ->  WorkTable Scan on team t  (cost=0.00..4.40 rows=220 width=8)