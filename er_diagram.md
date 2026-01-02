erDiagram
  FILMS {
    int film_id PK
    string film_name
    smallint release_year
    string genre
    smallint film_duration
    string film_country
    string film_language
    decimal film_budget
    decimal film_box_office
    bigint film_votes_count
    string film_release_platform
    tinyint film_name_word_count
    string film_age_rating
    smallint film_awards_count
    string studio_name
  }

  CHARACTERS {
    int char_id PK
    int film_id FK
    int billing_order
    string char_name
    string actor_name
    string char_gender
    string char_fate
    string hero_or_villain
    string personality_traits
    string is_protagonist
    float  screen_time_ratio
    string role_type
    string performance_type
  }

  CREW_MEMBERS {
    int crew_id PK
    int film_id FK
    string person_name
    string job_title
    string department
    string award_won_for_film
  }

  SOUNDTRACKS {
    int soundtrack_id PK
    int film_id FK
    string track_title
    string composer_name
    string performer_name
    string is_main_theme
    string music_genres
    string vocal_presence
    string cultural_instrument_usage
    string diegetic
    float  track_emotional_intensity
    string scene_usage_type
    string award_won
  }

  SETTINGS_AND_WORLD {
    int film_id PK, FK
    string setting_type
    string fictional_world_present
    string real_location_reference
    float  setting_importance_score
    string time_period
    string geographical_scope
    string weather_motif_present
    string dominant_color_tone
    string technological_level
    string societal_structure
    string environmental_condition
  }

  ANIMATION_SETTINGS {
    int film_id PK, FK
    string animation_type
    string visual_style
    int    frame_rate
    string render_technique
    string character_design_style
    string color_palette_type
    float  animation_realism_level
    string hand_drawn_elements_present
    string motion_capture_used
    string stop_motion_used
    string ai_generated_elements_present
    string production_software
    string art_direction_tone
    string animation_award_won
  }

  SYMBOLISM_AND_MOTIFS {
    int film_id PK, FK
    float symbolism_density
    string color_symbolism_present
    string water_motif_present
    string fire_motif_present
    string animal_symbolism_present
    string dream_sequence_present
    string mirror_or_reflection_motif
    string recurring_object_symbol
    string death_symbolism_present
    string religious_symbolism_present
    string technological_symbolism_present
    string nature_vs_industry_theme
    float  visual_metaphor_strength
    string symbolic_resolution
  }

  RELEASE_INFO {
    int film_id PK, FK
    date  release_date
    int   release_year
    string release_month
    string release_season
    string release_day_of_week
    string holiday_release
    string covid_era_release
    string theatrical_vs_digital
    string simultaneous_release
    string runtime_context
  }

  SOCIOPOLITICAL {
    int film_id PK, FK
    string political_content_present
    string political_alignment
    string social_issue_focus
    string lgbt_representation_present
    float  minority_representation_strength
    string gender_equality_focus
    string war_or_conflict_related
    string environmental_theme_present
    float  activism_message_strength
    float  controversy_level
    string propaganda_tone
  }

  RATING {
    int film_id PK, FK
    float audience_rating_mean
    float critic_rating_mean
    float rating_gap
    int   review_count
    float social_sentiment_score
    int   trending_duration_days
    string primary_source
    int   platform_coverage_count
    date  peak_popularity_date
  }

  CULTURAL_INFO {
    int film_id PK, FK
    float slang_intensity
    string accent_comedy_used
    string accent_region
    string cultural_humor_type
    string language_switching
    string cultural_instrument_usage
    float translation_difficulty_score
    string choreographic_dance_present
  }

  PARENTS_GUIDE {
    int film_id PK, FK
    float family_friendly_score
    float violence_intensity
    string sexual_content_present
    float sexual_content_intensity
    float language_intensity
    string substance_use_present
    float frightening_scenes_intensity
    string age_recommendation
    string age_rating_source
  }

  FRANCHISE {
    int film_id PK, FK
    string is_sequel
    int    sequel_number
    string franchise_name
    int    franchise_total_films
    decimal franchise_avg_rating
    string in_universe_order
  }

  FILMS ||--o{ CHARACTERS : has
  FILMS ||--o{ CREW_MEMBERS : has
  FILMS ||--o{ SOUNDTRACKS : has
  FILMS ||--|| SETTINGS_AND_WORLD : has
  FILMS ||--|| ANIMATION_SETTINGS : has
  FILMS ||--|| SYMBOLISM_AND_MOTIFS : has
  FILMS ||--|| RELEASE_INFO : has
  FILMS ||--|| SOCIOPOLITICAL : has
  FILMS ||--|| RATING : has
  FILMS ||--|| CULTURAL_INFO : has
  FILMS ||--|| PARENTS_GUIDE : has
  FILMS ||--|| FRANCHISE : has
