films

| Column                | Type          | Constraints  | Description                                    | Example      |
| --------------------- | ------------- | ------------ | ---------------------------------------------- | ------------ |
| film_id               | INT           | PK, NOT NULL | Unique film key                                | 101          |
| film_name             | NVARCHAR(200) | NOT NULL     | Film title                                     | Arrival      |
| release_year          | SMALLINT      |              | Four-digit year                                | 2016         |
| genre                 | NVARCHAR(200) |              | One or more genres, pipe-separated if multiple | Sci-Fi|Drama |
| film_duration         | SMALLINT      |              | Runtime in minutes                             | 116          |
| film_country          | NVARCHAR(50)  |              | Country                                        | USA          |
| film_language         | VARCHAR(10)   |              | ISO code or name                               | en           |
| film_budget           | DECIMAL(19,0) |              | Budget in USD                                  | 16000000     |
| film_box_office       | DECIMAL(19,0) |              | Worldwide gross in USD                         | 203000000    |
| film_votes_count      | BIGINT        |              | Vote count                                     | 650000       |
| film_release_platform | VARCHAR(20)   |              | Cinema|Streaming|Hybrid                        | Cinema       |
| film_name_word_count  | TINYINT       |              | Word count of title                            | 1            |
| film_age_rating       | VARCHAR(10)   |              | MPAA/BBFC or similar                           | PG-13        |
| film_awards_count     | SMALLINT      |              | Number of awards won                           | 8            |
| studio_name           | NVARCHAR(150) |              | Studio or distributor                          | Paramount    |

characters

| Column             | Type          | Constraints                 | Description                             | Example       |
| ------------------ | ------------- | --------------------------- | --------------------------------------- | ------------- |
| char_id            | INT           | PK, NOT NULL                | Global unique character key             | 50023         |
| film_id            | INT           | FK→films(film_id), NOT NULL | Parent film                             | 101           |
| billing_order      | INT           |                             | Order within film, starts at 1          | 1             |
| char_name          | NVARCHAR(200) |                             | Character name                          | Louise Banks  |
| actor_name         | NVARCHAR(200) |                             | Performer name                          | Amy Adams     |
| char_gender        | NVARCHAR(50)  |                             | Allowed: M|F|X|unknown                  | F             |
| char_fate          | NVARCHAR(50)  |                             | Allowed: alive|dead|ambiguous           | alive         |
| hero_or_villain    | NVARCHAR(50)  |                             | Allowed: hero|villain|neutral           | hero          |
| personality_traits | NVARCHAR(200) |                             | Lowercase tags, pipe-separated          | brave|curious |
| is_protagonist     | BIT           |                             | 1 if protagonist                        | 1             |
| screen_time_ratio  | FLOAT         |                             | 0–1 share of total runtime              | 0.62          |
| role_type          | NVARCHAR(200) |                             | Allowed: lead|supporting|cameo|villain  | lead          |
| performance_type   | NVARCHAR(200) |                             | Allowed: LiveAction|Voice|MotionCapture | LiveAction    |

crew_members

| Column             | Type         | Constraints                 | Description                                  | Example          |
| ------------------ | ------------ | --------------------------- | -------------------------------------------- | ---------------- |
| crew_id            | INT          | PK, NOT NULL                | Global unique crew key                       | 70012            |
| film_id            | INT          | FK→films(film_id), NOT NULL | Parent film                                  | 101              |
| person_name        | VARCHAR(150) |                             | Crew person name                             | Denis Villeneuve |
| job_title          | VARCHAR(60)  |                             | Role title (Director, Writer, etc.)          | Director         |
| department         | VARCHAR(40)  |                             | Broad dept (Directing, Writing, Production…) | Directing        |
| award_won_for_film | BIT          |                             | 1 if this person won an award for this film  | 0                |

soundtracks

