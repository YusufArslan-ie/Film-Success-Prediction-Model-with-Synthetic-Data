TABLES:

1. films
2. characters
3. crew_members
3. story_and_themes
4. soundtracks
5. settings_and_world
6. animation_settings
7. symbolism_and_motifs
8. release_info
9. sociopolitical
10. rating
11. cultural_info
12. parents_guide
13. franchise

COLUMNS:
1. films:
NOT NULL	PK	int		film_id
	nvarchar(200)	film_name
	smallint	release_year
	nvarchar(200)	genre
	smallint	film_duration
	nvarchar(50)	film_country
	varchar(10)	film_language
	decimal(19, 0)	film_budget
	decimal(19, 0)	film_box_office
	bigint	film_votes_count
	varchar(20)	film_release_platform
	tinyint	film_name_word_count
	varchar(10)	film_age_rating
	smallint	film_awards_count
	nvarchar(150)	studio_name
	
2. characters:
NOT NULL	PK	int	- **char_id**: Her filmden bağımsız olarak artan GLOBAL benzersiz tamsayı. Önceki filmin son değerinden devam et.
NOT NULL	FK	int	- **film_id**: films.csv ile eşleşen ID.
int	- **billing_order**: Film içi sıralama (1’den başlayarak film bazında artar).
nvarchar(200)	- **char_name**:
nvarchar(200)	- **actor_name**:
nvarchar(50)	- **char_gender**: M|F|X|unknown
nvarchar(50)	- **char_fate**: alive|dead|ambiguous
nvarchar(50)	- **hero_or_villain**: hero|villain|neutral
nvarchar(200)	- **personality_traits**: küçük harfli kısa etiketler, ‘|’ ile ayrılır (ör. brave|loyal|curious)
nvarchar(10)	- **is_protagonist**: TRUE/FALSE
float			- **screen_time_ratio**: 0–1 arası ondalık
nvarchar(200)			- **role_type**: lead|supporting|cameo|villain
nvarchar(200)	- **performance_type**: LiveAction|Voice|MotionCapture

 3. crew_members:
NOT NULL	PK	int	- crew_id film değişse de GLOBAL benzersiz olacak ve sürekli artacak.
NOT NULL	FK	int	- film_id: films.csv ile eşleşen ID.
varchar(150) - person_name:	
varchar(60)	- job_title: kısa ve tanımlayıcı (Director, Writer, Producer, Composer, Cinematographer, Editor, Art Director, Visual Effects Supervisor, vb.)
varchar(40)	- department: Directing, Writing, Production, Sound, Camera, Editing, Art, VisualEffects gibi geniş kategori.
varchar(5)	- award_won_for_film: TRUE/FALSE (kişinin bu filmle ödül kazanıp kazanmadığı).

4. soundtracks:
NOT NULL	PK	nvarchar(100)	**soundtrack_id**: globally unique integer, increasing independently of films.
NOT NULL	FK	nvarchar(100)	**film_id**: must match the ID from *films.csv*.
nvarchar(4000)	**track_title**: title of the track.
nvarchar(4000)	**composer_name**: composer of the track.
nvarchar(4000)	**performer_name**: performer or vocalist (leave blank if instrumental).
nvarchar(100)	**is_main_theme**: TRUE/FALSE.
nvarchar(4000)	**music_genres**: orchestral|ambient|ethnic|pop|electronic|romantic|jazz|rock|other (use “|” to separate multiple genres).
nvarchar(100)	**vocal_presence**: TRUE/FALSE.
nvarchar(100)	**cultural_instrument_usage**: TRUE/FALSE (TRUE if traditional or ethnic instruments are used).
nvarchar(100)	**diegetic**: TRUE/FALSE (TRUE if the music is heard by the characters within the scene).
nvarchar(100)	**track_emotional_intensity**: decimal 0–1 (emotional intensity of the piece).
nvarchar(100)	**scene_usage_type**: intro|battle|love|funeral|transition|credits|other.
nvarchar(100)	**award_won**: TRUE/FALSE (TRUE if the piece won an award for film music).

5. settings_and_world:
NOT NULL	PK,FK	int		film_id:	 must match the ID in films.csv.
varchar(20)		setting_type: Urban|Rural|Space|Underwater|FantasyWorld|Historical|PostApocalyptic|Maritime|Mixed.
varchar(5)		fictional_world_present: TRUE/FALSE.
varchar(5)		real_location_reference: TRUE/FALSE.
float 	setting_importance_score: decimal 0–1 (how central the setting is to the story).
varchar(10)		time_period: Past|Present|Future|Mixed.
varchar(20)		geographical_scope: Local|National|Global|Interplanetary.
varchar(5)		weather_motif_present: TRUE/FALSE (TRUE if climate/weather is used symbolically or dramatically).
varchar(20)		dominant_color_tone: Warm|Cold|Desaturated|HighContrast|Natural.
varchar(20)		technological_level: Primitive|Modern|Futuristic.
varchar(20)		societal_structure: Democracy|Empire|Dystopia|Tribal|Corporate|Unknown.
varchar(20)	environmental_condition: Intact|Polluted|Destroyed|Idealized.

6. animation_settings:
NOT NULL	PK,FK	int	- film_id: films.csv ile eşleşen ID.
varchar(15)	- animation_type: 2D|3D|StopMotion|Hybrid.
varchar(15)	- visual_style: Cartoony|Realistic|Stylized|Minimalist|Painterly.
int	- frame_rate: sayısal (ör. 24, 30, 60).
varchar(15)	- render_technique: RayTracing|PathTracing|Rasterization|Hybrid|Other.
varchar(15)	- character_design_style: Exaggerated|Proportional|Abstract|Realistic.
varchar(15)	- color_palette_type: Warm|Cold|Vibrant|Desaturated|Monochrome.
float	- animation_realism_level: 0–1 arası (gerçekçiliğin derecesi).
varchar(5)	- hand_drawn_elements_present: TRUE/FALSE.
varchar(5)	- motion_capture_used: TRUE/FALSE.
varchar(5)	- stop_motion_used: TRUE/FALSE.
varchar(5)	- ai_generated_elements_present: TRUE/FALSE (görsel üretimde üretken yapay zekâ unsuru kullanıldıysa TRUE).
varchar(20)	- production_software: Blender|Maya|Houdini|Unreal|Unity|Custom|Other.
varchar(20)	- art_direction_tone: Whimsical|Dark|Epic|Dreamlike|Futuristic|Naturalistic|Other.
varchar(5)	- animation_award_won: TRUE/FALSE.

7. symbolism_and_motifs:
NOT NULL	PK,FK	int	- film_id: films.csv ile eşleşen ID.
float	- symbolism_density: 0–1 arası (filmde sembollerin genel yoğunluğu).
varchar(5)	- color_symbolism_present: TRUE/FALSE (renklerin anlam taşıdığı sahneler varsa TRUE).
varchar(5)	- water_motif_present: TRUE/FALSE.
varchar(5)	- fire_motif_present: TRUE/FALSE.
varchar(5)	- animal_symbolism_present: TRUE/FALSE.
varchar(5)	- dream_sequence_present: TRUE/FALSE.
varchar(5)	- mirror_or_reflection_motif: TRUE/FALSE.
varchar(5)	- recurring_object_symbol: TRUE/FALSE.
varchar(5)	- death_symbolism_present: TRUE/FALSE. 
varchar(5)	- religious_symbolism_present: TRUE/FALSE.
varchar(5)	- technological_symbolism_present: TRUE/FALSE.
varchar(5)	- nature_vs_industry_theme: TRUE/FALSE.
float	- visual_metaphor_strength: 0–1 arası (görsel metafor gücü).
varchar(5)	- symbolic_resolution: TRUE/FALSE (filmin sonunda semboller açıklığa kavuşuyorsa TRUE).

8. release_info:
NOT NULL	PK,FK	int	- film_id must match films.csv.
date	- release_date: YYYY-MM-DD (verify via Wikipedia or IMDb).
int	- release_year: 4-digit year.
varchar(15)	- release_month: 1–12 or month name.
varchar(10)	- release_season: Winter|Spring|Summer|Fall (Northern Hemisphere).
varchar(10)	- release_day_of_week: Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Sunday.
varchar(5)	- holiday_release: TRUE/FALSE.
varchar(5)	- covid_era_release: TRUE/FALSE (TRUE if between 2020-03 and 2021-12).
varchar(15)	- theatrical_vs_digital: Cinema|Streaming|Hybrid.
varchar(5)	- simultaneous_release: TRUE/FALSE.
varchar(15)	- runtime_context: normal|limited|re-release|extended|special.