| Column                    | Type           | Constraints                 | Description                                         | Example            |
| ------------------------- | -------------- | --------------------------- | --------------------------------------------------- | ------------------ |
| soundtrack_id             | INT            | PK, NOT NULL                | Global unique soundtrack key                        | 900034             |
| film_id                   | INT            | FK→films(film_id), NOT NULL | Parent film                                         | 101                |
| track_title               | NVARCHAR(4000) |                             | Track title                                         | Main Theme         |
| composer_name             | NVARCHAR(4000) |                             | Composer                                            | Jóhann Jóhannsson  |
| performer_name            | NVARCHAR(4000) |                             | Vocalist/performer, blank if instrumental           | —                  |
| is_main_theme             | BIT            |                             | 1 if main theme                                     | 1                  |
| music_genres              | NVARCHAR(4000) |                             | Tags: orchestral|ambient|electronic… pipe-separated | orchestral|ambient |
| vocal_presence            | BIT            |                             | 1 if vocals present                                 | 0                  |
| cultural_instrument_usage | BIT            |                             | 1 if traditional/ethnic instruments used            | 0                  |
| diegetic                  | BIT            |                             | 1 if heard by characters                            | 0                  |
| track_emotional_intensity | FLOAT          |                             | 0–1 emotional intensity                             | 0.8                |
| scene_usage_type          | NVARCHAR(100)  |                             | intro|battle|love|funeral|transition|credits|other  | intro              |
| award_won                 | BIT            |                             | 1 if the piece won an award                         | 0                  |

settings_and_world

| Column                   | Type        | Constraints           | Description                                        | Example     |
| ------------------------ | ----------- | --------------------- | -------------------------------------------------- | ----------- |
| film_id                  | INT         | PK, FK→films(film_id) | One-to-one with films                              | 101         |
| setting_type             | VARCHAR(20) |                       | Urban|Rural|Space|Historical…                      | Urban       |
| fictional_world_present  | BIT         |                       | 1 if fictional world                               | 0           |
| real_location_reference  | BIT         |                       | 1 if real places referenced                        | 1           |
| setting_importance_score | FLOAT       |                       | 0–1 centrality of setting                          | 0.7         |
| time_period              | VARCHAR(10) |                       | Past|Present|Future|Mixed                          | Present     |
| geographical_scope       | VARCHAR(20) |                       | Local|National|Global|Interplanetary               | Global      |
| weather_motif_present    | BIT         |                       | 1 if weather as motif                              | 0           |
| dominant_color_tone      | VARCHAR(20) |                       | Warm|Cold|Desaturated|HighContrast|Natural         | Desaturated |
| technological_level      | VARCHAR(20) |                       | Primitive|Modern|Futuristic                        | Modern      |
| societal_structure       | VARCHAR(20) |                       | Democracy|Empire|Dystopia|Tribal|Corporate|Unknown | Democracy   |
| environmental_condition  | VARCHAR(20) |                       | Intact|Polluted|Destroyed|Idealized                | Intact      |

animation_settings

| Column                        | Type        | Constraints           | Description                                       | Example       |
| ----------------------------- | ----------- | --------------------- | ------------------------------------------------- | ------------- |
| film_id                       | INT         | PK, FK→films(film_id) | One-to-one with films                             | 101           |
| animation_type                | VARCHAR(15) |                       | 2D|3D|StopMotion|Hybrid                           | 3D            |
| visual_style                  | VARCHAR(15) |                       | Cartoony|Realistic|Stylized|Minimalist|Painterly  | Realistic     |
| frame_rate                    | INT         |                       | Frames per second                                 | 24            |
| render_technique              | VARCHAR(15) |                       | RayTracing|PathTracing|Rasterization|Hybrid|Other | Rasterization |
| character_design_style        | VARCHAR(15) |                       | Exaggerated|Proportional|Abstract|Realistic       | Proportional  |
| color_palette_type            | VARCHAR(15) |                       | Warm|Cold|Vibrant|Desaturated|Monochrome          | Desaturated   |
| animation_realism_level       | FLOAT       |                       | 0–1 realism                                       | 0.6           |
| hand_drawn_elements_present   | BIT         |                       | 1 if hand-drawn elements                          | 0             |
| motion_capture_used           | BIT         |                       | 1 if mocap used                                   | 0             |
| stop_motion_used              | BIT         |                       | 1 if stop-motion used                             | 0             |
| ai_generated_elements_present | BIT         |                       | 1 if gen-AI visuals used                          | 0             |
| production_software           | VARCHAR(20) |                       | Blender|Maya|Houdini|Unreal|Unity|Custom|Other    | Blender       |
| art_direction_tone            | VARCHAR(20) |                       | Whimsical|Dark|Epic|Dreamlike|Futuristic|…        | Futuristic    |
| animation_award_won           | BIT         |                       | 1 if won animation award                          | 0             |