9. sociopolitical:
NOT NULL	PK,FK	int	**film_id**: must match the ID from *films.csv*.
varchar(5)	**political_content_present**: TRUE/FALSE (TRUE if the film includes political or ideological subtext).
varchar(20)	**political_alignment**: neutral|progressive|conservative|anti_establishment|authoritarian.
varchar(15)	**social_issue_focus**: gender|race|class|environment|lgbt|war|other (primary social theme).
varchar(5)	**lgbt_representation_present**: TRUE/FALSE.
float	**minority_representation_strength**: decimal 0–1 (extent of minority or cultural diversity representation).
varchar(5)	**gender_equality_focus**: TRUE/FALSE (TRUE if gender equality or feminist themes are highlighted).
varchar(5)	**war_or_conflict_related**: TRUE/FALSE.
varchar(5)	**environmental_theme_present**: TRUE/FALSE.
float	**activism_message_strength**: decimal 0–1 (intensity of activism, rebellion, or social awareness message).
float	**controversy_level**: decimal 0–1 (degree of political or ethical controversy generated by the film).
varchar(5)	**propaganda_tone**: TRUE/FALSE (TRUE if the film explicitly promotes an ideology).

10. rating:
NOT NULL	PK,FK	int	film_id
float	audience_rating_mean
float	critic_rating_mean
float	rating_gap
int	review_count
float	social_sentiment_score
int	trending_duration_days
varchar(20)	primary_source
int	platform_coverage_count
date	peak_popularity_date

11. cultural_info:
NOT NULL	PK,FK	int	film_id: must match the ID from films.csv.
float	slang_intensity: decimal between 0 and 1 (level of slang usage).
varchar(20)	accent_comedy_used: TRUE/FALSE.
varchar(20)	accent_region: specify if a dialect/accent is used (e.g., Texas, Cockney, Black Sea); leave blank if none.
varchar(20)	cultural_humor_type: one of the following → dialect|dark_humor|absurd|slapstick|political|situational|satirical|wordplay|romantic|other.
varchar(20)	language_switching: TRUE/FALSE (TRUE if the film switches between different languages).
varchar(20)	cultural_instrument_usage: TRUE/FALSE (TRUE if traditional or ethnic instruments are used in the soundtrack).
float	translation_difficulty_score: decimal between 0 and 1 (difficulty of translating cultural or humor references).
varchar(20)	choreographic_dance_present: TRUE/FALSE (TRUE if the film contains notable choreographed dance scenes).

12. parents_guide:
NOT NULL	PK,FK	int			**film_id**: must match the ID from *films.csv*.
float		**family_friendly_score**: decimal 0–1 (overall family suitability, 1 = very family-friendly).
float		**violence_intensity**: decimal 0–1 (violence, war, or blood level).
varchar(5)	**sexual_content_present**: TRUE/FALSE.
float		**sexual_content_intensity**: decimal 0–1 (intensity of sexual scenes).
float		**language_intensity**: decimal 0–1 (amount of profanity or strong language).
varchar(5)	**substance_use_present**: TRUE/FALSE (TRUE if alcohol, smoking, or drug use appears).
float		**frightening_scenes_intensity**: decimal 0–1 (level of frightening or disturbing scenes).
varchar(10)	**age_recommendation**: All|7+|12+|13+|15+|16+|18+ (recommended viewing age).
varchar(20)	**age_rating_source**: IMDb|MPAA|BBFC|Netflix|RottenTomatoes (rating source).

13. franchise:
NOT NULL	PK,FK	int		**film_id**: must match the ID from *films.csv*.
varchar(5)	**is_sequel**: TRUE/FALSE.
int		**sequel_number**: only fill this if **is_sequel = TRUE** (use 2, 3, …). Leave blank otherwise.
varchar(100)	**franchise_name**: name of the franchise (leave blank if none).
int		**franchise_total_films**: total number of films in the franchise (leave blank if unknown).
decimal(4, 2)	**franchise_avg_rating**: decimal 0–10 (approximate average rating of the franchise, based on reliable sources; leave blank if unknown).
varchar(50)		**in_universe_order**: chronological order within the fictional universe (leave blank if unknown).
	