symbolism_and_motifs

| Column                          | Type  | Constraints           | Description                    | Example |
| ------------------------------- | ----- | --------------------- | ------------------------------ | ------- |
| film_id                         | INT   | PK, FK→films(film_id) | One-to-one with films          | 101     |
| symbolism_density               | FLOAT |                       | 0–1 overall symbolism density  | 0.5     |
| color_symbolism_present         | BIT   |                       | 1 if present                   | 1       |
| water_motif_present             | BIT   |                       |                                | 0       |
| fire_motif_present              | BIT   |                       |                                | 0       |
| animal_symbolism_present        | BIT   |                       |                                | 0       |
| dream_sequence_present          | BIT   |                       |                                | 0       |
| mirror_or_reflection_motif      | BIT   |                       |                                | 0       |
| recurring_object_symbol         | BIT   |                       |                                | 1       |
| death_symbolism_present         | BIT   |                       |                                | 0       |
| religious_symbolism_present     | BIT   |                       |                                | 0       |
| technological_symbolism_present | BIT   |                       |                                | 0       |
| nature_vs_industry_theme        | BIT   |                       |                                | 0       |
| visual_metaphor_strength        | FLOAT |                       | 0–1                            | 0.6     |
| symbolic_resolution             | BIT   |                       | 1 if symbols resolve in ending | 1       |

release_info

| Column                | Type        | Constraints           | Description                                     | Example    |
| --------------------- | ----------- | --------------------- | ----------------------------------------------- | ---------- |
| film_id               | INT         | PK, FK→films(film_id) | One-to-one with films                           | 101        |
| release_date          | DATE        |                       | YYYY-MM-DD                                      | 2016-11-11 |
| release_year          | INT         |                       | Four-digit year                                 | 2016       |
| release_month         | VARCHAR(15) |                       | 1–12 or month name                              | 11         |
| release_season        | VARCHAR(10) |                       | Winter|Spring|Summer|Fall (Northern Hemisphere) | Fall       |
| release_day_of_week   | VARCHAR(10) |                       | Monday…Sunday                                   | Friday     |
| holiday_release       | BIT         |                       | 1 if on/near holiday                            | 0          |
| covid_era_release     | BIT         |                       | 1 if 2020-03 to 2021-12                         | 0          |
| theatrical_vs_digital | VARCHAR(15) |                       | Cinema|Streaming|Hybrid                         | Cinema     |
| simultaneous_release  | BIT         |                       | 1 if simultaneous across channels               | 0          |
| runtime_context       | VARCHAR(15) |                       | normal|limited|re-release|extended|special      | normal     |

sociopolitical

| Column                           | Type        | Constraints           | Description                                                       | Example     |
| -------------------------------- | ----------- | --------------------- | ----------------------------------------------------------------- | ----------- |
| film_id                          | INT         | PK, FK→films(film_id) | One-to-one with films                                             | 101         |
| political_content_present        | BIT         |                       | 1 if political or ideological subtext                             | 1           |
| political_alignment              | VARCHAR(20) |                       | neutral|progressive|conservative|anti_establishment|authoritarian | neutral     |
| social_issue_focus               | VARCHAR(15) |                       | gender|race|class|environment|lgbt|war|other                      | environment |
| lgbt_representation_present      | BIT         |                       |                                                                   | 0           |
| minority_representation_strength | FLOAT       |                       | 0–1 extent of minority/cultural diversity                         | 0.4         |
| gender_equality_focus            | BIT         |                       |                                                                   | 0           |
| war_or_conflict_related          | BIT         |                       |                                                                   | 0           |
| environmental_theme_present      | BIT         |                       |                                                                   | 1           |
| activism_message_strength        | FLOAT       |                       | 0–1 intensity of activism/social awareness                        | 0.3         |
| controversy_level                | FLOAT       |                       | 0–1 controversy level                                             | 0.2         |
| propaganda_tone                  | BIT         |                       | 1 if explicit ideological promotion                               | 0           |

rating

| Column                  | Type        | Constraints           | Description                      | Example    |
| ----------------------- | ----------- | --------------------- | -------------------------------- | ---------- |
| film_id                 | INT         | PK, FK→films(film_id) | One-to-one with films            | 101        |
| audience_rating_mean    | FLOAT       |                       | Mean audience rating             | 7.9        |
| critic_rating_mean      | FLOAT       |                       | Mean critic rating               | 8.2        |
| rating_gap              | FLOAT       |                       | audience − critic                | -0.3       |
| review_count            | INT         |                       | Total reviews                    | 1250       |
| social_sentiment_score  | FLOAT       |                       | 0–1 normalized sentiment         | 0.76       |
| trending_duration_days  | INT         |                       | Days trending on major platforms | 12         |
| primary_source          | VARCHAR(20) |                       | IMDb|RT|Metacritic|TMDb|Other    | IMDb       |
| platform_coverage_count | INT         |                       | Number of platforms covered      | 4          |
| peak_popularity_date    | DATE        |                       | Date of peak interest            | 2016-11-18 |

cultural_info

| Column                       | Type        | Constraints           | Description                                                 | Example     |
| ---------------------------- | ----------- | --------------------- | ----------------------------------------------------------- | ----------- |
| film_id                      | INT         | PK, FK→films(film_id) | One-to-one with films                                       | 101         |
| slang_intensity              | FLOAT       |                       | 0–1 slang usage level                                       | 0.2         |
| accent_comedy_used           | BIT         |                       | 1 if accent/dialect humor used                              | 0           |
| accent_region                | VARCHAR(20) |                       | Region or dialect label, blank if none                      | Cockney     |
| cultural_humor_type          | VARCHAR(20) |                       | dialect|dark_humor|absurd|slapstick|political|situational|… | situational |
| language_switching           | BIT         |                       | 1 if multiple languages in dialogue                         | 0           |
| cultural_instrument_usage    | BIT         |                       | 1 if traditional/ethnic instruments used in soundtrack      | 0           |
| translation_difficulty_score | FLOAT       |                       | 0–1 difficulty of translating culture-bound references      | 0.3         |
| choreographic_dance_present  | BIT         |                       | 1 if notable choreographed dance scenes                     | 0           |

parents_guide

| Column                       | Type        | Constraints           | Description                           | Example |
| ---------------------------- | ----------- | --------------------- | ------------------------------------- | ------- |
| film_id                      | INT         | PK, FK→films(film_id) | One-to-one with films                 | 101     |
| family_friendly_score        | FLOAT       |                       | 0–1 overall suitability               | 0.7     |
| violence_intensity           | FLOAT       |                       | 0–1                                   | 0.2     |
| sexual_content_present       | BIT         |                       | 1 if any sexual content               | 0       |
| sexual_content_intensity     | FLOAT       |                       | 0–1                                   | 0.1     |
| language_intensity           | FLOAT       |                       | 0–1 profanity strength                | 0.3     |
| substance_use_present        | BIT         |                       | 1 if alcohol/smoking/drugs appear     | 1       |
| frightening_scenes_intensity | FLOAT       |                       | 0–1                                   | 0.2     |
| age_recommendation           | VARCHAR(10) |                       | All|7+|12+|13+|15+|16+|18+            | 13+     |
| age_rating_source            | VARCHAR(20) |                       | IMDb|MPAA|BBFC|Netflix|RottenTomatoes | MPAA    |

franchise

| Column                | Type         | Constraints           | Description               | Example |
| --------------------- | ------------ | --------------------- | ------------------------- | ------- |
| film_id               | INT          | PK, FK→films(film_id) | One-to-one with films     | 101     |
| is_sequel             | BIT          |                       | 1 if sequel               | 1       |
| sequel_number         | INT          |                       | Fill only if sequel       | 2       |
| franchise_name        | VARCHAR(100) |                       | Franchise label           | Alien   |
| franchise_total_films | INT          |                       | Total films in franchise  | 6       |
| franchise_avg_rating  | DECIMAL(4,2) |                       | 0–10 average rating       | 7.40    |
| in_universe_order     | VARCHAR(50)  |                       | Chronological order label | Prequel |


